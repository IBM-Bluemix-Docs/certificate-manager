---

copyright:
  years: 2017, 2020
lastupdated: "2020-01-23"

keywords: certificates, ssl, tls, manage certificates, cert ui, third-party issuer, pem format, openssl, import certificate, download certificate, renew certificates

subcollection: certificate-manager

---

{:external: target="_blank" .external}
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

# Managing certificates from the dashboard
{: #managing-certificates-from-the-dashboard}

You can use the {{site.data.keyword.cloudcerts_full}} service dashboard to manage certificates that you obtain from third-party issuers to use with your {{site.data.keyword.IBM_notm}} cloud-based apps or services.
{: shortdesc}

## Supported certificate formats and public key algorithms
{: supported-formats-and-algorithms}

### Certificate formats
* PEM

Review the OpenSSL documentation to learn how to convert other certificate formats (such as P12 and CRT) to PEM.
{: note} 

### Public key algorithms
* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman key agreement protocol (ECDH)

## Importing a certificate
{: #importing-a-certificate}

Import your certificates so that you can manage them.
{: shortdesc}

### Before you begin
{: #importing-before}

* Create a valid, unexpired certificate with a matching private key (key is optional).
* Convert the files into Privacy-enhanced Electronic Mail (PEM) format.
* The certificate must be a X.509 compliant certificate.
* Keep the private key unencrypted to ensure that it can be imported.

To import a certificate, click **Import Certificate** and provide the following details:

1. Provide a certificate name.
2. Select the certificate file in PEM format by clicking **Browse**.
3. Optional: Select the certificate's private key in PEM format by clicking **Browse**.
4. If applicable, provide the intermediate certificate file in PEM format.
5. Optional: Enter a description.
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
    <td>The certificate signature algorithm.</td>
  </tr>
  <tr>
    <td>Key algorithm</td>
    <td>The public key algorithm</td>
  </tr>
  <tr>
    <td>Expires in</td>
    <td>The number of remaining days before the certificate is no longer valid. </td>
  </tr>
  <tr>
    <td>Valid from</td>
    <td>The date on which the certificate became valid, in Coordinated Universal Time timezone. </td>
  </tr>
  <tr>
    <td>Expires on</td>
    <td>The date on which the certificate is no longer valid (in Coordinated Universal Time timezone). </td>
  </tr>
  <tr>
    <td>Status</td>
    <td>The status of your certificate. </td>
  </tr>
  <tr>
    <td>Certificate ID</td>
    <td>The generated ID given to the certificate upon import.</td>
  </tr>
</table>

</br>

## Reimporting a certificate
{: #reimport-certificate}

If your certificate is about to expire, you can update it by importing a new version that has the same domain as the existing certificate, but has a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup that can be downloaded if required.
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

Reimporting certificates is limited to five actions per minute.
{: note}

### Downloading a previous version of your certificate
{: #downloading-certificate}

To download the previous version of a certificate, complete the following steps:

1. Expand the row for the certificate.
2. Click the **Previous version** link.

## Ordering certificates
{: #order-certificates}

Before you order a certificate, [first complete the required setup](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates).  
To order a certificate, click **Order Certificate**, select either **{{site.data.keyword.cis_full_notm}}** or **Another DNS Provider** and provide the following details:

1. Certificate name.
2. Certificate Authority.
3. Required domains.
4. Appropriate algorithm and key algorithm.
5. Click **Order**.

Ordering certificates is limited to five orders/minute per {{site.data.keyword.cloudcerts_short}} instance, 100 orders per hour per IBM user account, and five certificates for the same domains per week.
{: note}

## Renewing certificates
{: #renew-certificates}

Ordered certificates can be either manually renewed or automatically renewed.

You can only renew certificates that you ordered through {{site.data.keyword.cloudcerts_short}}.
{: note}

To select a certificate to automatically renew:

1. While ordering the certificate, set the auto-renewal toggle to **On**.
2. After ordering a certificate, select **Enable Auto-renewal** from a certificate's side menu.

To disable a certificate from automatically renewing:

1. Select **Disable Auto-renewal** from a certificate's side menu.

If a manual renew is needed, complete the following steps:
1. Click the menu in the row of the certificate you want to renew.
2. Click **Renew Certificate**.
3. Optional: You can choose to rekey your certificate by checking the **Rekey certificate** check box. This renews your certificate with a new key pair.

  When you rekey a certificate, make sure to deploy the new certificates and keys everywhere they are in use.
  {: note}
  
4. Click **Renew**.

Renewing a certificate is limited to five renewal requests per certificate per minute, 100 renewal per hour per IBM user account.
{: note}

## Searching certificates
{: #searching-certificates}

If you manage many certificates, you can use the search bar to locate the required certificate.
{: shortdesc}

* To search for a certificate name, domain, or issuer, start to type your term into the search bar and press **Enter**.
* To search for an exact value, enclose your search term with double-quotes.
* To view all of your certificates, click the **X** icon in the search bar.

## Downloading certificates
{: #downloading-certificates}

When you are ready to deploy your certificate to your app or service, you can download the certificate and the associated private key.
{: shortdesc}

To download a certificate, complete the following steps:

1. Select the check box for the certificate that you want to download.
2. Click **Download Certificate**. Depending on what you imported into the service, you receive a compressed file that contains PEM files for the certificate, an associated private key, and an associated intermediate certificate.

You cannot download expired certificates.
{: note}

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
{: note}
