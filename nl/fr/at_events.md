---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: certificates, SSL, TLS, activity tracker,

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

# Evénements d'Activity Tracker  
{: #at_events}

Utilisez le service {{site.data.keyword.at_full}} pour savoir comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long}} dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Le service {{site.data.keyword.at_short}} enregistre les activités initiées par l'utilisateur qui changent l'état d'un service dans {{site.data.keyword.cloud_notm}}. Ainsi, quand vous importez un certificat, un événement est généré. pour plus d'informations, voir la [documentation {{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

Le tableau suivant répertorie les méthodes d'API qui génèrent un événement lorsqu'elles sont appelées.

<table>
  <caption>Tableau 1. Actions qui génèrent des événements</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Importe un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Réimporte un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>Commande un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.renew`</td>
	  <td>Renouvelle un certificat émis.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>Obtient les métadonnées d'un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Télécharge un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>Répertorie les certificats.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>Répertorie les métadonnées de certificat. Affiche les détails d'un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Recherche des certificats.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Recherche des métadonnées de certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Supprime un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Met à jour des métadonnées de certificat (en changeant, par exemple, la description d'un certificat).</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>Liste les canaux de notifications.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Crée un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Désactive ou active un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Met à jour le noeud final d'un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Supprime un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Teste un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>Une notification a été envoyée au noeud final d'un canal de notification.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>La clé publique a été demandée.</td>
  </tr>
</table>

## Où rechercher les événements ?
{: #at_ui}

Mettez à disposition une instance {{site.data.keyword.at_short}} au même emplacement que votre instance {{site.data.keyword.cloudcerts_short}}.

Exécutez la procédure suivante :

1. Accédez à [{{site.data.keyword.cloud_notm}} - Observabilité](https://cloud.ibm.com/observe/){: external}.
2. Mettez à disposition une instance {{site.data.keyword.at_short}} au même emplacement que votre instance {{site.data.keyword.cloudcerts_short}}.

Les événements sont automatiquement transmis à l'instance de service {{site.data.keyword.at_short}} au même emplacement que celui où le service {{site.data.keyword.cloudcerts_short}} est mis à disposition.

## Informations complémentaires
{: #info}

* La zone *requestData_str* inclut le nom lisible du certificat.

## Disponibilité
{: #at-availability}

Le support {{site.data.keyword.at_short}} est disponible pour les emplacements de **Dallas**, **Francfort**, **Tokyo** et **Londres**.
