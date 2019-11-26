---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-26"

keywords: certificates, ssl, tls, responsabilities, ibm, terms, conditions, managing service roles, regulation compliance, pci, dss, ha, backup, industry standard

subcollection: certificate-manager

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Understanding your responsibilities with using {{site.data.keyword.cloudcerts_short}}
{: #understanding-your-responsibilities-using-certificate-manager}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cloudcerts_long}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.cloudcerts_long}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops}

Tasks that pertain to any logs or activity in your {{site.data.keyword.cloudcerts_short}} instance.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Data | Provide integrations with select third-party partnership technologies, such as {{site.data.keyword.la_full}} and {{site.data.keyword.at_full}} | Use the provided tools to review instance logs and activities. For more information, see [Available Integrations](/docs/services/certificate-manager?topic=certificate-manager-available-integrations).  |
| | | {{site.data.keyword.cloudcerts_short}} does not deploy certificates to your TLS termination points. You can use the Kubernetes Service CLI to deploy certificates managed in Certificate Manager to your cluster. For more information, see [Available Integrations](/docs/services/certificate-manager?topic=certificate-manager-available-integrations). |
| | | Avoid outages because of expired certificates by configuring notification channels and handle expiring certificates notifications. |
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}

## Identity and access management
{: #iam-responsibilities}

Tasks that pertain to the optional access restrictions that you can place on certificates, notification channels, and the actions that can be performed within {{site.data.keyword.cloudcerts_short}}.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Data | Provide the ability to restrict access to resources. | Depending on your needs, you can restrict access to service functionality by using service policies. For more information, see [Managing service access roles](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles). |
{: caption="Table 2. Responsibilities for identity and access management" caption-side="top"}

## Security and regulation compliance
{: #security-compliance}

{{site.data.keyword.IBM_notm}} is responsible for the security and compliance of the {{site.data.keyword.cloudcerts_short}} service.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Data | Maintain controls commensurate to [various industry compliance standards](/docs/services/certificate-manager?topic=certificate-manager-compliance-and-standards), such as PCI DSS.  | |
{: caption="Table 3. Responsibilities for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

Tasks pertaining to recovery of the {{site.data.keyword.cloudcerts_short}} service and customer data.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
| Application | Continuously monitor to ensure the reliability and availability of the service environment by site reliability engineers. | |
| Data | Back up and recover data in the region that the service operates in. | To recover data in case of a regional failure we recommend for the customer to implement cross-region backup strategy. For more information see [High availability and disaster recovery](/docs/services/certificate-manager?topic=certificate-manager-compliance-and-standards#ha-dr). |
{: caption="Table 4. Responsibilities for disaster recovery" caption-side="top"}
