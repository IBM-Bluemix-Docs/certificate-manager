---

copyright:
  years: 2017, 2021
lastupdated: "2021-06-02"

keywords: access roles, access control, permissions, platform roles, service roles, certificates, notifications, access policies

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


# Managing IAM access for {{site.data.keyword.cloudcerts_short}}
{: #managing-service-access-roles}

You can secure services within {{site.data.keyword.cloud_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on platform resources, such as creating or deleting instances in your {{site.data.keyword.cloud_notm}} account.

| Action | Role | 
|-----|----| 
| View instances of {{site.data.keyword.cloudcerts_short}} | Administrator, Operator, Editor, Viewer |
| Create an instance of {{site.data.keyword.cloudcerts_short}} | Administrator, Editor |
| Delete an instance of {{site.data.keyword.cloudcerts_short}} | Administrator, Editor |
{: caption="Table 1. Actions that are mapped to platform access roles" caption-side="top"}

## Service access roles
{: #service-access-roles}

You can use service access roles to enable users to complete tasks in {{site.data.keyword.cloudcerts_short}} instances, such as importing, downloading, editing, or deleting certificates.

| Action | Role | 
|-----|----| 
| List certificates | Manager, Writer, Reader |
| Download a certificate and private key | Manager, Writer |
| Get certificate metadata | Manager, Writer, Reader |
| Update certificate's metadata | Manager, Writer |
| Import or reimport certificates, private keys, and intermediate certificates | Manager |
| Order or renew a certificate | Manager |
| Delete a certificate and private key | Manager |
| List all notification channels | Manager, Writer, Reader |
| Add, update, or delete a notification channel | Manager |
| Test a notification channel | Manager, Writer, Reader 
{: caption="Table 2. Actions that are mapped to service access roles" caption-side="top"}

For more information about user roles and permissions, see [User roles](/docs/account?topic=account-userroles#userroles).

## Configuring access policies
{: #configuring-access-policies}

You can configure access policies for a {{site.data.keyword.cloudcerts_short}} instance and all of the certificates in that instance. Additionally, you can set policies for individual certificates (resources) within an instance. Some of the options for assigning access include the following actions:

* Assign at least the Viewer role to every user so that every user can see service instances.
* Assign the Administrator or Editor role to a user if you want that user to create and delete instances.
* Assign at least the Reader role if you want a user to view certificates within an instance.

To configure access policies, complete the following steps:

1. Go to **Manage > Access (IAM)**. 
2. Select a single user from the Users list, or an Access group.
3. Click **Access policies** and then on **Assign access**.
4. Click **Assign access to resources**.
5. From the **Services** menu, select **{{site.data.keyword.cloudcerts_short}}**.
6. From the **Service instance** menu, select a {{site.data.keyword.cloudcerts_short}} instance, or use the default value `All instances`.
7. Assign a [platform access role](/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) to the user.
8. Assign a [service access role](/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) to the user.
9. Click **Assign** to assign the access policy to the user.

### Allowing access to a specific certificate
{: #allow-access-to-specific-certificate}

To allow access to a specific certificate, complete the following steps:

1. [Retrieve your certificate ID](/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Create two access policies:
   - The first policy: Assign at least **Viewer** platform access role for the service instance
   - The second policy: Assign at least **Reader** service access role
     - Enter `certificate` in the **Resource Type** field.
     - Enter the certificate ID in the **Resource ID** field.

### Retrieving the ID of a certificate
{: #get-certificate-id}

To retrieve the ID of a certificate, complete the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, select your {{site.data.keyword.cloudcerts_short}} instance.
2. From the navigation on the service details page, select **Manage**.
3. Select a certificate.
4. In the certificate details, find the certificate CRN.
5. Copy the certificate ID. The CRN contains different values that are all separated by a colon (`:`). The certificate ID is the last value in your CRN; for example: `e20cb664efcbfa2c2f57801230d246a6`
