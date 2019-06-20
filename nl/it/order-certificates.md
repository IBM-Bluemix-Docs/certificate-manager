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

# Ordinazione di certificati
{: #ordering-certificates}

Puoi utilizzare {{site.data.keyword.cloudcerts_long}} per ordinare certificati SSL/TLS pubblici per le tue applicazioni e i tuoi servizi firmati da autorità di certificazione (CA) esterne supportate. {{site.data.keyword.cloudcerts_short}} rende facile ordinare dei certificati pubblici oltre alla sicurezza aggiuntiva delle tue chiavi private SSL/TLS. Dopo che il tuo certificato è stato emesso, puoi distribuirlo ai servizi integrati o scaricarlo per utilizzarlo altrove.  
{: shortdesc}

Quando ordini un certificato, la tua chiave privata SSL/TLS viene generata direttamente in {{site.data.keyword.cloudcerts_short}} e archiviata in modo sicuro. Tutte le richieste e l'accesso ai certificati emessi possono essere gestiti tramite il [controllo dell'accesso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) e controllati automaticamente utilizzando [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).  

{{site.data.keyword.cloudcerts_short}} implementa il protocollo Automatic Certificate Management Environment (ACME) v2 come un client ACME. Il protocollo ACME rende possibile ottenere automaticamente i certificati attendili del browser senza intervento umano.

## Caratteristiche del certificato
I certificati ordinati tramite {{site.data.keyword.cloudcerts_short}} hanno le seguenti caratteristiche:

- Gratis
- Periodo di validità - 90 giorni
- Singolo dominio, multidominio (SAN) o certificati jolly
- Dominio convalidato - prima di emettere un certificato, l'autorità di certificazione (CA) controlla che gestisci il dominio per cui stai richiedendo un certificato.

Se hai bisogno della convalida estesa (EV) o della convalida dell'organizzazione (OV) dei certificati, puoi ottenerli altrove e importarli in {{site.data.keyword.cloudcerts_short}} per gestire il loro ciclo di vita.

## Autorità di certificazione (CA) supportate
{: #supported-certificate-authorities}

Un'autorità di certificazione (CA) è un'entità che emette certificati digitali. La CA agisce come un servizio di terze parti attendibile per il richiedente del certificato e il client che si basa sul certificato.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) è una CA gratuita, automatizzata e basata su ACME che fornisce dei certificati convalidati per dominio validi per 90 giorni. È un servizio fornito dall'ISRG (Internet Security Research Group).

## Configurazione dell'ordinazione dei certificati
{: #setup}

Prima che possa essere emesso un certificato, {{site.data.keyword.cloudcerts_short}} deve verificare che controlli tutti i domini che hai elencato nella tua richiesta. {{site.data.keyword.cloudcerts_short}} utilizza la convalida DNS per verificare il tuo controllo.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} invia una verifica nel formato di un record TXT DNS (Domain Name System) da aggiungere nel tuo servizio DNS. Per ogni dominio che richiedi nel tuo certificato, ricevi una record TXT DNS separato. Dopo aver aggiunto il record TXT DNS, {{site.data.keyword.cloudcerts_short}} e Let’s Encrypt controllano se si trova nel tuo servizio DNS. Se completi correttamente la verifica, viene emesso un certificato Let’s Encrypt disponibile nella tua istanza {{site.data.keyword.cloudcerts_short}}.

{{site.data.keyword.cloudcerts_short}} invia il record TXT a un URL di callback che hai fornito nelle impostazioni delle notifiche, che ti consente di automatizzare facilmente il processo di convalida del dominio.

Per iniziare ad ordinare i certificati, registra il tuo URL di callback come un canale di notifica in {{site.data.keyword.cloudcerts_short}}. Successivamente, aggiorna il tuo codice in modo che gestisca gli eventi di notifica che includono la verifica TXT. [Impara come configurare un canale di notifica URL di callback](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Rispondere alla verifica
{: #responding-to-challenge}

Il canale di notifica riceve una notifica con la seguente struttura:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

Quando la verifica TXT DNS viene inviata al tuo URL di callback, devi rispondere alla verifica entro 10 minuti. {{site.data.keyword.cloudcerts_short}} controlla se la verifica è stata completata. Dopo che {{site.data.keyword.cloudcerts_short}} controlla che hai risposto alla verifica, ti viene inviata una seconda notifica che ti informa che puoi rimuovere il record TXT.

[Controlla la pagina delle FAQ](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) per le domande più frequenti sull'ordinazione dei certificati.
{: tip}

## Ordinazione di certificati
{: #ordering-certificate}

1. Passa alla scheda Manage di {{site.data.keyword.cloudcerts_short}}.
2. Fai clic su **Order Certificate** e fornisci i seguenti dettagli:

    1. Fornisci un nome certificato.
    2. Seleziona un'autorità di certificazione (CA).
    3. Immetti il dominio primario e tutti i domini alternativi.
    4. Seleziona l'algoritmo appropriato e l'algoritmo chiave.
    5. Fai clic su **Order**.

Il tuo ordine viene inserito nello stato **Pending**. Dopo che hai risposto alla verifica di convalida del dominio e {{site.data.keyword.cloudcerts_short}} verifica che gestisci i domini richiesti, viene emesso il certificato e il suo stato verrà modificato con **Valid**. Vieni avvertito quando il tuo certificato è pronto o se si è verificato un problema, nel tuo canale Slack e/o URL di callback.

## Rinnovo dei certificati
{: #renew-certificate}

Se il tuo certificato sta per scadere, puoi richiedere di rinnovarlo tramite {{site.data.keyword.cloudcerts_short}}. Quando il tuo certificato viene rinnovato, la versione precedente del certificato viene conservata nel caso ne avessi bisogno. 

I rinnovi funzionano in modo simile all'ordinazione del certificato. Quando richiedi di rinnovare un certificato, {{site.data.keyword.cloudcerts_short}} invia le verifiche txt DNS al tuo URL di callback, in modo da poter provare nuovamente di gestire i domini per cui stai rinnovando il certificato.

Per rinnovare un certificato, completa la seguente procedura:
  1. Fai clic sul menu nella riga del certificato che vuoi rinnovare.
  2. Fai clic su **Renew Certificate**.
  3. Facoltativo: puoi scegliere di reimpostare le chiavi del tuo certificato selezionando la casella di spunta **Rekey certificate**. Questa azione rinnoverà il tuo certificato con una nuova coppia di chiavi.
  
  Quando reimposti le chiavi di un certificato, assicurati di distribuire i nuovi certificati e chiavi ovunque vengano utilizzati.
  {: note}
    
  4. Fai clic su **Renew**
  
  Puoi rinnovare solo i certificati che hai ordinato tramite {{site.data.keyword.cloudcerts_short}}.
  {: note}

Il tuo rinnovo viene inserito nello stato **Renew Pending**. Dopo che hai risposto alla verifica di convalida del dominio e {{site.data.keyword.cloudcerts_short}} verifica che gestisci i domini richiesti, riceverai un certificato rinnovato e il suo stato verrà modificato con **Valid**. Sarai avvertito quando il tuo certificato rinnovato è pronto o se si è verificato un problema, nel tuo canale Slack e/o URL di callback.
