---
description: Learn how to start an instance of a Process called a Request.
---

# How to Start a Process's Request

## Overview

This guide walks you through the steps to create a new Process instance, called a Request, using the ProcessMaker 4 REST API programmatically. The guide assumes that you already have an access token for authenticating your API requests. If you need a refresher on obtaining an access token, you can refer to the previous guide [here](https://processmaker.gitbook.io/developer-documentation/8zllD6BOHfOiMuczkiHv/v/api/working-with-the-api/how-to-get-an-access-token/python-example).

### Pre-requisites

{% tabs %}
{% tab title="Python" %}


| Requirement                                                  | Function                                                            | Version                                                                                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p>Python<br>Dependencies:</p><ul><li>requests<br></li></ul> | The programming language and modules we are using for this tutorial | <p>Python 3+<br>Requests will install default latest version which is fine.</p>                                        |
| Access token                                                 | For authenticating with the API.                                    | instructions for obtaining from the [How to Get an Access Token](../authentication/how-to-get-an-access-token.md) page |

## Step 1: Preparing Your Python Environment

Before starting, ensure that you have Python 3 and the `requests` library installed. You can verify your Python version by typing `python --version` in your command line. The `requests` library can be installed via pip, Python's package manager, with the command `pip install requests`.

{% hint style="info" %}
If the command `python` returns an error, it may be installed as `python3,` depending on your environment.
{% endhint %}

## Step 2: Setting Up Your API Request

The ProcessMaker 4 REST API uses HTTP protocols, and in this case, we will be sending a POST request to create a new request. For this, we must prepare the headers and the body of our request.

### Preparing the Headers

The headers of an HTTP request provide additional parameters that the request needs to fulfill. In our case, we need to provide the `Authorization` header with our access token to authenticate our request.

In Python, headers are represented as a dictionary with the header names as keys and the corresponding values as dictionary values.

Here's how you would set up the headers:

```python
headers = {
    'Authorization': f'Bearer {access_token}',
}
```

Replace `{access_token}` with your actual access token.

### Preparing the Request Body

The body of a POST request contains the data we want to send to the server. In this case, we'll use a blank dictionary (`{}`) however this is dependent on your process, you may require to send additional parameters to be used as request data within the request.

Here's an example of a blank request body:

```python
request_body = {}
```

## Step 3: Sending the Request to the API

Now that we have our headers and request body ready, we can send our POST request to the ProcessMaker 4 REST API.

The URL for creating a new process instance is `https://<your-instance>/api/1.0/process_events/<process_id>`. Replace `<your-instance>` with your actual ProcessMaker instance and `<process_id>` with the ID of the process you want to start.

If you need help obtaining the process id, you can look at the [Process api documentation](../platform-api-reference/processes.md) to get the id before making the request to initiate a new request.

Here's how you can send the POST request and print the response:

```renpy
# Make a request to the API to start a new process
response = requests.post(
    'https://<your-instance>/api/1.0/process_events/<process_id>', 
    headers=headers, 
    json=request_body
)

# Print the response
print(response.json())
```

The `response.json()` function converts the server's response from a JSON format to a Python dictionary for easier handling.

That's it! You now know how to create a new process instance using the ProcessMaker 4 REST API in Python. Remember to replace `<your-instance>`, `<your-access-token>`, and `<process_id>` with actual values :smile:
{% endtab %}

{% tab title="Node.js" %}


| Requirement                                                             | Function                                                            | Version                                                                                                                                                           |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Node.js<br>Dependencies:</p><ul><li><code>axios</code><br></li></ul> | The programming language and modules we are using for this tutorial | <ul><li>Nodejs 8+</li><li>NPM 8-16</li></ul><p>Note: this is the ProcessMaker compatible version, this tutorial should work with the latest versions as well.</p> |
| Access token                                                            | For authenticating with the API.                                    | instructions for obtaining from the [How to Get an Access Token](../authentication/how-to-get-an-access-token.md) page                                            |

## Step 1: Preparing Your Node.js Environment

Before starting, ensure that you have Node.js and the `axios` library installed. You can verify your Node.js version by typing `node --version` in your command line.

## Step 2: Setting Up Your API Request

The ProcessMaker 4 REST API uses HTTP protocols, and in this case, we will be sending a POST request to create a new request. For this, we need to prepare the headers and the body of our request.

### Preparing the Headers

The headers of an HTTP request provide additional parameters that the request needs to fulfill. In our case, we need to provide the `Authorization` header with our access token to authenticate our request.

In JavaScript, headers are represented as an object with the header names as keys and the corresponding values as object values.

Here's how you would set up the headers:

```javascript
const headers = {
    'Authorization': `Bearer ${access_token}`,
};
```

Replace `${access_token}` with your actual access token.

### Preparing the Request Body

Here's an example of an empty request body:

```javascript
const requestBody = {};
```

The body of a POST request contains the data we want to send to the server. In this case, we'll use an empty object (`{}`), however, this is dependent on your process, and you may require to send additional parameters to be used as request data within the request.

## Step 3: Sending the Request to the API

Now that we have our headers and request body ready, we can send our POST request to the ProcessMaker 4 REST API.

The URL for creating a new process instance is `https://<your-instance>/api/1.0/process_events/<process_id>`. Replace `<your-instance>` with your actual ProcessMaker instance and `<process_id>` with the ID of the process you want to start.

If you need help obtaining the process id, you can look at the [Process api documentation](../platform-api-reference/processes.md) to get the id before making the request to initiate a new request.

Here's how you can send the POST request and print the response:\


```javascript
const axios = require('axios');

axios.post(
  'https://<your-instance>/api/1.0/process_events/<process_id>', 
  requestBody,
  { headers: headers }
).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error(`Error: ${error}`);
});
```

This code will send the POST request and print the response data. If there's an error, it will print the error.

That's it! You now know how to create a new process request using the ProcessMaker 4 REST API in Node.js. Remember to replace `<your-instance>`, `<your-access-token>`, and `<process_id>` with actual values.
{% endtab %}

{% tab title="Postman" %}


| Requirement        | Function                                                          | Version                                                                                                                |
| ------------------ | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p>Postman<br></p> | The tool we will use to make API calls to ProcessMaker 4 REST API | Latest                                                                                                                 |
| Access token       | For authenticating with the API.                                  | instructions for obtaining from the [How to Get an Access Token](../authentication/how-to-get-an-access-token.md) page |

## Step 1: Open Postman

Start by opening Postman. If you haven't installed it yet, you can download it from the [official Postman website](https://www.postman.com/downloads/).

> TODO: Add screenshots

## Step 2: Create a New Request

In Postman, click on the "+" tab to create a new request.

## Step 3: Configure the Request

In the new request tab, you will need to set up the following:

* **HTTP method:** Choose `POST` from the dropdown menu next to the URL bar.
* **Request URL:** The URL for creating a new process instance is `https://<your-instance>/api/1.0/process_events/<process_id>`. Replace `<your-instance>` with your actual ProcessMaker instance and `<process_id>` with the ID of the process you want to start.
* **Headers:** Click on the "Headers" tab and add a new header. For the name, enter `Authorization`, and for the value, enter `Bearer <your-access-token>`. Replace `<your-access-token>` with your actual access token.
* **Body:** Click on the "Body" tab and choose the `raw` and `JSON` format. Here you can enter the data you want to send as the request body. In this case, you can use an empty JSON object (`{}`), but depending on your process, you may need to send additional parameters to be used as request data within the request.

## Step 4: Send the Request

Once you have configured the request, you can press the "Send" button to send the request to the ProcessMaker 4 REST API. The server's response will appear in the section below.



That's it! You now know how to create a new process instance using the ProcessMaker 4 REST API in Postman. Remember to replace `<your-instance>`, `<your-access-token>`, and `<process_id>` with actual values.
{% endtab %}

{% tab title="CURL" %}
## Pre-requisites

| Requirement                      | Function                                                          | Version                                                                                                                |
| -------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| <p>Postman or a Terminal<br></p> | The tool we will use to make API calls to ProcessMaker 4 REST API | Latest                                                                                                                 |
| Access token                     | For authenticating with the API.                                  | instructions for obtaining from the [How to Get an Access Token](../authentication/how-to-get-an-access-token.md) page |

## Step 1: Setting Up Your API Request

The ProcessMaker 4 REST API uses HTTP protocols. In this case, we will be sending a POST request to create a new request.

### Execute the following command in your terminal

{% code overflow="wrap" %}
```bash
curl -X POST "https://<your-instance>/api/1.0/process_events/<process_id>" \
     -H "Authorization: Bearer <access_token>" \
     -d '{"key1":"value1", "key2":"value2", ...}'
```
{% endcode %}

{% hint style="info" %}
Don't forget!

Replace:

* `<your-instance>` with your actual ProcessMaker instance URL.
* `<process_id>` with the ID of the process you wish to start.
* `<access_token>` with your actual access token.
*   `{"key1":"value1", "key2":"value2", ...}` with your actual payload data.

    \

{% endhint %}

## Step 2: Review the Response

After executing the command, you should receive a response from the server. This will provide details about the process instance you've started or any potential errors.

## Conclusion

Using the `curl` command directly from the command line offers a swift and efficient method to interact with the ProcessMaker 4 REST API. By following the steps outlined in this guide, you can seamlessly initiate a Process instance, termed a Request, without the need for intermediary scripts or tools. This approach not only simplifies the process but also enhances the speed at which developers can test and integrate with the API. Always ensure you handle your access tokens with care, as they are crucial for secure communication with the API.
{% endtab %}
{% endtabs %}
