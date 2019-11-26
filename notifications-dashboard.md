---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-26"

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

{{site.data.keyword.cloudcerts_full}} can send you notifications about certificate lifecycle events. These include reminders to renew certificates before they expire, and to deploy certificates when they are ready. To get notifications from {{site.data.keyword.cloudcerts_short}}, set up a Slack or Callback URL notification channel, or both.
{: shortdesc}

## Notifications to monitor certificate expiration
{: #notifications-monitoring-certificate-expiration}

Certificates are typically valid for a set amount of time. When a certificate that you use expires, you might experience downtime. To avoid downtime you can configure {{site.data.keyword.cloudcerts_short}} to send you notifications about certificates that are about to expire, so that you are reminded to renew them on time.

You are also alerted after renewing an ordered certificate or reimporting a renewed version of your certificate in place of the expiring one. This is to remind you to deploy it to SSL/TLS termination points. 

Notifications about reimported certificates are sent only to channels from [channel version 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) and higher.
{: note}

### When am I notified?
{: #notifications-notifified} 

Depending on the expiration date of the certificate, you are notified 90, 60, 30, 10, and 1 day before your certificate expires. In addition, you receive daily notifications about expired certificates. The daily notifications start on the first day after your certificate expired.

You must renew your ordered certificate, or reimport a renewed certificate in place of your old one to {{site.data.keyword.cloudcerts_short}} to stop notifications from being sent. When you renew or reimport a certificate, you receive a notification that your certificate was renewed or reimported to remind you to redeploy it.

Notifications for expiring certificates are sent based on the time zone used to check whether a certificate has expired, which is UTC at midnight.
{: note}

### What are my options to configure notifications?
{: #notifications-options}

You can send notifications to Slack by using a Slack Webhook or use any Callback URL that you like.

## Notifications related to ordering certificates
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} notifies you when a certificate that you order from {{site.data.keyword.cloudcerts_short}} is issued to you, or renewed successfully. You are also notified if your order fails, or a renewal fails.
{: shortdesc}

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

A Callback URL endpoint can be used for various tasks. For example, to send notifications to report about expiring notifications to PagerDuty, automatically open up a ticket in GitHub or elsewhere, or validate domain ownership before ordering or renewing certificates. You can also automatically trigger deployment of certificates in response to notifications when certificates are reimported or renewed successfully.
{: shortdesc}

You can find sample implementations in the [Examples section below](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#examples).

### Callback URL requirements
{: #callback-url-requirements}

Your Callback URL endpoint must meet the following requirements to be used with {{site.data.keyword.cloudcerts_short}}

- The endpoint must use the HTTPS protocol.
- The endpoint must not require HTTP headers. This requirement includes authorization headers.
- The endpoint must return a `200 OK` status code to indicate a successful notification delivery.

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

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Learn how to create GitHub issues for expiring certificate notifications.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Learn how to create PagerDuty incidents for expiring certificate notifications.
* [How to Automate TLS Certificate Rotation to Avoid Outages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/how-to-automate-tls-certificate-rotation-to-avoid-outages)  
   Learn how to automate certificate rotation for expiring certificates.  
* [How to validate a domain by using a Callback URL and a Cloud Function action ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)  
   Learn how to validate your domain ownership when ordering certificates.