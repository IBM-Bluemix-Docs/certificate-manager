---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-23"

keywords: certificates, ssl, tls, notifications, lifecycle events, expired certificate, deploy cert, callback url, slack, notification channel, renew certificate, notification format

subcollection: certificate-manager

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Configuring notifications
{: #configuring-notifications}

Certificates have an expiration date. When a certificate that you use expires, you might experience downtime. To avoid downtime you can configure {{site.data.keyword.cloudcerts_long}} to send you notifications about certificates that are about to expire, so that you are reminded to renew them on time.

{{site.data.keyword.cloudcerts_short}} also sends lifecycle events such as when a certificate is reimported, issued or renewed. You can use those events to automate the renewal of your certificates deployed to your TLS termination points.

To receive notifications from {{site.data.keyword.cloudcerts_short}}, set up a Slack or Callback URL notification channel, or both. 
{: shortdesc}

### When am I notified?
{: #notifications-notified} 

You will be notified based on the origin of your certificates, their renewal setting, and the operations you perform during the lifespan of your certificates.   
The following table provides an overview of when you will be notified:

| Operation | Lifecycle events | Expiration events |
|-----------|------------------|-------------------|
| Certificate re/imported | <ul><li>`cert_reimported` - When a certificate is re-imported. Notifies you to deploy the certificate [1].</li></ul> | <ul><li>`cert_about_to_expire_reimport_required` - 90, 60, 30, 10, and 1 days before your certificate expires. Reminds you to: obtain a renewed certificate, deploy it [1], and reimport it to {{site.data.keyword.cloudcerts_short}}.</li><li>`cert_expired_reimport_required` - Daily notifications[2]. Alerts you to obtain a renewed certificate, deploy it [1], and reimport it to {{site.data.keyword.cloudcerts_short}}.</li><ul> |
| Certificate ordered | <ul><li>`cert_issued` - When an ordered certificate is issued. Notifies you to download the certificate and to deploy it [1].</li><li>`cert_order_failed` - When a certificate order fails. Notifies you about the failure.</li></ul> | <ul><li>`cert_about_to_expire_renew_required` - 30, 10, and 1 days before your certificate expires. Reminds you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li><li>`cert_expired_renew_required` - Daily notifications [2]. Alerts you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li></ul> |
| Certificate ordered and not downloaded | <ul><li>`cert_issued_not_downloaded` - 30 days after certificate was issued. Reminds you to download the certificate and to deploy[1].</li></ul> | <ul><li>`cert_about_to_expire_renew_required` - 30, 10, and 1 days before your certificate expires. Reminds you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li><li>`cert_expired_renew_required` - Daily notifications [2]. Alerts you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li></ul> |
| Certificate renewed | <ul><li>`cert_renewed` - When a certificate is renewed. Notifies you to download the certificate and to deploy it [1], [4].</li><li>`cert_renew_failed` - When certificate renewal fails. Notifies you about the failure.</li></ul> | <ul><li>`cert_about_to_expire_renew_required` - 30, 10, and 1 days before your certificate expires. Reminds you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li><li>`cert_expired_renew_required` - Daily notifications [2]. Alerts you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li></ul> |
| Certificate renewed and not downloaded | <ul><li>`cert_renewed_not_downloaded` - 30, 10, 1, 0 days before your previous issued certificate [3] expires. Reminds you that your renewed certificate was not downloaded to replace the previously deployed certificate about to expire.</li></ul> | <ul><li>`cert_about_to_expire_renew_required` - 30, 10, and 1 days before your certificate expires. Reminds you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li><li>`cert_expired_renew_required` - Daily notifications [2]. Alerts you to renew the certificate in {{site.data.keyword.cloudcerts_short}} and deploy it [1].</li></ul> |  
{: caption="Table 1. Notifications overview" caption-side="top"}

[1] Deploy the certificate to its TLS termination point.  
[2] The daily expiration notifications start on the day your certificate expires. You must reimport a renewed certificate in place of your old one, or renew your {{site.data.keyword.cloudcerts_short}} issued certificate to stop expiration notifications from being sent.  
[3] The previous version of your issued certificate stored in {{site.data.keyword.cloudcerts_short}}.  
[4] When certificate auto-renew is enabled, automatic renewal will occur 31 days before expiration.  

Notifications for expiring certificates are sent based on the time zone used to check whether a certificate has expired, which is UTC at midnight.
{: note}

### What are my options to configure notifications?
{: #notifications-options}

You can send notifications to Slack by configuring a Webhook in your Slack account, or send notifications to any public Callback URL you own.

## Setting up a Slack Webhook
{: #setup-webhook}

To set up a Slack Webhook, complete the following steps:

1. Sign up for [Slack](https://slack.com/){: external} and set up your workspace.
2. Create a Slack channel where you want to post your notifications to.
3. [Set up a Webhook](https://api.slack.com/incoming-webhooks){: external} for the Slack channel

If you are already a member of a Slack workspace, skip to step 2.
{: tip}

## Setting up a Callback URL endpoint
{: #setup-callback}

A Callback URL endpoint can be used to automate various tasks such as:

* Sending notifications to report about expiring notifications to PagerDuty.
* Opening a ticket in GitHub or any other task management service.
* Deploy certificates obtained from {{site.data.keyword.cloudcerts_short}} to your TLS terminiation endpoints.
* Validate domain ownership when ordering or renewing certificates, in the case your domain is not managed in {{site.data.keyword.cis_full_notm}}.

You can find sample implementations in the [Examples section below](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#examples).

### Callback URL requirements
{: #callback-url-requirements}

Your Callback URL endpoint must meet the following requirements to be used with {{site.data.keyword.cloudcerts_short}}:

* The endpoint must be publically accessible.
* The endpoint must be protected with a valid CA TLS certificate.
* The endpoint must not require an authorization header, or any application headers.
* The endpoint must reply immediately to {{site.data.keyword.cloudcerts_short}} with  a `200 OK` status code to indicate a successful notification delivery. Potential long tasks should be performed asynchronously after the notificaton is delivered.

### Notification format
{: #notification_format}

The notification that is sent to your Callback URL is a JSON document that is signed with your instance's asymmetric key in the following format.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

After you decode and verify the payload, the content is a JSON string [according to the channel version](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configuring a notification channel
{: #adding-channel}

After you create a Slack Webhook or a Callback URL endpoint, you can add it to {{site.data.keyword.cloudcerts_short}} to start receiving notifications about expiring certificates, reimported certificates, issued certificates, renewed certificates, and challenges for domain validation.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} encrypts the endpoints that you configure to store them securely.
{: important}

To add a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Notifications**.
2. Click **Add Notification Channel**.
3. Choose the type of notification channel that you want to use.
4. Enter the Webhook or Callback URL where you want to send notifications to.
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

    When you save a Slack Webhook, {{site.data.keyword.cloudcerts_short}} automatically sends a confirmation notification to the Slack channel that you configured. Check your Slack channel to verify that you received this notification.
    {: tip}

7. Optional: Repeat these steps to add more channels.

You can implement a Callback URL to handle a variety of tasks, or create several Callback URLs, each handling a different task.
{: tip}

## Testing a notification channel
{: #testing-channel}

You can test a notification channel to ensure that your notification channel is configured correctly.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

To test a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Notifications**.
2. Find your notification channel, click the dots menu and select **Test Connection**.
3. Verify that you received a notification in the channel that you configured.

## Updating a notification channel
{: #updating-channel}

You can update your notification channel configuration, disable or enable notifications, or delete channels from {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

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

For channel versions see [Notification event types and payload versions](/docs/services/certificate-manager?topic=certificate-manager-event-types-payload-versions).

## Examples
{: #examples}

* [How to Use {{site.data.keyword.cloudcerts_short}} to Avoid Outages Using Callback URLs - Part 1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Learn how to create GitHub issues for expiring certificate notifications.
* [How to Use {{site.data.keyword.cloudcerts_short}} to Avoid Outages Using Callback URLs - Part 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Learn how to create PagerDuty incidents for expiring certificate notifications.
* [How to Automate TLS Certificate Rotation to Avoid Outages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/how-to-automate-tls-certificate-rotation-to-avoid-outages)  
   Learn how to automate certificate rotation for expiring certificates.  
* [How to validate a domain by using a Callback URL and a Cloud Function action ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)  
   Learn how to validate your domain ownership when ordering certificates.
