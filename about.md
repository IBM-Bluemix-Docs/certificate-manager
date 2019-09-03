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

# About {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_full}} helps you to obtain, store and manage SSL certificates that you use for {{site.data.keyword.cloud_notm}} deployments, or other Cloud and on-prem deployments.
{: shortdesc}

You can import SSL certificates that you obtain for your apps and services, store them securely, and get a central view of the certificates that you are using. Or, you can order public certificates through Certificate Manager from supported CAs.

You can manage your certificates in the following ways:

* Get notified before your certificates expire to ensure that you renew them on time  
* Use notifications to trigger automated certificate renewal  
* View the types of certificates across your deployments and ensure that they meet organization policies  
* Find certificates that need replacing when new compliance or security requirements are issued  
* Set controls on who can access and manage your certificates
* Order new public certificates


![High-level service architecture diagram](images/high-level-architecture.png)
<caption>Figure 1. High-level service architecture.</caption>



## Private key security
{: #private-key-security}

{{site.data.keyword.cloudcerts_short}} uses the [envelope encryption methodology](/docs/services/key-protect/concepts?topic=key-protect-envelope-encryption), where a root certificate is stored in, and never leaves, {{site.data.keyword.keymanagementservicelong_notm}}, which is also backed by HSM.

In addition, a per tenant managed encryption key is used to encrypt the certificates and private keys before they are stored to the database. As part of the encryption chain, {{site.data.keyword.cloudcerts_short}} uses the Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key.



## Availability
{: #availability}

{{site.data.keyword.cloudcerts_short}} is available in the Dallas, London, Frankfurt, Tokyo and Sydney locations.



## Limits
{: #limits}

You can upload a maximum of 1000 certificates per instance.



## Compliance and standards
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} has successfully completed several certifications and audits and meets several important standards.

### HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} meets the required IBM controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements.

### International Organization for Standardization (ISO)
{: #compliance-iso}

* {{site.data.keyword.IBM_notm}} Services (PaaS and SaaS) certificate - ISO 27001

### General Data Protection Regulation (GDPR)
{: #compliance-gdpr}

The GDPR seeks to create a harmonized data protection law framework across the EU and aims to give citizens back the control of their personal data, while imposing strict rules on those hosting and ‘processing’ this data, anywhere in the world. The Regulation also introduces rules relating to the free movement of personal data within and outside the EU. For more information, see the [IBM privacy statement](https://www.ibm.com/privacy/).


