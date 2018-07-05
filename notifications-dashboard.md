---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configuring notifications for expiring certificates
{: #configuring-notifications-for-expiring-certificates}

Certificates are typically valid only for a set amount of time. When a certificate that you use expires, you might experience downtime for your app. To avoid downtime, you can configure {{site.data.keyword.cloudcerts_full}} to send notifications for certificates that are about to expire so that you can renew your certificates on time. 
{: shortdesc}

**When do I get notified?** </br>
Depending on the expiration date of the certificate that you uploaded to {{site.data.keyword.cloudcerts_full}}, you are notified 90, 60, 30, 10, and 1 day before your certificate expires. In addition, you receive daily notifications about expired certificates starting on the first day after your certificate expired. 

You must renew your certificate, upload this certificate to {{site.data.keyword.cloudcerts_full}}, and delete the expired certificate to stop notification from continuing to be sent. 

**What are my options to configure notifications?** </br>
You can send notifications to Slack by using a Slack webhook or use any callback URL that you like. 

## Setting up a Slack webhook
{: #setup-callback}

1. Sign up for [Slack](https://slack.com/) and set up your workspace. 
2. Create a Slack channel where you want to post your notifications to. 
3. [Set up a webhook](https://api.slack.com/incoming-webhooks) for the Slack channel. 

## Setting up a callback URL
{: #callback}

You might want to use callback URL to post notification to the tools that you use daily to trigger the renewal process for your team. For example, you can send notifications to report to pager duty, automatically open up an issue in Github, or trigger renewal scripts.  
{: shortdesc}

**Important:** Your callback URL endpoint must meet the following requirements to be used with {{site.data.keyword.cloudcerts_short}}: 
* The endpoint must use the HTTPS protocol.
* The endpoint must not require HTTP headers. This requirement includes authorization headers.

### Using a callback URL to automatically open a GitHub issue 
{: #sample}

The following sample code shows how you can create a GitHub issue for expiring certificates when an {{site.data.keyword.cloudcerts_short}} notification is sent. You can run this code in {{site.data.keyword.openwhisk}}, or use the code in a different environment.   
{: shortdesc}

To run this code in {{site.data.keyword.openwhisk}}:

1. Create an [action in {{site.data.keyword.openwhisk}}](/docs/openwhisk/index.html#getting-started).
2. Use the following code to automatically create a GitHub issue: 

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "<PERSONAL_GITHUB_TOKEN>";

    /**
     * Returns the expiration data as short date string
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Creates the issue body string
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Gets the notification body and creates a Github issue
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Decode message to get information
        const data = jwtDecode(params.data);
        try {
            // Create request options to get the public key for verification
            const keysOptions = {
                method: 'GET',
                url: `https://<CERTIFICATE_MANAGER_CLUSTER_BASE_URL>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Send request to get the public key
            const keysResponse = await request(keysOptions);

            // Verify the data using the acquired public key
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Create request options to send a new issue to Github
            // Based on Github API - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<REPO_OWNER>/<REPO_NAME>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Certificates about to expire",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Send request to Github
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}
    
For other REST API commands see the [API documentation](https://console.bluemix.net/apidocs/cloudcerts)
{: tip}


## Configuring a notification channel
{: #adding-channel}

After you create a Slack webhook or a callback URL, you add it to {{site.data.keyword.cloudcerts_short}} to start receiving notifications about expiring certificates. {{site.data.keyword.cloudcerts_short}} encrypts the endpoint and stores it securely.
{: shortdesc}

To add a notification channel:

1. In the navigation on the service details page, click **Settings**. 
2. Open the **Notifications** tab.
3. Click **Add Notification Channel**. 
4. Choose the type of notification channel that you want to use. 
5. Enter the webhook or callback URL where you want to send notifications to.
6. Click **Save**. A summary of your configuration is displayed. 

   Example output: 
   <table>
   <caption> Information about the notification channel </caption>
   <thead>
    <th> Component </th>
    <th> Description </th>
   </thead>
   <tbody>
   <tr>
    <td>Type</td>
    <td>Notification channel type: <i>Slack</i> or <i>Callback URL</i></td>
   </tr>
   <tr>
    <td>Endpoint</td>
    <td>The notification channel endpoint where the notifications are sent to.</td>
   </tr>
   <tr>
    <td>Enablement toggle</td>
    <td>The notification channel state. If it's set to disabled, no notifications are sent.</td>
   </tr>
   <tr>
    <td>Test Connection button</td>
    <td>Sends a test notification to the channel that you configured. </td>
   </tr>
    <tr>
      <td>Dots menu</td>
      <td>Available actions that you can perform on the channel: <i>edit</i> or <i>delete</i></td>
    </tr>
    </tbody>
    </table>
   
    When you save a Slack webhook, {{site.data.keyword.cloudcerts_short}} automatically sends a confirmation notification to the Slack channel that you configured. Check your Slack channel to verify that you received this notification. 
    {: tip}
7. Optional: Repeat these steps to add more notification channels. 

## Testing a notification channel
{: #testing-channel}

You can test a notification channel to ensure that your notification channel is configured correctly.
{: shortdesc}

Before you begin, [configure a notification channel](#adding-channel). 

To test a notification channel: 

1. In the navigation on the service details page, click **Settings**. 
2. Find your notification channel and click **Test Connection**.
3. Verify that you received a notification in the channel that you configured. 


## Updating a notification channel
{: updating-channel}

You can update your notification channel configuration, disable or enable notifications, or delete notification channels from {{site.data.keyword.cloudcerts_short}}. 
{: shortdesc}

Before you begin, [configure a notification channel](#adding-channel). 

1. In the navigation on the service details page, click **Settings**. 
2. Select the **Notifications** tab. 
3. Choose from the following options. 
   - To disable or enable notifications for a channel, set the switch to **Disable** or **Enable**. 
   - To update settings for a channel, select **Edit** from the actions menu.
   - To delete a notification channel, select **Delete** from the actions menu. 
   
   
## Verifying the HTTP payload for a callback URL
{: #verify-callback}

Every HTTP payload that is sent from {{site.data.keyword.cloudcerts_short}} to your callback URL is automatically signed according to the JWT standard by using an asymmetric key pair.  
{: shortdesc}

For every {{site.data.keyword.cloudcerts_short}} instance, a private and a public key is generated that are not shared across other {{site.data.keyword.cloudcerts_short}} instances. The private key is used to sign the HTTP payload, and you can use the public key to verify that the payload is generated by {{site.data.keyword.cloudcerts_short}} and is not altered by a third party.

To download the public key:

1. From the navigation on the service details page, click **Settings**.
2. Open the **Notifications** tab.
3. Click the **Download Key** button. The key is downloaded as a PEM file.
