[previous](#search) | [top](#toc) | [next](#screening)   
[search strategy](#search-strategy) | [search](#search) |
[deduplication](#deduplication) | [screening](#screening)

<a id="deduplication"></a>
<h2 align="center" style="font-family:Times New Roman;font-variant: small-caps;">
Deduplication </h2>

The 'gold-standard' or consensus agreement among researchers seems to
converge on the idea that removal of duplicate records is best performed
in a process that involves three ordered stages. The first is
deduplication based on a unique record identifier, such as a digital
object identifier (DOI) number, PubMed identifier (PMID) number, or
clinicaltrials.gov (NCT) number. Then, as according to as described for
the second stage, the remaining records were deduplicated based on a
concatenated column consisting of the title, author, and year. The title
was standardized by converting to sentence case, and punctuation marks
and white spaces were removed. The character length was decreased to 50.
For the authors column, the last name of the first author was chosen to
be used. For the year of publication, the year was extracted from the
date of publication in the electronic version of the journal and
converted into a string data structure.

input file(s): `records.csv`, output file(s): `doi_deduplicated.csv`,
`pmid_deduplicated.csv`, `title+author+year_deduplicated.csv`, and
`title+year_deduplicated.csv`.

```python
    import pandas as pd
    import mermaid
    import os

    input_file_name = f"{root}/systematic_review/deduplication/records.csv"

    #input_file_name = f"{deduplication}/" + input('Enter file name: ') + '.csv'

    deduplication = f"{root}/systematic_review/deduplication",

    df = pd.read_csv(input_file_name) # A (records)
    cols_input = input('Enter the column for which to deduplicate based on: ')
    cols = [c.strip() for c in cols_input.split(',')]
    folder = '_'.join(cols)
    os.makedirs(f"{deduplication}/{folder}/", exist_ok = True)

    output_file = f"{deduplication}/{folder}/{folder}_deduplicated"
    output_file_name = f"{output_file}.csv"
    output_for_recycle = f"{deduplication}/{folder}_deduplicated.csv"
    prisma_file_name = f"{output_file}.mmd"

    nulls_mask = df[cols].isnull().any(axis=1)
    df_nulls = df[nulls_mask] # B
    df_non_nulls = df[~nulls_mask] # C

    duplicates_mask = df_non_nulls.duplicated(subset = cols, keep = False)
    df_non_duplicates = df_non_nulls[~duplicates_mask] # D
    df_duplicates = df_non_nulls[duplicates_mask] # E
    #df_duplicates.groupby(cols, as_index=False).agg(agg_map)
    df_kept = df_duplicates.drop_duplicates(subset = cols, keep = 'first')
    #df_kept = df_duplicates.groupby(cols, as_index=False).agg(lambda s: list(dict.fromkeys(s.dropna())) if s.name in ['subgroup', 'source'] else s.dropna().iloc[0] if len(s.dropna()) else pd.NA)
    #df_kept = df_duplicates.groupby(cols, as_index=False).agg(lambda s: list(dict.fromkeys(s.dropna())) if s.name == 'subgroup' else s.dropna().iloc[0] if len(s.dropna()) else pd.NA)
    df_removed = df_duplicates[~df_duplicates.index.isin(df_kept.index)]
    #df_kept = df_duplicates.groupby(cols, as_index=False).agg(lambda s: '; '.join(dict.fromkeys(s.dropna().astype(str).str.strip())) if s.name == 'subgroup' and s.dropna().astype(str).str.strip().nunique() > 1 else (s.dropna().astype(str).str.strip().iloc[0] if len(s.dropna().astype(str).str.strip()) else pd.NA))
    df_unique = df_non_nulls.drop_duplicates(subset = cols, keep = 'first') # df of unique
    df_deduplicated = pd.concat([df_non_duplicates, df_kept, df_nulls], ignore_index=True) # df of unique + df of non-duplicates

    results = {"records": len(df),  
    "nulls": len(df_nulls), 
    "non_nulls": len(df_non_nulls), 
    "non_duplicates": len(df_non_duplicates), 
    "duplicates": len(df_duplicates), 
    "removed": len(df_removed), 
    "kept": len(df_kept),
    "unique": len(df_unique),
    "deduplicated": len(df_deduplicated)
    }

    output_file_name = f"{deduplication}/deduplicated.csv"
    df_nulls.to_csv(output_file_name.replace('deduplicated','nulls'), index = False)
    df_deduplicated.to_csv(output_file_name, index = False)
    df_removed.to_csv(output_file_name.replace('deduplicated','duplicates_removed'), index = False)
    df_deduplicated.to_csv(output_for_recycle, index = False)

    graph_text = f"""---
    config:
    theme: neutral
    curve: stepBefore
    ---
    graph TD;
    A["`**records** (*n* = {results['records']})`"];
    B["`null (*n* = {results['nulls']})`"];
    C["`non-null (*n* = {results['non_nulls']})`"];
    D["`non-duplicates (*n* = {results['non_duplicates']})`"];
    E["`duplicates (*n* = {results['duplicates']})`"];
    F["`duplicates kept (*n* = {results['kept']})`"];
    G["`duplicates removed (*n* = {results['removed']})`"];
    H["`unique (*n* = {results['unique']})`"];
    I["`deduplicated (*n* = {results['deduplicated']})`"];

    A --> B & C;
    C --> D & E;
    E --> F & G;
    D & F --> H
    B & H --> I"""

    with open(prisma_file_name, "w") as f:
        f.write(graph_text)

    !mmdc -i "{prisma_file_name}" -o "{output_file}"_light.svg
    !mmdc -i "{prisma_file_name}" -o "{output_file}"_dark.svg -t dark -b transparent
    print(results)
```

