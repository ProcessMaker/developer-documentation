---
description: >-
  This guide covers three OAuth 2.0 grant types: Authorization Code Grant,
  Password Grant, and Personal Access Tokens.
---

# Postman Example

## **Step 1: Download and Install Postman**

[Download](https://www.postman.com/downloads/) and install Postman from their official website if you haven't already.

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](../../authentication/creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

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
