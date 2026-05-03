<a id="full_text_screening"></a>

<h2 align="center" style="font-family:Times New Roman;font-variant:small-caps;">
    Full-text Screening
</h2>

    from src.setup import requirements, import_modules, structure

    from src.full_text_screening import full_text_screening
    full_text_screening()

    {"model_id":"74a6267eef2a4441a6b32d2af8184f12","version_major":2,"version_minor":0}

    import pandas as pd
    import ipywidgets as widgets
    from IPython.display import display, HTML

    root = f"G:/My Drive/network_meta-analysis"
    df = pd.read_csv(f"{root}/systematic_review/screening/pdf/pdf.csv", encoding = "utf-8")

    doi = df["doi"]

    layout = widgets.Layout(style = {"border":"solid"})

    pdf = widgets.HTML(value = f"""
    <iframe src='https://doi.org/{doi}'></iframe>""")

    a = widgets.BoundedIntText(value = 0, description = "ID", min = 0, max = len(df)-1)
    k = widgets.HTML(value = "", description = "doi", layout = layout)

    def update(change):
        doi = df.loc[df["id"] == a.value, "doi"]

        if a.value > 0:
            k.value = f"https://doi.org/{str(doi.iloc[0])}"
            
        else:
            k.value = ""
            
    a.observe(update, names = "value") 

    out = widgets.Output()
    hbox = widgets.HBox([a,k])
    display(hbox, out)

    {"model_id":"8051151c175f489fa71e9a5681b435c1","version_major":2,"version_minor":0}

    {"model_id":"9ee4d90d24134856bc67f6bd5cb53b97","version_major":2,"version_minor":0}

    import ipywidgets as widgets
    from IPython.display import display
    import pandas as pd

    a = widgets.BoundedIntText(
        value=0,
        description="ID",
        min=0,
        max=len(df) - 1
    )

    K = widgets.HTML(value="", description = "doi")

    def update(change=None):
        row = df.loc[df["id"] == a.value, "doi"]

        if row.empty:
            K.value = "No record found."
            return

        doi = row.iloc[0]

        if pd.isna(doi) or doi == "":
            K.value = "No DOI available."
            return

        doi_url = f"https://doi.org/{doi}"
        
        K.value = f"""
        <a href="{doi_url}" target="_blank">{doi}</a>
        """

    a.observe(update, names="value")

    update()
    display(a, K)

    from src.full_text_screening import full_text_screening
    full_text_screening()

    {"model_id":"43cf39ab344f498daecf7c344a1d5f93","version_major":2,"version_minor":0}

    {"model_id":"6123fd8450e549288c04236d2bb6f018","version_major":2,"version_minor":0}

    {"model_id":"4f93abc9f4344871b3d39826d773ab8c","version_major":2,"version_minor":0}

    df.head()

       Unnamed: 0.2  Unnamed: 0.1  Unnamed: 0  id                study subgroup  \
    0             0             0           5   6  Martorell-de (2025)     BPTB   
    1             1             1           7   8     Obradović (2023)     BPTB   
    2             2             3          37  38    Iliopoulos (2017)     BPTB   
    3             3             4          47  48       Valentí (2014)     BPTB   
    4             4             5          51  52      Kautzner (2015)     BPTB   

                                                 authors  first_author  \
    0  Martorell-de Fortuny L, Torres-Claramunt R, Sá...  Martorell-de   
    1  Obradović M, Ninković S, Gvozdenović N, Tošić ...     Obradović   
    2  Iliopoulos E, Galanis N, Zafeiridis A, Iosifid...    Iliopoulos   
    3  Valentí Azcárate A, Lamo-Espinosa J, Aquerreta...       Valentí   
    4        Kautzner J, Kos P, Hanus M, Trc T, Havlas V      Kautzner   

                                                   title  \
    0  Patellar bone defect grafting does not reduce ...   
    1  Tubularization of Bone-Tendon-Bone Grafts: Eff...   
    2  Anatomic single-bundle anterior cruciate ligam...   
    3  Comparison between two different platelet-rich...   
    4  A comparison of ACL reconstruction using patel...   

                                             short_title  ...  source  \
    0  patellarbonedefectgraftingdoesnotreduceanterio...  ...  pubmed   
    1  tubularizationofbonetendonbonegrafts:effectson...  ...  pubmed   
    2  anatomicsinglebundleanteriorcruciateligamentre...  ...  pubmed   
    3  comparisonbetweentwodifferentplateletrichplasm...  ...  pubmed   
    4  acomparisonofaclreconstructionusingpatellarten...  ...  pubmed   

                                 doi  \
    0              10.1002/ksa.12449   
    1       10.3390/medicina59101764   
    2      10.1007/s00167-016-4229-4   
    3  10.1016/S0020-1383(14)70008-7   
    4      10.1007/s00264-014-2495-7   

                                             doi_url        pmid  \
    0              https://doi.org/10.1002/ksa.12449  39194385.0   
    1       https://doi.org/10.3390/medicina59101764  37893482.0   
    2      https://doi.org/10.1007/s00167-016-4229-4  27371291.0   
    3  https://doi.org/10.1016/S0020-1383(14)70008-7  25384473.0   
    4      https://doi.org/10.1007/s00264-014-2495-7  25128968.0   

                                        pmid_url  \
    0  https://pubmed.ncbi.nlm.nih.gov/39194385/   
    1  https://pubmed.ncbi.nlm.nih.gov/37893482/   
    2  https://pubmed.ncbi.nlm.nih.gov/27371291/   
    3  https://pubmed.ncbi.nlm.nih.gov/25384473/   
    4  https://pubmed.ncbi.nlm.nih.gov/25128968/   

                                       title+author+year  \
    0  Martorell-de+patellarbonedefectgraftingdoesnot...   
    1  Obradović+tubularizationofbonetendonbonegrafts...   
    2  Iliopoulos+anatomicsinglebundleanteriorcruciat...   
    3  Valentí+comparisonbetweentwodifferentplateletr...   
    4  Kautzner+acomparisonofaclreconstructionusingpa...   

                                              title+year  \
    0  patellarbonedefectgraftingdoesnotreduceanterio...   
    1  tubularizationofbonetendonbonegrafts:effectson...   
    2  anatomicsinglebundleanteriorcruciateligamentre...   
    3  comparisonbetweentwodifferentplateletrichplasm...   
    4  acomparisonofaclreconstructionusingpatellarten...   

                                                    tiab  \
    0  Patellar bone defect grafting does not reduce ...   
    1  Tubularization of Bone-Tendon-Bone Grafts: Eff...   
    2  Anatomic single-bundle anterior cruciate ligam...   
    3  Comparison between two different platelet-rich...   
    4  A comparison of ACL reconstruction using patel...   

                                            pdf.download  \
    0  https://sci.bban.top/pdf/10.1002/ksa.12449.pdf...   
    1  https://sci.bban.top/pdf/10.3390/medicina59101...   
    2  https://sci.bban.top/pdf/10.1007/s00167-016-42...   
    3  https://sci.bban.top/pdf/10.1016/S0020-1383(14...   
    4  https://sci.bban.top/pdf/10.1007/s00264-014-24...   

                                                pdf.view  
    0     https://sci.bban.top/pdf/10.1002/ksa.12449.pdf  
    1  https://sci.bban.top/pdf/10.3390/medicina59101...  
    2  https://sci.bban.top/pdf/10.1007/s00167-016-42...  
    3  https://sci.bban.top/pdf/10.1016/S0020-1383(14...  
    4  https://sci.bban.top/pdf/10.1007/s00264-014-24...  

    [5 rows x 24 columns]
