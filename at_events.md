---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: certificates, SSL, TLS, activity tracker,

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

# Activity Tracker events  
{: #at_events}

Use the {{site.data.keyword.at_full}} service to track how users and applications interact with the {{site.data.keyword.cloudcerts_long}} service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

The {{site.data.keyword.at_short}} service records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. For example, when you import a certificate, an event is generated. For more information, see the [{{site.data.keyword.at_short}} docs](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

The following table lists the API methods that generate an event when they are called.

<table>
  <caption>Table 1. Actions that generate events</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Import a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Reimport a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>Order a certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.renew`</td>
	  <td>Renew an issued certificate.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>Get a certificate metadata.</td>
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
{: #at_ui}

Provision an {{site.data.keyword.at_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.

Complete the following steps:

1. Go to [{{site.data.keyword.cloud_notm}} Observability](https://cloud.ibm.com/observe/){: external}.
2. Provision a {{site.data.keyword.at_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.

Events are automatically forwarded to the {{site.data.keyword.at_short}} service instance in the same location where the {{site.data.keyword.cloudcerts_short}} service is provisioned.

## Additional information
{: #info}

* The field *requestData_str* includes the human readable name of the certificate.

## Availability
{: #at-availability}

{{site.data.keyword.at_short}} support is available for the **Dallas**, **Frankfurt**, **Tokyo** and **London** locations.
