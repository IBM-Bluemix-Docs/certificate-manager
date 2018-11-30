---

copyright:
  years: 2017, 2018
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

# Configurazione delle notifiche per i certificati in scadenza
{: #configuring-notifications-for-expiring-certificates}

I certificati sono generalmente validi solo per un determinato periodo di tempo. Quando un certificato che utilizzi scade, potresti riscontrare tempi di inattività per la tua applicazione. Per evitare tempi di inattività, puoi configurare {{site.data.keyword.cloudcerts_full}} per inviare notifiche per i certificati che stanno per scadere in modo da poterli rinnovare in tempo.
{: shortdesc}

**Quando ricevo la notifica?**  
A seconda della data di scadenza del certificato che hai caricato in {{site.data.keyword.cloudcerts_full_notm}}, riceverai una notifica 90, 60, 30, 10 e 1 giorno prima della scadenza del certificato. Inoltre, ricevi notifiche giornaliere sui certificati scaduti. Le notifiche giornaliere iniziano il primo giorno dopo che il tuo certificato è scaduto.

Devi rinnovare il certificato, caricare questo certificato in {{site.data.keyword.cloudcerts_full_notm}} ed eliminare il certificato scaduto per impedire che la notifica continui ad essere inviata.

**Quali sono le mie opzioni per configurare le notifiche?**  
Puoi inviare notifiche a Slack usando un webhook Slack o utilizzare qualsiasi URL di callback che preferisci.

## Configurazione di un webhook Slack
{: #setup-callback}

Per configurare un webhook Slack, completa la seguente procedura:

1. Registrati in [Slack](https://slack.com/) e imposta il tuo spazio di lavoro.
2. Crea un canale Slack in cui desideri pubblicare le tue notifiche.
3. [Imposta un webhook](https://api.slack.com/incoming-webhooks) per il canale Slack.

## Configurazione di un URL di callback
{: #callback}

Potresti voler utilizzare l'URL di callback per inviare notifiche agli strumenti che utilizzi quotidianamente per attivare il processo di rinnovo per il tuo team. Ad esempio, puoi inviare notifiche per le segnalazioni a PagerDuty, aprire automaticamente un problema in GitHub o attivare gli script di rinnovo.  
{: shortdesc}

**Importante:** l'endpoint del tuo URL di callback deve soddisfare i seguenti requisiti per poter essere utilizzato con {{site.data.keyword.cloudcerts_short}}:

* L'endpoint deve utilizzare il protocollo HTTPS.
* L'endpoint non deve richiedere intestazioni HTTP. Questo requisito include le intestazioni di autorizzazione.
* L'endpoint deve restituire un codice di stato `200 OK` per indicare un corretto recapito della notifica.

### Formato della notifica
{: #notification_format}

La notifica inviata al tuo URL di callback è un documento JSON nel seguente formato:

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Dopo che hai decodificato e verificato il payload, il contenuto è una stringa JSON.

```
{
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
    "event_type": "<EVENT_TYPE>",
    "certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "name":"<CERTIFICATE_NAME>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}

## Configurazione di un canale di notifica
{: #adding-channel}

Dopo aver creato un webhook Slack o un URL di callback, lo aggiungi a {{site.data.keyword.cloudcerts_short}} per iniziare a ricevere notifiche sui certificati in scadenza. {{site.data.keyword.cloudcerts_short}} crittografa l'endpoint e lo memorizza in modo sicuro.
{: shortdesc}

Per aggiungere un canale di notifica, completa la seguente procedura:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Apri la scheda **Notifiche**.
3. Fai clic su **Aggiungi canale di notifica**.
4. Scegli il tipo di canale di notifica che vuoi utilizzare.
5. Immetti il webhook o l'URL di callback a cui desideri inviare le notifiche.
6. Fai clic su **Salva**. Viene visualizzato un riepilogo della tua configurazione.

   **Output di esempio**

   <table>
   <caption>Tabella 1. Informazioni sul canale di notifica</caption>
   <thead>
    <th> Componente </th>
    <th> Descrizione </th>
   </thead>
   <tbody>
   <tr>
    <td>Tipo</td>
    <td>Tipo di canale di notifica: <i>Slack</i> o <i>URL di callback</i></td>
   </tr>
   <tr>
    <td>Endpoint</td>
    <td>L'endpoint del canale di notifica a cui vengono inviate le notifiche.</td>
   </tr>
   <tr>
    <td>Alternanza dell'abilitazione</td>
    <td>Lo stato del canale di notifica. Se è impostato su disabilitato, non viene inviata alcuna notifica.</td>
   </tr>
   <tr>
    <td>Pulsante Verifica connessione</td>
    <td>Invia una notifica di test al canale che hai configurato. </td>
   </tr>
    <tr>
      <td>Menu di punti</td>
      <td>Azioni disponibili che puoi eseguire sul canale: <i>modifica</i> o <i>elimina</i></td>
    </tr>
    </tbody>
    </table>

    Quando salvi un webhook Slack, {{site.data.keyword.cloudcerts_short}} invia automaticamente una notifica di conferma al canale Slack che hai configurato. Controlla il tuo canale Slack per verificare di aver ricevuto questa notifica.
    {: tip}
7. (Facoltativo) Ripeti questi passi per aggiungere ulteriori canali di notifica.

## Verifica di un canale di notifica
{: #testing-channel}

Puoi verificare un canale di notifica per assicurarti che il tuo canale di notifica sia configurato correttamente.
{: shortdesc}

Prima di iniziare, [configura un canale di notifica](#adding-channel).

Per verificare un canale di notifica, completa la seguente procedura:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Trova il tuo canale di notifica e fai clic su **Verifica connessione**.
3. Verifica di aver ricevuto una notifica nel canale che hai configurato.

## Aggiornamento di un canale di notifica
{: updating-channel}

Puoi aggiornare la configurazione del tuo canale di notifica, disabilitare o abilitare le notifiche o eliminare i canali di notifica da {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Prima di iniziare, [configura un canale di notifica](#adding-channel).

Per aggiornare il tuo canale di notifica, completa la seguente procedura:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Seleziona la scheda **Notifiche**.
3. Scegli dalle seguenti opzioni:
   * Per disabilitare o abilitare le notifiche per un canale, imposta l'interruttore su **Disabilita** o **Abilita**.
   * Per aggiornare le impostazioni per un canale, seleziona **Modifica** dal menu di azioni.
   * Per eliminare un canale di notifica, seleziona **Elimina** dal menu di azioni.

## Verifica del payload HTTP per un URL di callback
{: #verify-callback}

Ogni payload HTTP inviato da {{site.data.keyword.cloudcerts_short}} al tuo URL di callback viene firmato automaticamente in base allo standard JWT utilizzando una coppia di chiavi asimmetriche.  
{: shortdesc}

Per ogni istanza di {{site.data.keyword.cloudcerts_short}}, viene generata una chiave privata e una chiave pubblica che non vengono condivise tra le altre istanze di {{site.data.keyword.cloudcerts_short}}. La chiave privata viene utilizzata per firmare il payload HTTP e puoi utilizzare la chiave pubblica per verificare che il payload sia generato da {{site.data.keyword.cloudcerts_short}} e non venga modificato da una terza parte.

Per scaricare la chiave pubblica, completa la seguente procedura:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Apri la scheda **Notifiche**.
3. Fai clic sul pulsante **Scarica chiave**. La chiave viene scaricata come file PEM.

## Esempi
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Impara come creare elementi di lavoro GitHub per le notifiche di certificato in scadenza.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Impara come creare elementi di lavoro di incidenti PagerDuty per le notifiche di certificato in scadenza.
