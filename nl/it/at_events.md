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

# Eventi di {{site.data.keyword.cloudaccesstrailshort}}  
{: #at_events}

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.cloudcerts_long_notm}} in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Ad esempio, quando importi un certificato viene generato un evento di {{site.data.keyword.cloudaccesstrailshort}}.

La seguente tabella elenca i metodi API che generano un evento quando vengono richiamati.

<table>
  <caption>Tabella 1. Azioni che generano eventi</caption>
  <tr>
    <th>Azione</th>
	  <th>Descrizione</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Importa un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Reimporta un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Scarica un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>Elenca i certificati.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>Elenca i metadati dei certificati. Mostra i dettagli di un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Ricerca i certificati.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Ricerca i metadati dei certificati.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Elimina un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Aggiorna i metadati del certificato, ad esempio, modifica la descrizione di un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>Elenca i canali di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Crea un canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Disabilita o abilita un canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Aggiorna l'endpoint di un canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Elimina un canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Verifica un canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>Una notifica è stata inviata a un endpoint di canale di notifiche.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>La chiave pubblica è stata richiesta.</td>
  </tr>
</table>

## Dove ricercare gli eventi
{: #ui}

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel **dominio dell'account** {{site.data.keyword.cloudaccesstrailshort}}, che è disponibile nell'ubicazione {{site.data.keyword.Bluemix_notm}} in cui vengono generati gli eventi.

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} vengono inoltrati automaticamente al servizio {{site.data.keyword.cloudaccesstrailshort}} nella stessa ubicazione in cui è stato eseguito il provisioning del servizio {{site.data.keyword.cloudcerts_short}}.

## Informazioni aggiuntive
{: #info}

Il campo *requestData_str* include il nome leggibile del certificato.
