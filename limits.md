---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-02"

keywords: certificates, limites, ssl, tls, free, renew certificate, order certificate, update operations, reimport, import certificates

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


# Limits
{: #limits}

## Plan limits
{: plan-limits}

### Free
{: free-plan-limits}

The following table lists the limits in instances of the Free plan of {{site.data.keyword.cloudcerts_short}}.

| Resource | Maximum | 
|-----|----| 
| Certificates | You can upload a maximum of 1000 certificates per instance. |

## API limits
{: api-limits}

The following table lists the various rate limits for {{site.data.keyword.cloudcerts_short}} APIs.

| API | Limit | 
|-----|----| 
| Create notifications channels | 5 actions per minute |
| Update notifications channels | 5 actions per minute |
| Test notifications channels | 1 action per second |
| Reimport certificates | 5 actions per minute for the same certificate | 
| Update operations on certificates | 5 actions per minute for the same certificate |
| Order certificates | 5 orders per minute per {{site.data.keyword.cloudcerts_short}} instance, 100 orders/hour per IBM user account, and 5 certificates for the same domains per week. |
| Renew certificates | 5 renews/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 renews/hour per IBM user account, and 5 certificates for the same domains per week. |
| Update order policy | 5 actions per minute for the same certificate | 
