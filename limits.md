---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-04"

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

# Limits
{: #limits}

Rate limiting is used to control the amount of traffic that is coming and going through your instance of {{site.data.keyword.cloudcerts_full}}. By limiting requests or resources, you can protect your applications.
{: shortdesc}

## plans
{: plan-limits}

### Free
{: free-plan-limits}

Review the following table to see the limits that are in place for free instances of {{site.data.keyword.cloudcerts_short}}.

<table>
  <tr>
    <th> Resource </th>
    <th> Maximum </th>
  </tr>
  <tr>
    <td>Certificates</td>
    <td>You can upload a maximum of 1000 certificates per instance.</td>
  </tr>
</table>

## API limits
{: api-limits}

<table>
  <tr>
    <th> API </th>
    <th> Limit </th>
  </tr>
  <tr>
    <td>Create notifications channels</td>
    <td>5 action per minute</td>
  </tr>
  <tr>
    <td>Update notifications channels</td>
    <td>5 action per minute</td>
  </tr>
  <tr>
    <td>Testing notifications channels</td>
    <td>1 action per second</td>
  </tr>
  <tr>
    <td>Re/importing certificates</td>
    <td>5 actions per minute</td>
  </tr>
  <tr>
    <td>Update operations on certificates</td>
    <td>5 actions per minute</td>
  </tr>
  <tr>
    <td>Ordering certificates</td>
    <td>5 orders/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 orders/hour per IBM user account, and 5 certificates for the same domains per week.</td>
  </tr>
  <tr>
    <td>Renewing certificates</td>
    <td>5 renews/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 renews/hour per IBM user account, and 5 certificates for the same domains per week.</td>
  </tr>
</table>