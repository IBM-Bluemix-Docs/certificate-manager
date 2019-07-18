---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# Commande de certificats
{: #ordering-certificates}

Vous pouvez utiliser {{site.data.keyword.cloudcerts_long}} pour commander des certificats SSL/TLS publics pour vos applications et services qui sont signés par des autorités de certification externes prises en charge. {{site.data.keyword.cloudcerts_short}} vous simplifie la commande de certificats publics en plus d'une sécurité renforcée pour vos clés privées SSL/TLS. Une fois que votre certificat est émis, vous pouvez le déployer sur des services intégrés ou le télécharger pour l'utiliser ailleurs.  
{: shortdesc}

Lorsque vous commandes un certificat, votre clé privée pour SSL/TLS est générée directement dans {{site.data.keyword.cloudcerts_short}} et stockée de manière sécurisée. L'ensemble des demandes et accès aux certificats émis peut être géré via le [contrôle d'accès](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles) et être automatiquement audité via [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events).  

{{site.data.keyword.cloudcerts_short}} implémente le protocole ACME (Automatic Certificate Management Environment) version 2 en tant que client ACME. Le protocole ACME rend possible l'obtention automatique de certificats de confiance de navigateur sans intervention humaine.

## Caractéristiques des certificats
{: #certificate-characteristics}

Lorsque vous commandez ces certificats via {{site.data.keyword.cloudcerts_short}} :

- Ils sont gratuits
- Ils sont valides pendant 90 jours
- Il peut s'agir de certificats de domaine unique, multi-domaine (SAN), ou générique
- Ils sont validés par le domaine

La validation de domaine inclut la vérification de votre possession du domaine pour lequel vous demandez un certificat. Si vous avez besoin de certificats EV (validation étendue) ou OV (validé par l'organisation), vous pouvez les obtenir ailleurs et les importer dans {{site.data.keyword.cloudcerts_short}} pour en gérer le cycle de vie.


## Autorités de certification prises en charge
{: #supported-certificate-authorities}

Une autorité de certification (CA) est une entité qui émet des certificats numériques. L'autorité de certification agit en tant tierce partie sécurisée pour le demandeur du certificat et le client qui se base sur ce certificat.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) est une autorité de certification gratuite, automatisée et basée ACME, qui fournit des certificats de domaine validés, valides pour 90 jours.  e service est fourni par la société Internet Security Research Group (ISRG). 

## Configuration de la commande de certificat
{: #setup}

Pour qu'un certificat puisse être émis pour vous, {{site.data.keyword.cloudcerts_short}} doit d'abord vérifie que vous contrôlez tous les domaines figurant dans votre demande. Pour ce faire, {{site.data.keyword.cloudcerts_short}} utilise une validation DNS.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} envoie une demande d'authentification sous forme d'enregistrement TXT de DNS (Domain Name System) pour que vous l'ajoutiez à votre service DNS. Pour chaque domaine demandé dans votre certificat vous recevez un enregistrement TXT DNS distinct. Une fois que vous avez ajouté l'enregistrement TXT DNS, {{site.data.keyword.cloudcerts_short}} et Let’s Encrypt s'assurent qu'il est dans votre service DNS. Si la demande d'authentification aboutit, vous recevez un certificat Let’s Encrypt valable dans votre instance {{site.data.keyword.cloudcerts_short}}.

La façon dont vous vérifiez la propriété de domaine dépend de votre utilisation d'{{site.data.keyword.cis_full_notm}} ou d'un autre fournisseur DNS.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

Si vous gérez vos domaines dans {{site.data.keyword.cis_short}}, exécutez la procédure suivante pour vérifier la propriété :

1. Accédez à **{{site.data.keyword.cloud_notm}} >Gérer > Accès (IAM) > Autorisations**. 
2. Cliquez sur **Créer** et affectez un service source et un service cible. L'accès au service cible est accordé au service source en fonction des rôles que vous définissez à l'étape suivante.
  * Source : {{site.data.keyword.cloudcerts_short}}
  * Cible : Internet Services
3. Indiquez une instance de service pour les service source et cible.
4. Affectez le rôle **Lecteur** afin d'autoriser {{site.data.keyword.cloudcerts_short}} à afficher l'instance {{site.data.keyword.cis_short_notm}} et ses domaines. Cliquez ensuite sur **Autoriser**.

  Vous pouvez, à des fins de test, affecter le rôle d'accès au service **Responsable** via l'interface utilisateur, ce afin de gérer l'ensemble de vos domaines. Dans ce cas, vous n'avez pas besoin d'exécuter l'étape 5. Pour les environnements de production, il est recommandé d'affecter le rôle d'accès au service **Lecteur** et d'utiliser l'API, comme illustré à l'étape 5, afin de contrôler des domaines spécifiques.
  {: note}
   
5. Pour contrôler des domaines spécifiques, affectez le rôle **Responsable** via l'API afin que {{site.data.keyword.cloudcerts_short}} puisse gérer les enregistrements DNS pour les domaines individuels existant dans votre instance {{site.data.keyword.cis_short_notm}}. Vous pouvez copier la commande dans un fichier texte afin de faciliter l'édition des paramètres requis. 
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>Jeton IAM valide. Pour trouver la valeur, vous pouvez utiliser l'interface CLI {{site.data.keyword.cloud_notm}} : <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>ID du compte où existent les instances {{site.data.keyword.cloudcerts_short}} et {{site.data.keyword.cis_short_notm}}. Pour trouver la valeur, accédez à <b>{{site.data.keyword.cloud_notm}} > Gérer > Compte > Paramètres du compte</b> ou utilisez l'interface CLI {{site.data.keyword.cloud_notm}} : <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>ID basé GUID pour votre instance de {{site.data.keyword.cloudcerts_short}}. Pour trouver la valeur, utilisez l'interface CLI {{site.data.keyword.cloud_notm}} : <code>ibmcloud resource service-instance "nom de l'instance"</code>.</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>ID basé GUID pour votre instance de {{site.data.keyword.cis_short_notm}}. Pour trouver la valeur, utilisez l'interface CLI {{site.data.keyword.cloud_notm}} : <code>ibmcloud resource service-instance "nom de l'instance"</code>.</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>ID de votre domaine tel qu'il figure dans {{site.data.keyword.cis_short_notm}}. Pour trouver la valeur, utilisez l'interface CLI {{site.data.keyword.cloud_notm}} pour exécuter la commande <code>ibmcloud cis domains</code>. Pour gérer plusieurs domaines, modifiez le tableau <code>resources</code>.</td>
    </tr>
  </table>

Vous êtes maintenant prêt à [commander un certificat](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)!


### Autre fournisseur DNS 
{: #other_provider}

Pour vérifier votre contrôle sur un domaine lorsque vous utilisez un fournisseur DNS tiers, {{site.data.keyword.cloudcerts_short}} envoie un enregistrement TXT à un canal de notification d'URL de rappel que vous indiquez, ce qui permet d'automatiser le processus de validation de domaine.

Dans un premier temps, vous implémentez une action IBM Cloud Function pour la validation de domaine, puis vous indiquez son noeud final à un canal de notification d'URL de rappel. Pour commencer, voir la [configuration d'un canal de notification d'URL de rappel](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

Pour plus d'informations sur la configuration de la validation de domaine via un canal de notification d'URL de rappel, voir [cet article de blog](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}.
{: tip}


#### Réponse à la demande d'authentification
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

Pour consulter les questions les plus fréquemment posées à propos de la commande de certificats, [consultez la page de la foire aux questions (FAQ)](/docs/services/certificate-manager?topic=certificate-manager-faq).
{: tip}

## Commande de certificats
{: #ordering-certificate}

Pour commander un certificat, procédez comme suit :

1. Accédez à l'onglet Gérer de {{site.data.keyword.cloudcerts_short}}.
2. Cliquez sur **Demander un certificat** 
3. Sélectionnez votre fournisseur DNS - {{site.data.keyword.cis_full_notm}} ou un autre fournisseur DNS.
4. Si vous avez sélectionné **{{site.data.keyword.cis_full_notm}}**, procédez comme suit :
   1. Suivez les instructions de configuration requises
   2. Indiquez un nom de certificat, et éventuellement une description
   3. Sélectionnez une autorité de certification
   4. Sélectionnez l'instance {{site.data.keyword.cis_full_notm}} pour laquelle vous avez affecté un rôle d'accès au service
   5. Sélectionnez le type de certificat dont vous avez besoin
   6. Sélectionnez le domaine
   7. Sélectionnez l'algorithme et l'algorithme de clé appropriés
   8. Cliquez sur **Commander**
5. Si vous avez sélectionné **Autre fournisseur DNS**, procédez comme suit :
   1. Suivez les instructions de configuration requises
   2. Indiquez un nom de certificat, et éventuellement une description
   3. Sélectionnez une autorité de certification.
   4. Indiquez le domaine principal et tout domaine de remplacement
   5. Sélectionnez l'algorithme et l'algorithme de clé appropriés
   6. Cliquez sur **Commander**

Votre commande passe à l'état **En attente**. Une fois que vous avez répondu à la demande d'authentification de validation de domaine et que {{site.data.keyword.cloudcerts_short}} a vérifié que vous détenez bien le domaine concerné, vous recevez le certificat, dont l'état passe à **Valide**. Vous recevez une notification quand le certificat est prêt ou en cas de problème, dans votre canal de notification Slack et/ou URL de rappel.

## Renouvellement de certificats
{: #renew-certificate}

Si votre certificat arrive bientôt à expiration, vous pouvez demander à le renouveler via {{site.data.keyword.cloudcerts_short}}. Quand votre certificat est renouvelé, la version précédente du certificat est conservée au cas où vous en auriez besoin. 

Les renouvellements fonctionnent de façon similaire à la commande de certificat. Lorsque vous demandez à renouveler un certificat, {{site.data.keyword.cloudcerts_short}} envoie des demandes d'authentification TXT DNS à votre URL de rappel afin que vous puissiez à nouveau prouver que vous possédez les domaines pour lesquels vous renouvelez le certificat.

Pour renouveler un certificat, procédez comme suit :
  1. Cliquez sur le menu sur la ligne du certificat à renouveler.
  2. Cliquez sur **Renouveler le certificat**.
  3. Facultatif : Vous pouvez choisir de recomposer votre certificat en cochant la case **Recomposer le certificat**. Le certificat est alors renouvelé avec une nouvelle paire de clés. Lorsque vous recomposez un certificat, veillez à déployer les nouveaux certificats et clés partout où ils sont utilisés.
  4. Cliquez sur **Renouveler**.


Vous pouvez uniquement renouveler des certificats commandés via {{site.data.keyword.cloudcerts_short}}.
{: note}

Votre renouvellement passe à l'état **en attente**. Une fois que vous avez répondu à la demande d'authentification de validation de domaine et que {{site.data.keyword.cloudcerts_short}} a vérifié que vous détenez bien le domaine concerné, vous recevez un certificat renouvelé, dont l'état passe à **Valide**. Vous recevez une notification quand le certificat renouvelé est prêt ou en cas de problème, dans votre canal de notification Slack et/ou URL de rappel.
