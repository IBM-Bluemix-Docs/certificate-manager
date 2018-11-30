---

copyright:
  years: 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Notes sur l'édition
{: #release-notes}

Les fonctions et modifications suivantes sont disponibles pour le service {{site.data.keyword.cloudcerts_long}}.

## 14 novembre 2018
{: 14November2018}

- **Réimporter**  
Vous pouvez mettre à jour un certificat en important une nouvelle version avec le même domaine que le certificat existant, mais avec une nouvelle date d'expiration. Lorsqu'un certificat est réimporté, la version existante de celui-ci est conservée en tant que sauvegarde. Voir [Réimportation d'un certificat](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).


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
  Les API **Importer un certificat** et **Mettre à jour les métadonnées du certificat** version 2 sont obsolètes et seront supprimées le 1er décembre 2018. Vous devez les mettre à niveau vers les API version 3. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/apidocs/certificate-manager).

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
  Les API version 1 ne sont plus disponibles. Si vous n'avez pas encore mis à jour votre API, vous devez le faire dès que possible. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/apidocs/).

- **Rôles de plateforme remplacés par des rôles de service**  
  Vous pouvez contrôler l'accès aux instances {{site.data.keyword.cloudcerts_short}} à l'aide de rôles de service. [En savoir plus sur la gestion des accès](access-management.html).

## 12 juillet 2018
{: 12July2018}

- **Notifications de rappel**  
  Ajout de la prise en charge des rappels pour les notifications. Vous pouvez choisir d'envoyer des notifications à Slack ou utiliser toute URL de rappel pour envoyer des notifications. Par exemple, vous pouvez envoyer des notifications à PagerDuty, ouvrir automatiquement un problème dans GitHub u déclencher des scripts de renouvellement. [En savoir plus sur les notifications](notifications-dashboard.html).

## 12 juin 2018
{: 12June2018}

- **Notifications Slack**  
  Ajout de notifications Slack de sorte qui vous préviennent lorsqu'un certificat qui arrive à expiration. [En savoir plus sur les notifications](notifications-dashboard.html).

## 8 janvier 2018
{: 8January2018}

- **API obsolètes**  
  Les API version 1 sont obsolètes et seront retirées le 8 septembre 2018. Vous devez les mettre à niveau vers les API version 2. Pour plus d'informations, [voir la documentation API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/apidocs/certificate-manager).

## 19 décembre 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} est disponible en tant que service bêta**  
  Le service {{site.data.keyword.cloudcerts_short}} est disponible en tant que service bêta dans {{site.data.keyword.cloud_notm}}.
