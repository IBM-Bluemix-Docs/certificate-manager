---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-04"

keywords: certificates, SSL,

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

# Release notes
{: #release-notes}

The following features and changes to the {{site.data.keyword.cloudcerts_long}} service are available.

## 2 September 2019
{: 2September2019}

- **Live in Sydney**  
  {{site.data.keyword.cloudcerts_long_notm}} is available in the Sydney location.

- **Exact search**  
  Enclose your search term with double-quotes to search for an exact value.
  
## 8 July 2019
{: 8July2019}

- **IBM Cloud Internet Services as a DNS provider**  
  You can now use IBM Cloud Internet Services as a DNS provider, simplifying the certificate ordering experience. [Learn more about ordering certificates](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 10 June 2019
{: 10June2019}

- **Renew ordered Let's Encrypt certificates**  
  You can now renew Let's Encrypt certificates that you have ordered using {{site.data.keyword.cloudcerts_short}}. [Learn more about ordering certificates](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 6 May 2019
{: 6May2019}

- **Order Let's Encrypt certificates**  
  You can now order Let's Encrypt certificates. [Learn more about ordering certificates](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 18 February 2019
{: 18February2019}

- **Live in Tokyo**  
  {{site.data.keyword.cloudcerts_long_notm}} is available in the Tokyo location.

## 13 January 2019
{: 13January2019}
- **Callback payload version 3**  
  [See the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/certificate-manager).

## 6 January 2019
{: 6January2019}
- **Deprecated APIs**  
  The **List certificates** and **Search certificates repository** v2 APIs are deprecated and will be removed at a future date. You must upgrade to v3 APIs. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/certificate-manager).

## 9 December 2018
{: 9December2018}
- **Additional certificate formats**    
{{site.data.keyword.cloudcerts_short}} supports the following certificate formats: RSA, DSA, ECDSA, ECDH.

## 5 December 2018
{: 5December2018}
- **Reimport Notification**    
When you reimport a renewed certificate in place of an expiring one, you can get a notification that the certificate was reimported. This will remind you and your team to deploy the renewed certificate to SSL/TLS termination points. This notification is available only for newly created notification channels.

- **{{site.data.keyword.cloudcerts_short}} is available in the Frankfurt location.**     
The service is compliant with the EU requirements.

## 2 December 2018
{: 2December2018}
- **Callback and Slack payload version 2**  
  [See the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/certificate-manager).

## 14 November 2018
{: 14November2018}

- **Reimport**  
  You can update a certificate by reimporting a new version that has the same domain as the existing certificate, but with a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup, see [Reimporting a certificate](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

- **1000 certificates per instance**  
  You can import up to 1000 certificates per instance.

## 28 October 2018
{: 28October2018}

- **Announcements banner**  
  Service announcements, such as API deprecations and other news, are displayed in the **Manage** tab.

## 12 September 2018
{: 12September2018}

- **Certificate name is mandatory**  
  It is mandatory to supply a value for the certificate's name when you import a certificate.  

- **Deprecated APIs**  
  The **Import a certificate** and **Update a certificate's metadata** v2 APIs are deprecated and will be removed on 1 December 2018. You must upgrade to v3 APIs. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/certificate-manager).

- **Grouped Slack notifications**  
  Notifications in Slack are grouped by expiration date.

## 2 September 2018
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} is generally available**  
  The {{site.data.keyword.cloudcerts_short}} service is generally available (GA) in {{site.data.keyword.cloud_notm}}.

## 22 August 2018
{: 22August2018}

- **Live in London**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta is available in the London location.

## 15 August 2018
{: 15August2018}

- **Remove deprecated v1 APIs**  
  Version 1 APIs are no longer available. If you haven't updated your API yet, you must do it as soon as possible. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/).

- **Platform roles replaced with Service roles**  
  You can control access to {{site.data.keyword.cloudcerts_short}} instances by using Service roles. [Learn more about access management](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12 July 2018
{: 12July2018}

- **Callback notifications**  
  Added callback support for notifications. You can choose to either send notifications to Slack or use any callback URL to post notifications. For example, you can send notifications to PagerDuty, automatically open an issue in GitHub, or trigger renewal scripts. [Learn more about notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback).

## 12 June 2018
{: 12June2018}

- **Slack notifications**  
  Added Slack notifications so that you never miss an expiring certificate. [Learn more about notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8 January 2018
{: 8January2018}

- **Deprecated APIs**  
  Version 1 APIs are deprecated and will be removed on 8 September 2018. You must upgrade to v2 APIs. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/certificate-manager).

## 19 December 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} is available as a beta service**  
  The {{site.data.keyword.cloudcerts_short}} service is available as a beta service in {{site.data.keyword.cloud_notm}}.
