---

copyright:
  years: 2017, 2021
lastupdated: "2021-01-26"

keywords: certificate lifecycle, ssl, tls, notifications, notification channels, events, event types, slack, payload, callback url

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


# Notifications event types
{: #notifications-event-types}

When you're working with {{site.data.keyword.cloudcerts_short}}, you can configure notification channels that alert you to various lifecycle events. The type of event and the payload that is delivered might be different depending on the version of the notification channel that you're using.
{: shortdesc}

## Event types
{: #notification-types}

Check out the following tables to see which event types are available for each notification channel version.

## Test notification channel
{: #test-notification-channel}

Notification event type for testing a channel.

| Notification description | Event type | Supported Callback URL channel version | Supported Slack channel version |
|--------------------------|------------|----------------------------------------|---------------------------------|
| Test channel | `test_notification_channel`    | v1 or higher | v1 or higher |

### For imported certificates  
{: #imported-certificates}

Notification event types for imported certificates.

| Notification description | Event type | Supported Callback URL channel version | Supported Slack channel version |
|--------------------------|------------|----------------------------------------|---------------------------------|
| Imported certificate about to expire | `cert_about_to_expire_reimport_required`    | v1 or higher | v1 or higher |
| Imported certificate expired | `cert_expired_reimport_required` | v1 or higher | v1 or higher |
| Certificate reimported | `cert_reimported` | v2 or higher |    v2 or higher |
{: caption="Table 1. Notification event types for imported certificates and the version on which they're available" caption-side="top"}

### For ordered certificates   
{: #ordered-certificates}

Notification event types for ordered certificates.

| Notification description | Event type | Supported Callback URL channel version | Supported Slack channel version |
|--------------------------|------------|----------------------------------------|---------------------------------|
| Ordered certificate issued | `cert_issued` | v4 or higher | v3 or higher |
| Ordered certificate renewed | `cert_renewed` | v4 or higher | v3 or higher |
| Certificate order failed | `cert_order_failed` | v4 or higher | v3 or higher |
| Certificate renewal failed | `cert_renew_failed` | v4 or higher | v3 or higher |
| Issued certificate about to expire | `cert_about_to_expire_renew_required` | v4 or higher | v3 or higher |
| Issued certificate expired | `cert_expired_renew_required` | v4 or higher | v3 or higher |
| Certificate domain validation required | `cert_domain_validation_required` | v4 or higher |  N/A |
| Certificate domain validation completed | `cert_domain_validation_completed` | v4 or higher  | N/A | 
| Certificate issued but not download | `cert_issued_not_downloaded` | v4 or higher  | v3 or higher | 
| Certificate renewed but not download | `cert_renewed_not_downloaded` | v4 or higher  | v3 or higher | 
{: caption="Table 2. Notification event types for ordered certificates and the version on which they're available" caption-side="top"}

Newly created notification channels are always created with the latest version release.
{: tip}

For more information about the differences between the channel versions, see the following updates.

## Slack channel versions
{: #slack-channel-versions}

### Version 3 (updated) (February 9th, 2020)
{: #slack-v3-update}

- Added new event types:
  - Issued certificate was not downloaded
  - Renewed certificate was not downloaded

### Version 3
{: #slack-v3}

- New event types:
   - Ordered certificate issued
   - Ordered certificate renewed
   - Certificate order failed
   - Certificate renew failed
   - Issued certificate about to expire
   - Issued certificate expired

### Version 2
{: #slack-v2}

- New notification for reimported certificates

### Version 1
{: #slack-v1}

- Notifications are sent only for expiring certificates.

## Callback URL payload versions
{: #callback-url-payload-versions}

### Latest available version of notifications payload structure
{: #callback-url-latest}


#### Certificates lifecycle notification
{: #callback-lifecycle} 

```
{
   "instance_crn": <instance crn>,
   "certificate_manager_url": <url for instance's dashboard>,
   "event_type": <event type>,
   "expiry_date": <timestamp of midnight of expiration date, for events of type cert_about_to_expire_reimport_required, cert_about_to_expire_renew_required>,
   "certificates":[
      {
         "cert_crn": <certificate crn>,
         "name": <certificate name>,
         "domains": <list of domains delimited with comma>,
         "expires_on": <certificate expiration timestamp>,
         "additional_info": <error info if certificate order was failed, for events of types cert_renew_failed, cert_order_failed>,
         "auto_renewed": <true/false - if certificate was autorenewed, for events of types cert_renewed, cert_renew_failed and cert_renewed_not_downloaded>
         "previous_expires_on": <expiration of certificate before renew, for events of type cert_renewed_not_downloaded>
      },
      ...
   ],
   "version": 4,
   "latestVersion": <latest available channel version>
} 
```

#### Domain validation notification
{: #callback-domain-validation}

```
{
   "instance_crn": <instance crn>,
   "certificate_manager_url": <url for instance's dashboard>,
   "event_type": <event type>,
   "certificateCRN": <certificate crn>,
   "domain_validation_method": <domain validation type, for example, dns-01>
   "domain": <domain to validate>,
   "challenge": {
      "txt_record_name": <txt record name>,
      "txt_record_val": <txt record value>
   },
   "version": 4,
   "latestVersion": <latest available channel version>
}
```

### Version 4 (updated) (February 9th, 2020)
{: #callback-v4-update}

- Added new event types
   - `cert_issued_not_downloaded`
   - `cert_renewed_not_downloaded`
- Field `auto_renewed = true` added to auto renewed certificates in the events `cert_renewed` and `cert_renewed_not_downloaded`
- Field `previous_expires_on` added to renewed certificates in the event `cert_renewed_not_downloaded`. It contains expiration for the previous version of renewed certificate

### Version 4 (May 6th, 2019)
{: #callback-v4}

- New event types:
  - `cert_issued`
  - `cert_renewed`
  - `cert_order_failed`
  - `cert_renew_failed`
  - `cert_about_to_expire_renew_required`
  - `cert_expired_renew_required`
- `expiry_date` field is present only in event types `cert_about_to_expire_reimport_required` and `cert_about_to_expire_renew_required`. The payload structure remains the same as version 3.
- Added notifications for the new event types `cert_domain_validation_required` and `cert_domain_validation_completed`, with a new payload structure: 

   ```
   {
      "instance_crn": "<INSTANCE_CRN>",
      "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
      "event_type": "<EVENT_TYPE>",
      "certificateCRN": "<CERTIFICATE_CRN>",
      "domain_validation_method": "<DOMAIN_VALIDATION_TYPE>", // dns-01
      "domain": "<DOMAIN_TO_VALIDATE>",
      "challenge": {
         "txt_record_name": "<TXT_RECORD_NAME>" ,
         "txt_record_val": "<TXT_RECORD_VALUE>"
      },
      "version": 4,
      "latestVersion": <latest available channel version>
   }
   ```

### Version 3
{: #callback-v3}

- The `expiry_date` field is present only in event type `cert_about_to_expire_reimport_required`.
- The field `expires_on` is added to each certificate in an array. For example:

   ```
   {
      "instance_crn": "<INSTANCE_CRN>",
      "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
      "event_type": "<EVENT_TYPE>",
      "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
      "certificates":[
            {
               "cert_crn":"<CERTIFICATE_CRN>",
               "name":"<CERTIFICATE_NAME>",
               "domains":"<CERTIFICATE_DOMAIN>",
               "expires_on": <EXPIRY_DAY_TIMESTAMP>,
            },
            ...
      ],
      "version": 3,
      "latestVersion": <latest available channel version>     
   }
   ```

### Version 2
{: #callback v2}

- A new notification for reimported certificates.
- The field name `expiring_certificates` is changed to `certificates`.
- The field name `event_type` is new. Possible options include: 
   - `cert_about_to_expire_reimport_required`
   - `cert_expired_reimport_required`
   - `cert_reimported`
   - `test_notification_channel`
- The updated payload looks similar to the following example:

   ```
   {
      "instance_crn": "<INSTANCE_CRN>",
      "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
      "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
      "event_type": "<EVENT_TYPE>",
      "certificates":[
            {
               "cert_crn":"<CERTIFICATE_CRN>",
               "name":"<CERTIFICATE_NAME>",
               "domains":"<CERTIFICATE_DOMAIN>"
            },
            ...
      ],
      "version": 2,
      "latestVersion": <latest available channel version>     
   }
   ```

### Version 1
{: #callback-v1}

- Your notification is returned as a payload. For example:

   ```
   {
      "instance_crn": "<INSTANCE_CRN>",
      "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
      "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
      "expiring_certificates":[
            {
               "cert_crn":"<CERTIFICATE_CRN>",
               "name":"<CERTIFICATE_NAME>",
               "domains":"<CERTIFICATE_DOMAIN>"
            },
            ...
      ],
      "version": 1,
      "latestVersion": <latest available channel version>        
   }
   ```
