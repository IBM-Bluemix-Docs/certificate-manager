---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-30"

keywords: certificates, SSL, dns,

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

{{site.data.keyword.cloudcerts_short}} sends a challenge in the form of a Domain Name System (DNS) TXT record for you to add in your DNS service. For each domain that you request in your certificate, you get a separate DNS TXT record. After you add the DNS TXT record, {{site.data.keyword.cloudcerts_short}} and Let’s Encrypt check whether it's in your DNS service. If you successfully complete the challenge, you are issued a Let’s Encrypt certificate that is available in your {{site.data.keyword.cloudcerts_short}} instance.

How you verify domain ownership depends on which DNS provider you are using:

- {{site.data.keyword.cis_full_notm}}
- Another DNS Provider

### {{site.data.keyword.cis_full_notm}}
{: #cis}

If you manage your domains in {{site.data.keyword.cis_short}}, complete these instructions:

1. Assign your {{site.data.keyword.cloudcerts_short}} instance a **Reader** service access role for your instance of {{site.data.keyword.cis_short_notm}} from {{site.data.keyword.cloud_notm}} > Manage (IAM)  > Authorizations.

   For testing purposes you can assign **Manager** service access role instead, to manage all domains in your {{site.data.keyword.cis_full_notm}} instance. When assigning this service access role, step 2 below is not required. This setting is not recommended for use in production environment.
   {: note}

2. Assign a **Manager** service access role for your instance of {{site.data.keyword.cloudcerts_short}} so that it can manage select domains in your {{site.data.keyword.cis_short_notm}} instance.

  From command-line, execute the following `cURL` request:
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies -H 'Accept: application/json' -H 'Content-Type: application/json'  -H 'Authorization: Bearer Replace-with-User-token' -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": <Replace-with-account-ID }, { "name": "serviceInstance", "value": Replace-with-Certificate-Manager-GUID-based-instance ID } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": <accountId>  }, { "name": "serviceInstance", "value": Replace-with-Cloud-Internet-Services-GUID-based-instance-ID}, { "name": "domainId", "value": <domainId> }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: pre} 
  
   
  Replace the following placeholders: 

  - **User token** - A valid IAM token. Find the value using the {{site.data.keyword.cloud_notm}} CLI: `ibmcloud iam oauth-tokens`.
  - **accountId** - The account ID where the {{site.data.keyword.cloudcerts_short}} and {{site.data.keyword.cis_short_notm}} instances were created at. Find the value either in **{{site.data.keyword.cloud_notm}} > Manage > Account > Account Settings**, or using the {{site.data.keyword.cloud_notm}} CLI: `ibmcloud account show`. The value must be prefixed with `a/<the accountId>`. 
  - **{{site.data.keyword.cloudcerts_short}} GUID-based instance ID** - Find the value using the {{site.data.keyword.cloud_notm}} CLI: `ibmcloud resource service-instance "Instance name"` and copy the returned **GUID**.
  - **{{site.data.keyword.cis_short_notm}} GUID-based instance ID** - Find the value using the {{site.data.keyword.cloud_notm}} CLI: `ibmcloud resource service-instance "Instance name"` and copy the returned **GUID**.
  - **domainId** - Find the value in the {{site.data.keyword.cis_short_notm}} UI, or using the {{site.data.keyword.cloud_notm}} CLI: `ibmcloud cis domains`.  
  If you would like to manage multiple domains, modify the the `resources` array.  

You can now proceed to [Ordering certificates](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate).

### Another DNS Provider
{: #other_provider}

To verify your control over a domain when using a 3rd party DNS provider, {{site.data.keyword.cloudcerts_short}} sends the TXT record to a Callback URL notifications channel that you provide, which allows you to automate the domain validation process.

First implement an IBM Cloud Function action, and provide its endpoint to a Callback URL notifications channel in {{site.data.keyword.cloudcerts_short}}.  
[Learn how to set up a Callback URL notifications channel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

You can follow the instructions provided in [this blog post ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains) to setup this type of domain validation.
{: tip}

#### Responding to challenge
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

To order a certificate, complete the following steps:

1. Navigate to the Manage tab of the {{site.data.keyword.cloudcerts_short}}.
2. Click **Order Certificate** 
3. Select your DNS provider - either {{site.data.keyword.cis_full_notm}}, or Another DNS Provider
4. If you've selected **{{site.data.keyword.cis_full_notm}}**, provide the following details:
   1. Complete the required setup instructions
   2. Provide a certificate name and optionally a description
   3. Select a Certificate Authority
   4. Select the {{site.data.keyword.cis_full_notm}} instance you've assigned **Manager** service access role for
   5. Select the certificate type you need
   6. Select the domain
   7. Select the appropriate algorithm and key algorithm
   8. Click **Order**
5. If you've selected **Another DNS Provider**, provide the following details:
   1. Complete the required setup instructions
   2. Provide a certificate name and optionally a description
   3. Select a Certificate Authority.
   4. Enter the primary domain and any alternative domains
   5. Select the appropriate algorithm and key algorithm
   6. Click **Order**

Your order is placed in a **Pending** state. Once you answer the domain validation challenge and {{site.data.keyword.cloudcerts_short}} verifies you own the requested domain(s), you are issued the certificate and its state will change to **Valid**. You're notified when your certificate is ready or if there was a problem, in your Slack and/or Callback URL notifications channel.

## Renewing certificates
{: #renew-certificate}

If your certificate is about to expire, you can request to renew your certificate through {{site.data.keyword.cloudcerts_short}}. When your certificate is renewed, the previous version of your certificate is retained in case you need it. 

Renewals work similar to certificate ordering. When you request to renew a certificate, {{site.data.keyword.cloudcerts_short}} sends DNS txt challenges to your callback URL, so you can again prove that you own the domains for which you are renewing the certificate.

To renew a certificate, complete the following steps:
  1. Click on the menu in the row of the certificate you want to renew
  2. Click **Renew Certificate**
  3. Optional: You can choose to rekey your certificate by checking the **Rekey certificate** check box. This will renew your certificate with a new key pair. When you rekey a certificate, make sure to deploy the new certificates and keys everywhere they are in use
  4. Click **Renew**


You can only renew certificates that you ordered through {{site.data.keyword.cloudcerts_short}}.
{: note}

Your renewal is placed in a **Renew pending** state. Once you answer the domain validation challenge and {{site.data.keyword.cloudcerts_short}} verifies you own the requested domain(s), you'll get a renewed certificate and its state will change to **Valid**. You'll be notified when your renewed certificate is ready or if there was a problem, in your Slack and/or Callback URL notifications channel.
