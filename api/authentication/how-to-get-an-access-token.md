---
description: >-
  This guide covers three OAuth 2.0 grant types: Authorization Code Grant,
  Password Grant, and Personal Access Tokens.
---

# How to Get an Access Token

## Overview

This guide walks you through the steps of obtaining an access token for making restful api calls to ProcessMaker. You will be able to obtain an access token and then consume the api. After you complete this document, you will want to go to  [how-to-start-a-processs-request.md](../working-with-the-api/how-to-start-a-processs-request.md "mention")

{% hint style="info" %}
Don't forget to replace placeholders like `<your-instance>`, `<your-client-id>`, etc., with your actual values. Always protect your client secret, access tokens, personal access tokens, and user credentials.
{% endhint %}

{% tabs %}
{% tab title="Python" %}
## **Step 1: Install Necessary Python Libraries**

Before starting, ensure you have the necessary Python libraries installed. You'll need `requests` for making HTTP requests and `oauthlib` for handling OAuth.

Install them via pip:

```
pip install requests oauthlib
```

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

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
{% endtab %}

{% tab title="Node.js" %}
## Step 1: **Setting up Node.js and required libraries**

Before starting this example, ensure Node.js installed. Node.js is a JavaScript runtime that allows us to run JavaScript on our server. Download Node.js from the [official website](https://nodejs.org/en/download/).

After installing Node.js, install the library required to make HTTP requests. Use the `request` library. Open your terminal and navigate to the directory where you'll be writing your code. Then, run the following command:

```
npm install request
```

This command tells npm (node package manager) to install the `request` library. It's like going to the store and buying a new tool for your toolbox!

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

## **Step 3: Writing the code**

Now that you have your tools, you can start writing our code. Create a new JavaScript file named `app.js`. Inside this file, write the code to get our access token.

First, import the `request` library at the top of our file:

```javascript
var request = require('request');
```

This line is like taking the tool out of the toolbox and laying it out on our workbench.

Now, define the details of our client application. These are like the blueprint for your project:

```javascript
var clientId = 'YOUR_CLIENT_ID';
var clientSecret = 'YOUR_CLIENT_SECRET';
```

Replace `YOUR_CLIENT_ID` and `YOUR_CLIENT_SECRET` with your actual client ID and secret provided by ProcessMaker.

## **Step 4: Making the request**

Now you're ready to make our request to the API! This is the exciting part - it's like turning on the power drill and driving in the screw.

```javascript
request({
    url: 'https://MyOrganization.processmaker.net/oauth/token',
    method: 'POST',
    auth: {
        user: clientId,
        pass: clientSecret
    },
    form: {
        grant_type: 'client_credentials'
    }
}, function(err, res, body) {
    if (err) {
        console.log('Oops, something went wrong!', err);
    } else {
        var json = JSON.parse(body);
        var accessToken = json.access_token;
        console.log('Yay! We got an access token: ', accessToken);
    }
});
```

This code sends a POST request to the ProcessMaker API to get an access token. If the request is successful, the access token logs to the console. If something goes wrong, the log records an error message.

And voila! You've just written a Node.js script to get an access token from the ProcessMaker API. You're now a certified API wrangler! Keep this script handy, as you'll need the access token for making authenticated requests to the API. Happy coding!
{% endtab %}

{% tab title="Postman" %}
## **Step 1: Download and Install Postman**

[Download](https://www.postman.com/downloads/) and install Postman from their official website if you haven't already.

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

## **Step 3: Create a New Request**

Open Postman, click on the **+** button to create a new tab, then click on the **Authorization** tab.

## **Step 4: Use the Correct Grant Type**

For each grant type, select the type from the **Type** drop-down under the **Authorization** tab and fill in the necessary details.

### **Authorization Code Grant**

1. Type: Choose **OAuth 2.0** from the drop-down.
2. Add auth data to: Choose **Request Headers**.
3. Configure New Token:
   * **Token Name:** Any name for your reference.
   * **Grant Type:** Authorization Code.
   * **Callback URL:** The callback URL specified in your OAuth application.
   * **Auth URL:** The authorization URL of the OAuth server.
   * **Access Token URL:** The token URL of the OAuth server.
   * **Client ID:** The client ID of your OAuth application.
   * **Client Secret:** The client secret of your OAuth application.
   * **Scope:** The scope of the access request.
   * **Client Authentication:** Send as Basic Auth header.
4. Click **Get New Access Token**.
5. After the user authenticates and authorizes the application, the access token will be automatically filled in the **Access Token** field.

### **Password Grant**

1. Type: Choose **OAuth 2.0** from the drop-down.
2. Add auth data to: Choose **Request Headers**.
3. Configure New Token:
   * **Token Name:** Any name for your reference.
   * **Grant Type:** Password Credentials.
   * **Access Token URL:** The token URL of the OAuth server.
   * **Username:** The username of the user.
   * **Password:** The password of the user.
   * **Client ID:** The client ID of your OAuth application.
   * **Client Secret:** The client secret of your OAuth application.
   * **Scope:** The scope of the access request.
   * **Client Authentication:** Send as Basic Auth header.
4. Click **Get New Access Token**. The access token will be automatically filled in the **Access Token** field.

### **Client Credentials Grant**

1. Type: Choose **OAuth 2.0** from the drop-down.
2. Add auth data to: Choose **Request Headers**.
3. Configure New Token:
   * **Token Name:** Any name for your reference.
   * **Grant Type:** Client Credentials.
   * **Access Token URL:** The token URL of the OAuth server.
   * **Client ID:** The client ID of your OAuth application.
   * **Client Secret:** The client secret of your OAuth application.
   * **Scope:** The scope of the access request.
   * **Client Authentication:** Send as Basic Auth header.
4. Click **Get New Access Token**. The access token will be automatically filled in the **Access Token** field.

## **Step 5: Making API Requests**

After obtaining the access token, Postman automatically adds the `Authorization: Bearer <access-token>` header to your requests. You can now make requests to the API with the access token.

Remember: Always protect your client secret, access tokens, and user credentials. These allow access to the API and should be treated like passwords.

That's it! You now know how to get an access token using OAuth 2.0 in Postman.
{% endtab %}

{% tab title="cURL" %}
## Step 1: Set Up Your Client Application

If you arrived here before [creating your client application](creating-a-client-application.md), you first need to do so. Otherwise, proceed to step 2 if you have your client ID and client secret already.



## Step 2: Use the Correct Grant Type

### **Authorization Code**

This is used by web and mobile applications and involves the following steps:

1. Redirect the user to the authorization server (ProcessMaker).
2. The user authorizes the application.
3. The application exchanges an authorization code for an access token.

{% code overflow="wrap" %}
```bash
# Redirect user to authorization URL
echo "Please go to the following URL and authorize the app: https://<your-instance>.processmaker.net/oauth/authorize?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&scope=<your-scope>"

# Exchange the authorization code for an access token
curl -X POST "https://<your-instance>.processmaker.net/oauth/token" \
     -d "grant_type=authorization_code&code=<authorization-code>&client_id=<your-client-id>&client_secret=<your-client-secret>&redirect_uri=<your-redirect-uri>"
```
{% endcode %}

### **Password Grant**

This is used by applications that are highly trusted, like those installed on a personal device by the user.

{% code overflow="wrap" %}
```bash
curl -X POST "https://<your-instance>.processmaker.net/oauth/token" \
     -d "grant_type=password&username=<your-username>&password=<your-password>&client_id=<your-client-id>&client_secret=<your-client-secret>"
```
{% endcode %}

### **Personal Access Tokens**

A Personal Access Token (PAT) is an alternative to using a password for authentication to the API.

```bash
curl -X GET "https://<your-instance>.processmaker.net/api/<your-endpoint>" \
     -H "Authorization: Bearer <your-personal-access-token>"
```

### Step 3: Making API Request

After obtaining your access token, you can use it to make authenticated requests to the API.

```bash
curl -X GET "https://<your-instance>.processmaker.net/api/<your-endpoint>" \
     -H "Authorization: Bearer <your-access-token>"
```

## Conclusion

Utilizing `curl` provides a straightforward and efficient method for interacting with the ProcessMaker API. By following the steps outlined in this guide, developers can seamlessly obtain access tokens and make authenticated requests to the API. As with all authentication methods, it's imperative to handle credentials with care, ensuring they remain confidential. With the power of `curl` at your fingertips, you're well-equipped to harness the capabilities of the ProcessMaker platform, driving innovation and efficiency in your workflows.
{% endtab %}
{% endtabs %}



