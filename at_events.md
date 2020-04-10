---

copyright:
  years: 2017, 2020
lastupdated: "2020-04-10"

keywords: activity, events, order certificates, import certificates, renew certificates, list certificates, issued, search certificates, certificates, certificate metadata

subcollection: certificate-manager

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:script: data-hd-video='script'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}



# Auditing events for {{site.data.keyword.cloudcerts_short}} 
{: #at_events}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full}} service to track how users and applications interact with the {{site.data.keyword.cloudcerts_long}} service in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

The {{site.data.keyword.at_short}} service records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. For example, when you import a certificate, an event is generated. For more information, see the [{{site.data.keyword.at_short}} docs](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## Certificate events
{: #at-cert-events}

The following table lists the certificate actions that generate an event:

| Action                                           | Description                                                    |
| ------------------------------------------------ | -------------------------------------------------------------- |
| `cloudcerts.certificate.import`                  | Import a certificate.                                          |
| `cloudcerts.certificate.reimport`                | Reimport a certificate.                                        |
| `cloudcerts.certificate.order`                   | Order a certificate.                                           |
| `cloudcerts.certificate-order-autorenew.set-on`  | Enable auto-renewal for a certificate.                         |
| `cloudcerts.certificate-order-autorenew.set-off` | Disable auto-renewal for a certificate.                        |
| `cloudcerts.certificate.renew`                   | Renew a certificate.                                           |
| `cloudcerts.certificate.issued`                  | Request to import, order, or renew a certificate is processed. |
| `cloudcerts.certificates.read`                   | List certificates.                                             |
| `cloudcerts.certificates.search`                 | Search certificates.                                           |
| `cloudcerts.certificate-metadata.read`           | Get certificate metadata.                                      |
| `cloudcerts.certificates-metadata.search`        | Search certificate metadata.                                   |
| `cloudcerts.certificate-metadata.update`         | Update certificate metadata.                                   |
| `cloudcerts.certificate.download`                | Download a certificate.                                        |
| `cloudcerts.certificate.delete`                  | Delete a certificate.                                          |
{: caption="Table 1. {{site.data.keyword.cloudcerts_short}} actions that generate Activity Tracker events" caption-side="top"}

## Notification channel events
{: #at-notification-events} 

The following table lists the notification channel actions that generate an event:

| Action                                            | Description                                      |
| ------------------------------------------------- | ------------------------------------------------ |
| `cloudcerts.notification-channel.create`          | Create a notification channel.                   |
| `cloudcerts.notification-channels.list`           | List notification channels.                      |
| `cloudcerts.notification-channel.test`            | Test a notification channel.                     |
| `cloudcerts.notification-channel.set-on`          | Enable a notification channel.                   |
| `cloudcerts.notification-channel.set-off`         | Disable a notification channel.                  |
| `cloudcerts.notification-channel.update`          | Update a notification channel.                   |
| `cloudcerts.notification-channel.delete`          | Delete a notification channel.                   |
| `cloudcerts.notification.send`                    | Notification is sent to a channel.               |
| `cloudcerts.notification-channels-publickey.read` | Request a public key for a notification channel. |
{: caption="Table 2. {{site.data.keyword.cloudcerts_short}} actions that generate Activity Tracker events" caption-side="top"}

## Viewing events
{: #at-ui}

Events that are generated by a {{site.data.keyword.cloudcerts_short}} service instance are forwarded automatically to the {{site.data.keyword.at_full_notm}} instance that is available in the same location. 

{{site.data.keyword.at_short}} support is available in the Dallas, London, Frankfurt, Tokyo, and Sydney locations.
{: preview} 

To view {{site.data.keyword.cloudcerts_short}} events:

1. Log in to the {{site.data.keyword.cloud_notm}} console.
2. Go to &#x2630; **IBM Cloud** &gt; **Observability** to access your [Observability dashboard](https://{DomainName}/observe){: external}.
3. From the left navigation menu, click **Activity Tracker**.
4. Select an {{site.data.keyword.at_short}} instance, and click **View LogDNA** to launch the web UI.

   Don't have an {{site.data.keyword.at_short}} instance? Create an instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance so that service events are forwarded automatically to your account. To learn more, check out the [{{site.data.keyword.at_short}} docs](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).

## Analyzing events
{: #at-analyze-events}

The `requestData` and `responseData` objects in each {{site.data.keyword.at_short}} event show identifying information about your certificate, such as its corresponding domains, certificate ID, and expiration time. If an initiator updates, renews, or downloads a specific certificate, the {{site.data.keyword.at_short}} also shows the human-readable name of the certificate in the `target.name` field of the event log.