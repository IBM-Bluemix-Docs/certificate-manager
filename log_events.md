---

copyright:
  years: 2017, 2020
lastupdated: "2020-04-08"

keywords: certificates, ssl, tls, logging, activity, monitor app, monitor certificates

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




# Log Analysis events
{: #log_events}

Use the {{site.data.keyword.la_full}} service to view {{site.data.keyword.cloudcerts_long}} service logs for your instance in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

{{site.data.keyword.la_full_notm}} offers administrators, DevOps teams, and developers advanced features to filter, search, and tail log data, define alerts, and design custom views to monitor application and system logs. For more information, see the [{{site.data.keyword.la_short}} docs](/docs/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started).

## Where to look for the logs
{: #log_ui}

Provision an {{site.data.keyword.at_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.

Complete the following steps:

1. Go to [{{site.data.keyword.cloud_notm}} Observability](https://cloud.ibm.com/observe/).
2. Provision a {{site.data.keyword.la_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.
3. Click **Configure platform service logs**, select the region and the instance that you provisioned in step 2.


## Availability
{: #la-availability}

{{site.data.keyword.la_short}} support is available for the **Dallas**, **London**, **Frankfurt**, **Tokyo**, and **Sydney** locations.


