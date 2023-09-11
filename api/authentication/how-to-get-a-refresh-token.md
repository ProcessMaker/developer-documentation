---
description: This guide covers the OAuth 2.0 refresh token mechanism.
---

# How to Get a Refresh Token

## Overview

This guide walks you through the steps of refreshing an access token for making RESTful API calls to ProcessMaker. Access tokens typically have a limited lifespan, and once they expire, they need to be refreshed using a refresh token. This guide assumes you already have a refresh token. If not, refer to the ["How to Get an Access Token"](how-to-get-an-access-token.md) guide.

{% tabs %}
{% tab title="Python" %}
## Step 1: Obtaining the access token

{% content-ref url="how-to-get-an-access-token.md" %}
[how-to-get-an-access-token.md](how-to-get-an-access-token.md)
{% endcontent-ref %}

## Step 2: Install Necessary Python Dependencies

Before starting, ensure you have the necessary Python libraries installed. You'll need `requests` for making HTTP requests.

You can install it via pip:

```
pip install requests
```

## Step 3: Refreshing the Access Token

Use the following Python code to refresh your access token:

```python
import requests

# Define the token endpoint
token_url = "https://<your-instance>.processmaker.net/oauth/token"

# Define the payload
payload = {
    "grant_type": "refresh_token",
    "refresh_token": "<your-refresh-token>",
    "client_id": "<your-client-id>",
    "client_secret": "<your-client-secret>"
}

# Make the POST request
response = requests.post(token_url, data=payload)
token_info = response.json()

# Print the new access token
print(f'New Access Token: {token_info["access_token"]}')

```

{% hint style="info" %}
Don't forget!

Replace:

* `<your-instance>` with your actual ProcessMaker instance URL.
* `<your-refresh-token>` with the refresh token you received when you first obtained your access token.
* `<your-client-id>` and `<your-client-secret>` with the client ID and secret of your application.
{% endhint %}

## Step 4: Review the Response

After executing the script, you should receive a new access token and possibly a new refresh token. Store these securely, as you'll need the access token for future API requests and the refresh token for future token refreshes.

## Conclusion

Refreshing your access token is an essential step in maintaining uninterrupted access to the ProcessMaker API. By using Python and the `requests` library, you can easily and efficiently refresh your token. Always ensure you handle your tokens securely, as they are vital for maintaining secure communication with the API.
{% endtab %}

{% tab title="Node.js" %}
## Step 1: Obtaining the access token

{% content-ref url="how-to-get-an-access-token.md" %}
[how-to-get-an-access-token.md](how-to-get-an-access-token.md)
{% endcontent-ref %}

## Step 2: Install Necessary Node.js Libraries

Before starting, ensure you have the necessary Node.js libraries installed. You'll need `axios` for making HTTP requests.

You can install it via npm:

```
npm install axios
```

## Step 3: Refreshing the Access Token

Use the following Node.js code to refresh your access token:

```javascript

const axios = require('axios');

// Define the token endpoint
const token_url = "https://<your-instance>.processmaker.net/oauth/token";

// Define the payload
const payload = {
    grant_type: "refresh_token",
    refresh_token: "<your-refresh-token>",
    client_id: "<your-client-id>",
    client_secret: "<your-client-secret>"
};

// Make the POST request
axios.post(token_url, payload)
    .then(response => {
        console.log(`New Access Token: ${response.data.access_token}`);
    })
    .catch(error => {
        console.error('Error refreshing token:', error.response.data);
    });


```

{% hint style="info" %}
Don't forget!

Replace:

* `<your-instance>` with your actual ProcessMaker instance URL.
* `<your-refresh-token>` with the refresh token you received when you first obtained your access token.
* `<your-client-id>` and `<your-client-secret>` with the client ID and secret of your application.
{% endhint %}

## Step 3: Review the Response

After executing the script, you should receive a new access token and possibly a new refresh token. Store these securely, as you'll need the access token for future API requests and the refresh token for future token refreshes.

## Conclusion

Refreshing your access token is an essential step in maintaining uninterrupted access to the ProcessMaker API. By using Node.js and the `axios` library, you can easily and efficiently refresh your token. Always ensure you handle your tokens securely, as they are vital for maintaining secure communication with the API.\

{% endtab %}

{% tab title="Postman" %}
## Step 1: Obtaining the access token

{% content-ref url="how-to-get-an-access-token.md" %}
[how-to-get-an-access-token.md](how-to-get-an-access-token.md)
{% endcontent-ref %}

## Step 2: Download and Install Postman

If you haven't already, [download](https://www.postman.com/downloads/) and install Postman from their official website.

## Step 3: Set Up Your Client Application

If you navigated to this guide before creating your client application, you first need to do so. If you already have your client ID and client secret, proceed to step 3.

## Step 4: Create a New Postman Request Tab

Open Postman and click on the + button to create a new tab. Then, click on the Authorization tab.

## Step 5: Use the Refresh Token Grant Type



For the refresh token grant type, follow these steps:

**Refresh Token Grant**

* **Type**: Choose OAuth 2.0 from the drop-down.
* **Add auth data to**: Choose Request Headers.
* **Configure New Token**:
  * **Token Name**: Any name for your reference.
  * **Grant Type**: Refresh Token.
  * **Access Token URL**: The token URL of the OAuth server.
  * **Refresh Token**: The refresh token you received when you first obtained your access token.
  * **Client ID**: The client ID of your OAuth application.
  * **Client Secret**: The client secret of your OAuth application.
  * **Scope**: The scope of the access request (if any).
  * **Client Authentication**: Send as Basic Auth header.
* Click "Get New Access Token". The new access token will be automatically filled in the Access Token field.

## Step 6: Making API Requests

After obtaining the refreshed access token, Postman will automatically add the `Authorization: Bearer <access-token>` header to your requests. You can now continue making requests to the API using the refreshed access token.

{% hint style="info" %}
**Remember**: Always protect your client secret, refresh tokens, and access tokens. These grant access to the API and should be treated with the same care as passwords.
{% endhint %}

## Conclusion

That's it! You now know how to refresh an access token using OAuth 2.0 in Postman. Regularly refreshing your access token ensures uninterrupted access to the ProcessMaker API.
{% endtab %}

{% tab title="cURL" %}
## Step 1: Obtaining the access token

{% content-ref url="how-to-get-an-access-token.md" %}
[how-to-get-an-access-token.md](how-to-get-an-access-token.md)
{% endcontent-ref %}

## Step 2: Refreshing the Access Token

Execute the following command in your terminal:

{% code overflow="wrap" %}
```bash
curl -X POST "https://<your-instance>.processmaker.net/oauth/token" \
     -d "grant_type=refresh_token&refresh_token=<your-refresh-token>&client_id=<your-client-id>&client_secret=<your-client-secret>"
```
{% endcode %}

Replace:

* `<your-instance>` with your actual ProcessMaker instance URL.
* `<your-refresh-token>` with the refresh token you received when you first obtained your access token.
* `<your-client-id>` and `<your-client-secret>` with the client ID and secret of your application.

## Step 3: Review the Response

After executing the command, you should receive a response from the server. This will provide a new access token and possibly a new refresh token. Store these securely, as you'll need the access token for future API requests and the refresh token for future token refreshes.

#### Conclusion

Refreshing your access token is a crucial step in maintaining uninterrupted access to the ProcessMaker API. By using the `curl` command, you can easily and efficiently refresh your token directly from the command line. Always ensure you handle your tokens securely, as they are vital for maintaining secure communication with the API.
{% endtab %}
{% endtabs %}

####

####
