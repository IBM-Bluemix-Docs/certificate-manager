
---
copyright:
  years: 2018
lastupdated: "2018-09-13"

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

## 12 septembre 2018
{: 12September2018}

- **Un nom de certificat est obligatoire**  
  Il est obligatoire de fournir une valeur pour nom du certificat lorsque vous importez un certificat.  
  En outre, les API **Importer un certificat** et **Mettre à jour les métadonnées du certificat** version 2 sont obsolètes et seront supprimées le 1er novembre 2018. Vous devez les mettre à niveau vers les API version 3. Pour plus d'informations, voir la [documentation sur les API](https://console.bluemix.net/apidocs/certificate-manager).

- **Notifications Slack regroupées**  
  Dans Slack, les notifications sont regroupées par date d'expiration.

## 2 septembre 2018
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} est en disponibilité générale**  
  Le service {{site.data.keyword.cloudcerts_short}} est en disponibilité générale dans {{site.data.keyword.cloud_notm}}.

## 22 août 2018
{: 22August2018}

- **Opérationnel au Royaume-Uni**  
  {{site.data.keyword.cloudcerts_long_notm}} version bêta est disponible dans le sud du Royaume-Uni.

## 15 août 2018
{: 15August2018}

- **Suppression des API version 1 obsolètes**  
  Les API version 1 ne sont plus disponibles. Si vous n'avez pas encore mis à jour votre API, vous devez le faire dès que possible. [Revoyez la documentation relative aux API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/apidocs/).

- **Rôles de plateforme remplacés par des rôles de service**  
  Vous pouvez contrôler l'accès aux instances {{site.data.keyword.cloudcerts_short}} à l'aide de rôles de service. [En savoir plus sur la gestion des accès](access-management.html).

## 12 juillet 2018
{: 12July2018}

- **Notifications de rappel**  
  Ajout de la prise en charge des rappels pour les notifications. Vous pouvez choisir d'envoyer des notifications à Slack ou utiliser toute URL de rappel pour envoyer des notifications. Par exemple, vous pouvez envoyer des notifications à PagerDuty, ouvrir automatiquement un problème dans GitHub u déclencher des scripts de renouvellement. [En savoir plus sur les notifications](notifications-dashboard.html).

## 12 juin 2018
{: 12June2018}

- **Notifications Slack**  
  Ajout de notifications Slack de sorte que vous êtes averti lorsqu'un certificat qui arrive à expiration. [En savoir plus sur les notifications](notifications-dashboard.html).

## 19 décembre 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} est disponible en tant que service bêta**  
  Le service {{site.data.keyword.cloudcerts_short}} est disponible en tant que service bêta dans {{site.data.keyword.cloud_notm}}.
