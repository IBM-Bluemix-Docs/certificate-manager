---

copyright:
  years: 2017, 2020
lastupdated: "2020-10-26"

keywords: certificates, SSL, private key security, encryption, tls, gdpr, ha, dr, high-availability, disaster recovery

subcollection: certificate-manager

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}



# Understanding high availability and disaster recovery for {{site.data.keyword.cloudcerts_short}}
{: #ha-dr}

{{site.data.keyword.cloudcerts_long}} is a highly available, regional service that runs in the following regions:

* Dallas (`us-south`)
* Frankfurt (`eu-de`)
* London (`eu-gb`)
* Sydney (`au-syd`)
* Tokyo (`jp-tok`)
* Washington (`us-east`)

In each supported region, the service exists in multiple availability zones with no single point of failure. Data is backed-up daily in the same region. However, because {{site.data.keyword.cloudcerts_short}} is a regional service, there is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.cloudcerts_short}} becomes unavailable in that location. To establish cross-region high availability and implement a recovery plan, you need to create and maintain backup instances in multiple regions.

To learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}, see [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime) or [Service Level Agreements](/docs/overview?topic=overview-slas).



## Manually backing up
{: #manual-backup}

To manually back up your certificates across regions, you must first have an instance of {{site.data.keyword.cloudcerts_short}} in another region. Then, use the following steps to ensure cross-region availability.

1. From the {{site.data.keyword.cloudcerts_short}} service UI, select **All certificates**.
2. Click **Download**.
3. Import your downloaded certificates to the newly created instance.

## Automatically backing up
{: #auto-backup}

Creating an automatic backup of your certificates is possible by automating the manual flow, which can be done in various ways. Check out some of the following examples to see whether one of them might work for you.

* Create a script that periodically downloads all of your certificates and then reimports them into your backup instance.
* Create a Callback URL notifications channel in {{site.data.keyword.cloudcerts_short}} that points to an IBM Cloud Functions action. Configure the action to listen for certificate lifecycle events such as reimport, order, or renewal. Then, when the action receives the event it downloads the certificate from one instance and imports it to the backup in a continuous fashion.

To learn about the various available certificate lifecycle event types see [Configuring notifications](/docs/certificate-manager?topic=certificate-manager-configuring-notifications). 
{: note}


