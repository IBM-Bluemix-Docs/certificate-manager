---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

keywords: certificates, SSL, TLS, activity tracker,

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

# Evénements d'Activity Tracker  
{: #at_events}

Utilisez le service {{site.data.keyword.at_full}} pour suivre comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long}} dans {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Le service {{site.data.keyword.at_short}} enregistre des activités initiées par l'utilisateur qui change l'état d'un service dans {{site.data.keyword.cloud_notm}}. Ainsi, quand vous importez un certificat, un événement est généré. pour plus d'informations, voir la [documentation {{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

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
    <td>`cloudcerts.certificate.order`</td>
	  <td>Commande un certificat.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Réimporte un certificat.</td>
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

Les événements sont automatiquement transmis à l'instance de service {{site.data.keyword.at_short}} au même emplacement que celui où le service {{site.data.keyword.cloudcerts_short}} est mis à disposition.

## Informations complémentaires
{: #info}

* La zone *requestData_str* inclut le nom lisible du certificat.

## Disponibilité
{: #at-availability}

* La prise en charge pour {{site.data.keyword.at_short}} est actuellement disponible pour les emplacements **Dallas** et **Francfort**.
* Pour d'autres emplacements, mettez à disposition une instance du service Activity Tracker obsolète en attendant qu'{{site.data.keyword.at_short}} soit disponible.
