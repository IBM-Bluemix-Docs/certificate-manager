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


# Eventi di {{site.data.keyword.cloudaccesstrailshort}}  
{: #at_events}

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.cloudcerts_long}} in {{site.data.keyword.Bluemix}}.
{:shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Ad esempio, quando importi un certificato viene generato un evento di {{site.data.keyword.cloudaccesstrailshort}}.

La seguente tabella elenca i metodi API che generano un evento quando vengono richiamati:

<table>
  <caption>Azioni che generano eventi</caption>
  <tr>
    <th>Azione</th>
	  <th>Descrizione</th>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>Importa un certificato emesso da un'autorità di certificazione di terze parti.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>Scarica un certificato.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>Elenca i certificati.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>Elenca i metadati dei certificati. Mostra i dettagli di un certificato.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>Ricerca i certificati.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>Ricerca i metadati dei certificati.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>Elimina un certificato.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>Aggiorna un certificato, ad esempio, modifica la descrizione di un certificato.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channels.list</td>
	  <td>Elenca i canali di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.create</td>
	  <td>Crea un canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.state</td>
	  <td>Disabilita o abilita un canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.update</td>
	  <td>Aggiorna l'endpoint di un canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.delete</td>
	  <td>Elimina un canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.test</td>
	  <td>Verifica un canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notification.sent</td>
	  <td>Una notifica è stata inviata a un endpoint di canale di notifiche.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications.publickey</td>
	  <td>La chiave pubblica è stata richiesta.</td>
  </tr>
</table>

## Dove ricercare gli eventi
{: #ui}

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel **dominio dell'account** {{site.data.keyword.cloudaccesstrailshort}}, che è disponibile nella regione {{site.data.keyword.Bluemix_notm}} in cui vengono generati gli eventi.

Gli eventi di {{site.data.keyword.cloudaccesstrailshort}} vengono inoltrati automaticamente al servizio {{site.data.keyword.cloudaccesstrailshort}} nella stessa regione in cui è stato eseguito il provisioning del servizio {{site.data.keyword.cloudcerts_short}}.

## Informazioni aggiuntive
{: #info}

Il campo *requestData_str* include il nome leggibile del certificato.
