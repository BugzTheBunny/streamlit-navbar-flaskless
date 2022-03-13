# streamlit-navbar-flaskless
A navbar component for streamlit.

A navbar component which does not require any external dependencies to be used.  
![navbar](https://user-images.githubusercontent.com/44586585/158054199-95576e41-5541-43ff-b16e-2988172104e1.gif)

Tested on `streamlit 1.7.0`  
Written in `python 3.8` (Using 3.10 you can use switch case if you preffer).

**Structure:**  
`views`: contains views which are rendered on navigation.  
`main`: the root, contains navigation function, some settings and activation of navigation.  
`utils`: contains some utilities & navbar component.  
`PATHS`: contains paths for navbar & settings.  

`How it works?`
There are 2 things injected into the page.
1. The component itself, the navbar with the icon & drop down.
2. The JS which is injected via `from streamlit.components.v1 import html` which allows to inject an iframe with JS.

To actually interact from withing the iframe in part 2, I am using `window.parent.document.getElementsBy...` which allows interaction from withing the dataframe with the parent document, which allows me to use JS in the places it's required.

```
def navbar_component():
    with open("assets/images/settings.png", "rb") as image_file:
        image_as_base64 = base64.b64encode(image_file.read())

    navbar_items = ''
    for key, value in NAVBAR_PATHS.items():
        navbar_items += (f'<a class="navitem" href="/?nav={value}">{key}</a>')

    settings_items = ''
    for key, value in SETTINGS.items():
        settings_items += (
            f'<a href="/?nav={value}" class="settingsNav">{key}</a>')

    component = rf'''
            ....
    '''
    st.markdown(component, unsafe_allow_html=True)
    
    js = '''
    <script>
    ....
    </script>
    '''
    html(js)

```
