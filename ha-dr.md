---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-19"

keywords: certificates, SSL, private key security, encryption, tls, gdpr, ha, dr, high-availability, disaster recovery

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



# Compliance and standards
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} has successfully completed several certifications and audits and meets several important standards.

## Private key security
{: #private-key-security}

{{site.data.keyword.cloudcerts_short}} uses the [envelope encryption methodology](/docs/services/key-protect/concepts?topic=key-protect-envelope-encryption), where a root certificate is stored in, and never leaves, {{site.data.keyword.keymanagementservicelong_notm}}, which is also backed by HSM.

In addition, a per tenant-managed encryption key is used to encrypt the certificates and private keys before they are stored in the database. As part of the encryption chain, {{site.data.keyword.cloudcerts_short}} uses the Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key.

## HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} meets the required IBM controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements.

## International Organization for Standardization (ISO)
{: #compliance-iso}

* {{site.data.keyword.IBM_notm}} Services (PaaS and SaaS) certificate - ISO 27001

## General Data Protection Regulation (GDPR)
{: #compliance-gdpr}

The EU seeks to give their citizens control over their personal data by creating harmonized data protection. To do so, they use a law framework, which is known as the GDPR, to impose strict rules on those who host and process data; regardless of where they're located. The regulation also introduces rules that relate to the free movement of personal data within and outside the EU. For more information, see [IBM privacy statement](https://www.ibm.com/privacy/).


## High availability and disaster recovery
{: #ha-dr}

High availability and disaster recovery for {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* The {{site.data.keyword.cloudcerts_short}} service is a highly available, regional, service. In each supported location, the service exists in multiple availability zones with no single point of failure.
* Data that is stored in the {{site.data.keyword.cloudcerts_short}} database is backed-up daily in same region. If a recovery of a location is necessary, the data is available to be restored. However, {{site.data.keyword.cloudcerts_short}} does not provide cross-regional failover. If a regional disaster occurs, data might not be recoverable. It is recommended that you create and maintain backup instances in other regions.


### Manually backing up
{: #manual-backup}

To manually back up your certificates across regions, you must first have an instance of {{site.data.keyword.cloudcerts_short}} in another region. Then, use the following steps to ensure cross-region availability.

1. From the {{site.data.keyword.cloudcerts_short}} service UI, select **All certificates**.
2. Click **Download**.
3. Import your downloaded certificates to the newly created instance.

### Automatically backing up
{: #auto-backup}

Creating an automatic backup of your certificates is possible by automating the manual flow, which can be done in various ways. Check out some of the following examples to see whether one of them might work for you.

* Create a script that periodically downloads all of your certificates and then reimports them into your backup instance.
* Create a Callback URL notifications channel in {{site.data.keyword.cloudcerts_short}} that points to an IBM Cloud Functions action. Configure the action to listen for certificate lifecycle events such as reimport, order, or renewal. Then, when the action receives the event it downloads the certificate from one instance and imports it to the backup in a continuous fashion.

To learn about the various available certificate lifecycle event types see [Configuring notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications). 
{: note}
