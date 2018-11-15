---

copyright:
  years: 2018,
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
{:faq: data-hd-content-type='faq'}

# Frequently asked questions (FAQs)
{: #faq}

Frequently asked questions about {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## What type of certificates can I store in {{site.data.keyword.cloudcerts_short}}?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} supports PEM formatted certificates only.

## Can I upload password-protected private keys?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} does not support importing certificates with password-protected private keys.

## I’m trying to upload a certificate and private key and get this error: `Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}
{: faq}

Depending on whether your private key is encrypted, choose one of the following options:

* The private key is encrypted. Make sure you decrypt the private key before you upload it.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* The private key is not encrypted. Make sure the certificate and the private key match by comparing the results of the following command, where `<certificate-file>` is the name of your certificate file and `<key-file>` is the name of your private key file:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## Can I receive email notifications for expiring certificates?
{: #email-notifications}
{: faq}

Only Callback and Slack notifications are supported.

## Can I version control my certificates?
{: #certificate-versioning}
{: faq}

You can update a certificate by reimporting a new version of the certificate that has the same domain as the existing certificate, but has a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup, see [Reimporting a certificate](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

## Can I make specific certificates visible only to specific users?
{: #access-policies}
{: faq}

Certificates can be protected by using IAM access policies to achieve granular access control, see [Managing service access roles](access-management.html).
