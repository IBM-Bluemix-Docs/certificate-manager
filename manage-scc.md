---

copyright:
  years: 2020
lastupdated: "2020-10-07"

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

With {{site.data.keyword.compliance_short}}, you can use {{site.data.keyword.cloudcerts_short}} to:

- Implement controls and goals that continuously evaluate your current posture
- Define rules to standardize resource configuration
- Gain insight into suspicious activity across your apps and accounts.

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

As a security focal, you can use the {{site.data.keyword.compliance_short}} to define rules for the instances of {{site.data.keyword.cloudcerts_short}} that you create.

Config rules are defined as a JSON object with two sections: a target and a required config. The target details information about the {{site.data.keyword.cloud_notm}} service and resource kind that you want to create a rule for. The required config details the specific property within the target that you want to check to ensure it is configured to your standards.

This service only supports the ability to view the results of your configuration scans in the {{site.data.keyword.compliance_short}}.
{: note}

The following table details the information that you need to create a config rule for the {{site.data.keyword.cloudcerts_short}} service.

| Resource kind | Property | Operator type | Value | Description |
|:--------------|:---------|:--------------|:------|:------------|
| `instance` | `private_network_only` | Boolean | - | Indicates whether access to an instance of the service is allowed only through a private network. |
{: caption="Table 2. Available rule configurations" caption-side="top"}

To learn more about governing the configuration of resources, check out [Working with config rules](/docs/security-compliance?topic=security-compliance-rules).


## Gaining security insight with {{site.data.keyword.cloudcerts_short}}
{: #insights-certificate-manager}

With the {{site.data.keyword.compliance_short}}, you can gain insight into potential issues through built-in security capabilities. By default, {{site.data.keyword.cloudcerts_short}} is an integrated service. The {{site.data.keyword.compliance_short}} gathers and presents information related to the certificate lifecycle in order to display all of your security alerts in one place.

To learn more about how you can use security insights, see [Monitoring certificates](/docs/security-advisor?topic=security-advisor-setup-services#setup-certificates).

