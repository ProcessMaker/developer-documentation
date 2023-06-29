---
description: >-
  This guide covers three OAuth 2.0 grant types: Authorization Code Grant,
  Password Grant, and Personal Access Tokens.
---

# Node.js Example

## Step 1: **Setting up Node.js and required libraries**

Before starting this example, ensure Node.js installed. Node.js is a JavaScript runtime that allows us to run JavaScript on our server. Download Node.js from the [official website](https://nodejs.org/en/download/).

After installing Node.js, install the library required to make HTTP requests. Use the `request` library. Open your terminal and navigate to the directory where you'll be writing your code. Then, run the following command:

```
npm install request
```

This command tells npm (node package manager) to install the `request` library. It's like going to the store and buying a new tool for your toolbox!

## **Step 2: Set Up Your Client Application**

If you came here before [creating your client application](../../authentication/creating-a-client-application.md), you first need to do so. Otherwise, go to step 3 if you have your client id and client secret already.

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
