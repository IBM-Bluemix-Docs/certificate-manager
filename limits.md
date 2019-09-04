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

## Plan limits
{: plan-limits}

### Free
{: free-plan-limits}

The following tables lists the limits in instances of the Free plan of {{site.data.keyword.cloudcerts_short}}.

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

The following tables lists the various rate limits for {{site.data.keyword.cloudcerts_short}} APIs.

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
    <td>Test notifications channels</td>
    <td>1 action per second</td>
  </tr>
  <tr>
    <td>Re/import certificates</td>
    <td>5 actions per minute</td>
  </tr>
  <tr>
    <td>Update operations on certificates</td>
    <td>5 actions per minute</td>
  </tr>
  <tr>
    <td>Order certificates</td>
    <td>5 orders/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 orders/hour per IBM user account, and 5 certificates for the same domains per week.</td>
  </tr>
  <tr>
    <td>Renew certificates</td>
    <td>5 renews/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 renews/hour per IBM user account, and 5 certificates for the same domains per week.</td>
  </tr>
</table>