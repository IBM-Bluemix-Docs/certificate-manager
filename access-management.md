---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-04"

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


### Platform access roles
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


### Service access roles
{: #service-acceess-roles}

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


### Assigning user access roles
{: #assigning-user--access-roles}

You can configure access policies for a Certificate Manager instance (and thereby for all the certificates in that instance), or you can set policies for individual certificates (resources) within an instance.    
To assign an access role at the account-level, complete the steps below.
If the user is not part of your organization, start by sending an invitation to that user.

1. Go to **Manage > Account > Users**.
2. Click on a user and then click on the **Assign access** button, or Select a user in the table, and from the **Actions** menu, select **Assign access**.
3. Click **Assign access to resources**.
4. Under **Services**, select **Certificate Manager**.
5. Select a **Service instance** or use the default, **All instances**.
6. Optional: If you want to configure a policy for an individual certificate, in the **Resource Type** field, type the word _‘certificate’_ and in the **Resource ID** field, type the Certificate ID which is the last part of the Certificate CRN. Find instructions to get this ID below.
7. Under **Select roles > Assign platform access roles**, select the appropriate access level.
8. Under **Select roles > Assign service access roles**, select the appropriate access level.
9. Click **Assign** to assign the policy.

**Examples:**
* Assign at least the Viewer role to every user so that every user can see service instances.
* Assign the Administrator or Editor role to a user if you want that user to create/delete instances.
* Assign at least the Reader role if you want a user to view certificates within an instance.

**Getting the Certificate ID used for configuring a certificate level access policy:** 
1. Go to your Certificate Manager instance
2. Select the certificate 
3. Find the certificate crn in the certificate details
4. Copy the last part of the crn (e.g e20cb664efcbfa2c2f57801230d246a6)
This is the certificate ID




