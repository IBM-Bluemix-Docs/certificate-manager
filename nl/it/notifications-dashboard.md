---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

keywords: certificates, SSL,

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

# Configurazione delle notifiche
{: #configuring-notifications}

{{site.data.keyword.cloudcerts_full}} può inviarti le notifiche sugli eventi del ciclo di vita del certificato. Queste notifiche includono dei promemoria per rinnovare i certificati prima che scadano e di distribuire i certificati quando sono pronti. Per ricevere le notifiche da {{site.data.keyword.cloudcerts_short}}, puoi configurare un canale di notifica. Puoi specificare un webhook Slack, un URL di callback o una qualsiasi combinazione dei due.
{: shortdesc}

La funzione delle notifiche viene utilizzata anche quando [ordini i certificati](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates) da {{site.data.keyword.cloudcerts_short}}. Per provare che gestisci il dominio per cui stai richiedendo un certificato, {{site.data.keyword.cloudcerts_short}} invia una verifica come una notifica al tuo URL di callback. La verifica è un record di testo, che puoi inserire nel servizio DNS (Domain Name System) in cui viene registrato il tuo dominio. Quando il record di testo viene inserito, la verifica viene considerata completata. Poiché la verifica è inviata come una notifica al tuo URL di callback, puoi automatizzare il processo di convalida del dominio eseguendo del codice in risposta all'evento di notifica.

## Notifiche per monitorare la scadenza del certificato
{: #notifications-monitoring-certificate-expiration}

I certificati sono generalmente validi per un determinato periodo di tempo. Quando un certificato che utilizzi scade, potresti riscontrare tempi di inattività per la tua applicazione. Per evitare tempi di inattività puoi configurare {{site.data.keyword.cloudcerts_short}} per farti inviare le notifiche per i certificati che stanno per scadere in modo da essere avvertito in tempo per rinnovarli. 

Vieni avvertito anche quando una versione rinnovata del tuo certificato viene reimportata in {{site.data.keyword.cloudcerts_short}} al posto di quella scaduta. Questo per ricordarti di distribuirla nei punti di terminazione SSL/TLS. Questa notifica dei certificati reimportati viene inviata solo ai canali dalla [versione 2 del canale](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


**Quando ricevo la notifica?**   
A seconda della data di scadenza del certificato che hai caricato in {{site.data.keyword.cloudcerts_short}}, riceverai una notifica 90, 60, 30, 10 e 1 giorno prima della scadenza del certificato. Inoltre, ricevi notifiche giornaliere sui certificati scaduti. Le notifiche giornaliere iniziano il primo giorno dopo che il tuo certificato è scaduto.

Devi rinnovare il tuo certificato e reimportare questo certificato al posto di quello vecchio in {{site.data.keyword.cloudcerts_short}} per arrestare l'invio delle notifiche. Quando reimporti il tuo certificato ricevi una notifica che indica che il tuo certificato è stato reimportato e ti ricorda di ridistribuirlo. 

**Quali sono le mie opzioni per configurare le notifiche?**  
Puoi inviare notifiche a Slack usando un webhook Slack o utilizzare qualsiasi URL di callback preferisci.

## Notifiche correlate all'ordinazione dei certificati
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} ti avverte quando un certificato che ordini da {{site.data.keyword.cloudcerts_short}} viene emesso o rinnovato correttamente. Ricevi una notifica anche se il tuo ordine o un rinnovo ha esito negativo.
{: shortdesc}

La configurazione di un canale di notifica URL di callback e la possibilità di gestire gli eventi correlati alla convalida del dominio, sono dei prerequisiti per l'ordinazione e il rinnovo dei certificati. Quando ordini un certificato, {{site.data.keyword.cloudcerts_short}} invia un record txt di verifica al tuo URL di callback che utilizzi per provare di gestire il dominio per cui stai richiedendo il certificato. Un record txt di verifica viene inviato anche quando richiedi di rinnovare un certificato. 


## Configurazione di un webhook Slack
{: #setup-callback}

Per configurare un webhook Slack, completa la seguente procedura:

1. Registrati in [Slack](https://slack.com/) e imposta il tuo spazio di lavoro.
2. Crea un canale Slack in cui desideri pubblicare le tue notifiche.
3. [Imposta un webhook](https://api.slack.com/incoming-webhooks) per il canale Slack.

## Configurazione di un URL di callback
{: #callback}

Per attivare il processo di rinnovo per il tuo team, puoi utilizzare un URL di callback per inviare notifiche agli strumenti che utilizzi. Ad esempio, puoi inviare notifiche per le segnalazioni a PagerDuty, aprire automaticamente un problema in GitHub o attivare gli script di rinnovo. Puoi anche attivare automaticamente la distribuzione dei certificati nella risposta alle notifiche quando i certificati vengono reimportati o emessi correttamente.
{: shortdesc}

Un URL di callback è un prerequisito per l'ordinazione di certificati.
{: note}

**Importante:** l'endpoint del tuo URL di callback deve soddisfare i seguenti requisiti per poter essere utilizzato con {{site.data.keyword.cloudcerts_short}}:
* L'endpoint deve utilizzare il protocollo HTTPS.
* L'endpoint non deve richiedere intestazioni HTTP. Questo requisito include le intestazioni di autorizzazione.
* L'endpoint deve restituire un codice di stato `200 OK` per indicare un corretto recapito della notifica.

### Formato della notifica
{: #notification_format}

La notifica che viene inviata al tuo URL di callback è un documento JSON firmato con la tua chiave asimmetrica dell'istanza nel seguente formato. 

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Dopo che hai decodificato e verificato il payload, il contenuto è una stringa JSON [che si basa sulla versione del canale](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configurazione di un canale di notifica
{: #adding-channel}

Dopo aver creato un webhook Slack o un URL di Callback, lo puoi aggiungere a {{site.data.keyword.cloudcerts_short}} per iniziare a ricevere notifiche sui certificati in scadenza, reimportati, emessi e sulle verifiche per la convalida del dominio. {{site.data.keyword.cloudcerts_short}} crittografa l'endpoint e lo memorizza in modo sicuro.
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
   <caption>Tabella 1. Informazioni sul canale di notifica </caption>
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

Prima di iniziare, [configura un canale di notifica](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Per verificare un canale di notifica, completa la seguente procedura:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Trova il tuo canale di notifica e fai clic su **Verifica connessione**.
3. Verifica di aver ricevuto una notifica nel canale che hai configurato.

## Aggiornamento di un canale di notifica
{: #updating-channel}

Puoi aggiornare la configurazione del tuo canale di notifica, disabilitare o abilitare le notifiche o eliminare i canali di notifica da {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Prima di iniziare, [configura un canale di notifica](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

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

## Versioni del canale
{: #channel-versions}

Man mano che Certificate Manager si evolve, potremmo modificare il formato della struttura del payload delle notifiche di volta in volta. Per garantire la compatibilità con le versioni precedenti, il payload inviato ai canali esistenti non cambierà.    

Se hai canali di notifica esistenti (Slack o URL di callback), per iniziare a utilizzare la nuova versione del payload:

1. Per l'URL di callback, assicurati che la tua implementazione possa accettare il nuovo payload.
2. Crea un nuovo canale di notifica (i nuovi canali vengono sempre creati con la versione del canale più recente).
3. Verifica che il nuovo canale funzioni correttamente.
4. Elimina il vecchio canale.

Per le versioni dei canali, controlla la [documentazione API](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Esempi
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Impara come creare elementi di lavoro GitHub per le notifiche di certificato in scadenza.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Impara come creare incidenti PagerDuty per le notifiche di certificato in scadenza.
* [How to validate a domain using a Callback URL and a Cloud Function action ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
