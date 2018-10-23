---

copyright:
  years: 2018,
lastupdated: "2018-10-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Frequently asked questions (FAQs)
{: #faq}

Frequently asked questions about {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## What type of certificates can I store in {{site.data.keyword.cloudcerts_short}}?
{: #supported-certificate-types}

{{site.data.keyword.cloudcerts_short}} supports PEM formatted certificates only.

## Can I upload password-protected private keys?
{: #password-protected-private-keys}

{{site.data.keyword.cloudcerts_short}} does not support importing certificates with password-protected private keys.

## I’m trying to upload a certificate and private key and get this error: `Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}

1. The private key is encrypted. Make sure you decrypt the private key before you upload it.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

2. The private key is not encrypted. Make sure the certificate and the private key match by comparing the results of the following command, where `<certificate-file>` is the name of your certificate file and `<key-file>` is the name of your private key file:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## Can I receive email notifications for expiring certificates?
{: #email-notifications}

Callback and Slack notifications only are supported.

## Can I version control my certificates?
{: #certificate-versioning}

You cannot re-import or change the version a certificate. Instead, you can import another copy of the certificate, with a renewed expiration date.

## Can I make specific certificates visible only to specific users?
{: #access-policies}

Certificates can be protected by using IAM access policies to achieve granular access control, see [Managing service access roles](access-management.html).
