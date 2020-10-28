---

copyright:
  years: 2020
lastupdated: "2020-10-27"

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

The {{site.data.keyword.compliance_short}} is built directly into the platform and integrated with {{site.data.keyword.cloudcerts_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.cloudcerts_short}}
* Define rules for {{site.data.keyword.cloudcerts_short}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.cloudcerts_short}}
{: #monitor-certificate-manager}

As a security or compliance focal, you need to ensure that your organization is adhering to the external and internal standards for your industry. By scanning the configurations in your accounts against a profile, the {{site.data.keyword.compliance_short}} can help you to identify potential issues as they arise.

Each goal is automatically added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

**Available goals for {{site.data.keyword.cloudcerts_short}}**

* Check whether certificates are automatically renewed before expiration.

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).


## Governing {{site.data.keyword.cloudcerts_short}} resource configuration
{: #govern-certificate-manager}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define config rules for the instances of {{site.data.keyword.cloudcerts_short}} that you create.

This service only supports the ability to view the results of your configuration scans in the {{site.data.keyword.compliance_short}}.
{: note}

[Config rules](x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the about the data that you can use to create a rule for {{site.data.keyword.cloudcerts_short}}, review the following table.


| Resource kind | Property | Operator| Value | Description |
|:--------------|:---------|:--------------|:------|:------------|
| `instance` | `private_network_only` | `is_true`<br>`is_false` | - | Indicates whether access to an instance of the service is allowed only through a private network. |
| `certificate` | `days_to_expiration` | `num_greater_than`| Number of days | Checks whether the number of days before a certificate expires is greater than the specified value. |
{: caption="Table 1. Available rule configurations" caption-side="top"}

To learn more about config rules, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule).


## Gaining security insight with {{site.data.keyword.cloudcerts_short}}
{: #insights-certificate-manager}

With the {{site.data.keyword.compliance_short}}, you can gain insight into potential issues through built-in security capabilities. By default, {{site.data.keyword.cloudcerts_short}} is an integrated service. The {{site.data.keyword.compliance_short}} gathers and presents information related to the certificate lifecycle in order to display all of your security alerts in one place.

To learn more about how you can use security insights, see [Monitoring certificates](/docs/security-advisor?topic=security-advisor-setup-services#setup-certificates).

