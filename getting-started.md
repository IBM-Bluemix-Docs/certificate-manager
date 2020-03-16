---

copyright:
  years: 2017, 2020
lastupdated: "2020-03-16"

keywords: certificates, ssl, tls, import certificate, tutorial, order certificate, cert

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
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Getting started tutorial
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} helps you to obtain, store, and manage SSL/TLS certificates for your {{site.data.keyword.cloud_notm}}-based apps. Get started by creating a new {{site.data.keyword.cloudcerts_short}} service instance by completing the following steps.
{: shortdesc}

To create an instance from the {{site.data.keyword.cloud_notm}} console:

1.	In the {{site.data.keyword.cloud_notm}} catalog, select **{{site.data.keyword.cloudcerts_short}}**.
2.	Give your service instance a name, or use the preset name.
3.	Click **Create**.
4.	To import your organization's certificates into **{{site.data.keyword.cloudcerts_short}}**, click **Import Certificate**.
5.	To order a new certificate, click **Order Certificate**.

<br/>
To create an instance from the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started):

1. Log in to {{site.data.keyword.cloud_notm}} and follow the on-screen instructions.

   ```
   ibmcloud login
   ```

2. Create an instance.

   ```
   ibmcloud resource service-instance-create "My {{site.data.keyword.cloudcerts_short}} instance" cloudcerts free us-south
   ```

   - Replace **My {{site.data.keyword.cloudcerts_short}} instance** with your choice of instance name.
   - Replace **us-south** with either **us-south** (Dallas), **eu-gb** (London), **eu-de** (Frankfurt), **jp-tok** (Tokyo), or **au-syd** (Sydney).

<br/>

[Learn more](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) about what you get from {{site.data.keyword.cloudcerts_short}}, and [provide user feedback in {{site.data.keyword.IBM_notm}} Developer](/docs/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) to enhance {{site.data.keyword.cloudcerts_short}} as it develops. To find out about what's new in the service, see [Release notes](/docs/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}
