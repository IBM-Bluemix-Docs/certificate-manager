---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-02"

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

# Available integrations
{: #available-integrations}

The following lists available integration supported by {{site.data.keyword.cloudcerts_full}}.

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
    <td>You can easily and securely deploy custom domain TLS certificates from {{site.data.keyword.cloudcerts_short}} to your Kubernetes cluster. Cluster administrators can use the [Kubernetes Service plug-in commands](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) to update TLS certificates as Kubernetes secrets with a new certificate without causing downtime. To get started, check out the [Ingress annotations in the documentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Store your custom domain certificates in the {{site.data.keyword.cloudcerts_short}} service, then use certificate CRNs to bind with custom domains in {{site.data.keyword.apiconnect_short}}. [Learn more about {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-getting-started#getting-started).</p></td>
  </tr>
  <tr>
    <td>IBM Cloud™ Load Balancer for VPC</td>
    <td>A TLS certificate is required for load balancers to perform TLS offloading tasks. You may manage the TLS certificates through IBM Certificate Manager. Enable service-to-service authorization to give a load balancer access to your certificate. [Learn more about this integration](/docs/vpc-on-classic-network?topic=vpc-on-classic-network---using-load-balancers-in-ibm-cloud-vpc#ssl-offloading-and-required-authorizations)</td>
  </tr>
</table>

## Services that {{site.data.keyword.cloudcerts_short}} is integrated with
{: #servuce-integrations-2}

<table>
<caption>Table 2. {{site.data.keyword.cloud_notm}} services that {{site.data.keyword.cloudcerts_short}} provides an integration with.</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) centralizes the information about {{site.data.keyword.cloud_notm}} services. The information includes the indication of expired certificates and certificates that are about to expire in instances of {{site.data.keyword.cloudcerts_short}} in your {{site.data.keyword.cloud_notm}} account. [Learn more about {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_full_notm}}</td>
    <td>You can use [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) to track how users and applications interact with the {{site.data.keyword.cloudcerts_long_notm}} service in the {{site.data.keyword.cloud_notm}}.
    <p>To get the list of actions that generate an event, see [{{site.data.keyword.at_short}} events](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.la_full_notm}}</td>
    <td>You can use [{{site.data.keyword.la_short}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started) offers administrators, DevOps teams, and developers advanced features to filter, search, and tail log data, define alerts, and design custom views to monitor application and system logs related to {{site.data.keyword.cloudcerts_short}}.
    <p>To get started, see [{{site.data.keyword.at_short}} events](/docs/services/certificate-manager?topic=certificate-manager-log_events#log_events).</p></td>
  </tr>
</table>