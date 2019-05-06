---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

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
{:faq: data-hd-content-type='faq'}

# Frequently asked questions (FAQs)
{: #faq}

Frequently asked questions about {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## What format do my certificates need to be in?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} supports PEM formatted certificates only.

## What type of public key algorithms are supported?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} supports certificates with public keys generated using the following public key algorithms:

* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman key agreement protocol (ECDH)


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

You can update a certificate by reimporting a new version of the certificate that has the same domain as the existing
certificate, but has a new expiry date. When a certificate is reimported, the existing version of the certificate is
retained as a backup, see [Reimporting a certificate](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

## Can I make specific certificates visible only to specific users?
{: #access-policies}
{: faq}

Certificates can be protected by using IAM access policies to achieve granular access control, see [Managing service access roles](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## How do I revoke an issued certificate?
{: #revoke-certificate}
{: faq}

{{site.data.keyword.cloudcerts_short}} currently has no revocation API you can use. However, you can use the Let's
Encrypt API to revoke certificates by using the certificate private key. You can
learn how to revoke Let's Encrypt certificates in the [Let's Encrypt documentation](https://letsencrypt.org/docs/revoking/)

## My certificate order status is in pending state for a long time

{: #certificate-order-status}
{: faq}

On slow DNS networks an order may take up to about 20 minutes to complete successfully.

## For how long will Certificate Manager try to validate that you own  domains you requested in your certificate order?

{: #certificate-order-validation}
{: faq}

After sending the domain validation challenge, {{site.data.keyword.cloudcerts_short}} will try to validate that you own the domains you requested for up to 10 minutes.
If your dns is not updated with the TXT record challenge within 10 minutes, your order will fail.

## How do I check the status of my certificate order using the {{site.data.keyword.cloudcerts_short}} public API?

{: #certificate-order-status}
{: faq}

 Use the `Get certificate metadata` API to poll the certificate order status.

## Can I be notified once my order is complete?

{: #certificate-order-notification}
{: faq}

If you have a notification channel configured, you will be notified once your certificate is issued, or if your order failed.
Note that the version of your notification channel should be v4 or higher.

## My order failed. Why?

{: #certificate-order-failure}
{: faq}

You can find an error code and message in the certificate metadata, UI, and in the notification you received when your order failed.

## Why am I not receiving certificate order events in my existing Slack notification channel?
{: #missing-notification-for-ordered-certificate}
{: faq}

Upgrade your Slack notification channel to the latest version in the Certificate Manager Settings tab.
