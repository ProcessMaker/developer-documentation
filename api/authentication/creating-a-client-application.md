# Creating a Client Application

## Configure Password Authentication for the Client Application

Follow these steps to configure password authentication for the client application:

1.  [View authenticated clients](broken-reference). The **Auth Clients** page displays.&#x20;

    <figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
2.  Click the **+Auth Client** button. The **Create Auth-Client** screen displays.&#x20;

    <figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
3. In the **Name** setting, enter a name for the client authentication.
4. Select the grant type you will be using.
5. Click **Save**. A new authenticated client is created.
6.  The authenticated client in the **Auth Clients** page contains the client secret, and the client id is the primary key of the table. In the example above, Passwrod Grant application has the client id of `3`, and then click the **Copy Client Secret to Clipboard** icon.

    <figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

That's it. You are now ready to attempt authenticating with the ProcessMaker REST API.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td>Python Example</td><td></td><td></td><td><a href="broken-reference">Broken link</a></td><td><a href="../.gitbook/assets/py.jpg">py.jpg</a></td></tr><tr><td>Node.js Example</td><td></td><td></td><td><a href="broken-reference">Broken link</a></td><td><a href="../.gitbook/assets/nodejs.jpg">nodejs.jpg</a></td></tr><tr><td>Postman Example</td><td></td><td></td><td><a href="broken-reference">Broken link</a></td><td><a href="../.gitbook/assets/postman-logo-vert-2018.jpg">postman-logo-vert-2018.jpg</a></td></tr></tbody></table>

{% hint style="info" %}
If you want to dig deeper into client applications, you can see the [full documentation here](https://processmaker.gitbook.io/processmaker/processmaker-platform-administration/auth-client-management/manage-client-authentications/view-all-client-authentication-keys).
{% endhint %}

{% hint style="info" %}
If you need more details about which grant type to use, you can look at the relevant [documentation here](broken-reference).
{% endhint %}
