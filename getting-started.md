---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-22"

keywords: getting started tutorial, getting started, Certificate Manager, certificates, ssl, tls, import certificate, tutorial, order certificate, cert

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



# Getting started with {{site.data.keyword.cloudcerts_short}}
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} helps you to obtain, store, and manage SSL/TLS certificates that you use for cloud or on-premises deployments. Get started by creating a new service instance by completing the following steps.
{: shortdesc}

## Provisioning an instance of {{site.data.keyword.cloudcerts_short}} with the console
{: #provision-certificate-manager-console}

You can provision a public instance of {{site.data.keyword.cloudcerts_short}} with the {{site.data.keyword.cloud_notm}} console by completing the following steps.

1.	In the {{site.data.keyword.cloud_notm}} catalog, select **{{site.data.keyword.cloudcerts_short}}**.
2.	Give your service instance a name, or use the preset name.
3. Add any tags that you might use to help organize your service instances.
4. Select the type of endpoints that you want to use. Options include `public and private endpoints` and `private only`.
5.	Click **Create**.


## Provisioning a public {{site.data.keyword.cloudcerts_short}} instance with the CLI
{: #provision-certificate-manager-public}

You can provision a public instance of {{site.data.keyword.cloudcerts_short}} with the {{site.data.keyword.cloud_notm}} CLI by completing the following steps.

1. Log in to {{site.data.keyword.cloud_notm}} and follow the on-screen instructions.

   ```
   ibmcloud login
   ```
   {: codeblock}

   If you're using a federated ID, be sure to append `--sso` to your command.
   {: tip}

2. Create an instance.

   ```
   ibmcloud resource service-instance-create "<instance_name>" cloudcerts free <region>
   ```
   {: codeblock}

   <table>
      <tr>
         <th>Parameter</th>
         <th>Description</th>
      </tr>
      <tr>
         <td><code>instance_name</code></td>
         <td>The name that you want to give your instance of the service.</td>
      </tr>
      <tr>
         <td><code>region</code></td>
         <td>The region in which you want to provision the service. Options include: <code>us-south</code>, <code>eu-gb</code>, <code>eu-de</code>, <code>jp-tok</code>, <code>au-syd</code>, and <code>us-east</code></td>
      </tr>
   </table>


## Provisioning a private {{site.data.keyword.cloudcerts_short}} instance with the CLI
{: #provision-certificate-manager-private}

You can provision a private instance of {{site.data.keyword.cloudcerts_short}} with the {{site.data.keyword.cloud_notm}} CLI by completing the following steps.

1. Log in to {{site.data.keyword.cloud_notm}} and follow the on-screen instructions.

   ```
   ibmcloud login
   ```
   {: codeblock}

   If you're using a federated ID, be sure to append `--sso` to your command.
   {: tip}

2. Create an instance.

   ```
   ibmcloud resource service-instance-create "<instance_name>" cloudcerts free <region> -p '{"allowed_network": "private-only"}'
   ```
   {: codeblock}

   <table>
      <tr>
         <th>Parameter</th>
         <th>Description</th>
      </tr>
      <tr>
         <td><code>instance_name</code></td>
         <td>The name that you want to give your instance of the service.</td>
      </tr>
      <tr>
         <td><code>region</code></td>
         <td>The region in which you want to provision the service. Options include: <code>us-south</code>, <code>eu-gb</code>, <code>eu-de</code>, <code>jp-tok</code>, <code>au-syd</code>, and <code>us-east</code></td>
      </tr>
   </table>


## Next steps
{: #next-steps}

With your instance provisioned, you can choose whether to import a certificate that you already have or order a new one.

[![This image is a visual link to the instructions for importing a certificate.](images/getting-started-import.svg)](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate)     [![This image is a visual link to the instructions for ordering a certificate.](images/getting-started-order.svg)](/docs/certificate-manager?topic=certificate-manager-ordering-certificates)

