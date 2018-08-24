---

copyright:
  years: 2018
lastupdated: "2018-08-16"

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

Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour suivre comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long}} dans {{site.data.keyword.Bluemix}}.
{:shortdesc}

Le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre des activités initiées par l'utilisateur qui change l'état d'un service dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Ainsi, quand vous importez un certificat, un événement {{site.data.keyword.cloudaccesstrailshort}} est généré.

Le tableau suivant répertorie les méthodes d'API générant un événement lorsqu'elles sont appelées :

<table>
  <caption>Actions qui génèrent des événements</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>Importe un certificat qui est émis par une autorité de certification tiers.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>Télécharge un certificat.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>Répertorie les certificats.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>Répertorie les métadonnées de certificat. Affiche les détails d'un certificat.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>Recherche des certificats.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>Recherche des métadonnées de certificat.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>Supprime un certificat.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>Met à jour un certificat (en changeant, par exemple, sa description).</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channels.list</td>
	  <td>Liste les canaux de notifications.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.create</td>
	  <td>Crée un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.state</td>
	  <td>Désactive ou active un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.update</td>
	  <td>Met à jour le noeud final d'un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.delete</td>
	  <td>Supprime un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.test</td>
	  <td>Teste un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notification.sent</td>
	  <td>Une notification a été envoyée au noeud final d'un canal de notification.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications.publickey</td>
	  <td>La clé publique a été demandée.</td>
  </tr>
</table>

## Où rechercher les événements ?
{: #ui}

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont disponibles dans le **domaine de compte** {{site.data.keyword.cloudaccesstrailshort}} qui se trouve dans la région {{site.data.keyword.Bluemix_notm}} où les événements sont générés.

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont automatiquement transférés vers le service {{site.data.keyword.cloudaccesstrailshort}} dans la même région que celle où le service {{site.data.keyword.cloudcerts_short}} est mis à disposition.

## Informations complémentaires
{: #info}

La zone *requestData_str* inclut le nom lisible du certificat.
