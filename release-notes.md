
---

copyright:
  years: 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Release notes
{: #release-notes}

The following features and changes to the {{site.data.keyword.cloudcerts_long}} service are available.

## 14 November 2018
{: 14November2018}

- **Reimport**    
  You can update a certificate by reimporting a new version that has the same domain as the existing certificate, but with a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup, see [Reimporting a certificate](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).
  
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
  The **Import a certificate** and **Update a certificate's metadata** v2 APIs are deprecated and will be removed on 1 December 2018. You must upgrade to v3 APIs. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/certificate-manager).

- **Grouped Slack notifications**  
  Notifications in Slack are grouped by expiration date.

## 2 September 2018
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} is generally available**  
  The {{site.data.keyword.cloudcerts_short}} service is generally available (GA) in {{site.data.keyword.cloud_notm}}.

## 22 August 2018
{: 22August2018}

- **Live in the United Kingdom**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta is available in the United Kingdom region (UK South).

## 15 August 2018
{: 15August2018}

- **Remove deprecated v1 APIs**  
  Version 1 APIs are no longer available. If you haven't updated your API yet, you must do it as soon as possible. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/).

- **Platform roles replaced with Service roles**  
  You can control access to {{site.data.keyword.cloudcerts_short}} instances by using Service roles. [Learn more about access management](access-management.html).

## 12 July 2018
{: 12July2018}

- **Callback notifications**  
  Added callback support for notifications. You can choose to either send notifications to Slack or use any callback URL to post notifications. For example, you can send notifications to PagerDuty, automatically open an issue in GitHub, or trigger renewal scripts. [Learn more about notifications](notifications-dashboard.html).

## 12 June 2018
{: 12June2018}

- **Slack notifications**  
  Added Slack notifications so that you'll never miss an expiring certificate. [Learn more about notifications](notifications-dashboard.html).

## 8 January 2018
{: 8January2018}

- **Deprecated APIs**  
  Version 1 APIs are deprecated and will be removed on 8 September 2018. You must upgrade to v2 APIs. For more information, [see the API documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/certificate-manager).

## 19 December 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} is available as a beta service**  
  The {{site.data.keyword.cloudcerts_short}} service is available as a beta service in {{site.data.keyword.cloud_notm}}.
