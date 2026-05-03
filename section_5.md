<a id="title_abstract_screening"></a>

<h2 align="center" style="font-family:Times New Roman;font-variant:small-caps;">
    Title abstract screening
</h2>

    from src.title_abstract_screening import title_abstract_screening
    title_abstract_screening()

    {"model_id":"98e34c613a6d4c7baccfbe70f1f6d847","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"265bbc36ccf648ae8f0222763680c3e2","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"a7a5f7ce04cf4e86848fb258439db953","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"e1674667596949d3a9bc4985728ad5af","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"c59e55a855434af1abd114269d59cef4","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"b4f7b30972f741d6ad39ad11d80bed35","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"782ab0f8dba8438782066bebe8de2868","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"80ec5e5acc8b412e9a9adb816bbd5af3","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"01055bb5076d4ec8b0b5a6c725a5f0f2","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"ec38035bdafa4382b9ad3f8ac9b4b689","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"6b7781e875144ea19ba837a2527e0386","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    {"model_id":"db167fde3ae147d199d9448a7699e042","version_major":2,"version_minor":0}

    {"model_id":"0445e46c72f240419c15228705274f67","version_major":2,"version_minor":0}

    import ipywidgets as widgets
    from IPython.display import display

    yes = widgets.Button(value = "Yes", description = "Yes", icon = "check", button_style = "success", layout = {"width":"200px",
                                                                                                                "alignitems":"right"})
    maybe = widgets.Button(value = "Maybe", description = "Maybe", icon = "", button_style = "warning")
    no = widgets.Button(value = "No", description = "No", icon = "times", button_style = "danger")
    save = widgets.Button(value = "Save", description = "Save", icon = "floppy-o", button_style = "info")

    out = widgets.Output()

    buttons = [yes, maybe, no, save]
    display(yes, maybe, no, save)

    {"model_id":"a7e2eea41d9f49f299116d71f4563269","version_major":2,"version_minor":0}

    {"model_id":"af805133fb4647458f0626887b16c592","version_major":2,"version_minor":0}

    {"model_id":"87df5160ada64ef5a5fbb73567bb23ac","version_major":2,"version_minor":0}

    {"model_id":"60c79e423cc84de1a957e60f393464a3","version_major":2,"version_minor":0}

    {"model_id":"8c04c91aecbf4e42b95758885ef89db6","version_major":2,"version_minor":0}

    uploader = widgets.FileUpload(layout = {"width":"40%"})
    out = widgets.Output()

    submit = widgets.Button(description = "Submit", button_style = "info", layout = {"width":"30%"})

    hbox = widgets.HBox(children = [uploader, submit])
    text = widgets.Text(layout = {"width":"70.5%"}, 
                        placeholder = "Enter the full search query")

    def read_file():
        import codecs
        uploaded_file = uploader.value[0]
        uploaded_file.content.tobytes()
        inputcodecs.decode(uploaded_file.content, encoding = "utf-8")

    submit.on_click(read_file)

    {"model_id":"04e7eba53ff34ff680b16a7f688b5f51","version_major":2,"version_minor":0}
