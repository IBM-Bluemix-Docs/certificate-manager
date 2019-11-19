---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-19"

keywords: certificates, ssl, tls, logging, activity, monitor app, monitor certificates

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

# Log Analysis events
{: #log_events}

Use the {{site.data.keyword.la_full}} service to view {{site.data.keyword.cloudcerts_long}} service logs for your instance in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

{{site.data.keyword.la_full_notm}} offers administrators, DevOps teams, and developers advanced features to filter, search, and tail log data, define alerts, and design custom views to monitor application and system logs. For more information, see the [{{site.data.keyword.la_short}} docs](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started).

## Where to look for the logs
{: #log_ui}

Provision an {{site.data.keyword.at_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.

Complete the following steps:

1. Go to [{{site.data.keyword.cloud_notm}} Observability](https://cloud.ibm.com/observe/).
2. Provision a {{site.data.keyword.la_short}} instance in the same location as your {{site.data.keyword.cloudcerts_short}} instance.
3. Click **Configure platform service logs**, select the region and the instance that you provisioned in step 2.


## Availability
{: #la-availability}

{{site.data.keyword.la_short}} support is available for the **Dallas**, **Frankfurt**, **Tokyo**, **London**, and **Sydney** locations.
