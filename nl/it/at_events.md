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

# Eventi del programma di traccia dell'attività   
{: #at_events}

Utilizza il servizio {{site.data.keyword.at_full}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.cloudcerts_long}} in {{site.data.keyword.cloud_notm}}.
{:shortdesc}

Il servizio {{site.data.keyword.at_short}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}. Ad esempio, quando importi un certificato viene generato un evento. Per ulteriori informazioni, vedi la [documentazione {{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

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
    <td>`cloudcerts.certificate.order`</td>
	  <td>Ordina un certificato. </td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Reimporta un certificato.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>Ottieni i metadati del certificato. </td>
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
{: #at_ui}

Esegui il provisioning di un'istanza {{site.data.keyword.at_short}} nella stessa ubicazione della tua istanza {{site.data.keyword.cloudcerts_short}}.

Gli eventi vengono inoltrati automaticamente all'istanza del servizio {{site.data.keyword.at_short}} nella stessa ubicazione in cui hai eseguito il provisioning del servizio {{site.data.keyword.cloudcerts_short}}.

## Informazioni aggiuntive
{: #info}

* Il campo *requestData_str* include il nome leggibile del certificato.

## Disponibilità
{: #at-availability}

* Il supporto {{site.data.keyword.at_short}} è al momento disponibile per le ubicazioni **Dallas** e **Francoforte**.
* Per le altre ubicazioni, esegui il provisioning di un'istanza del programma di traccia dell'attività obsoleto finché è disponibile {{site.data.keyword.at_short}}.
