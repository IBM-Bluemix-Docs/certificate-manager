---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing service access roles
{: #managing-service-access-roles}

You can secure services within {{site.data.keyword.Bluemix_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}


## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on platform resources, such as creating or deleting instances in your {{site.data.keyword.Bluemix_notm}} account.

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

Platform roles also give access to certain actions on certificates within instances. These actions are deprecated.


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
    <td>Update certificate data</td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
    <td>Upload certificates, private keys, and intermediate certificates </td>
    <td> Manager  </td>
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


For more information about user roles and permissions, see [User roles](/docs/iam/users_roles.html#userroles).


## Configuring access policies for users
{: #configuring-access-policies}

You can configure access policies for users to grant access to a {{site.data.keyword.cloudcerts_short}} instance, or to a subset of certificates that are stored in the instance. 
{: shortdesc}

1.  Navigate to **Manage** > **Account** > **Users**. A list of the users with access to your {{site.data.keyword.Bluemix_notm}} account is shown.
2.  Click the name of the user that you want to assign an access policy. If the user is not shown, click **Invite users** to [add the user to your {{site.data.keyword.Bluemix_notm}} account](/docs/iam/iamuserinv.html#iamuserinv). 
3.  Click **Assign access**. 
4.  Click **Assign access to resources**. 
5.  From the **Services** drop-down menu, select **Certificate Manager**. 
6.  From the **Service instance** drop-down menu, select a {{site.data.keyword.cloudcerts_short}} instance, or use the default value **All instances**. 
7.  Optional: Configure access to a specific certificate. 
    1. [Retrieve your certificate ID](#get-certificate-id). 
    2. Enter `certificate` in the **Resource Type** field. 
    3. Enter the certificate ID in the **Resource ID** field. 
8.  Assign a [platform access role](#platform-access-roles) to the user. 
9.  Assign a [service access role](#service-access-roles) to the user. 
10. Click **Assign** to assign the access policy to the user. 

### Retrieving the ID of a certificate
{: #get-certificate-id}

1. From the {{site.data.keyword.Bluemix_notm}} dashboard, select your {{site.data.keyword.cloudcerts_short}} instance. 
2. From the navigation on the service details page, select **Manage**. 
3. Select a certificate. 
4. In the certificate details, find the certificate CRN. 
5. Copy the certificate ID. The CRN contains different values that are all separated by a colon (`:`). The certificate ID is the last value in your CRN. 

