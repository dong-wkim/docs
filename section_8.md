<a id="forms"></a>

<div align="center">
    <h1 style="font-family:Times New Roman;font-variant: small-caps;">
        Forms
    </h1>
</div>

    import pandas as pd
    import ipywidgets as widgets
    from IPython.display import display, HTML, Javascript

    reports = pd.read_csv("https://raw.githubusercontent.com/dong-wkim/network_meta-analysis/31a9070ff303d8df83f2ad164b4331f8465a7e6d/systematic_review/screening/pdf/pdf.csv", encoding = "utf-8")
    reports.head()
    reports["id"] = range(1, len(reports)+1)

    df = pd.DataFrame(columns = ["id", "study", "study_design", "level_evidence", "subgroup(s)", "outcome(s)", "arm(s)"])
    df["id"] = reports["id"]
    df["study"] = reports["study"]
    df = df.fillna("")
    df.head()

       id                study study_design level_evidence subgroup(s) outcome(s)  \
    0   1  Martorell-de (2025)                                                      
    1   2     Obradović (2023)                                                      
    2   3    Iliopoulos (2017)                                                      
    3   4       Valentí (2014)                                                      
    4   5      Kautzner (2015)                                                      

      arm(s)  
    0         
    1         
    2         
    3         
    4         

    a = widgets.BoundedIntText(description = "ID", layout = {"width":"50%"})
    b = widgets.HTML(description = "study", value = "")
    l = widgets.Dropdown(description = "study design", options = ["",
        "Randomized controlled trial", 
        "Non-randomized controlled trial",
        "Prospective cohort study",
        "Retrospective cohort study",
        "Case-control study",
        "Longitudinal study",
        "Cross-sectional study",
        "Case series",
        "Case report",
        "Review"], value = "",layout = {"width":"50%"})

    m = widgets.SelectMultiple(options = [
        'BPTB', 
        'HT', 
        'QT', 
        'PLT', 
        'AT', 
        'TA'], value = ["BPTB"], description = "subgroup(s)", layout = {"width": "50%"})


    n = widgets.Dropdown(options = [
        '',
        'single-arm',
        'two-arm',
        'multi-arm'], value = "", description = "arm(s)")

    o = widgets.SelectMultiple(options = [
        '',
        'IKDC subjective',
        'Lysholm',
        'Tegner',
        'Instrumental laxity',
        'Pivot shift',
        'Lachman',
        'Graft rupture'
    ], value = ("",), description = "outcome(s)")
                               

    save = widgets.Button(description="Save", button_style="info", icon = "save")
    out = widgets.Output()

    columns = ["study_design", "subgroup(s)", "outcome(s)", "arm(s)"]
    for col in columns:
        if col not in df.columns:
            df[col] = ""

    def save_values(change):
        row_id = a.value

        df.loc[df["id"] == row_id, "study"] = b.value
        df.loc[df["id"] == row_id, "study_design"] = l.value
        df.loc[df["id"] == row_id, "subgroup(s)"] = ", ".join(m.value)
        df.loc[df["id"] == row_id, "arm(s)"] = n.value
        df.loc[df["id"] == row_id, "outcome(s)"] = o.value

        with out:
            out.clear_output()
            print(f"Saved values for ID {row_id}")


    display(
        a,
        b,
        l,
        m,
        n,
        o,
        save,
        out
    )

    def update_study(change):
        row = df.loc[df["id"] == a.value]

        if not row.empty:
            b.value = str(row["study"].iloc[0])
        else:
            b.value = ""

    l.observe(update_study, names="value")
    m.observe(update_study, names="value")
    n.observe(update_study, names="value")
    o.observe(update_study, names="value")

    save.on_click(save_values)

    {"model_id":"74aeb935ad324bc996c6ee7314da83d2","version_major":2,"version_minor":0}

    {"model_id":"41bedec58e3b483f8c20c45c617efccc","version_major":2,"version_minor":0}

    {"model_id":"75185e079f394745883330bd46438311","version_major":2,"version_minor":0}

    {"model_id":"55dee772746e4f4aac688ea93661de8b","version_major":2,"version_minor":0}

    {"model_id":"df78f19987454e8b96c50d24df8f7707","version_major":2,"version_minor":0}

    {"model_id":"162da1a6ca9347439e0dbca790e3ec54","version_major":2,"version_minor":0}

    {"model_id":"2175a4f4aa2d45ed88ba7ddf8f654f97","version_major":2,"version_minor":0}

    {"model_id":"869bac2e7400411799679f2d6ac0da27","version_major":2,"version_minor":0}

    widgets.Button().keys

    ['_dom_classes',
     '_model_module',
     '_model_module_version',
     '_model_name',
     '_view_count',
     '_view_module',
     '_view_module_version',
     '_view_name',
     'button_style',
     'description',
     'disabled',
     'icon',
     'layout',
     'style',
     'tabbable',
     'tooltip']

    import ipywidgets as widgets
    from IPython.display import display
    import pandas as pd
    import re
    layout = widgets.Layout()
    keys = layout.keys
    list = "\n".join(keys)
    list = re.sub(r"_(.*?)", "", list)
    print(list)

    modelmodule
    modelmoduleversion
    modelname
    viewcount
    viewmodule
    viewmoduleversion
    viewname
    aligncontent
    alignitems
    alignself
    borderbottom
    borderleft
    borderright
    bordertop
    bottom
    display
    flex
    flexflow
    gridarea
    gridautocolumns
    gridautoflow
    gridautorows
    gridcolumn
    gridgap
    gridrow
    gridtemplateareas
    gridtemplatecolumns
    gridtemplaterows
    height
    justifycontent
    justifyitems
    left
    margin
    maxheight
    maxwidth
    minheight
    minwidth
    objectfit
    objectposition
    order
    overflow
    padding
    right
    top
    visibility
    width

    columns = ["study", "study_design", "subgroup(s)", "arm(s)", "outcome(s)"]

    for col in columns:
        if col not in df.columns:
            df[col] = ""
            
    a = widgets.BoundedIntText(
        value=int(df["id"].min()),
        min=int(df["id"].min()),
        max=int(df["id"].max()),
        description="ID",
        layout={"width": "30%"}
    )

    b = widgets.HTML(
        description="study",
        value=""
    )

    l = widgets.Dropdown(
        description="study design",
        options=[
            "",
            "Randomized controlled trial",
            "Non-randomized controlled trial",
            "Prospective cohort study",
            "Retrospective cohort study",
            "Case-control study",
            "Longitudinal study",
            "Cross-sectional study",
            "Case series",
            "Case report",
            "Review"
        ],
        value=""
    )

    m = widgets.SelectMultiple(
        description="subgroup",
        options=["BPTB", "HT", "QT", "PLT", "AT", "TA"],
        value=(),
        layout={"width": "50%"}
    )

    n = widgets.Dropdown(
        description="arm(s)",
        options=["", "Single-arm", "Two-arm", "Multi-arm"],
        value=""
    )

    o = widgets.SelectMultiple(
        description="outcome(s)",
        options=[
            "IKDC",
            "Lysholm",
            "Tegner",
            "Instrumental laxity",
            "Pivot shift",
            "Lachman",
            "Graft failure"
        ],
        value=(),
        layout={"width": "50%"}
    )

    p = widgets.Dropdown(
        description = "level evidence",
        options = ["", "I", "II", "III", "IV", "V"],
        value = "")
    save = widgets.Button(description="Save", button_style="info")
    out = widgets.Output()

    state = {}

    def remember_values():
        state[a.value] = {
            "study": b.value,
            "study_design": l.value,
            "subgroup(s)": m.value,
            "arm(s)": n.value,
            "outcome(s)": o.value,
            "level_evidence": p.value
        }

    def update_study(change=None):
        row_id = a.value
        row = df.loc[df["id"] == row_id]

        if row.empty:
            b.value = ""
            l.value = ""
            m.value = ()
            n.value = ""
            o.value = ()
            return

        row = row.iloc[0]

        if row_id in state:
            b.value = state[row_id]["study"]
            l.value = state[row_id]["study_design"]
            m.value = state[row_id]["subgroup(s)"]
            n.value = state[row_id]["arm(s)"]
            o.value = state[row_id]["outcome(s)"]

        else:
            b.value = "" if pd.isna(row["study"]) else str(row["study"])
            l.value = "" if pd.isna(row["study_design"]) else str(row["study_design"])
            n.value = "" if pd.isna(row["arm(s)"]) else str(row["arm(s)"])

            subgroups = "" if pd.isna(row["subgroup(s)"]) else str(row["subgroup(s)"])
            outcomes = "" if pd.isna(row["outcome(s)"]) else str(row["outcome(s)"])

            m.value = tuple(x.strip() for x in subgroups.split(",") if x.strip())
            o.value = tuple(x.strip() for x in outcomes.split(",") if x.strip())


    def save_values(change):
        row_id = a.value

        remember_values()

        df.loc[df["id"] == row_id, "study"] = b.value
        df.loc[df["id"] == row_id, "study_design"] = l.value
        df.loc[df["id"] == row_id, "subgroup(s)"] = ", ".join(m.value)
        df.loc[df["id"] == row_id, "arm(s)"] = n.value
        df.loc[df["id"] == row_id, "outcome(s)"] = ", ".join(o.value)
        df.loc[df["id"] == row_id, "level_evidence"] = p.value
        
        with out:
            out.clear_output()
            print(f"Saved values for ID {row_id}")

    def remember_on_change(change):
        remember_values()

    l.observe(remember_on_change, names="value")
    m.observe(remember_on_change, names="value")
    n.observe(remember_on_change, names="value")
    o.observe(remember_on_change, names="value")

    a.observe(update_study, names="value")
    save.on_click(save_values)

    # load first ID
    update_study()

    display(
        a,
        b,
        l,
        p,
        m,
        n,
        o,
        save,
        out
    )

    df.fillna("")
    df.head(50)
    df.to_csv("./data_collection.csv", encoding = "utf-8")

    # use greek alphabet for variables that pertain to floats and int that will undergo analysis DOWNSTREAM.

    theta = f"θ"
    sigma = f"σ"

    {"model_id":"28f8da0a924e49a2a00d61e99eea20e4","version_major":2,"version_minor":0}

    {"model_id":"c01cff98e6104b1b9c3a1cedd216256e","version_major":2,"version_minor":0}

    {"model_id":"cfa8478dad86449f8242f6f89c68fd70","version_major":2,"version_minor":0}

    {"model_id":"9f246330aabf416689696e31a1049728","version_major":2,"version_minor":0}

    {"model_id":"7c2216f1b539428287ae024a3df13ba0","version_major":2,"version_minor":0}

    {"model_id":"eea4a6f8d42f4fc3bedf8b9a6a90d202","version_major":2,"version_minor":0}

    {"model_id":"34773f7c8e744f7fa572d9ff9d5fa7c1","version_major":2,"version_minor":0}

    {"model_id":"4bce99ac58074667a1197a840fbbc7ae","version_major":2,"version_minor":0}

    {"model_id":"97e234049beb44888dbfd803b0e07c29","version_major":2,"version_minor":0}

    df.head(3)

       id                study study_design level_evidence   subgroup(s)  \
    0   1  Martorell-de (2025)  Case report             II  BPTB, HT, QT   
    1   2     Obradović (2023)                                             
    2   3    Iliopoulos (2017)                                             

      outcome(s)   arm(s)  
    0             Two-arm  
    1                      
    2                      
