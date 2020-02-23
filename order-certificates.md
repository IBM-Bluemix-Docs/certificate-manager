---

copyright:
  years: 2017, 2020
lastupdated: "2020-02-23"

keywords: certificates, ssl, tls, dns, renewal, renew certificate, order certificate, private key, certificate authority, secure, public cert, lets encrypt, pending state

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
{:help: data-hd-content-type='help'} 
{:support: data-reuse='support'}

# Ordering certificates
{: #ordering-certificates}

You can use {{site.data.keyword.cloudcerts_long}} to order public SSL/TLS certificates for your apps and services that are signed by supported external Certificate Authorities. {{site.data.keyword.cloudcerts_short}} makes it easy for you to order public certificates in addition to providing extra security for your SSL/TLS private keys. After your certificate is issued, you can deploy it to integrated services, or download it for use elsewhere.  
{: shortdesc}

When you order a certificate, your private key for SSL/TLS is generated directly in {{site.data.keyword.cloudcerts_short}} and stored securely. All requests and access to issued certificates can be managed through [access control](/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles) and automatically audited by using [{{site.data.keyword.at_short}}](/docs/certificate-manager?topic=certificate-manager-at_events).  

{{site.data.keyword.cloudcerts_short}} implements the Automatic Certificate Management Environment (ACME) v2 Protocol as an ACME client. The ACME protocol makes it possible to automatically obtain browser trusted certificates without human intervention.

## Certificate characteristics
{: #certificate-characteristics}

When you order certificates through {{site.data.keyword.cloudcerts_short}}:

- They are free
- They are valid for 90 days
- They can be Single Domain, Multi-Domain (SAN), or a wildcard
- They are domain validated

Domain validation includes the verification that you own the domain for which you are requesting a certificate. If you need Extended Validation (EV) or Organization Validated (OV) certificates, you can obtain them elsewhere and import them to {{site.data.keyword.cloudcerts_short}} to manage their lifecycle.

## Certificate ordering limitations
{: #certificate-ordering-limitations}

* You can order a certificate only for domains that can resolve the Authoritative Name Server. On Linux or macOS it can be checked using the command: `host -t ns <your_domain>`. On Windows it can be checked using `nslookup <your_domain>`.
* You can order a certificate for a CNAME subdomain which spans up to 3 levels to your host domain. Example: you can order a certificate for CNAME _c3.c2.c1_ in the domain _mydomain.org_. 
* You can order a SAN certificate with a wildcard domain and additional domains not including direct subdomains. Example: You can order a certificate for the domains _*.mydomain.org_ and _*.www.mydomain.org_, but not for the domains _*.mydomain.org_ and _www.mydomain.org_.
* You can order a certificate with a primary domain length that is no longer than 64 characters.
* The {{site.data.keyword.cloudcerts_short}} console is limited to display up to 100 domains to select from, when using {{site.data.keyword.cis_short}} (CIS) as the DNS provider. If you don't see the domain(s) you need to make the order use the {{site.data.keyword.cloudcerts_short}} order API and specify the domain(s).

## Supported Certificate Authorities
{: #supported-certificate-authorities}

A Certificate Authority (CA) is an entity that issues digital certificates. The CA acts as a trusted third party for both the requester of the certificate and the client that relies on the certificate.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) is a free, automated, ACME-based CA that provides domain validated certificates valid for 90 days. It is a service that is provided by the Internet Security Research Group (ISRG).

## Setting up certificate ordering
{: #setup}

Before a certificate can be issued to you, {{site.data.keyword.cloudcerts_short}} must verify that you control all of the domains that you list in your request. To do so, {{site.data.keyword.cloudcerts_short}} uses DNS validation. Note that certificate ordering is an asynchronous operation.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} sends a challenge in the form of a Domain Name System (DNS) TXT record for you to add in your DNS service. For each domain that you request in your certificate, you get a separate DNS TXT record. After you add the DNS TXT record, {{site.data.keyword.cloudcerts_short}} and Let’s Encrypt check whether it's in your DNS service. If you successfully complete the challenge, you are issued a Let’s Encrypt certificate that is available in your {{site.data.keyword.cloudcerts_short}} instance.

How you verify domain ownership depends on whether you use {{site.data.keyword.cis_full_notm}} or another DNS provider.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

If you manage your domains in {{site.data.keyword.cis_short}}, complete the following steps to verify ownership:

1. Navigate to **{{site.data.keyword.cloud_notm}} > Manage > Access (IAM) > Authorizations**.
2. Click **Create** and assign a source and target service. The source service is granted access to the target service based on the roles that you set in the next step.
  * Source: {{site.data.keyword.cloudcerts_short}}
  * Target: Internet Services
3. Specify a service instance for both the source and the target.
4. Assign the **Reader** role to allow {{site.data.keyword.cloudcerts_short}} to view the {{site.data.keyword.cis_short_notm}} instance and its domains. Then, click **Authorize**.

  For testing purposes, you can assign the **Manager** service access role through the UI to manage all of your domains. If you do so, then you do not need to complete step 5. For production environments it is recommended that you assign the **Reader** service access role, and use the API as shown in step 5 to control specific domains.  
  {: note}
   
5. To control specific domains, assign the **Manager** role by using the API so that {{site.data.keyword.cloudcerts_short}} can manage the DNS records for the individual domains that exist in your {{site.data.keyword.cis_short_notm}} instance. You might want to copy the command to a text file to make it easy to edit the required parameters.
   
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 

  <table>
    <caption>Table 1. The variables for the previous command explained</caption>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><b>token</b></td>
      <td>A valid IAM token. You can find the value by using the {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><b>account ID</b></td>
      <td>The ID for the account where the {{site.data.keyword.cloudcerts_short}} and {{site.data.keyword.cis_short_notm}} instances exist. You can find the value by navigating to <b>{{site.data.keyword.cloud_notm}} > Manage > Account > Account Settings</b> or by using the {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><b>Certificate-Manager-GUID-based-instanceID</b></td>
      <td>The GUID-based ID for your instance of {{site.data.keyword.cloudcerts_short}}. To find the value, use the {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><b>Cloud-Internet-Services-GUID-based-instanceID</b></td>
      <td>The GUID-based ID for your instance of {{site.data.keyword.cis_short_notm}}. To find the value, use the {{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><b>domain ID</b></td>
      <td>The ID of your domain as it is found in {{site.data.keyword.cis_short_notm}}. To find the value, use the {{site.data.keyword.cloud_notm}} CLI to run <code>ibmcloud cis domains</code>. To manage multiple domains, modify the <code>resources</code> array.</td>
    </tr>
  </table>

You're now ready to [order a certificate](/docs/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)!


### Another DNS Provider
{: #other_provider}

To verify your control over a domain when you're using a third-party DNS provider, {{site.data.keyword.cloudcerts_short}} sends a TXT record to a Callback URL notifications channel that you provide, which allows for you to automate the domain validation process.

A Callback URL is a prerequisite for ordering certificates when using a DNS Provider that is not {{site.data.keyword.cis_full_notm}}. [Learn more about configuring a callback URL](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).  
{: note}

First, you implement a callback server for domain validation, and then you provide its endpoint to a Callback URL notifications channel.  To get started, see [setting up a Callback URL notifications channel](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

For more information about setting up domain validation by using a Callback URL notifications channel, see [this blog post](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}. Also provided are [these sample implementations of domain validation](https://github.com/ibm-cloud-security/certificate-manager-domain-validation-cloud-function-sample){: external} using Cloud Function actions for {{site.data.keyword.cis_short_notm}}, Cloudflare, and SoftLayer.  
{: tip}

#### Responding to a challenge
{: #responding-to-challenge}

The notifications channel receives a notification with the following structure:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notifications channel version that supports order related notifications - 4 and greater
}
```
{: screen}

Once the DNS TXT challenge is sent to your Callback URL, you have to answer the challenge within 10 minutes. {{site.data.keyword.cloudcerts_short}} checks to see whether the challenge is complete. Once it is verified that you answered the challenge, you are sent a second notification to let you know you can remove the TXT record.

To see frequently asked questions about ordering certificates, [review the FAQ page](/docs/certificate-manager?topic=certificate-manager-faq).  
{: tip}

## Ordering certificates
{: #ordering-certificate}
{: help} 
{: support}

To order a certificate, use the {{site.data.keyword.cloudcerts_short}} dashboard.

1. Navigate to the Manage tab of the {{site.data.keyword.cloudcerts_short}}.
2. Click **Order Certificate** 
3. Select your DNS provider - either {{site.data.keyword.cis_full_notm}}, or another DNS Provider.
4. If you've selected **{{site.data.keyword.cis_full_notm}}**, provide the following details:
   - Complete the required setup instructions
   - Provide a certificate name and optionally a description
   - Select a Certificate Authority
   - Select the {{site.data.keyword.cis_full_notm}} instance you've assigned a service access role for
   - Select the certificate type that you need
   - Select the domain
   - Select the appropriate algorithm and key algorithm
   - Click **Order**
5. If you've selected **Another DNS Provider**, provide the following details:
   - Complete the required setup instructions.
   - Provide a certificate name and optionally a description.
   - Select a Certificate Authority.
   - Enter the primary domain and any alternative domains.
   - Select the appropriate algorithm and key algorithm.
   - Click **Order**.

Your order is placed in a **Pending** state. After you answer the domain validation challenge and {{site.data.keyword.cloudcerts_short}} verifies that you own the requested domain, you are issued the certificate and its state will change to **Valid**. You're notified when your certificate is ready or if there was a problem, in your Slack and/or Callback URL notifications channel.

## Renewing certificates
{: #renew-certificate}
{: help} 
{: support}

When you order certificates from {{site.data.keyword.cloudcerts_short}}, you can choose to enable auto-renewal. When you set up auto-renewal, requests are handled in the same way as they are when you order a certificate. Like when you order, {{site.data.keyword.cloudcerts_short}} sends a DNS txt challenge to your callback URL, so that you can prove that you own the domains that correlate to the certificates that you're trying to renew.

There are a few things to keep in mind:

  * When your certificate is renewed, the previous version of your certificate is retained in case you need it.
  * By default, {{site.data.keyword.cloudcerts_short}} does not automatically renew ordered certificates.
  * You can only renew certificates that you ordered through {{site.data.keyword.cloudcerts_short}}.

When you start the renewal process, your renewal is placed in a **Renew pending** state. When the domain validation challenge completes and {{site.data.keyword.cloudcerts_short}} verifies that you own the requested domain, you get a renewed certificate and its state changes to **Valid**. You are notified when your automatically renewed certificate is ready or if there was a problem, in your notification channels.

After renewing a certificate either manually or automatically you must deploy it. [Learn how to automate deployments](/docs/certificate-manager?topic=certificate-manager-automating-deployments).
{: important}

### Enabling automatic renewal of certificates 
{: #enable-autorenew}  
To select a certificate to automatically renew:

1. While ordering the certificate, set the auto-renewal toggle to **On**.
2. After ordering a certificate, select **Enable Auto-renew** from a certificate's side menu.

Auto-renewed certificate will be renewed 31 days before they expire.  
{: tip}

If you enable Auto-renew for a certificate that expire in less than 31 days, it must be manually renewed before expiration.  Only then, following renewal cycles will become automatic.  
{: important}

### Disabling automatic renewal of certificates
{: #disable-autorenew}

To disable a certificate from automatically renewing:

1. Select **Disable Auto-renew** from a certificate's side menu.

### Manually renewing certificates
{: #manual-renew}

You can also request to renew your certificate through {{site.data.keyword.cloudcerts_short}} manually.  

1. Select **Renew Certificate** from a certificate's side menu.
2. Optional: You can choose to rekey your certificate by checking the **Rekey certificate** check box. This renews your certificate with a new key pair. When you rekey a certificate, make sure to deploy the new certificates and keys everywhere they are in use.
3. Click **Renew**.
