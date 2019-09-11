---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-10"

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



# Compliance and standards
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} has successfully completed several certifications and audits and meets several important standards.

## Private key security
{: #private-key-security}

{{site.data.keyword.cloudcerts_short}} uses the [envelope encryption methodology](/docs/services/key-protect/concepts?topic=key-protect-envelope-encryption), where a root certificate is stored in, and never leaves, {{site.data.keyword.keymanagementservicelong_notm}}, which is also backed by HSM.

In addition, a per tenant managed encryption key is used to encrypt the certificates and private keys before they are stored to the database. As part of the encryption chain, {{site.data.keyword.cloudcerts_short}} uses the Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key.

## HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} meets the required IBM controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements.

## International Organization for Standardization (ISO)
{: #compliance-iso}

* {{site.data.keyword.IBM_notm}} Services (PaaS and SaaS) certificate - ISO 27001

## General Data Protection Regulation (GDPR)
{: #compliance-gdpr}

The GDPR seeks to create a harmonized data protection law framework across the EU and aims to give citizens back the control of their personal data, while imposing strict rules on those hosting and ‘processing’ this data, anywhere in the world. The Regulation also introduces rules relating to the free movement of personal data within and outside the EU. For more information, see the [IBM privacy statement](https://www.ibm.com/privacy/).

## High availability and disaster recovery
{: #ha-dr}

High availability and disaster recovery for {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

* The {{site.data.keyword.cloudcerts_short}} service is a highly available, regional, service. In each supported location, the service exists in multiple availability zones with no single point of failure.
* Data that is stored in the {{site.data.keyword.cloudcerts_short}} database is backed-up daily. If a recovery of a location is required, the data is available to be restored. Note, however, that {{site.data.keyword.cloudcerts_short}} does not provide cross regional failover. In cases of regional disaster data might not be recoverable. You are advised to create backup instances in alternate regions.
