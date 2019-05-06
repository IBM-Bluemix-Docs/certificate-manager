---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

keywords: certificates, SSL,

subcollection: certificate-manager

---

{:new_window: target="_blank"}
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

{{site.data.keyword.cloudcerts_full}} can send you notifications about certificate lifecycle events. These include reminders to renew certificates before they expire, and to deploy certificates when they are ready. To get notifications from {{site.data.keyword.cloudcerts_short}}, you can set up a notification channel. You can specify either a Slack Webhook, a Callback URL, or any combination of the two.
{: shortdesc}

The notifications feature is also used when you [order certificates](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates) from {{site.data.keyword.cloudcerts_short}}. To prove that you own the domain for which you are requesting a certificate, {{site.data.keyword.cloudcerts_short}} sends a challenge as a notification to your Callback URL. The challenge is a text record, which you place in the Domain Name System (DNS) Service where your domain is registered. When the text record is in place, the challenge is considered complete. Because the challenge is sent as a notification to your Callback URL, you are able to automate the domain validation process by running code in response to the notification event.

## Notifications to monitor certificate expiration
{: #notifications-monitoring-certificate-expiration}

Certificates are typically valid for a set amount of time. When a certificate that you use expires, you might experience downtime for your app. To avoid downtime you can configure {{site.data.keyword.cloudcerts_short}} to send you notifications about certificates that are about to expire, so that you are reminded to renew them on time.

You are also alerted when a renewed version of your certificate is reimported to {{site.data.keyword.cloudcerts_short}} in place of the expiring one. This is to remind you to deploy it to SSL/TLS termination points. This notification about reimported certificates is sent only to channels from [channel version 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


**When am I notified?**  
Depending on the expiration date of the certificate that you uploaded to {{site.data.keyword.cloudcerts_short}}, you are notified 90, 60, 30, 10, and 1 day before your certificate expires. In addition, you receive daily notifications about expired certificates. The daily notifications start on the first day after your certificate expired.

You must renew your certificate and reimport this certificate in place of your old one to {{site.data.keyword.cloudcerts_short}} to stop notifications from being sent. When you reimport your certificate you receive a notification that your certificate was reimported to remind you to redeploy it.

**What are my options to configure notifications?**  
You can send notifications to Slack by using a Slack Webhook or use any Callback URL that you like.

## Notifications related to ordering certificates
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} notifies you when a certificate that you order from {{site.data.keyword.cloudcerts_short}} is issued to you. You are also notified if your order fails.
{: shortdesc}

Setting up a Callback URL notification channel and having the ability to handle events that are related to domain validation are prerequisites for ordering certificates. When you order a certificate, {{site.data.keyword.cloudcerts_short}} sends a challenge txt record to your Callback URL that you use to prove that you own the domain for which you are requesting the certificate.

## Setting up a Slack Webhook
{: #setup-callback}

To set up a Slack Webhook, complete the following steps:

1. Sign up for [Slack](https://slack.com/) and set up your workspace.
2. Create a Slack channel where you want to post your notifications to.
3. [Set up a Webhook](https://api.slack.com/incoming-webhooks) for the Slack channel.

## Setting up a Callback URL
{: #callback}

To trigger the renewal process for your team, you can use a Callback URL to post notifications to the tools that you use. For example, you can send notifications to report to PagerDuty, automatically open up an issue in GitHub, or trigger renewal scripts. You can also automatically trigger deployment of certificates in response to notifications when certificates are reimported or issued successfully.
{: shortdesc}

A Callback URL is a prerequisite for ordering certificates.
{: note}

**Important:** Your Callback URL endpoint must meet the following requirements to be used with {{site.data.keyword.cloudcerts_short}}:
* The endpoint must use the HTTPS protocol.
* The endpoint must not require HTTP headers. This requirement includes authorization headers.
* The endpoint must return a `200 OK` status code to indicate a successful notification delivery.

### Notification format
{: #notification_format}

The notification that is sent to your Callback URL is a JSON document that is signed with your instance asymmetric key in the following format.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

After you decode and verify the payload, the content is a JSON string [according to the channel version](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configuring a notification channel
{: #adding-channel}

After you create a Slack Webhook or a Callback URL, you can add it to {{site.data.keyword.cloudcerts_short}} to start receiving notifications about expiring certificates, reimported certificates, issued certificates, and challenges for domain validation. {{site.data.keyword.cloudcerts_short}} encrypts the endpoint and stores it securely.
{: shortdesc}

To add a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Settings**.
2. Open the **Notifications** tab.
3. Click **Add Notification Channel**.
4. Choose the type of notification channel that you want to use.
5. Enter the Webhook or Callback URL where you want to send notifications to.
6. Click **Save**. A summary of your configuration is displayed.

   **Example output**

   <table>
   <caption>Table 1. Information about the notification channel </caption>
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
    <td>The notification channel state. If set to disabled, no notifications are sent.</td>
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

    When you save a Slack Webhook, {{site.data.keyword.cloudcerts_short}} automatically sends a confirmation notification to the Slack channel that you configured. Check your Slack channel to verify that you received this notification.
    {: tip}
7. (Optional) Repeat these steps to add more notification channels.

## Testing a notification channel
{: #testing-channel}

You can test a notification channel to ensure that your notification channel is configured correctly.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

To test a notification channel, complete the following steps:

1. In the navigation on the service details page, click **Settings**.
2. Find your notification channel and click **Test Connection**.
3. Verify that you received a notification in the channel that you configured.

## Updating a notification channel
{: #updating-channel}

You can update your notification channel configuration, disable or enable notifications, or delete notification channels from {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Before you begin, [configure a notification channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

To update your notification channel, complete the following steps:

1. In the navigation on the service details page, click **Settings**.
2. Select the **Notifications** tab.
3. Choose from the following options:
   * To disable or enable notifications for a channel, set the switch to **Disable** or **Enable**.
   * To update settings for a channel, select **Edit** from the actions menu.
   * To delete a notification channel, select **Delete** from the actions menu.

## Verifying the HTTP payload for a Callback URL
{: #verify-callback}

Every HTTP payload that is sent from {{site.data.keyword.cloudcerts_short}} to your Callback URL is automatically signed according to the JWT standard by using an asymmetric key pair.  
{: shortdesc}

For every {{site.data.keyword.cloudcerts_short}} instance, a private and a public key is generated that are not shared across other {{site.data.keyword.cloudcerts_short}} instances. The private key is used to sign the HTTP payload, and you can use the public key to verify that the payload is generated by {{site.data.keyword.cloudcerts_short}} and is not altered by a third party.

To download the public key, complete the following steps:

1. From the navigation on the service details page, click **Settings**.
2. Open the **Notifications** tab.
3. Click the **Download Key** button. The key is downloaded as a PEM file.

## Channel versions
{: #channel-versions}

As Certificate Manager evolves, we might modify the format of the notifications payload structure from time to time. To ensure compatibility with earlier versions, the payload that is sent to your existing channels won’t change.   

If you have existing notification channels (Slack or Callback URL), to start getting the new version of the payload:

1. For Callback URL, make sure your implementation can accept the new payload.
2. Create a new notification channel (new channels are always created with the latest channel version).
3. Test that the new channel works correctly.
4. Delete the old channel.

For Channel versions check out the [API documentation](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Examples
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Learn how to create GitHub issues for expiring certificate notifications.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Learn how to create PagerDuty incidents issues for expiring certificate notifications.
