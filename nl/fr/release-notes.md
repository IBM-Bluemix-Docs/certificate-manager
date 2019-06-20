---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-10"

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

# Notes sur l'édition
{: #release-notes}

Les fonctions et modifications suivantes sont disponibles pour le service {{site.data.keyword.cloudcerts_long}}.


## 10 juin 2019
{: 10June2019}

- **Renouveler les certificats Let's Encrypt commandés**  
  Vous pouvez désormais renouveler les certificats Let's Encrypt que vous avez commandés via {{site.data.keyword.cloudcerts_short}}. [En savoir plus sur la commande de certificats](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).


## 6 mai 2019
{: 6May2019}

- **Commander des certificats Let's Encrypt**  
  Vous pouvez désormais commander des certificats Let's Encrypt. [En savoir plus sur la commande de certificats](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 18 février 2019
{: 18February2019}

- **Opérationnel à Tokyo**  
  {{site.data.keyword.cloudcerts_long_notm}} est disponible à Tokyo.

## 13 janvier 2019
{: 13January2019}
- **Contenu de rappel version 3**  
  [Voir la documentation d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/certificate-manager).

## 6 janvier 2019
{: 6January2019}
- **API obsolètes**  
  Les API **Répertorier les certificats** et **Rechercher dans un référentiel de certificats** v2 sont obsolètes et seront retirées à une date ultérieure. Vous devez les mettre à niveau vers les API version 3. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/certificate-manager).

## 9 décembre 2018
{: 9December2018}
- **Autres formats de certificat**    
{{site.data.keyword.cloudcerts_short}} prend en charge les formats de certificat suivants : RSA, DSA, ECDSA, ECDH.

## 5 décembre 2018
{: 5December2018}
- **Notification de réimportation**    
Lorsque vous réimportez un certificat renouvelé à la place de celui qui est sur le point d'expirer, vous pouvez recevoir une notification vous indiquant que le certificat a été réimporté. Cela a pour but de vous rappeler et de rappeler à votre équipe que le certificat renouvelé doit être déployé sur les points de terminaison SSL/TLS. Cette notification est disponible uniquement pour les canaux de notification nouvellement créés.

- **{{site.data.keyword.cloudcerts_short}} est disponible à Francfort.**     
Le service est conforme aux exigences de l'Union Européenne.

## 2 décembre 2018
{: 2December2018}
- **Contenu de rappel et Slack version 2**  
  [Voir la documentation d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/certificate-manager).

## 14 novembre 2018
{: 14November2018}

- **Réimporter**  
  Vous pouvez mettre à jour un certificat en important une nouvelle version avec le même domaine que le certificat existant, mais avec une nouvelle date d'expiration. Lorsqu'un certificat est réimporté, la version existante de celui-ci est conservée en tant que sauvegarde. Voir [Réimportation d'un certificat](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

- **1 000 certificats par instance**  
  Vous pouvez importer jusqu'à 1 000 certificats par instance.

## 28 octobre 2018
{: 28October2018}

- **Bannière des annonces**  
  Les annonces de service, telles que les obsolescences d'API et d'autres nouvelles, sont affichées dans l'onglet **Gérer**.

## 12 septembre 2018
{: 12September2018}

- **Un nom de certificat est obligatoire**  
  Il est obligatoire de fournir une valeur pour nom du certificat lorsque vous importez un certificat.  

- **API obsolètes**  
  Les API **Importer un certificat** et **Mettre à jour les métadonnées du certificat** version 2 sont obsolètes et seront supprimées le 1er décembre 2018. Vous devez les mettre à niveau vers les API version 3. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/certificate-manager).

- **Notifications Slack regroupées**  
  Dans Slack, les notifications sont regroupées par date d'expiration.

## 2 septembre 2018
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} est en disponibilité générale**  
  Le service {{site.data.keyword.cloudcerts_short}} est en disponibilité générale dans {{site.data.keyword.cloud_notm}}.

## 22 août 2018
{: 22August2018}

- **Opérationnel à Londres**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta est disponible à Londres.

## 15 août 2018
{: 15August2018}

- **Suppression des API version 1 obsolètes**  
  Les API version 1 ne sont plus disponibles. Si vous n'avez pas encore mis à jour votre API, vous devez le faire dès que possible. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/).

- **Rôles de plateforme remplacés par des rôles de service**  
  Vous pouvez contrôler l'accès aux instances {{site.data.keyword.cloudcerts_short}} à l'aide de rôles de service. [En savoir plus sur la gestion des accès](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12 juillet 2018
{: 12July2018}

- **Notifications de rappel**  
  Ajout de la prise en charge des rappels pour les notifications. Vous pouvez choisir d'envoyer des notifications à Slack ou utiliser toute URL de rappel pour envoyer des notifications. Par exemple, vous pouvez envoyer des notifications à PagerDuty, ouvrir automatiquement un problème dans GitHub u déclencher des scripts de renouvellement. [En savoir plus sur les notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback).

## 12 juin 2018
{: 12June2018}

- **Notifications Slack**  
  Ajout de notifications Slack de sorte qui vous préviennent lorsqu'un certificat qui arrive à expiration. [En savoir plus sur les notifications](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8 janvier 2018
{: 8January2018}

- **API obsolètes**  
  Les API version 1 sont obsolètes et seront retirées le 8 septembre 2018. Vous devez les mettre à niveau vers les API version 2. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/certificate-manager).

## 19 décembre 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} est disponible en tant que service bêta**  
  Le service {{site.data.keyword.cloudcerts_short}} est disponible en tant que service bêta dans {{site.data.keyword.cloud_notm}}.
