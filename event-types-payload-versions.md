---

copyright:
  years: 2017, 2019
lastupdated: "2019-11-19"

keywords: certificate lifecycle, ssl, tls, notifications, notification channels, events, event types, slack, payload, callback url

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
{: #event-types-payload-versions}

When you're working with {{site.data.keyword.cloudcerts_short}}, you can configure notification channels that alert you to various lifecycle events. The type of event and the payload that is delivered might be different depending on the version of the notification channel that you're using.
{: shortdesc}

## Notification event types
{: #notification-event-types}

Check out the following table to see which event types are available for each notification channel version.
{: shortdesc}

| Notification description | Event type | Supported Callback URL channel version | Supported Slack channel version |
|--------------------------|------------|----------------------------------------|---------------------------------|
| Imported certificate about to expire | `cert_about_to_expire_reimport_required`    | v1 or higher | v1 or higher |
| Imported certificate expired | `cert_expired_reimport_required` | v1 or higher | v1 or higher |
| Certificate reimported | `cert_reimported` | v2 or higher |    v2 or higher |
| Ordered certificate issued | `cert_issued` | v4 or higher | v3 or higher |
| Ordered certificate renewed | `cert_renewed` | v4 or higher | v3 or higher |
| Certificate order failed | `cert_order_failed` | v4 or higher | v3 or higher |
| Certificate renewal failed | `cert_renew_failed` | v4 or higher | v3 or higher |
| Issued certificate about to expire | `cert_about_to_expire_renew_required` | v4 or higher | v3 or higher |
| Issued certificate expired | `cert_expired_renew_required` | v4 or higher | v3 or higher |
| Certificate domain validation required | `cert_domain_validation_required` | v4 or higher |  N/A |
| Certificate domain validation completed | `cert_domain_validation_completed` | v4 or higher  | N/A | 
{: caption="Table 1. Notification event types and the version on which they're available" caption-side="top"}

Newly created notification channels are always created with the latest version release.
{: tip}


## Slack channel versions
{: #slack-channel-versions}

For more information about the differences between the Slack channel versions, see the following updates.

<dl>
   <dt>Version 3</dt>
      <dd>New event types:<ul><li>Ordered certificate issued</li> <li>Ordered certificate renewed</li> <li>Certificate order failed</li> <li>Issued certificate about to expire</li> <li>Issued certificate expired</li></ul></dd>

   <dt>Version 2</dt>
      <dd>New notification for reimported certificates.</dd>

   <dt>Version 1</dt>
      <dd>Notifications are sent only for expiring certificates.</dd>
</dl>

## Callback URL payload versions
{: #callback-url-payload-versions}

For more information about the differences between the Callback URL payload versions, see the following updates.

<dl>
   <dt>Version 4</dt>
      <dd>New event types:<ul><li><code>cert_issued</code></li> <li><code>cert_renewed</code></li> <li><code>cert_renew_failed</code></li> <li><code>cert_about_to_expire_renew_required</code></li> <li><code>cert_expired_renew_required</code></li></ul></dd><br>
      <dd>The <code>expiry_date</code> field is present in event types <code>cert_about_to_expire_reimport_required</code> and <code>cert_about_to_expire_renew_required</code>. The payload structure remains the same as version 3.</dd><br>
      <dd>Added notifications for the new event types <code>cert_domain_validation_required</code> and <code>cert_domain_validation_completed</code>, which updated the payload structure. New payload structure: <pre class="screen"><code> {
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
   </code></pre></dd>

   <dt>Version 3</dt>
      <dd>The <code>expiry_date</code> field is present in event type <code>cert_about_to_expire_reimport_required</code>.</dd><br>
      <dd>The field <code>expires_on</code> is added to each certificate in an array. For example: <pre class="screen"><code> {
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
   </code></pre></dd>

   <dt>Version 2</dt>
      <dd>A new notification for reimported certificates.</dd><br>
      <dd>The field name <code>certificates</code> is changed to <code>expiring_certificates</code>.</dd><br>
      <dd>The field name <code>event_type</code> is new. Possible options include: <ul><li><code>cert_about_to_expire_reimport_required</code></li> <li><code>cert_expired_reimport_required</code></li> <li><code>cert_reimported</code></li></ul><br>The updated payload looks similar to the following example: <pre class="screen"><code> {
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
   </code></pre></dd>

   <dt>Version 1</dt>
      <dd>Your notification is returned as a payload. For example: <pre class="screen"><code> {
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
   </code></pre></dd>
</dl>

