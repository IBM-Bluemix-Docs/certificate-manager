---

copyright:
  years: 2017, 2020
lastupdated: "2020-10-28"

keywords: data encryption in Certificate Manager, data storage for Certificate Manager, bring your own keys for Certificate Manager, BYOK for Certificate Manager, key management for Certificate Manager, key encryption for Certificate Manager, personal data in Certificate Manager, data deletion for Certificate Manager, data in Certificate Manager, data security in Certificate Manager

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


# Securing your data in {{site.data.keyword.cloudcerts_short}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.cloudcerts_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored personal data. 
{: shortdesc}



## How your data is stored and encrypted in {{site.data.keyword.cloudcerts_short}}
{: #data-storage}

When you work with the {{site.data.keyword.cloudcerts_short}} service, your data is encrypted at rest with provider-managed encryption. The service generates 256-bit data encryption keys for your instance that are used to encrypt your certificates, private keys, and intermediate certificate chains before they are stored in the service database. To protect the data keys, the service uses an [envelope encryption](#x9860393){: term} process, with a service root key that is managed in {{site.data.keyword.keymanagementservicelong_notm}} as its root of trust, and per-tenant instance keys. {{site.data.keyword.keymanagementserviceshort}} keys are secured by FIPS 140-2 Level 3 certified cloud-based [hardware security modules (HSMs)](#x6704988){: term}.

{{site.data.keyword.cloudcerts_short}} also uses the following security mechanisms to protect your data in transit.

- TLS 1.2+ for end to end communications
- HTTPS for internal communications
- Web App Firewall and DDoS protection



## Deleting your data in {{site.data.keyword.cloudcerts_short}}
{: #data-delete}

When you delete your instance of {{site.data.keyword.cloudcerts_short}}, all of the user data that is associated with it is also deleted. When the service instance is deleted, a 7-day reclamation period begins. During that time, you're able to restore the instance and all of its associated user data. However, if the instance and data are permanently deleted, it can no longer be restored. {{site.data.keyword.cloudcerts_short}} does not store any data from permanently deleted instances.

The {{site.data.keyword.cloudcerts_short}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.cloudcerts_short}} service description, which you can find in the [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).

### Deleting a {{site.data.keyword.cloudcerts_short}} instance
{: #service-delete}

If you no longer need an instance of {{site.data.keyword.cloudcerts_short}}, you can delete the service instance and any data that is stored. Your instance enters a disabled state, and after 7 days its data is permanently deleted. You can also choose to delete your service instance by using the console.

1. Delete the service and place it in a reclamation period of 7 days.

    ```
    ibmcloud resource service-instance-delete "<instance_name>"
    ```
    {: pre}

    Replace `<instance_name>` with the name of the {{site.data.keyword.cloudcerts_short}} instance that you want to delete.

2. Optional: To permanently delete your instance, get the reclamation ID.

    ```
    ibmcloud resource reclamations --resource-instance-id <instance_ID>
    ```
    {: pre}

    Replace `<instance_ID>` with your {{site.data.keyword.cloudcerts_short}} instance ID.

    If you choose to permanently delete the instance by deleting its reclamation, you cannot restore your data.
    {: pre}

3. Optional: Permanently delete the reclamation instance.

    ```
    ibmcloud resource reclamation-delete <reclamation_ID>
    ```
    {: pre}

    Replace `<reclamation_ID>` with the value that you retrieved in the previous step.

### Restoring a deleted service instance
{: #restore-instance}

If you haven't permanently deleted your instance, you can restore it during the 7-day reclamation period. 

1. View which service instances are available for restoration.

  ```
  ibmcloud resource reclamations
  ```
  {: codeblock}

  From the list of available instances, copy the reclamation ID of the {{site.data.keyword.cloudcerts_short}} instance that you want to restore. 

2. Restore the reclamation.

  ```
  ibmcloud resource reclamation-restore <reclamation_ID>
  ```
  {: codeblock}

  Replace `<reclamation_ID>` with the value that you retrieved in the previous step.
