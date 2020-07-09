---

copyright:
  years: 2017, 2020
lastupdated: "2020-07-09"

keywords: certificates, ssl, tls, integrations, kube, kubernetes, custom domain

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



# Available integrations
{: #available-integrations}

The following tables lists supported integrations by {{site.data.keyword.cloudcerts_full}}.

## Services that are integrated with {{site.data.keyword.cloudcerts_short}} 
{: #service-integrations-1}

<table>
<caption>Table 1. {{site.data.keyword.cloud_notm}} services that provide an integration with {{site.data.keyword.cloudcerts_short}}</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Easily and securely deploy custom domain TLS certificates from {{site.data.keyword.cloudcerts_short}} to your Kubernetes cluster. Cluster administrators can use the [Kubernetes Service plug-in commands](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) to update TLS certificates as Kubernetes secrets with a new certificate without causing downtime. To get started, check out the [Ingress annotations in the documentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Store your custom domain certificates in the {{site.data.keyword.cloudcerts_short}} service, then use certificate CRNs to bind with custom domains in {{site.data.keyword.apiconnect_short}}. [Learn more about {{site.data.keyword.apiconnect_short}}](/docs/apiconnect?topic=apiconnect-getting-started#getting-started).</p></td>
  </tr>
  <tr>
    <td>IBM Cloud Load Balancer for VPC</td>
    <td>A TLS certificate is required for load balancers to perform TLS offloading tasks. You may manage the TLS certificates through {{site.data.keyword.cloudcerts_short}}. Enable service-to-service authorization to give a load balancer access to your certificate. [Learn more about this integration](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-load-balancers-in-ibm-cloud-vpc#ssl-offloading-and-required-authorizations)</td>
  </tr>
</table>

## Services that {{site.data.keyword.cloudcerts_short}} is integrated with
{: #service-integrations-2}

<table>
<caption>Table 2. {{site.data.keyword.cloud_notm}} services that {{site.data.keyword.cloudcerts_short}} provides an integration for.</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.cis_full_notm}}</td>
    <td>Order Let's Encrypt certificates with ease by leveraging {{site.data.keyword.cis_full_notm}} as your DNS provider. To get started, see the [Ordering certificates](/docs/certificate-manager?topic=certificate-manager-order-certificates) documentation.</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/security-advisor?topic=security-advisor-getting-started#getting-started) centralizes the information about {{site.data.keyword.cloud_notm}} services. The information includes the indication of expired certificates and certificates that are about to expire in instances of {{site.data.keyword.cloudcerts_short}} in your {{site.data.keyword.cloud_notm}} account. [Learn more about {{site.data.keyword.security-advisor_short}}](/docs/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_full_notm}}</td>
    <td>You can use [{{site.data.keyword.at_short}}](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started) to track how users and applications interact with the {{site.data.keyword.cloudcerts_long_notm}} service in the {{site.data.keyword.cloud_notm}}.
    <p>To get the list of actions that generate an event, see [{{site.data.keyword.at_short}} events](/docs/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.la_full_notm}}</td>
    <td>You can use [{{site.data.keyword.la_short}}](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-getting-started) offers administrators, DevOps teams, and developers advanced features to filter, search, and tail log data, define alerts, and design custom views to monitor application and system logs related to {{site.data.keyword.cloudcerts_short}}.
    <p>To get started, see [{{site.data.keyword.at_short}} events](/docs/certificate-manager?topic=certificate-manager-log_events#log_events).</p></td>
  </tr>
</table>