---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-12"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing certificates from the dashboard
{: #managing-certificates-from-the-dashboard}

You can use the {{site.data.keyword.cloudcerts_full}} service dashboard to manage certificates that you obtain from third-party issuers to use with your {{site.data.keyword.IBM_notm}} cloud-based apps or services. After you import certificates and keys, they're encrypted and stored by the service.
{: shortdesc}

## Importing a certificate
{: #importing-a-certificate}

To help you to manage your certificates, you can upload them.
{: shortdesc}

Before you begin:

* Create a valid, unexpired certificate with a matching private key.
* Convert the files into Privacy-enhanced Electronic Mail (PEM) format.
* Keep the private key unencrypted to ensure that it can be imported.

To import a certificate, click **Import Certificate** and provide the following details:

1. Enter a display name.
2. Click **Browse**, select the certificate file in PEM format.
3. Click **Browse**, select the certificate's private key in PEM format.
4. If applicable, provide the intermediate certificate file in PEM format.
5. Optional: Enter a description.
6. Click **Import**.  

**Note**: To renew an imported certificate, obtain a new certificate from your certificate authority (CA) and import the new certificate into {{site.data.keyword.cloudcerts_short}}. After the new certificate is deployed, you can delete your old one.

After you import a certificate, the following information is displayed in the Certificates table. To view more certificate information, you can select the certificate in the table row.

<table>
<caption> Table 1. Information about the imported certificate </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Name</td>
    <td>A meaningful display name. Maximum length 256 characters. </td>
  </tr>
  <tr>
    <td>Description</td>
    <td>Optional: Descriptive text for the certificate. Maximum length 1024 characters.</td>
  </tr>
  <tr>
    <td>Domain</td>
    <td>The domain or domains for which the certificate is valid. </td>
  </tr>
  <tr>
    <td>Issuer</td>
    <td>The CA that issued the certificate.</td>
  </tr>
  <tr>
    <td>Algorithm</td>
    <td>The encryption type by which the certificate is created. </td>
  </tr>
  <tr>
    <td>Key algorithm</td>
    <td>The key type and size that is used by the algorithm. </td>
  </tr>
  <tr>
    <td>Expires in </td>
    <td>The number of remaining days before the certificate is no longer valid. </td>
  </tr>
  <tr>
    <td>Date issued</td>
    <td>The date when the certificate was issued. </td>
  </tr>
  <tr>
    <td>Valid from</td>
    <td>The date on which the certificate became valid. </td>
  </tr>
  <tr>
    <td>Expires on</td>
    <td>The date on which the certificate is no longer valid. </td>
  </tr>
  <tr>
    <td>Certificate ID</td>
    <td>The generated ID given to the certificate upon import. </td>
  </tr>
</table>

## Searching certificates
{: #searching-certificates}
 
If you manage many certificates, you can use the search bar to locate the required certificate.
{: shortdesc}
 
-   To search for certificate name, certificate domain, or certificate issuer, type your search term into the Search bar and press Enter.
-   To view all of your certificates, click the **X** icon in the Search bar.

## Downloading certificates
{: #downloading-certificates}

When you are ready to deploy your certificate to your app or service, you can download the certificate and the associated private key.
{: shortdesc}

To download a certificate:

1. Select the check box for the certificate that you want to download.
2. Click **Download Certificate**. Depending on what you imported into the service, you receive a compressed file that contains PEM files for the certificate, an associated private key, and an associated intermediate certificate.


## Deleting certificates
{: #deleting-certificates}

If you want to stop tracking a certificate, you can delete it.
{: shortdesc}  

To delete a certificate:

1. Select the check box for the certificate that you want to delete.
2. Click the **Trash** icon.

## Updating certificates metadata
{: #updating-certificates-metadata}

You can also update the name and description of a certificate.
{: shortdesc}

To update a certificate:

1. Select a row to open the details for that certificate.
2. Update the name or description.
3. Save your changes.

**Note**: You can perform up to 5 update actions per minute.
