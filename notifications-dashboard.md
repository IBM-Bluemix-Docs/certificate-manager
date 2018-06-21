---

copyright:
  years: 2018
lastupdated: "2018-06-21"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring notifications for expiring certificates from the dashboard
{: #configuring-notifications-for-expiring-certificates-from-the-dashboard}

Certificates are typically valid only for a set period of time. When deployed certificates expire, outages can occur. Therefore it is important to renew certificates on time, and deploy the renewed certificates in place of the old ones.

{{site.data.keyword.cloudcerts_full}} sends you Slack notifications when the certificates you upload to {{site.data.keyword.cloudcerts_short}} are about to expire. You are notified 90 days, 60 days, 30 days, 10 days, and one day before certificates expire, and after a certificate expires.

To start receiving notifications, you must configure a Slack channel to which notifications can be posted. Therefore, you must create a Slack channel, and a webhook for that channel, by following the [Slack documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://api.slack.com/incoming-webhooks).
{: shortdesc}


## Adding a channel
{: #adding-channel}

After you create a Slack webhook, you must add it to {{site.data.keyword.cloudcerts_short}} so that you start to receive notifications in Slack about expiring certificates. {{site.data.keyword.cloudcerts_short}} encrypts the webhook and stores it securely.
{: shortdesc}

To add a notification channel:

1. Click **Settings** in the left navigation, and open the **Notifications** tab.
2. Click **Add Notification Channel** and provide the following details:

   * Select the channel type from the provided list.
   * Enter the channel endpoint (URL) into the text field.

3. Click **Save**.

After you click **Save**, {{site.data.keyword.cloudcerts_short}} sends a confirmation notification to Slack if your channel is configured correctly. Check your Slack channel for this notification.

After you add a notification channel, the following information is displayed.

<table>
<caption> Table 1. Information about the notification channel </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Type</td>
    <td>The notification channel type: Slack</td>
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
    <td>Sends a test notification to your channel.</td>
  </tr>
    <tr>
      <td>Dots menu</td>
      <td>Available actions that you can perform on the channel: <i>edit</i> or <i>delete</i></td>
    </tr>
</table>

You can add multiple Slack channels if you choose.


## Testing a channel
{: #testing-channel}

Testing a channel ensures that your notification channel is configured correctly.
{: shortdesc}

To test a notification channel, click the **Test Connection** button for the required channel and check your Slack channel to see if you receive a test notification.


## Disabling a channel
{: #disabling-channel}

To stop sending notifications to a channel, you can disable the channel.
{: shortdesc}

To disable the channel, click the toggle in the relevant channel row. You can also enable a channel again by clicking the toggle.


## Updating a channel
{: #updating-channel}

You can update the endpoint of your channel.
{: shortdesc}

1. To update the endpoint of a channel, click the Dots menu on the relevant row and select **Edit**.
2. To save your changes, click **Save** or click **Cancel** to revert your changes.
3. After you click **Save**, check your Slack channel for a test notification.


## Deleting a channel
{: #deleting-channel}

You can delete any of the channels.
{: shortdesc}

To delete the endpoint for a channel, click the Dots menu on the relevant row and select **Delete**.
