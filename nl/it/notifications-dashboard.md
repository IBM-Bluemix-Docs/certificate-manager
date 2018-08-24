---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configurazione delle notifiche per i certificati in scadenza
{: #configuring-notifications-for-expiring-certificates}

I certificati sono generalmente validi solo per un determinato periodo di tempo. Quando un certificato che utilizzi scade, potresti riscontrare tempi di inattività per la tua applicazione. Per evitare tempi di inattività, puoi configurare {{site.data.keyword.cloudcerts_full}} per inviare notifiche per i certificati che stanno per scadere in modo da poterli rinnovare in tempo.
{: shortdesc}

**Quando ricevo la notifica?** </br>
A seconda della data di scadenza del certificato che hai caricato in {{site.data.keyword.cloudcerts_full}}, riceverai una notifica 90, 60, 30, 10 e 1 giorno prima della scadenza del certificato. Inoltre, ricevi notifiche giornaliere sui certificati scaduti a partire dal primo giorno successivo alla scadenza del tuo certificato.

Devi rinnovare il certificato, caricare questo certificato in {{site.data.keyword.cloudcerts_full}} ed eliminare il certificato scaduto per impedire che la notifica continui ad essere inviata.

**Quali sono le mie opzioni per configurare le notifiche?** </br>
Puoi inviare notifiche a Slack usando un webhook Slack o utilizzare qualsiasi URL di callback che preferisci.

## Configurazione di un webhook Slack
{: #setup-callback}

1. Registrati in [Slack](https://slack.com/) e imposta il tuo spazio di lavoro.
2. Crea un canale Slack in cui desideri pubblicare le tue notifiche.
3. [Imposta un webhook](https://api.slack.com/incoming-webhooks) per il canale Slack.

## Configurazione di un URL di callback
{: #callback}

Potresti voler utilizzare l'URL di callback per inviare notifiche agli strumenti che utilizzi quotidianamente per attivare il processo di rinnovo per il tuo team. Ad esempio, puoi inviare notifiche per le segnalazioni a pagerduty, aprire automaticamente un problema in Github o attivare gli script di rinnovo.  
{: shortdesc}

**Importante:** l'endpoint del tuo URL di callback deve soddisfare i seguenti requisiti per poter essere utilizzato con {{site.data.keyword.cloudcerts_short}}:
* L'endpoint deve utilizzare il protocollo HTTPS.
* L'endpoint non deve richiedere intestazioni HTTP. Questo requisito include le intestazioni di autorizzazione.


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
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>
    "expiring_certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}


### Utilizzo di un URL di callback per aprire automaticamente un problema GitHub
{: #sample}

Il seguente codice di esempio ti mostra come puoi creare un problema GitHub per i certificati in scadenza quando viene inviata una notifica. Puoi eseguire questo codice in {{site.data.keyword.openwhisk}} o utilizzare il codice in un ambiente diverso.   
{: shortdesc}

Per eseguire questo codice in {{site.data.keyword.openwhisk_short}}:

1. Crea un'azione in [Cloud Functions](/docs/openwhisk/index.html#index).
2. Utilizza il seguente codice per creare automaticamente un problema GitHub:

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "<PERSONAL_GITHUB_TOKEN>";

    /**
     * Returns the expiration data as short date string
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Creates the issue body string
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Gets the notification body and creates a Github issue
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Decode message to get information
        const data = jwtDecode(params.data);
        try {
            // Create request options to get the public key for verification
            const keysOptions = {
                method: 'GET',
                url: `https://<CERTIFICATE_MANAGER_CLUSTER_BASE_URL>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Send request to get the public key
            const keysResponse = await request(keysOptions);

            // Verify the data using the acquired public key
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Create request options to send a new issue to Github
            // Based on Github API - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<REPO_OWNER>/<REPO_NAME>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Certificates about to expire",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Send request to Github
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}

Per altri comandi API REST, vedi la [documentazione API](https://console.bluemix.net/apidocs/cloudcerts)
{: tip}


## Configurazione di un canale di notifica
{: #adding-channel}

Dopo aver creato un webhook Slack o un URL di callback, lo aggiungi a {{site.data.keyword.cloudcerts_short}} per iniziare a ricevere notifiche sui certificati in scadenza. {{site.data.keyword.cloudcerts_short}} crittografa l'endpoint e lo memorizza in modo sicuro.
{: shortdesc}

Per aggiungere un canale di notifica:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Apri la scheda **Notifiche**.
3. Fai clic su **Aggiungi canale di notifica**.
4. Scegli il tipo di canale di notifica che vuoi utilizzare.
5. Immetti il webhook o l'URL di callback a cui desideri inviare le notifiche.
6. Fai clic su **Salva**. Viene visualizzato un riepilogo della tua configurazione.

   Output di esempio:
   <table>
   <caption> Informazioni sul canale di notifica </caption>
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
7. Facoltativo: ripeti questi passi per aggiungere ulteriori canali di notifica.

## Verifica di un canale di notifica
{: #testing-channel}

Puoi verificare un canale di notifica per assicurarti che il tuo canale di notifica sia configurato correttamente.
{: shortdesc}

Prima di iniziare, [configura un canale di notifica](#adding-channel).

Per verificare un canale di notifica:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Trova il tuo canale di notifica e fai clic su **Verifica connessione**.
3. Verifica di aver ricevuto una notifica nel canale che hai configurato.


## Aggiornamento di un canale di notifica
{: updating-channel}

Puoi aggiornare la configurazione del tuo canale di notifica, disabilitare o abilitare le notifiche o eliminare i canali di notifica da {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Prima di iniziare, [configura un canale di notifica](#adding-channel).

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Seleziona la scheda **Notifiche**.
3. Scegli tra le seguenti opzioni.
   - Per disabilitare o abilitare le notifiche per un canale, imposta l'interruttore su **Disabilita** o **Abilita**.
   - Per aggiornare le impostazioni per un canale, seleziona **Modifica** dal menu di azioni.
   - Per eliminare un canale di notifica, seleziona **Elimina** dal menu di azioni.


## Verifica del payload HTTP per un URL di callback
{: #verify-callback}

Ogni payload HTTP inviato da {{site.data.keyword.cloudcerts_short}} al tuo URL di callback viene firmato automaticamente in base allo standard JWT utilizzando una coppia di chiavi asimmetriche.  
{: shortdesc}

Per ogni istanza di {{site.data.keyword.cloudcerts_short}}, viene generata una chiave privata e una chiave pubblica che non vengono condivise tra le altre istanze di {{site.data.keyword.cloudcerts_short}}. La chiave privata viene utilizzata per firmare il payload HTTP e puoi utilizzare la chiave pubblica per verificare che il payload sia generato da {{site.data.keyword.cloudcerts_short}} e non venga modificato da una terza parte.

Per scaricare la chiave pubblica:

1. Dalla navigazione nella pagina dei dettagli del servizio, fai clic su **Impostazioni**.
2. Apri la scheda **Notifiche**.
3. Fai clic sul pulsante **Scarica chiave**. La chiave viene scaricata come file PEM.
