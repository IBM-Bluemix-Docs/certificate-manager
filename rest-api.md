---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Using the REST API
{: #using-rest-api}
The {{site.data.keyword.cloudcerts_full}} service provides REST endpoints to manage [certificates](#import-certificate) and [notification channels](#list-notification-channels). Using {{site.data.keyword.iamshort}}, you can also [assign policies for a specific certificate](#assigning-advanced-policies).
{: shortdesc}

## Testing APIs
{: #testing}

You can test REST endpoints by using Swagger or by running cURL requests in the command line.  
Swagger is available in the US-South {{site.data.keyword.Bluemix_notm}} region only.
{: shortdesc}

## Prerequisites
{: #prereq-api}

You must complete the following tasks before you can use {{site.data.keyword.cloudcerts_full}}.
{: shortdesc}

* Install the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) to obtain the  required data.

* When you work with the {{site.data.keyword.cloudcerts_short}} API, you can use the following variables in your calls.


<table>
<caption> Table 1. Command components explained </caption>
  <tr>
    <th> Component </th>
    <th> Explanation </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> You can obtain your {{site.data.keyword.iamshort}} (IAM) access token by logging in to {{site.data.keyword.Bluemix_notm}} and running the <code>ibmcloud iam oauth-tokens</code> command. </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> The [Cloud Resource Name (CRN)-based instance ID](/docs/overview/crn.html#format) that is assigned to your service instance after it is created. You can retrieve the instance ID in the following ways:
    <ul>
      <li>In the <strong>Manage</strong> page of the service.</li>
      <li>Run the <code>ibmcloud resource service-instance</code> command, replacing <i>&lt;Instance_Name&gt;</i> with the name of your service instance.
      <pre>ibmcloud resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Call the {{site.data.keyword.Bluemix_notm}} Resource Controller <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST endpoint, which requires the <code>Authorization</code> header with your account administrator's IAM token.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td> <code>certificateId</code> </td>
    <td> The [Cloud Resource Name (CRN)-based certificate ID](/docs/overview/crn.html#format) that is assigned to your certificate after it is imported. You can find your certificate ID by using one of the following options: <ul><li> In the <strong>Manage</strong> tab of the service, view the certificate information by selecting it in the <strong>Certificates</strong> table. <li> By using the API to [list your available certificates](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> The account ID of the user that manages the {{site.data.keyword.Bluemix_notm}} account. You can find your account ID by running the <code>ibmcloud info</code> command. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> The URL of the service in the {{site.data.keyword.Bluemix_notm}} region in which it was created. You can find the URL in the Swagger UI. </td>
  </tr>
  <tr>
    <td>  <code> name (Optional) </code> </td>
    <td> The display name for the imported certificate. </td>
  </tr>
  <tr>
    <td> <code> description (Optional) </code> </td>
    <td> The description for the imported certificate. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> The certificate data, escaped. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> The private key data, escaped. </td>
  </tr>
  <tr>
    <td> <code> intermediate (Optional) </code> </td>
    <td> The intermediate certificate data, escaped. </td>
  </tr>
  <tr>
    <td> <code> channelId </code> </td>
    <td> The UUID that is assigned to your notification channel after it is created.
    You can find your notification channel ID by [list all available notification channels](#list-notification-channels).</td>
  </tr>
  <tr>
      <td>  <code> type </code> </td>
      <td> The notification channel type. The only available value is <code>slack</code>.</td>
    </tr>
    <tr>
      <td> <code> endpoint </code> </td>
      <td> The notification channel endpoint that you want to send the notifications to.</td>
    </tr>
    <tr>
      <td> <code> is_active </code> </td>
      <td> The notification channel state, the value can be <code>true</code> or <code>false</code>.</td>
    </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>The ID of the user that you want to assign an access policy to. To find the user ID, see [Retrieving the user ID](#retrieve-user-id). </td>
  </tr>
</table>

## Importing a certificate
{: #import-certificate}  

Import a certificate in Privacy-enhanced Electronic Mail (PEM) format with its private key. You can also import an intermediate certificate.
{: shortdesc}


Run the following `curl` command:

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_,  _&lt;privateKey&gt;_, and _&lt;intermediate&gt;_ with the appropriate values. The _&lt;name&gt;_, _&lt;description&gt;_, and _&lt;intermediate&gt;_ values are optional.


## Updating certificate metadata
{: #update-certificate-metadata}  

Update a certificate’s optional `name`, `description`, or both, properties.

**Note**: Update operations are limited to five actions per minute.  
{: shortdesc}

Run the following `curl` command:

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/certificate/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, and _&lt;description&gt;_ with the appropriate values.


## Listing all of your certificates
{: #list-certificates}  

Retrieve a list of all of your available certificates.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```
  {: codeblock}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, and _&lt;instanceId&gt;_ with the appropriate values.


## Downloading a certificate
{: #get-certificate}  

Use a retrieved certificate ID to download the certificate data.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```
  {: codeblock}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, and _&lt;certificateId&gt;_ with the appropriate values.


## Deleting a certificate
{: #delete-certificate}  

Use a retrieved certificate ID to delete the certificate and its data.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```
  {: codeblock}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, and _&lt;certificateId&gt;_ with the appropriate values.


## Listing all of your notification channels
{: #list-notification-channels}

Retrieve a list of all of your notification channels.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/instances/<instanceId>/notifications/channels
  ```
  {: codeblock}

Replace _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, and _&lt;instanceId&gt;_ with the appropriate values.


## Adding a notification channel
{: #import-certificate}

Add a notification channel where you will receive notifications about expiring certificates.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -X PUT \
  https://<cluster-url>/api/v1/instances/<instanceId>/notifications/channels \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"type":"<type>",
	"endpoint":"<endpoint>",
	"is_active":<is_active>
  }'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;type&gt;_, _&lt;endpoint&gt;_, and
 _&lt;is_active&gt;_ with the appropriate values.


## Updating a notification channel endpoint
{: #update-notification-channel}

Update a notification channel endpoint property.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/instances/<instanceId>/notifications/<channelId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
      	"endpoint":"<endpoint>"
        }'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;channelId&gt;_, _&lt;IAM-token&gt;_, and _&lt;endpoint&gt;_ with the appropriate values.


## Enable or disable notification channels
{: #enable-disable-notification-channels}

Enable or disable a notification channel. If a channel is disabled, no notifications are sent to the channel.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -X PUT \
  https://<cluster-url>/api/v1/instances/<instanceId>/notifications/<channelId>/state \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
      	"enabled":true/false
        }'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;channelId&gt;_, and _&lt;IAM-token&gt;_ with the appropriate values.


## Deleting a notification channel
{: #delete-notification-channel}

Delete a notification channel.
{: shortdesc}

Run the following `curl` command:

  ```
  curl -X DELETE \
  https://<cluster-url>/api/v1/instances/<instanceId>/notifications/<channelId> \
  -H 'authorization: Bearer <IAM-token>'
  ```
  {: codeblock}

Replace _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;channelId&gt;_, and _&lt;IAM-token&gt;_ with the appropriate values.
