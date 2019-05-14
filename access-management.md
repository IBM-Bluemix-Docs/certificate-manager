---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-14"

keywords: certificates, SSL,

subcollection: certificate-manager

---

{:new_window: target="_blank"}
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

# Managing service access roles
{: #managing-service-access-roles}

You can secure services within {{site.data.keyword.cloud_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on platform resources, such as creating or deleting instances in your {{site.data.keyword.cloud_notm}} account.

<table>
<caption> Table 1. Actions that are mapped to platform access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>View instances of {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrator, Operator, Editor, Viewer </td>
  </tr>
  <tr>
    <td>Create an instance of {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
  <tr>
    <td>Delete an instance of {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
</table>

## Service access roles
{: #service-access-roles}

You can use service access roles to enable users to complete tasks in {{site.data.keyword.cloudcerts_short}} instances, such as importing, downloading, editing, or deleting certificates.

<table>
<caption> Table 2. Actions that are mapped to service access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>List certificates</td>
    <td> Manager, Writer, Reader </td>
  </tr>
  <tr>
    <td>Download a certificate and private key </td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
     <td>Get certificate metadata </td>
     <td> Manager, Writer, Reader </td>
  </tr>      
  <tr>
    <td>Update certificate's metadata</td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
    <td>Import or reimport certificates, private keys, and intermediate certificates </td>
    <td> Manager </td>
  </tr>
  <tr>
    <td>Order a certificate </td>
    <td> Manager </td>
  </tr>
  <tr>
    <td>Delete a certificate and private key </td>
    <td> Manager </td>
  </tr>
      <tr>
        <td>List all notification channels </td>
        <td> Manager, Writer, Reader </td>
      </tr>
   <tr>
     <td>Add, update, or delete a notification channel </td>
     <td> Manager </td>
   </tr>
     <tr>
       <td>Test a notification channel </td>
       <td> Manager, Writer, Reader </td>
     </tr>

</table>

For more information about user roles and permissions, see [User roles](/docs/iam?topic=iam-userroles#userroles).

## Configuring access policies for users
{: #configuring-access-policies}

You can configure access policies for a {{site.data.keyword.cloudcerts_short}} instance (and therefore for all the certificates in that instance), or you can set policies for individual certificates (resources) within an instance.

**Examples of role allocation**

* Assign at least the Viewer role to every user so that every user can see service instances.
* Assign the Administrator or Editor role to a user if you want that user to create and delete instances.
* Assign at least the Reader role if you want a user to view certificates within an instance.

{: shortdesc}

### Configuring access policies
{: #configuring-access-policies}

To configure access policies, complete the following steps:

1. Navigate to **Manage > Access (IAM) > Users**. A list of the users with access to your {{site.data.keyword.cloud_notm}} account is shown.
2. Click the name of the user that you want to assign an access policy to. If the user is not shown, click **Invite users** to [add the user to your {{site.data.keyword.cloud_notm}} account](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Click on **Access policies** and then on **Assign access**.
4. Click **Assign access to resources**.
5. From the **Services** menu, select **Certificate Manager**.
6. From the **Service instance** menu, select a {{site.data.keyword.cloudcerts_short}} instance, or use the default value `All instances`.
7. Assign a [platform access role](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) to the user.
8. Assign a [service access role](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) to the user.
9. Click **Assign** to assign the access policy to the user.

### Allowing access to a specific certificate
{: #allow-access-to-specific-certificate}

To allow access to a specific certificate, complete the following steps:

1. [Retrieve your certificate ID](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Create two access policies:
   - The first policy: Assign at least **Viewer** platform access role for the service instance
   - The second policy: Assign at least **Reader** service access role
     - Enter `certificate` in the **Resource Type** field.
     - Enter the certificate ID in the **Resource ID** field.

### Retrieving the ID of a certificate
{: #get-certificate-id}

To retrieve the ID of a certificate, complete the following steps:

1. From the {{site.data.keyword.cloud_notm}} dashboard, select your {{site.data.keyword.cloudcerts_short}} instance.
2. From the navigation on the service details page, select **Manage**.
3. Select a certificate.
4. In the certificate details, find the certificate CRN.
5. Copy the certificate ID. The CRN contains different values that are all separated by a colon (`:`). The certificate ID is the last value in your CRN; for example: `e20cb664efcbfa2c2f57801230d246a6`
