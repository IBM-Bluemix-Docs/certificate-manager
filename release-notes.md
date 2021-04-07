---

copyright:
  years: 2017, 2021
lastupdated: "2021-04-07"

keywords: certificates, ssl, tls, new, sydney, exact search, dns provider, lets encrypt, renew certificate, order certificates

subcollection: certificate-manager

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}


# What's new
{: #release-notes}

The following features and changes to the {{site.data.keyword.cloudcerts_long}} service are available.

## 7 April 2021
{: #7april2021}

- **Live in Osaka**
  {{site.data.keyword.cloudcerts_short}} is available in the Osaka location.

## 18 January 2021
{: #18january2021}

- **Bring your own key (BYOK) support**
  You can now integrate with {{site.data.keyword.keymanagementserviceshort}} and {{site.data.keyword.hscrypto}} to encrypt your certificates by using a root key that you own and manage. For more information, see [Protecting your sensitive data in {{site.data.keyword.cloudcerts_short}}](/docs/certificate-manager?topic=certificate-manager-mng-data#data-encryption).

## 15 June 2020
{: #15june2020}

- **{{site.data.keyword.cloud_notm}} service endpoints support in London, Frankfurt, Tokyo and Sydney**
  You can now connect to {{site.data.keyword.cloudcerts_short}} in the London, Frankfurt, Tokyo, and Sydney locations by using the {{site.data.keyword.cloud_notm}} private network. To learn more, see [Regions and endpoints](/docs/certificate-manager?topic=certificate-manager-regions-endpoints).

## 25 May 2020
{: #25may2020}

- **Live in Washington DC**
  {{site.data.keyword.cloudcerts_short}} is available in the Washington DC location.

- **{{site.data.keyword.cloud_notm}} service endpoints support in Dallas and Washington DC**
  Connect to {{site.data.keyword.cloudcerts_short}} by using a private IP that is accessible only through the {{site.data.keyword.cloud_notm}} private network. To learn more, see [Regions and endpoints](/docs/certificate-manager?topic=certificate-manager-regions-endpoints).

## 14 May 2020
{: #14May2020}

- **Deprecated endpoint URLs that end in `bluemix.net`**
  {{site.data.keyword.cloudcerts_short}} API endpoints that end in `bluemix.net` are now deprecated with end of support scheduled for 12 September 2020. After 12 September 2020, the following API endpoints for {{site.data.keyword.cloudcerts_short}} will no longer be accessible:
    - `https://us-south.certificate-manager.bluemix.net`
    - `https://eu-gb.certificate-manager.bluemix.net`

  If you're using these endpoints to target {{site.data.keyword.cloudcerts_short}} operations, search for the deprecated endpoints in your scripts, {{site.data.keyword.openwhisk_short}} actions, and other apps that manage {{site.data.keyword.cloudcerts_short}} resources. Then, replace the endpoints with the following supported URLs:
    - `https://us-south.certificate-manager.cloud.ibm.com`
    - `https://eu-gb.certificate-manager.cloud.ibm.com`

  To view a list of supported API endpoints for {{site.data.keyword.cloudcerts_short}}, see [Regions and endpoints](/docs/certificate-manager?topic=certificate-manager-regions-endpoints).

## 8 March 2020
{: #8March2020}

- **Support for any subdomain**
  Certificate ordering now extends to any subdomain.

## 25 February 2020
{: #25February2020}

- **Certificate ordering for subdomains and for wildcard multi-domain (SAN)**
  Certificate ordering now extends to subdomains, and for wildcard multi-domains.

## 9 February 2020
{: #9February2020}

- **Certificate auto-renewal**
  Ordered certificates can be enabled to be auto-renewed 31 days before expiration. [Learn more about ordering certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates).

- **Latest channel version**
  The payload received by a Callback URL contains the current channel version and the latest channel version available. See [Notification event types and payload versions](/docs/certificate-manager?topic=certificate-manager-notifications-event-types).

- **Changes to life-cycle events**
  - Ordered/Renewed Let's Encrypt certificates will no longer trigger the `cert_about_to_expire_renew_required` notification once issued and 60 days before expiration.
  - `cert_issued_not_downloaded` notification will be triggered if the certificate is not downloaded 30 days after it was issued.
  - `cert_renewed_not_downloaded` notification will be triggered if the renewed certificate is not downloaded, 30, 10, 1 days before and the day your previous issued certificate expires.
  - Test notification channel triggers new event type: `test_notification_channel`

## 21 November 2019
{: #21November2019}

- **PCI certification**
  {{site.data.keyword.cloudcerts_short}} is PCI compliant.

## 2 September 2019
{: #2September2019}

- **Live in Sydney**
  {{site.data.keyword.cloudcerts_short}} is available in the Sydney location.

- **Exact search**
  Enclose your search term with double-quotes to search for an exact value.

## 8 July 2019
{: #8July2019}

- **IBM Cloud Internet Services as a DNS provider**
  You can now use IBM Cloud Internet Services as a DNS provider, simplifying the certificate ordering experience. [Learn more about ordering certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates).

## 10 June 2019
{: 10June2019}

- **Renew ordered Let's Encrypt certificates**
  You can now renew Let's Encrypt certificates that you have ordered using {{site.data.keyword.cloudcerts_short}}. [Learn more about ordering certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates).

## 6 May 2019
{: #6May2019}

- **Order Let's Encrypt certificates**
  You can now order Let's Encrypt certificates. [Learn more about ordering certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates).

## 18 February 2019
{: #18February2019}

- **Live in Tokyo**
  {{site.data.keyword.cloudcerts_long_notm}} is available in the Tokyo location.

## 13 January 2019
{: #13January2019}
- **Callback payload version 3**
  [See the API documentation](/apidocs/certificate-manager){: external}.

## 6 January 2019
{: #6January2019}
- **Deprecated APIs**
  The **List certificates** and **Search certificates repository** v2 APIs are deprecated and will be removed at a future date. You must upgrade to v3 APIs. For more information, [see the API documentation](/apidocs/certificate-manager){: external}.

## 9 December 2018
{: #9December2018}
- **Additional certificate formats**
{{site.data.keyword.cloudcerts_short}} supports the following certificate formats: RSA, DSA, ECDSA, ECDH.

## 5 December 2018
{: #5December2018}
- **Reimport notification**
When you reimport a renewed certificate in place of an expiring one, you can get a notification that the certificate was reimported. This will remind you and your team to deploy the renewed certificate to SSL/TLS termination points. This notification is available only for newly created notification channels.

- **{{site.data.keyword.cloudcerts_short}} is available in the Frankfurt location.**
The service is compliant with the EU requirements.

## 2 December 2018
{: #2December2018}
- **Callback and Slack payload version 2**
  [See the API documentation](/apidocs/certificate-manager){: external}.

## 14 November 2018
{: #14November2018}

- **Reimport**
  You can update a certificate by reimporting a new version that has the same domain as the existing certificate, but with a new expiry date. When a certificate is reimported, the existing version of the certificate is retained as a backup, see [Reimporting a certificate](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

- **1000 certificates per instance**
  You can import up to 1000 certificates per instance.

## 28 October 2018
{: #28October2018}

- **Announcements banner**
  Service announcements, such as API deprecations and other news, are displayed in the **Manage** tab.

## 12 September 2018
{: #12September2018}

- **Certificate name is mandatory**
  It is mandatory to supply a value for the certificate's name when you import a certificate.

- **Deprecated APIs**
  The **Import a certificate** and **Update a certificate's metadata** v2 APIs are deprecated and will be removed on 1 December 2018. You must upgrade to v3 APIs. For more information, [see the API documentation](/apidocs/certificate-manager){: external}.

- **Grouped Slack notifications**
  Notifications in Slack are grouped by expiration date.

## 2 September 2018
{: #2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} is generally available**
  The {{site.data.keyword.cloudcerts_short}} service is generally available (GA) in {{site.data.keyword.cloud_notm}}.

## 22 August 2018
{: #22August2018}

- **Live in London**
  {{site.data.keyword.cloudcerts_long_notm}} Beta is available in the London location.

## 15 August 2018
{: #15August2018}

- **Remove deprecated v1 APIs**
  Version 1 APIs are no longer available. If you haven't updated your API yet, you must do it as soon as possible. For more information, [see the API documentation](/apidocs/certificate-manager){: external}.

- **Platform roles replaced with Service roles**
  You can control access to {{site.data.keyword.cloudcerts_short}} instances by using Service roles. [Learn more about access management](/docs/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12 July 2018
{: #12July2018}

- **Callback notifications**
  Added callback support for notifications. You can choose to either send notifications to Slack or use any callback URL to post notifications. For example, you can send notifications to PagerDuty, automatically open an issue in GitHub, or trigger renewal scripts. [Learn more about notifications](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 12 June 2018
{: #12June2018}

- **Slack notifications**
  Added Slack notifications so that you never miss an expiring certificate. [Learn more about notifications](/docs/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8 January 2018
{: #8January2018}

- **Deprecated APIs**
  Version 1 APIs are deprecated and will be removed on 8 September 2018. You must upgrade to v2 APIs. For more information, [see the API documentation](/apidocs/certificate-manager){: external}.

## 19 December 2017
{: #19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} is available as a beta service**
  The {{site.data.keyword.cloudcerts_short}} service is available as a beta service in {{site.data.keyword.cloud_notm}}.
