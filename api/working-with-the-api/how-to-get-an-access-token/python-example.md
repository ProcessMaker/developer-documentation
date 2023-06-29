---
description: >-
  This guide discusses three OAuth 2.0 grant types: Authorization Code Grant,
  Password Grant, and Personal Access Tokens.
---

# Python Example

## **Step 1: Install Necessary Python Libraries**

Before starting, ensure you have the necessary Python libraries installed. You'll need `requests` for making HTTP requests and `oauthlib` for handling OAuth.

Install them via pip:

```
pip install requests oauthlib
```

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](../../authentication/creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

## **Step 3: Use the Correct Grant Type**

### **Authorization Code**

This is used by web and mobile applications which involves the following:

* Redirect the user to the authorization server (ProcessMaker).
* The user accepts the application.
* The application exchanges an authorization code for an access token.

```python
import requests
from oauthlib.oauth2 import WebApplicationClient

# Initialize the OAuth client
client = WebApplicationClient(client_id='<your-client-id>')

# Generate the authorization URL
auth_url, _ = client.prepare_request_uri(
    'https://<your-instance>.processmaker.net/oauth/authorize',
    redirect_uri='<your-redirect-uri>',
    scope='<your-scope>',
)

print(f'Please go to the following URL and authorize the app: {auth_url}')

# After the user has authorized the app, they will be redirected to the redirect URI
# with a code in the query string. Paste that code here.
code = input('Enter the authorization code: ')

# Exchange the authorization code for an access token
token_url = 'https://<your-instance>.processmaker.net/oauth/token'
token_data = client.prepare_request_body(
    code=code,
    client_id='<your-client-id>',
    client_secret='<your-client-secret>',
    redirect_uri='<your-redirect-uri>',
)

response = requests.post(token_url, data=token_data)
token_info = response.json()

print(f'Access token: {token_info["access_token"]}')
```

### **Password**

This is used by applications that are highly trusted, like those installed on a personal device by the user. This involves the client application collecting the user's username and password and exchanging them directly for an access token.

```python
import requests
from oauthlib.oauth2 import LegacyApplicationClient

# Initialize the OAuth client
client = LegacyApplicationClient(client_id='<your-client-id>')

# Prepare the request body for the token request
token_url = 'https://<your-instance>.processmaker.net/oauth/token'
token_data = client.prepare_request_body(
    username='<your-username>',
    password='<your-password>',
    client_id='<your-client-id>',
    client_secret='<your-client-secret>',
)

# Request an access token
response = requests.post(token_url, data=token_data)
token_info = response.json()

print(f'Access token: {token_info["access_token"]}')
```

### **Personal Access Tokens**

A Personal Access Token (PAT) is an alternative to using a password for authentication to the API. The PAT is usually generated in the application's user interface and can be revoked at any time.

```python
import requests

# Prepare the headers for the request
headers = {
    'Authorization': f'Bearer <your-personal-access-token>',
}

# Make a request to the API
response = requests.get('https://<your-instance>.processmaker.net/api/<your-endpoint>', headers=headers)

print(response.json())

```

## **Step 4: Making API Requests**

After you have your access token, you can use it to make authenticated requests to the API. Here's an example of how to do this:

```python
import requests

# Prepare the headers for the request
headers = {
    'Authorization': f'Bearer <your-access-token>',
}

# Make a request to the API
response = requests.get('https://<your-instance>.processmaker.net/api/<your-endpoint>', headers=headers)

print(response.json())

```

Replace `<your-instance>`, `<your-access-token>`, and `<your-endpoint>` with your actual values.

Remember: Always protect your client secret, access tokens, personal access tokens, and user credentials. These allow access to the API and should be treated like passwords.

That's it! You now have an access token that you can use to make authenticated requests to the API. Depending on the grant type used and the settings of the OAuth server, this token may expire after some time. If the token does expire, you will need to go through the flow again to get a new token.
