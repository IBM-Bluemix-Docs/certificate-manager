---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-18"

keywords: Certificate Manager, certificates, getting started, ssl, tls, import certificate, tutorial, order certificate, cert

subcollection: certificate-manager

content-type: tutorial
account-plan: lite
completion-time: 10m

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


# Getting started with {{site.data.keyword.cloudcerts_short}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With {{site.data.keyword.cloudcerts_full}}, you can obtain, store, and manage SSL/TLS certificates that you use for cloud or on-premises deployments.
{: shortdesc}

You can provision an instance of {{site.data.keyword.cloudcerts_short}} with the {{site.data.keyword.cloud_notm}} CLI by completing the following steps.

## Log in
{: #getting-started-step1}
{: step}

Log in to {{site.data.keyword.cloud_notm}} and follow the on-screen instructions.

  ```
  ibmcloud login
  ```
  {: codeblock}

  If you're using a federated ID, be sure to append `--sso` to your command.
  {: tip}

## Create an instance
{: #getting-started-step2}
{: step}

  ```
  ibmcloud resource service-instance-create "<instance_name>" cloudcerts free <region>
  ```
  {: codeblock}

  To provision an instance of {{site.data.keyword.cloudcerts_short}} that uses private endpoints only, append `-p '{"allowed_network": "private-only"}'` to your command. [Learn more](/docs/certificate-manager?topic=certificate-manager-regions-endpoints#connectivity).
  {: note}

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
      <td>The region in which you want to provision the service. Options include: <code>us-south</code>, <code>eu-de</code>, <code>eu-gb</code>, <code>jp-osa</code>, <code>au-syd</code>, <code>jp-tok</code>, <code>ca-tor</code> and <code>us-east</code></td>
    </tr>
  </table>

### Provisioning an instance of {{site.data.keyword.cloudcerts_short}} with the console
{: #provision-console}

Alternatively, you can provision an instance of {{site.data.keyword.cloudcerts_short}} with the {{site.data.keyword.cloud_notm}} console by completing the following steps.

1. In the {{site.data.keyword.cloud_notm}} catalog, select **{{site.data.keyword.cloudcerts_short}}**.
2. Give your service instance a name, or use the preset name.
3. Organize your service instances by adding tags.
4. Select the type of endpoints that you want to use. Options include `public and private endpoints` and `private only`.
5. Click **Create**.

## Next steps
{: #next-steps}

With your instance provisioned, you can choose whether to import your own certificate or order a new one to start working with the service.

[![This image is a visual link to the instructions for importing a certificate.](images/getting-started-import.svg)](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate)     [![This image is a visual link to the instructions for ordering a certificate.](images/getting-started-order.svg)](/docs/certificate-manager?topic=certificate-manager-ordering-certificates)

