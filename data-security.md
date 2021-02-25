---

copyright:
  years: 2017, 2021
lastupdated: "2021-02-24"

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

To ensure that you can securely manage your data when you use {{site.data.keyword.cloudcerts_full}}, it is important to know exactly what data is stored and encrypted and how you can delete any stored personal data. Data encryption by using customer-managed keys is supported by integrations with {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}}.
{: shortdesc}



## How your data is stored and encrypted in {{site.data.keyword.cloudcerts_short}}
{: #data-storage}

When you work with the {{site.data.keyword.cloudcerts_short}} service, your data is encrypted at rest with [envelope encryption](#x9860393){: term}. The service generates 256-bit data encryption keys for your instance that are used to encrypt your certificates, private keys, and intermediate certificate chains before they are stored in the service database. To protect the data keys, the service encrypts them with a root key that is managed in a key management service and backed by FIPS-validated, cryptographic hardware. At no time are your certificates available in clear text while they are stored in the service.

{{site.data.keyword.cloudcerts_short}} also uses the following security mechanisms to protect your data in transit.

- TLS 1.2+ for end to end communications
- HTTPS for internal communications
- Web App Firewall and DDoS protection

## Protecting your sensitive data in {{site.data.keyword.cloudcerts_short}}
{: #data-encryption}

You can add a higher level of encryption control to your data at rest (when it is stored) by enabling integration with a key management service.

The data that you store in {{site.data.keyword.cloud_notm}} is encrypted at rest by using envelope encryption. If you need to control the encryption keys, you can integrate a key management service. This process is commonly referred to as Bring your own keys (BYOK). With a key management service, you can create, import, and manage encryption keys. You can assign access policies to the keys, assign users or service IDs to the keys, or give the key access only to a specific service.

The following table describes your options for managing the encryption of your {{site.data.keyword.cloudcerts_short}} data.

| Encryption | Description |
| ---- | ---- |
| Provider-managed encryption | The data that you store in {{site.data.keyword.cloudcerts_short}} is encrypted at rest by using an IBM-managed key. This is the default setting. |
| Customer-managed encryption | The data that is stored in {{site.data.keyword.cloudcerts_short}} is encrypted at rest by using an encryption key that you own and manage. You can use a root key that you manage in [{{site.data.keyword.keymanagementserviceshort}}](/catalog/services/key-protect) or [{{site.data.keyword.hscrypto}}](/catalog/services/hs-crypto). |
{: caption="Table 1. Encryption options for {{site.data.keyword.cloudcerts_short}}" caption-side="top"}

### About customer-managed keys
{: #about-encryption}

{{site.data.keyword.cloudcerts_short}} uses envelope encryption to implement customer-managed keys. Envelope encryption describes encrypting one encryption key with another encryption key. The key used to encrypt the actual data is known as a [data encryption key (DEK)](#x4791827){: term}. The DEK itself is never stored but is wrapped by a second key that is known as the key encryption key (KEK) to create a wrapped DEK. To decrypt data, the wrapped DEK is unwrapped to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key that is stored in your key management service.

Depending on the sensitivity of your workload, you might choose to work with either {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}} to achieve your wanted level of encryption control. For more information, see [How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-differentiators-key-protect).
{: note}


### Enabling customer-managed keys for {{site.data.keyword.cloudcerts_short}}
{: #using-byok}

If you choose to work with a key that you manage, you must ensure that valid IAM authorization is assigned to the instance of {{site.data.keyword.cloudcerts_short}} that you're working with. To create that authorization, you can use the following steps.

1. Create an instance of [{{site.data.keyword.keymanagementserviceshort}}](/catalog/services/key-protect) or [{{site.data.keyword.hscrypto}}](/catalog/services/hs-crypto)
2. [Generate or import a root key](/docs/key-protect?topic=key-protect-create-root-keys) to your key management service instance.

    When you use {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}} to create a root key, the service generates cryptographic key material that is rooted in cloud-based HSMs. Be sure that the name of your key does not contain any personal information such as your name or location.
3. Grant service access to {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}}.

    You must be the account owner or an administrator for the instance of the key management service that you're working with. You must also have at least Viewer access for the {{site.data.keyword.cloudcerts_short}} service.

    1. Go to **Manage > Access IAM > Authorizations**.
    2. Select the {{site.data.keyword.cloudcerts_short}} service as the source service.
    3. Select the instance of the {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}} as the target service.
    4. Select the key that you created in the previous steps.
    5. Assign the Reader role.
    6. Click **Authorize** to confirm the authorization.

4. Create an instance of the {{site.data.keyword.cloudcerts_short}} service.

    1. Select the region that corresponds to the region for the instance of the key management service that you created previously.
    2. Select your {{site.data.keyword.keymanagementserviceshort}} or {{site.data.keyword.hscrypto}} instance.
    3. Select the **Root key** that you previously authorized.
    4. Click **Create**.

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
