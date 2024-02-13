# Introduction

A slight tweak of the fantastic upstream version provided [here](https://github.com/kawsarnoor/Streamlit-Authenticator) by `mkhorasani`. Allows user to send user credentials to be authenticated in exterrnal API.

# Installation

```
pip install git+https://github.com/kawsarnoor/Streamlit-Authenticator-External-API 
```

# Dependencies

You will need `streamlit` and `pyyaml`

```
pip install streamlit
pip install pyyaml
```

# Useage

The external API needs to have the same usernames as those in the `config.yaml` file.

```
import streamlit as st
import streamlit_authenticator_external_api as stauth
import yaml
from yaml import SafeLoader


external_api_endpoint = "http://my_external_api_url:xxxx"

with open('config.yaml') as file:
    config = yaml.load(file, Loader=SafeLoader)

authenticator = stauth.Authenticate(
    config['credentials'],
    config['cookie']['name'],
    config['cookie']['key'],
    config['cookie']['expiry_days'],
    config['preauthorized'],
    authentication_endpoint=external_api_endpoint
)

authenticator.login()
if st.session_state["authentication_status"]:
    authenticator.logout()
    st.write(f'Welcome *{st.session_state["name"]}*')
    st.title('Some content')
elif st.session_state["authentication_status"] is False:
    st.error('Username/password is incorrect')
elif st.session_state["authentication_status"] is None:
    st.warning('Please enter your username and password')
```
 