---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-30"

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

# Ordering certificates
{: #ordering-certificates}

You can use {{site.data.keyword.cloudcerts_long}} to order public SSL/TLS certificates for your apps and services that are signed by supported external Certificate Authorities. {{site.data.keyword.cloudcerts_short}} makes it easy for you to order public certificates in addition to extra security for your SSL/TLS private keys. After your certificate is issued, you can deploy it to integrated services, or download it to use it elsewhere.  
{: shortdesc}

When you order a certificate, your private key for SSL/TLS is generated directly in {{site.data.keyword.cloudcerts_short}} and stored securely. All requests and access to issued certificates can be managed through [access control](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) and automatically audited by using [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).  

{{site.data.keyword.cloudcerts_short}} implements the Automatic Certificate Management Environment (ACME) v2 Protocol as an ACME client. The ACME protocol makes it possible to automatically obtain browser trusted certificates without human intervention.

## Certificate characteristics
Certificates that are ordered through {{site.data.keyword.cloudcerts_short}} have the following characteristics:

- Free
- Validity Period - 90 days
- Single domain, Multi-Domain (SAN), or Wildcard certificate
- Domain Validated - before issuing a certificate to you, the Certificate Authority checks that you own the domain for which you are requesting a certificate.

If you need Extended Validation (EV) or Organization Validated (OV) certificates, you can obtain them elsewhere and import them to {{site.data.keyword.cloudcerts_short}} to manage their lifecycle.

## Supported Certificate Authorities
{: #supported-certificate-authorities}

A Certificate Authority (CA) is an entity that issues digital certificates. The CA acts as a trusted 3rd party for both the requester of the certificate and the client that relies on the certificate.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) is a free, automated, ACME-based CA that provides domain validated certificates valid for 90 days. It is a service provided by the Internet Security Research Group (ISRG).

## Setting up certificate ordering
{: #setup}

Before a certificate can be issued to you, {{site.data.keyword.cloudcerts_short}} must verify that you control all of the domains that you listed in your request. {{site.data.keyword.cloudcerts_short}} uses DNS validation to verify your control.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} sends a challenge in the form of a Domain Name System (DNS) TXT record for you to add in your DNS service. For each domain that you request in your certificate, you get a separate DNS TXT record. After you add the DNS TXT record, {{site.data.keyword.cloudcerts_short}} and Let’s Encrypt checks to see whether it's in your DNS service. If you successfully complete the challenge, you are issued a Let’s Encrypt certificate that is available in your {{site.data.keyword.cloudcerts_short}} instance.

{{site.data.keyword.cloudcerts_short}} sends the TXT record to a Callback URL that you provide in the Notifications settings, which allows you to easily automate the domain validation process.

To start ordering certificates, register your Callback URL as a Notification channel in {{site.data.keyword.cloudcerts_short}}. Then, update your code to handle the notification events that include the TXT challenge. [Learn how to set up a Callback URL notification channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Responding to challenge
{: #responding-to-challenge}

The notification channel receives a notification with the following structure:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

Once the DNS TXT challenge is sent to your callback URL, you have to answer the challenge within 10 minutes. {{site.data.keyword.cloudcerts_short}} checks to see whether the challenge is complete. Once {{site.data.keyword.cloudcerts_short}} verifies that you answered the challenge, you are sent a second notification to let you know you can remove the TXT record.

[Review the FAQ page](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) for frequently asked questions about ordering certificates.
{: tip}

## Ordering certificates
{: #ordering-certificate}

1. Navigate to the Manage tab of the {{site.data.keyword.cloudcerts_short}}.
2. Click **Order Certificate** and provide the following details:

    1. Provide a certificate name.
    2. Select a Certificate Authority.
    3. Enter the primary domain and any alternative domains.
    4. Select the appropriate algorithm and key algorithm.
    5. Click **Order**.

Your order is placed in a **Pending** state. Once you answer the domain validation challenge and {{site.data.keyword.cloudcerts_short}} verifies you own the requested domain(s), you are issued the certificate and its state will change to **Valid**. You're notified when your certificate is ready or if there was a problem, in your Slack and/or Callback URL channel.

## Renewing certificates
{: #renew-certificate}

Renewing certificates in {{site.data.keyword.cloudcerts_short}} is currently not supported. You can order a new certificate for the same domains before your existing certificate expires. Let's Encrypt certificates are valid for 90 days. So, we recommend that you order a new one 30 days before your certificate expires to prevent any downtime. You can use {{site.data.keyword.cloudcerts_short}} notifications to be alerted 30 days before your certificate expires.
