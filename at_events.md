---

copyright:
  years: 2018
lastupdated: "2018-10-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}} events  
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.cloudcerts_long}} service in the {{site.data.keyword.Bluemix}}.
{:shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.Bluemix_notm}}. For more information, see [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). For example, when you import a certificate, an {{site.data.keyword.cloudaccesstrailshort}} event is generated.

The following table lists the API methods that generate an event when they are called:

<table>
  <caption>Actions that generate events</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Import a certificate that is issued by a third-party certificate authority.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Download a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>List certificates.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>List certificates metadata. Show details of a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Search certificates.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Search certificates metadata.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Delete a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Update certificate metadata, for example, change the description of a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>List notifications channels.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Create a notifications channel.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Disable or enable a notifications channel.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Update a notifications channel's endpoint.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Delete a notifications channel.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Test a notifications channel.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>A notification was sent to a notifications channel endpoint.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>The public key was requested.</td>
  </tr>
</table>

## Where to look for the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.

{{site.data.keyword.cloudaccesstrailshort}} events are automatically forwarded to the {{site.data.keyword.cloudaccesstrailshort}} service in the same region where the {{site.data.keyword.cloudcerts_short}} service is provisioned.

## Additional information
{: #info}

The field *requestData_str* includes the human readable name of the certificate.
