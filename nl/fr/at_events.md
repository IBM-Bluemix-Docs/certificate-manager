---

copyright:
  years: 2018
lastupdated: "2018-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Evénements {{site.data.keyword.cloudaccesstrailshort}}  
{: #at_events}

Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour suivre comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long_notm}} dans {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre des activités initiées par l'utilisateur qui change l'état d'un service dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Ainsi, quand vous importez un certificat, un événement {{site.data.keyword.cloudaccesstrailshort}} est généré.

Le tableau suivant répertorie les méthodes d'API qui génèrent un événement lorsqu'elles sont appelées. 

<table>
  <caption>Tableau 1. Actions qui génèrent des événements</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Importe un certificat. </td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Réimporte un certificat. </td>
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
	  <td>Met à jour des métadonnées de certificat (en changeant, par exemple, la description d'un certificate).</td>
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
{: #ui}

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont disponibles dans le **domaine de compte** {{site.data.keyword.cloudaccesstrailshort}} qui se trouve à l'endroit {{site.data.keyword.Bluemix_notm}} où les événements sont générés.

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont automatiquement transférés vers le service {{site.data.keyword.cloudaccesstrailshort}} au même endroit que celui où le service {{site.data.keyword.cloudcerts_short}} est mis à disposition.

## Informations complémentaires
{: #info}

La zone *requestData_str* inclut le nom lisible du certificat.
