---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

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




# High availability and disaster recovery
{: #ha-dr}

High availability and disaster recovery for {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* The {{site.data.keyword.cloudcerts_short}} service is a highly available, regional, service. In each supported location, the service exists in multiple availability zones with no single point of failure.
* Data that is stored in the {{site.data.keyword.cloudcerts_short}} database is backed-up daily in same region. If a recovery of a location is necessary, the data is available to be restored. However, {{site.data.keyword.cloudcerts_short}} does not provide cross-regional failover. If a regional disaster occurs, data might not be recoverable. It is recommended that you create and maintain backup instances in other regions.


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

To learn about the various available certificate lifecycle event types see [Configuring notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications). 
{: note}


## Restoring a deleted service instance
{: #restore-instance}

After you delete an instance of the {{site.data.keyword.cloudcerts_short}} service, you can restore the deleted service instance within the data retention period of seven days. After the seven-day period expires, the service instance is permanently deleted.

To view which service instances are available for restoration, use the `ibmcloud resource reclamations` command. To restore a deleted service, use the `ibmcloud resource reclamation-restore` command.

Learn more about [managing resources](/docs/resources?topic=resources-manage_resource).
{: note}
