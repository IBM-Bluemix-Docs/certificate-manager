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

You can use the {{site.data.keyword.cloudcerts_full}} service dashboard to manage notification channels,
where you will be notified on about to expire certificates. Notifications will be sent on predefined times - 90, 60, 10, 1 days prior to the cert expiration date and once when the certificate is expired.
{: shortdesc}

## Adding a channel
{: #adding-channel}

To help you to manage your certificates, you can add notification channels where you will be notified when certificates are about to expire.
{: shortdesc}

To add a notification channel:

1. Click **Setting** in the left navigation, then select the **Notifications** tab
2. Click the **Add Notification Channel** button and provide the following details:

  *. Select the channel type from the provided list
  *. Enter the channel endpoint (URL) into the text field

3. Click the **Save** button

After you add a notification channel, the following information is displayed.

<table>
<caption> Table 1. Information about the notification channel </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Type</td>
    <td>Notification channel type. Optional values are <i>Slack</i> or <i>Callback URL</i>.</td>
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
      <td>Available actions to be performed on the channel.</td>
    </tr>
</table>


## Testing a channel
{: #testing-channel}

Helps you ensure the notification channel is configured correctly.
{: shortdesc}

To test a notification channel, simply click the **Test Connection** button for the required channel and wait for a meesage to arrive.
> If an error will occur you will be notified on screen.

## Disabling a channel
{: #disabling-channel}
You can disable / enable each channel to stop sending notifications to that channel.
{: shortdesc}

To disable / enable the channel click the toggle in the relevant channel row.

## Updating a channel
{: #updating-channel}

You can update the endpoint of your channel.
{: shortdesc}

To update the endpoint of a channel, click the dots menu on the relevant row and select the **Edit** option.
The endpoint field should now be editable.
To save your changes click the **Save** button, or click the **Cancel** button to revert your changes.

## Deleting a channel
{: #updating-channel}

You can delete any of the channels.
{: shortdesc}

To delete the endpoint of a channel, click the dots menu on the relevant row and select the **Delete** option.
