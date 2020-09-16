---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-16"

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
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:script: data-hd-video='script'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:video: .video}




# Compliance and standards
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} has successfully completed several certifications and audits and meets several important standards.

## Private key security
{: #private-key-security}

{{site.data.keyword.cloudcerts_short}} uses the [envelope encryption methodology](/docs/key-protect/concepts?topic=key-protect-envelope-encryption), where a root key is stored in, and never leaves, {{site.data.keyword.keymanagementservicelong_notm}}, which is also backed by HSM.

In addition, a per tenant-managed encryption key is used to encrypt the certificates and private keys before they are stored in the database. As part of the encryption chain, {{site.data.keyword.cloudcerts_short}} uses the Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key.

## HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} meets the required IBM controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements.

## Payment Card Industry (PCI)
{: #compliance-pci}
{{site.data.keyword.cloudcerts_short}} is compliant with the PCI data security standards.

## International Organization for Standardization (ISO)
{: #compliance-iso}

* {{site.data.keyword.IBM_notm}} Services (PaaS and SaaS) certificate - ISO 27001

## General Data Protection Regulation (GDPR)
{: #compliance-gdpr}

The EU seeks to give their citizens control over their personal data by creating harmonized data protection. To do so, they use a law framework, which is known as the GDPR, to impose strict rules on those who host and process data; regardless of where they're located. The regulation also introduces rules that relate to the free movement of personal data within and outside the EU. For more information, see [IBM privacy statement](https://www.ibm.com/privacy/).