---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-02"

keywords: certificates, ssl, tls, notifications, lifecycle events, expired certificate, deploy cert, callback url, slack, notification channel, renew certificate, notification format

subcollection: certificate-manager

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}


# Configuring notifications
{: #configuring-notifications}

With {{site.data.keyword.cloudcerts_long}}, you can receive notifications about various events that can help you to better manage your certificates. One of the most important notifications that you can receive is that your certificates are expiring. Certificates do have an expiration date and when they expire, you can experience downtime if you're not prepared. The notifications feature can help you to remember you need to renew your certificates before it's too late. Even better - you can use your notifications to automate the renewal of your certificates that are deployed to your TLS termination points.
{: shortdesc}


## When am I notified?
{: #notifications-notified} 

When you work with {{site.data.keyword.cloudcerts_short}}, you are notified about your lifecycle events based on the origin of your certificates, their renewal settings, and the operations that you perform during their lifespan. To avoid any downtime and limit your notifications, configure [automatic certificate renewal](/docs/certificate-manager?topic=certificate-manager-ordering-certificates#renew-certificate).


For an overview of when and why you are notified, check out the following table. 

Daily notifications begin the day that your certificate expires. To stop the notifications, reimport a renewed certificate to replace the previous version of the certificate that is stored in the service or renew your {{site.data.keyword.cloudcerts_short}} issued certificate. 
{: tip}


| Event             | Description      | Notified          |
|-------------------|------------------|-------------------|
| `cert_reimported` | A certificate is reimported to the service and it's time to deploy the certificate to its TLS termination point. | Single notification |
| `cert_about_to_expire_reimport_required` | Reminders to obtain a new certificate, deploy it, and then reimport it. | You are notified every 90, 60, 30, 10, and 1 day before your certificate expires. |
| `cert_expired_reimport_required` | It is time to obtain a new certificate, deploy it, and then reimport it. | Daily notifications. |
{: class="simple-tab-table"}
{: caption="Table 1. Understanding the types of reimport notifications" caption-side="top"}
{: #reimport-table}
{: tab-title="Imported/Reimported"}
{: tab-group="Notifications"}

| Event             | Description      | Notified          |
|-------------------|------------------|-------------------|
| `cert_issued` | An ordered certificate is issued. | Single alert that it's time to download the certificate and deploy it.
| `cert_order_failed` | A certificate order failed. | Single alert upon a failed order. |
| `cert_about_to_expire_renew_required` | Reminders to renew a certificate and then deploy it. | You are notified every 30, 10, and 1 day before your certificate expires. |
| `cert_expired_renew_required` | Reminders that alert you to renew your certificate and deploy it because it is expired. | You are notified daily. |
| `cert_issued_not_downloaded` | Reminder to download the certificate that you ordered and deploy it. | You are notified 30 days after the certificate is issued. |
{: class="simple-tab-table"}
{: caption="Table 1. Understanding the types of order notifications" caption-side="top"}
{: #ordered-table}
{: tab-title="Ordered"}
{: tab-group="Notifications"}

| Event             | Description      | Notified          |
|-------------------|------------------|-------------------|
| `cert_renewed` | A renewed certificate is issued. | Single alert that it's time to download the certificate and deploy it.
| `cert_renew_failed` | A certificate renewal has failed. | Single alert upon a failed renewal. |
| `cert_about_to_expire_renew_required` | Reminders to renew a certificate and then deploy it. | You are notified every 30, 10, and 1 day before your certificate expires. |
| `cert_expired_renew_required` | Reminders that alert you to renew your certificate and deploy it because it is expired. | You are notified daily. |
| `cert_renewed_not_downloaded` | Reminder to download the certificate that was renewed and deploy it. | You are notified 30, 10, 1 days before and the day your previous issued certificate expires. |
{: class="simple-tab-table"}
{: caption="Table 1. Understanding the types of renew notifications" caption-side="top"}
{: #renewed-table}
{: tab-title="Renewed"}
{: tab-group="Notifications"}


Notifications for expiring certificates are sent based on Coordinated Universal Time midnight, which is when the check is completed.
{: note}

### What are my options to configure notifications?
{: #notifications-options}

You can send notifications to Slack by configuring a webhook in your Slack account, or send notifications to any public callback URL you own.

## Setting up a Slack webhook
{: #setup-webhook}

To set up a Slack webhook, complete the following steps:

1. Sign up for [Slack](https://slack.com/){: external} and set up your workspace.
2. Create a Slack channel where you want to post your notifications to.
3. [Set up a webhook](https://api.slack.com/incoming-webhooks){: external} for the Slack channel

If you are already a member of a Slack workspace, skip to step 2.
{: tip}

## Setting up a Callback URL endpoint
{: #setup-callback}

A Callback URL endpoint can be used to automate various tasks such as:

* Sending notifications to report about expiring notifications to PagerDuty.
* Opening a ticket in GitHub or any other task management service.
* Deploy certificates that are obtained from {{site.data.keyword.cloudcerts_short}} to your TLS termination endpoints.
* Validate domain ownership when you order or renew certificates, in the case your domain is not managed in {{site.data.keyword.cis_full_notm}}.

You can find sample implementations in [Examples](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#examples).

### Callback URL requirements
{: #callback-url-requirements}

Your Callback URL endpoint must meet the following requirements to be used with {{site.data.keyword.cloudcerts_short}}:

* The endpoint must be publicly accessible.
* The endpoint must be protected with a valid CA TLS certificate.
* The endpoint must not require an authorization header, or any application headers.
* The endpoint must reply immediately to {{site.data.keyword.cloudcerts_short}} with a 2xx HTTP status code to indicate a successful notification delivery. Potential long tasks can be performed asynchronously after the notification is delivered.

### Notification format
{: #notification_format}

The notification that is sent to your Callback URL is a JSON document that is signed with your instance's asymmetric key in the following format.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

After you decode and verify the payload, the content is a JSON string [according to the channel version](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configuring a notification channel
{: #adding-channel}

After you create a Slack webhook or a Callback URL endpoint, you can add it to {{site.data.keyword.cloudcerts_short}} to start receiving notifications about expiring certificates, reimported certificates, issued certificates, renewed certificates, and challenges for domain validation.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} encrypts the endpoints that you configure to store them securely.
{: important}

To add a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Notifications**.
2. Click **Add Notification Channel**.
3. Choose the type of notification channel that you want to use.
4. Enter the webhook or Callback URL where you want to send notifications to.
5. Click **Save**. A summary of your configuration is displayed.

   <table>
   <caption>Table 1. Information about the notification channel </caption>
      <tr>
         <th> Component </th>
         <th> Description </th>
      </tr>
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
         <td>The notification channel state. If set to disabled, no notifications are sent.</td>
      </tr>
      <tr>
         <td>Dots menu</td>
         <td>Available actions that you can perform on the channel: <i>edit</i>, <i>test</i>, or <i>delete</i>.</td>
      </tr>
   </table>

    When you save a Slack webhook, {{site.data.keyword.cloudcerts_short}} automatically sends a confirmation notification to the Slack channel that you configured. Check your Slack channel to verify that you received this notification.
    {: tip}

7. Optional: Repeat these steps to add more channels.

You can implement a Callback URL to handle various tasks, or create several Callback URLs, each handling a different task.
{: tip}

## Testing a notification channel
{: #testing-channel}

You can test a notification channel to ensure that your notification channel is configured correctly.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

To test a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Notifications**.
2. Find your notification channel, click the dots menu, and select **Test Connection**.
3. Verify that you received a notification in the channel that you configured:
    * in Slack channel you will see test message
    * in Callback URL channel you will get notification with event type `test_notification_channel`

## Updating a notification channel
{: #updating-channel}

You can update your notification channel configuration, disable or enable notifications, or delete channels from {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

To update your notification channel, complete the following steps:

1. In the navigation on the service details page, click **Notifications**.
2. Choose from the following options:
   * To disable or enable notifications for a channel, set the switch to **Off** or **On**.
   * To update settings for a channel, select **Edit** from the actions menu.
   * To delete a notification channel, select **Delete** from the actions menu.

## Verifying the HTTP payload for a Callback URL
{: #verify-callback}

Every HTTP payload that is sent from {{site.data.keyword.cloudcerts_short}} to your Callback URL is automatically signed according to the JWT standard by using an asymmetric key pair.  
{: shortdesc}

For every {{site.data.keyword.cloudcerts_short}} instance, a private and a public key is generated that are not shared across other {{site.data.keyword.cloudcerts_short}} instances. The private key is used to sign the HTTP payload, and you can use the public key to verify that the payload is generated by {{site.data.keyword.cloudcerts_short}} and is not altered by a third party.

To download the public key, complete the following steps:

1. From the navigation on the service details page, click **Notifications**.
2. Click the **Download Key** button. The key is downloaded as a PEM file.

## Channel versions
{: #channel-versions}

As {{site.data.keyword.cloudcerts_short}} evolves, we might modify the format of the notifications payload structure from time to time. To ensure compatibility with earlier versions, the payload that is sent to your existing channels won’t change.   

If you have existing notification channels (Slack or Callback URL), to start getting the new version of the payload:

1. For Callback URL, make sure that your implementation can accept the new payload.
2. Create a new notification channel (new channels are always created with the latest channel version).
3. Test that the new channel works correctly.
4. Delete the old channel.

For channel versions, see [Notification event types and payload versions](/docs/certificate-manager?topic=certificate-manager-notifications-event-types).

## Examples
{: #examples}

* [How to Use {{site.data.keyword.cloudcerts_short}} to Avoid Outages Using Callback URLs - Part 1](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls){: external}  
   Learn how to create GitHub issues for expiring certificate notifications.
* [How to Use {{site.data.keyword.cloudcerts_short}} to Avoid Outages Using Callback URLs - Part 2](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2){: external}  
   Learn how to create PagerDuty incidents for expiring certificate notifications.
* [How to Automate TLS Certificate Rotation to Avoid Outages](https://www.ibm.com/cloud/blog/how-to-automate-tls-certificate-rotation-to-avoid-outages){: external}  
   Learn how to automate certificate rotation for expiring certificates.  
* [How to validate a domain by using a Callback URL and a Cloud Function action](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}  
   Learn how to validate your domain ownership when you order certificates.
