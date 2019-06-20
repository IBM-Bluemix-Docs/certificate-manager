---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

keywords: certificates, SSL,

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

# Commande de certificats
{: #ordering-certificates}

Vous pouvez utiliser {{site.data.keyword.cloudcerts_long}} pour commander des certificats SSL/TLS publics pour vos applications et services qui sont signés par des autorités de certification externes prises en charge. {{site.data.keyword.cloudcerts_short}} vous simplifie la commande de certificats publics en plus d'une sécurité renforcée pour vos clés privées SSL/TLS. Une fois que votre certificat est émis, vous pouvez le déployer sur des services intégrés ou le télécharger pour l'utiliser ailleurs.  
{: shortdesc}

Lorsque vous commandes un certificat, votre clé privée pour SSL/TLS est générée directement dans {{site.data.keyword.cloudcerts_short}} et stockée de manière sécurisée. L'ensemble des demandes et accès aux certificats émis peut être géré via le [contrôle d'accès](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) et être automatiquement audité via [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).  

{{site.data.keyword.cloudcerts_short}} implémente le protocole ACME (Automatic Certificate Management Environment) version 2 en tant que client ACME. Le protocole ACME rend possible l'obtention automatique de certificats de confiance de navigateur sans intervention humaine.

## Caractéristiques des certificats
Les certificats commandés via {{site.data.keyword.cloudcerts_short}} possèdent les caractéristiques suivantes :

- Gratuité
- Période de validité de 90 jours
- Certificats de domaine unique, multi-domaine (SAN), ou générique
- Domaine validé : avant d'émettre un certificat pour vous, l'autorité de certification vérifie que vous détenez le domaine pour lequel vous demandez un certificat.

Si vous avez besoin de certificats EV (validation étendue) ou OV (validé par l'organisation), vous pouvez les obtenir ailleurs et les importer dans {{site.data.keyword.cloudcerts_short}} pour en gérer le cycle de vie.

## Autorités de certification prises en charge
{: #supported-certificate-authorities}

Une autorité de certification (CA) est une entité qui émet des certificats numériques. L'autorité de certification agit en tant que tierce partie digne de confiance pour le demandeur du certificat et le client qui s'appuie sur le certificat.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) est une autorité de certification gratuite, automatisée et basée ACME, qui fournit des certificats de domaine validés, valides pour 90 jours. Ce service est fourni par la société Internet Security Research Group (ISRG). 

## Configuration de la commande de certificat
{: #setup}

Pour qu'un certificat puisse être émis pour vous, {{site.data.keyword.cloudcerts_short}} doit d'abord vérifie que vous contrôlez tous les domaines figurant dans votre demande. {{site.data.keyword.cloudcerts_short}} utilise la validation DNS pour vérifier votre contrôle.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} envoie une demande d'authentification sous forme d'enregistrement TXT de DNS (Domain Name System) pour que vous l'ajoutiez à votre service DNS. Pour chaque domaine demandé dans votre certificat vous recevez un enregistrement TXT DNS distinct. Une fois que vous avez ajouté l'enregistrement TXT de DNS, {{site.data.keyword.cloudcerts_short}} et Let’s Encrypt lance une vérification pour s'assurer qu'il est dans votre service DNS. Si la demande d'authentification aboutit, vous recevez un certificat Let’s Encrypt valable dans votre instance {{site.data.keyword.cloudcerts_short}}.

{{site.data.keyword.cloudcerts_short}} envoie l'enregistrement TXT à une URL de rappel que vous avez indiquée dans les paramètres de notification, ce qui vous permet de facilement automatiser le processus de validation de domaine.

Pour pouvoir commencer à commander des certificats, enregistrez votre URL de rappel en tant que canal de notification dans {{site.data.keyword.cloudcerts_short}}. Mettez ensuite à jour le code permettant de gérer les événements de notification incluant la demande d'authentification TXT. [Apprenez à configurer un canal de notification d'URL de rappel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Réponse à la demande d'authentification
{: #responding-to-challenge}

Le canal de notification reçoit une notification avec la structure suivante :

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

Une fois la demande d'authentification TXT DNS envoyée à votre URL de rappel, vous disposez de 10 minutes pour répondre. {{site.data.keyword.cloudcerts_short}} vérifie si la demande d'authentification est terminée. Une fois que {{site.data.keyword.cloudcerts_short}} a vérifié que vous avez répondu à la demande d'authentification, vous recevez une deuxième notification pour vous indiquer que vous pouvez retirer l'enregistrement TXT.

[Consultez la page Foire aux questions](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) pour des réponses aux questions les plus fréquemment posées concernant la commande de certificats.
{: tip}

## Commande de certificats
{: #ordering-certificate}

1. Accédez à l'onglet Gérer de {{site.data.keyword.cloudcerts_short}}.
2. Cliquez sur **Demander un certificat** et indiquez les informations suivantes :

    1. Indiquez un nom de certificat.
    2. Sélectionnez une autorité de certification.
    3. Indiquez le domaine principal ainsi que tout domaine de remplacement.
    4. Sélectionnez l'algorithme et l'algorithme de clé appropriés. 
    5. Cliquez sur **Commander**.

Votre commande passe à l'état **En attente**. Une fois que vous avez répondu à la demande d'authentification de validation de domaine et que {{site.data.keyword.cloudcerts_short}} a vérifiez que vous détenez bien le ou les domaines, vous recevez le certificat, dont l'état passe à **Valide**. Vous recevez une notification quand le certificat est prêt ou en cas de problème, dans votre canal Slack et/ou URL de rappel.

## Renouvellement de certificats
{: #renew-certificate}

Si votre certificat arrive bientôt à expiration, vous pouvez demander à le renouveler via {{site.data.keyword.cloudcerts_short}}. Quand votre certificat est renouvelé, la version précédente du certificat est conservée au cas où vous en auriez besoin.  

Les renouvellements fonctionnent de façon similaire à la commande de certificat. Lorsque vous demandez à renouveler un certificat, {{site.data.keyword.cloudcerts_short}} envoie des demandes d'authentification TXT DNS à votre URL de rappel afin que vous puissiez à nouveau prouver que vous possédez les domaines pour lesquels vous renouvelez le certificat.

Pour renouveler un certificat, procédez comme suit :
  1. Cliquez sur le menu sur la ligne du certificat à renouveler.
  2. Cliquez sur **Renouveler le certificat**.
  3. Facultatif : Vous pouvez choisir de recomposer votre certificat en cochant la case **Recomposer le certificat**. Le certificat sera alors renouvelé avec une nouvelle paire de clés. 
  
  Lorsque vous recomposez un certificat, veillez à déployer les nouveaux certificats et clés partout où ils sont utilisés.
  {: note}
    
  4. Cliquez sur **Renouveler**
  
  Vous pouvez uniquement renouveler des certificats commandés via {{site.data.keyword.cloudcerts_short}}.
  {: note}

Votre renouvellement passe à l'état **en attente**. Une fois que vous avez répondu à la demande d'authentification de validation de domaine et que {{site.data.keyword.cloudcerts_short}} a vérifiez que vous détenez bien le ou les domaines, vous recevez un certificat renouvelé, dont l'état passe à **Valide**. Vous recevez une notification quand votre certificat renouvelé est prêt ou en cas de problème, dans votre canal Slack et/ou URL de rappel.
