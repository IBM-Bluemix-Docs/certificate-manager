---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-03"

keywords: certificates, SSL, 

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


# High availability and disaster recovery
{: #ha-dr}

High availability and disaster recovery for {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* The {{site.data.keyword.cloudcerts_short}} service is a highly available, regional, service. In each supported location, the service exists in multiple availability zones with no single point of failure.
* Data that is stored in the {{site.data.keyword.cloudcerts_short}} database is backed-up daily. If a recovery of a location is required, the data is available to be restored. Note, however, that {{site.data.keyword.cloudcerts_short}} does not provide cross regional failover. In cases of regional disaster data might not be recoverable. You are advised to create backup instances in alternate regions.


