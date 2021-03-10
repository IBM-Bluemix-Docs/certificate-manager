---

copyright:
  years: 2021
lastupdated: "2021-03-10"

keywords: security for {{site.data.keyword.cloudcerts_short}}, compliance for {{site.data.keyword.cloudcerts_short}}, security and compliance for {{site.data.keyword.cloudcerts_short}}, rules for {{site.data.keyword.cloudcerts_short}},

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



# Managing security and compliance with {{site.data.keyword.cloudcerts_short}}
{: #manage-security-compliance}

{{site.data.keyword.cloudcerts_short}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.cloudcerts_short}}
* Define rules for {{site.data.keyword.cloudcerts_short}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.cloudcerts_short}}
{: #monitor-certificate-manager}

As a security or compliance focal, you can use the {{site.data.keyword.cloudcerts_short}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identity potential issues as they arise.

All of the goals for {{site.data.keyword.cloudcerts_short}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.cloudcerts_short}}
{: #certificate-manager-available-goals}

* Check whether certificates are automatically renewed before expiration.



## Governing {{site.data.keyword.cloudcerts_short}} resource configuration
{: #govern-certificate-manager}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define config rules for the instances of {{site.data.keyword.cloudcerts_short}} that you create.

{{site.data.keyword.cloudcerts_short}} supports only the ability to view the results of your configuration scans in the {{site.data.keyword.compliance_short}}. This service does not yet support customizing default values with [templates](/docs/security-compliance?topic=security-compliance-what-is-template).
{: note}

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the about the data that you can use to create a rule for {{site.data.keyword.cloudcerts_short}}, review the following table.


| Resource kind | Property | Operator| Value | Description |
|:--------------|:---------|:--------------|:------|:------------|
| *instance* | *private_network_only** | *is_true*<br>*is_false* | - | Indicates whether access to an instance of the service is allowed only through a private network. |
| *certificate* | *days_to_expiration** | *num_greater_than*| Number of days | Checks whether the number of days before a certificate expires is greater than the specified value. |
{: caption="Table 1. Configuration properties for {{site.data.keyword.cloudcerts_short}}" caption-side="top"}

_*Properties not compatible with templates._

To learn more about using rules to define guardrails for your resources, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule).


## Gaining security insight with {{site.data.keyword.cloudcerts_short}}
{: #insights-certificate-manager}

With the {{site.data.keyword.compliance_short}}, you can gain insight into potential issues through built-in security capabilities. By default, {{site.data.keyword.cloudcerts_short}} is an integrated service. The {{site.data.keyword.compliance_short}} gathers and presents information related to the certificate lifecycle in order to display all of your security alerts in one place.

To learn more about how you can use security insights, see [Monitoring certificates](/docs/security-advisor?topic=security-advisor-setup-services#setup-certificates).

