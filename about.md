---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-30"

keywords: certificates, SSL,

subcollection: certificate-manager

---

{:new_window: target="_blank"}
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

{{site.data.keyword.cloudcerts_full}} helps you to obtain, store and manage SSL certificates for your {{site.data.keyword.cloud_notm}}-based apps.
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

When you import or order a certificate into {{site.data.keyword.cloudcerts_short}}, the service uses an Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key. {{site.data.keyword.cloudcerts_short}} saves this unique encrypted key to use with your service instance.

## Integrations
{: #integrations}

<table>
<caption>Table 1. {{site.data.keyword.cloud_notm}} services that use {{site.data.keyword.cloudcerts_short}}</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>You can easily and securely deploy custom domain TLS certificates from {{site.data.keyword.cloudcerts_short}} to your Kubernetes cluster. Cluster admins can use the [Kubernetes Service plug-in commands](/docs/containers?topic=containers-cs_cli_reference) to update TLS certificates as Kubernetes secrets with a new certificate without causing downtime. To get started, check out the [Ingress annotations in the documentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) centralizes the information about {{site.data.keyword.cloud_notm}} services. The information includes the indication of expired certificates and certificates that are about to expire in instances of {{site.data.keyword.cloudcerts_short}} in your {{site.data.keyword.cloud_notm}} account. [Learn more about {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>You can use [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) to track how users and applications interact with the {{site.data.keyword.cloudcerts_long_notm}} service in the {{site.data.keyword.cloud_notm}}.
    <p>To get the list of actions that generate an event, see [{{site.data.keyword.at_short}} events](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Store your custom domain certificates in the {{site.data.keyword.cloudcerts_short}} service, then use certificate CRNs to bind with custom domains in {{site.data.keyword.apiconnect_short}}. [Learn more about {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index).</p></td>
  </tr>
</table>

## Availability
{: #availability}

{{site.data.keyword.cloudcerts_short}} is available in the Dallas, London, Frankfurt, and Tokyo locations.



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
