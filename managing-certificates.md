---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Managing certificates from the dashboard
{: #managing-certificates-from-the-dashboard}

You can use the {{site.data.keyword.cloudcerts_full}} service dashboard to manage certificates that you obtain from third-party issuers to use with your {{site.data.keyword.IBM_notm}} cloud-based apps or services. After you import the certificates and keys, they're encrypted and stored by the service.
{: shortdesc}

## Importing a certificate
{: #importing-a-certificate}

Import your certificates so that you can manage them.
{: shortdesc}

**Before you begin**

* Create a valid, unexpired certificate with a matching private key.
* Convert the files into Privacy-enhanced Electronic Mail (PEM) format.
* Keep the private key unencrypted to ensure that it can be imported.

To import a certificate, click **Import Certificate** and provide the following details:

1. Enter a display name.
2. Select the certificate file in PEM format by clicking **Browse**.
3. Select the certificate's private key in PEM format by clicking **Browse**.
4. If applicable, provide the intermediate certificate file in PEM format.
5. (Optional) Enter a description.
6. Click **Import**.

After you import a certificate, the following information is displayed in the Certificates table. To view more information about the certificate, you can expand the certificate's row in the Certificates table.

<table>
<caption> Table 1. Information about the imported certificate </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Name</td>
    <td>A meaningful display name. The maximum length is 256 characters. </td>
  </tr>
  <tr>
    <td>Description</td>
    <td>(Optional) Descriptive text for the certificate. The maximum length is 1024 characters.</td>
  </tr>
  <tr>
    <td>Domain</td>
    <td>The domain or domains for which the certificate is valid. </td>
  </tr>
  <tr>
    <td>Issuer</td>
    <td>The certificate authority (CA) that issued the certificate.</td>
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

## Reimporting a certificate
{: #reimport-certificate}

If your certificate is about to expire, you can update the certificate by importing a new version of the certificate that has the same domain as the existing certificate, but has a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup that can be downloaded if required.
{: shortdesc}

### Reimporting your certificate
{: #reimporting-certificate}

To reimport a certificate, complete the following steps:

1. Expand the row for the certificate.
2. Click **Reimport Certificate**.
3. Select the new certificate file in PEM format by clicking **Browse**.
4. (Optional) Select the new certificate's private key in PEM format by clicking **Browse**.
5. (Optional) Provide a new intermediate certificate file in PEM format by clicking **Browse**.
6. Click **Reimport** and then **Done**.

### Downloading a previous version of your certificate
{: #downloading-certificate}

To download the previous version of a certificate, complete the following steps:

1. Expand the row for the certificate.
2. Click the **Previous version** link.

Reimporting certificates is limited to five actions per minute.
{: tip}

## Searching certificates
{: #searching-certificates}

If you manage many certificates, you can use the search bar to locate the required certificate.
{: shortdesc}

* To search for certificate name, certificate domain, or certificate issuer, type your search term into the Search bar and press Enter.
* To view all of your certificates, click the **X** icon in the Search bar.

## Downloading certificates
{: #downloading-certificates}

When you are ready to deploy your certificate to your app or service, you can download the certificate and the associated private key.
{: shortdesc}

To download a certificate, complete the following steps:

1. Select the check box for the certificate that you want to download.
2. Click **Download Certificate**. Depending on what you imported into the service, you receive a compressed file that contains PEM files for the certificate, an associated private key, and an associated intermediate certificate.

## Deleting certificates
{: #deleting-certificates}

If you want to stop tracking a certificate, you can delete it.
{: shortdesc}  

To delete a certificate, complete the following steps:

1. Select the check box for the certificate that you want to delete.
2. Click the **Trash** icon.

## Updating certificates metadata
{: #updating-certificates-metadata}

You can also update the name and description of a certificate.
{: shortdesc}

To update a certificate, complete the following steps:

1. Select a row to open the details for that certificate.
2. Update the name or description.
3. Save your changes.

You can perform up to five update actions per minute.
{: tip}
