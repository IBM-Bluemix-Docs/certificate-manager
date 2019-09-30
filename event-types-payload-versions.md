---

copyright:
  years: 2017, 2019
lastupdated: "2019-09-30"

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

# Available event types
{: event-types-payload-versions}

When you're working with Certificate Manager, you can configure notifications that alert you to common lifecycle management activities. Notifications are devlivered through channels that you configure. The type of event and payload that is delivered might be different depending on the version of the channel that you're using.
{: shortdesc}



## Notification event types
{: notification-event-types}

Check out the following table to see which event types are available for each channel version.
{: shortdesc}

| Notification description | Event type | Supported Callback URL channel version | Supported Slack channel version |
|--------------------------|------------|----------------------------------------|---------------------------------|
| Imported certificate about to expire | cert_about_to_expire_reimport_required    | v1 or higher | v1 or higher |
| Imported certificate expired | cert_expired_reimport_required | v1 or higher | v1 or higher |
| Certificate reimported | cert_reimported | v2 or higher |    v2 or higher |
| Ordered certificate issued | cert_issued | v4    or higher | v3 or higher |
| Ordered certificate renewed | cert_renewed | v4    or higher | v3 or higher |
| Certificate order failed | cert_order_failed | v4 or higher | v3 or higher |
| Certificate renewal failed | cert_renew_failed | v4 or higher | v3 or higher |
| Issued certificate about to expire | cert_about_to_expire_renew_required | v4 or higher |    v3 or higher |
| Issued certificate expired | cert_expired_renew_required | v4 or higher |    v3 or higher |
| Certificate domain validation required | cert_domain_validation_required | v4 or higher |    N/A |
| Certificate domain validation completed | cert_domain_validation_completed | v4 or higher    | N/A | 
{: caption="Table 1. Notification event types and the version on which they're available" caption-side="top"}

Newly created notification channels are always created with the latest version release.
{: tip}


## Slack channel versions
{: slack-channel-versions}

When new capabilities are available to the Slack notifications channel, the version number increases.

<dl>
   <dt>Version 3</dt>
      <dd>New event types:<ul><li>Ordered certificate issued</li> <li>Ordered certificate renewed</li> <li>Certificate order failed</li> <li>Issued certificate about to expire</li> <li>Issued certificate expired</li></ul>Version 2</dd>
   <dt>Version 2</dt>
      <dd>New notification for reimported certificates.</dd>
   <dt>Version 1</dt>
      <dd>Notifications are sent only for expiring certificates.</dd>
</dl>



## Callback URL payload versions
{: callback-url-payload-versions}



### Version 4 (May 6th, 2019)
* Added new event types:
   * cert_issued
   * cert_renewed
   * cert_order_failed
   * cert_renew_failed
   * cert_about_to_expire_renew_required
   * cert_expired_renew_required

* Field `expiry_date` exists only in messages with event type `cert_about_to_expire_reimport_required` or `cert_about_to_expire_renew_required` and doesn't exist in messages with other event types.    

Payload structure (no change from v3):       
```
{
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "event_type": "<EVENT_TYPE>",

    // event data
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
    "certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "name":"<CERTIFICATE_NAME>",
             "domains":"<CERTIFICATE_DOMAIN>",
             "expires_on": <EXPIRY_DAY_TIMESTAMP>,
          },
          ...
     ]     
}
```

* Added notifications for new event types with new payload structure:
   * **cert_domain_validation_required**
   * **cert_domain_validation_completed**    

 New payload structure:  
 ```
 {
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "event_type": "<EVENT_TYPE>",

    //event data
    "userToken": "<TOKEN_OF_USER_ORDERED_CERTIFICATE>",
    "certificateCRN": "<CERTIFICATE_CRN>",
    "domain_validation_method": "<DOMAIN_VALIDATION_TYPE>", // dns-01
    "domain": "<DOMAIN_TO_VALIDATE>",
    "challenge": {
        "txt_record_name": "<TXT_RECORD_NAME>" ,
        "txt_record_val": "<TXT_RECORD_VALUE>"
    }
 }   
 ```

#### Version 3 (January 13th, 2019)
* Field `expiry_date` exists only in messages with event type **cert_about_to_expire_reimport_required** and doesn't exist in  messages with other event types.
* Field `expires_on` was added to each certificate in array.

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
     ]     
}
```

#### Version 2 (December 2nd, 2018)
* New notification for reimported certificates.
* Field name was changed from `expiring_certificates` to `certificates`.  
* New field `event_type` was added. Possible values:
  * **cert_about_to_expire_reimport_required** - for certificates that are about to expire in 1,10,30,60,90 days
  * **cert_expired_reimport_required** - for certificates that expired today or earlier
  * **cert_reimported** - for certificates that were reimported

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
    ]      
}
```

#### Version 1  
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
     ]     
}
```