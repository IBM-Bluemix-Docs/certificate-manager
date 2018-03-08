---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# About
{: #about-certificate-manager}

Find out about {{site.data.keyword.cloudcerts_full}}.

## What is {{site.data.keyword.cloudcerts_short}}
{: #what-is-certificate-manager}

{{site.data.keyword.cloudcerts_short}} helps you to manage the SSL certificates for your {{site.data.keyword.IBM_notm}} cloud-based apps and services.
{: shortdesc}

You can import SSL certificates that you obtain for your apps and services, store them securely, and get a central view of the certificates that you are using.

You can manage your certificates in the following ways:

* Monitor the expiry dates of your certificates to make sure you that you renew them on time
* View the types of certificates across your deployments and ensure that they meet organization policies
* Find certificates that need replacing when new compliance or security requirements are issued
* Set controls on who can access and manage your certificates

## Availability
{: #availability}

{{site.data.keyword.cloudcerts_short}} is available in the US-South region only.

## Private key security
{: #private-key-security}

When you import a certificate and the corresponding private key into {{site.data.keyword.cloudcerts_short}}, the service uses an Advanced Encryption Standard (AES) 256 algorithm to encrypt the private key. {{site.data.keyword.cloudcerts_short}} saves this unique encrypted key to use with your service instance.

## Identity and Access Management
{: #identity-access-management}

You can secure services within {{site.data.keyword.Bluemix_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}

### Platform access roles
{: #platform-access-roles}

**Note:** using platform access roles is deprecated. Please use service access roles instead, see Table 2 below.

<table>
<caption> Table 1. Actions that are mapped to platform access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>List certificates</td>
    <td> Administrator, Operator, Editor, Viewer </td>
  </tr>
  <tr>
    <td>Download a certificate and private key </td>
    <td> Administrator, Operator </td>
  </tr>
  <tr>
    <td>Update certificate data</td>
    <td> Administrator, Editor </td>
  </tr>
  <tr>
    <td>Upload certificates, private keys, and intermediate certificates </td>
    <td> Administrator, Editor  </td>
  </tr>
  <tr>
    <td>Delete a certificate and private key </td>
    <td> Administrator, Editor </td>
  </tr>
</table>

### Service access roles
{: #service-acceess-roles}

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
    <td> Manager, Writer  </td>
  </tr>
  <tr>
    <td>Delete a certificate and private key </td>
    <td> Manager </td>
  </tr>
</table>

For more information about user roles and permissions, see [User roles](/docs/iam/users_roles.html#userroles).

### Assigning user access roles
{: #assigning-user--access-roles}

To assign an access role on the account-level or resource group-level, complete the following steps.
If the user is not part of your organization, start by sending an invitation to that user.

1. Go to **Manage > Account > Users**.
2. From the **Actions** menu, select **Assign policy**.
3. Click **Assign access to resources** or **Assign access within a resource group**.
4. Under **Services**, select **Certificate Manager**.
5. Optional: Select a **Region** or use the default, **All regions**.
6. Optional: Select a **Service instance** or use the default, **All instances**.
7. Under **Select roles > Assign platform/service access roles**, select the appropriate access level.
