---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring notifications for expiring certificates from the dashboard
{: #configuring-notifications-for-expiring-certificates-from-the-dashboard}

Certificates are typically valid only for a set period of time. When deployed certificates expire, outages can occur. Therefore it is important to renew certificates on time, and deploy the renewed certificates in place of the old ones.

{{site.data.keyword.cloudcerts_full}} will send you Slack notifications when the certificates you upload to certificate manager are about to expire. You will be notified 90, 60, 30, 10, and 1 days before certificates expire, and once a certificate expires.

To start receiving notifications, you need to configure a Slack channel where notifications will be posted to. For that you need to create a Slack channel, and a webhook for that channel, following the [Slack documentation](https://api.slack.com/incoming-webhooks).

{: shortdesc}

## Adding a channel
{: #adding-channel}

Once you have a Slack webhook, you can add the Slack webhook to Certificate Manager to start receiving notifications in Slack about expiring certificates. Certificate Manager will encrypt the webhook that you provide so that.
{: shortdesc}

To add a notification channel:

1. Click **Settings** in the left navigation, and view the **Notifications** tab
2. Click the **Add Notification Channel** button and provide the following details:

   * Select the channel type from the provided list
   * Enter the channel endpoint (URL) into the text field

3. Click the **Save** button

Once you click 'Save,' Certificate Manager will send a confirmation notification to Slack if your channel was configured correctly. Check your Slack channel for this notification.

After you add a notification channel, the following information is displayed.

<table>
<caption> Table 1. Information about the notification channel </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Type</td>
    <td>Notification channel type - <i>Slack</i></td>
  </tr>
  <tr>
    <td>Endpoint</td>
    <td>Notification channel endpoint - where the notifications will be sent to.</td>
  </tr>
  <tr>
    <td>Enablment Toggle</td>
    <td>Notification channel state - if set to disabled no notifications are sent.</td>
  </tr>
  <tr>
    <td>Test Connection Button</td>
    <td>Sends a test notification to your channel.</td>
  </tr>
    <tr>
      <td>Dots Menu</td>
      <td>Available actions to be performed on the channel - edit or delete</td>
    </tr>
</table>

You can add multiple Slack channels if you choose.


## Testing a channel
{: #testing-channel}

Helps you ensure that your notification channel is configured correctly.
{: shortdesc}

To test a notification channel, simply click the **Test Connection** button for the required channel and check your Slack channel to see if you received a test notification.

## Disabling a channel
{: #disabling-channel}
You can disable each channel to stop sending notifications to that channel.
{: shortdesc}

To disable the channel click the toggle in the relevant channel row. You can also enable a channel again after disabling it by clicking the toggle to 'enable.'

## Updating a channel
{: #updating-channel}

You can update the endpoint of your channel.
{: shortdesc}

To update the endpoint of a channel, click the dots menu on the relevant row and select the **Edit** option.
The endpoint field should now be editable. To save your changes click the **Save** button,
or click the **Cancel** button to revert your changes. When you click **Save**
check your Slack channel for a test notification.
## Deleting a channel
{: #updating-channel}

You can delete any of the channels.
{: shortdesc}

To delete the endpoint for a channel, click the dots menu on the relevant row and select the **Delete** option.
