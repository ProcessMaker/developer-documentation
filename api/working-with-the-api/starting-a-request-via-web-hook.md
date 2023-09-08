---
description: >-
  This guide discusses how to integrate ProcessMaker with web hooks into
  third-party web applications to initiate new requests.
---

# Starting a Request via Web Hook

## Overview

In this guide, you will learn how to integrate the ProcessMaker app into third-party applications using web hooks to **initiate new process requests**. This integration allows you to seamlessly kick off workflow processes within the ProcessMaker environment from your own application.

By the end of this guide, you will have accomplished the following:&#x20;

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>ProcessMaker Integration using web hooks into a third-party application</p></figcaption></figure>

## Prerequisites

{% hint style="warning" %}
Before proceeding with the guide, it's important to assess your skill level as a developer. The following skills and knowledge are highly recommended to ensure a smooth implementation: web hooks and API.
{% endhint %}

| Requirement           | Function                                                                                                                                                  | Version     |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| ProcessMaker Platform | Access to the ProcessMaker app with administrative privileges.                                                                                            | 4.6+        |
| Code Editor           | Choose a code editor of your choice that suits your preferences. Popular code editors for development include Visual Studio Code, Sublime Text, and Atom. | Your choice |

## Steps to Integrate ProcessMaker using Web Hooks

By following the steps below, seamlessly integrate your ProcessMaker's workflow/process into your application to initiate new requests.

### Step 1: Configure Web Hook in ProcessMaker

To seamlessly integrate ProcessMaker workflow/processes using web hooks begin by generating the web hook. Follow this example to generate the [ProcessMaker web hook](https://docs.processmaker.com/examples/screen-design-examples/example-signal-design-with-webhooks).

#### Web Hook Link

```html
https://my-server.processmaker.net/webhook/0a089078587bdcdef5f7a2c2f0fd7a3c
```

#### JSON Format Example

Based on the screen/form variables that you've defined within the ProcessMaker platform for your process, ensure to adjust the below example with your defined ProcessMaker form variables.&#x20;

Example that shows the JSON data you need to send to the webhook:

```json
{
 "companyName":"InsuCare",
 "email":"john.doe@insucare.com",
 "serviceArea":"123 Boeing Avenue",
 "typeBusiness":"Insurance",
 "country":"United States",
 "products":"Laptop"
}
```

#### Postman Example

Below is an illustrative example demonstrating the utilization of the web hook through Postman to trigger the API and initiate a request.&#x20;

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Initiate a request using a ProcessMaker web hook</p></figcaption></figure>

### Step 2: Integrate the Web Hook into Your Application

Now, that you have the web hook link, identify the appropriate location within your application to integrate the ProcessMaker workflow/process form. This could be a specific page, a modal window, or any other suitable area.

Below is a straightforward illustration showcasing how the integration can be implemented within a web application. Feel free to utilize the provided sample HTML code as a starting point:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rocket ERP</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
  <style>
    /* CSS styles for the ERP website */
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
      background-color: #f1f1f1;
    }
    header {
      background-color: #98cc09f1; /* New color for the header */
      color: #fff !important;
      padding: 15px;
      text-align: left;
      font-size: 24px;
      padding-left: 40px;
    }
    .container {
      display: flex;
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
    }
    .sidebar {
      background-color: #f9f9f9;
      width: 200px;
      padding: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .sidebar h3 {
      margin-top: 0;
      font-size: 1.2rem;
      color: #555;
    }
    .sidebar ul {
      list-style-type: none;
      padding: 0;
      margin: 10px 0;
    }
    .sidebar li {
      margin-bottom: 5px;
    }
    .sidebar a {
      text-decoration: none;
      color: #333;
      display: flex;
      align-items: center;
    }
    .sidebar .material-icons {
      margin-right: 5px;
    }
    .main-content {
      flex: 1;
      background-color: #fff;
      padding: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    h1 {
      margin: 0;
      color: #8350fc; /* New color for the heading */
      font-size: 2.5rem;
      margin-bottom: 20px;
      text-align: center;
    }
    input {
      width: 100%;
      padding: 8px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      background-color: #8350fc;
      color: #fff;
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      width: 100%;
    }

    button:hover {
      background-color: #4808df;
    }
  </style>
</head>
<body>
  <header>
    <i class="material-icons">rocket</i>Rocket ERP
  </header>
  <div class="container">
    <!-- Sidebar -->
    <div class="sidebar">
        <h3>Menu</h3>
        <ul>
            <li>
            <a href="#"><i class="material-icons">dashboard</i> Dashboard</a>
            </li>
            <li>
            <a href="#"><i class="material-icons">inventory</i> Inventory</a>
            </li>
            <li>
            <a href="#"><i class="material-icons">shopping_basket</i> Sales</a>
            </li>
            <li>
            <a href="#"><i class="material-icons">add_shopping_cart</i> Purchases</a>
            </li>
        </ul>
    </div>

    <div class="main-content">
      <h1>Request Form</h1>
      <form id="webhookForm">
          <label for="companyName">Company Name:</label>
          <input type="text" id="companyName" name="companyName">
          
          <label for="email">Email:</label>
          <input type="text" id="email" name="email">
          
          <label for="serviceArea">Service Area:</label>
          <input type="text" id="serviceArea" name="serviceArea">
          
          <label for="typeBusiness">Type of Business:</label>
          <input type="text" id="typeBusiness" name="typeBusiness">
          
          <label for="country">Country:</label>
          <input type="text" id="country" name="country">
          
          <label for="products">Products:</label>
          <input type="text" id="products" name="products">
          
          <button type="button" onclick="postData()">Submit</button>
      </form>
    </div>
  </div>
</body>
</html>
```

JavaScript example to send data to the ProcessMaker's process/workflow to initiate a request.

```javascript
<script>
    function postData() {
        const data = {
            companyName: document.getElementById('companyName').value,
            email: document.getElementById('email').value,
            serviceArea: document.getElementById('serviceArea').value,
            typeBusiness: document.getElementById('typeBusiness').value,
            country: document.getElementById('country').value,
            products: document.getElementById('products').value
        };

        fetch('https://my-server.processmaker.net/webhook/0a089078587bdcdef5f7a2c2f0fd7a3c', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
        .then(response => response.json())
        .then(responseData => {
            alert('Webhook response: ' + JSON.stringify(responseData));
        })
        .catch(error => {
            console.error('Error posting data:', error);
        });
    }
  </script>
```

### Step 3: Customize the Form and Attributes (Optional)

You can customize the form attributes according to your requirements. For example, you can adjust the form fields, font size, and other attributes of the form to fit your application's design and layout.

### Step 4: Test and Verify the Integration

Save your changes and reload your Web application. Ensure to change the web hook generated in the previous step inside the html template. Test the functionality of the form, such as submitting a new request to ensure that everything works as expected.

#### Output Preview: ProcessMaker Integration using web hooks into a third-party application

After you have completed the steps above, verify the form inside your application, initiate requests, and make sure it sends the information to the web hook.&#x20;

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>ProcessMaker Integration using web hooks into a third-party application </p></figcaption></figure>

## Conclusion

By following the steps outlined in this guide, you can integrate the ProcessMaker's forms into your Web application using Web Hooks to initiate new requests.
