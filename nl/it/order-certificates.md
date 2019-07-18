---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

subcollection: certificate-manager

---

{:external: target="_blank" .external}
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

Quando ordini un certificato, la tua chiave privata SSL/TLS viene generata direttamente in {{site.data.keyword.cloudcerts_short}} e archiviata in modo sicuro. Tutte le richieste e l'accesso ai certificati emessi possono essere gestiti tramite il [controllo dell'accesso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles) e controllati automaticamente utilizzando [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events).  

{{site.data.keyword.cloudcerts_short}} implementa il protocollo Automatic Certificate Management Environment (ACME) v2 come un client ACME. Il protocollo ACME rende possibile ottenere automaticamente i certificati attendili del browser senza intervento umano.

## Caratteristiche del certificato
{: #certificate-characteristics}

Quando ordini dei certificati tramite {{site.data.keyword.cloudcerts_short}}:

- Sono gratuiti
- Sono validi per 90 giorni
- Sono a singolo dominio, multidominio (SAN) o jolly
- Sono stati convalidati dal dominio

La convalida del dominio include la verifica che gestisci il dominio per cui stai richiedendo un certificato. Se hai bisogno della convalida estesa (EV) o della convalida dell'organizzazione (OV) dei certificati, puoi ottenerli altrove e importarli in {{site.data.keyword.cloudcerts_short}} per gestire il loro ciclo di vita.


## Autorità di certificazione (CA) supportate
{: #supported-certificate-authorities}

Un'autorità di certificazione (CA) è un'entità che emette certificati digitali. La CA agisce come un servizio di terze parti attendibile per il richiedente del certificato e il client che si basa sul certificato.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) è una CA gratuita, automatizzata e basata su ACME che fornisce dei certificati convalidati per dominio validi per 90 giorni. È un servizio fornito dall'ISRG (Internet Security Research Group).

## Configurazione dell'ordinazione dei certificati
{: #setup}

Prima che possa essere emesso un certificato, {{site.data.keyword.cloudcerts_short}} deve verificare che controlli tutti i domini che elenchi nella tua richiesta. Per farlo, {{site.data.keyword.cloudcerts_short}} utilizza la convalida DNS.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} invia una verifica nel formato di un record TXT DNS (Domain Name System) da aggiungere nel tuo servizio DNS. Per ogni dominio che richiedi nel tuo certificato, ricevi una record TXT DNS separato. Dopo aver aggiunto il record TXT DNS, {{site.data.keyword.cloudcerts_short}} e Let’s Encrypt controllano se si trova nel tuo servizio DNS. Se completi correttamente la verifica, viene emesso un certificato Let’s Encrypt disponibile nella tua istanza {{site.data.keyword.cloudcerts_short}}.

Come verifichi la proprietà del dominio dipende dal fatto se utilizzi {{site.data.keyword.cis_full_notm}} o un altro provider DNS.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

Se gestisci i tuoi domini in {{site.data.keyword.cis_short}}, completa la seguente procedura per verificare la proprietà:

1. Vai a **{{site.data.keyword.cloud_notm}} >Gestisci > Accesso (IAM) > Autorizzazioni**. 
2. Fai clic su **Crea** e assegna un servizio di origine e destinazione. Al servizio di origine viene concesso l'accesso al servizio di destinazione in base ai ruoli che imposti nel prossimo passo.
  * Origine: {{site.data.keyword.cloudcerts_short}}
  * Destinazione: Internet Services
3. Specifica un'istanza del servizio per l'origine e la destinazione.
4. Assegna il ruolo **Lettore** per consentire a {{site.data.keyword.cloudcerts_short}} di visualizzare l'istanza {{site.data.keyword.cis_short_notm}} e i relativi domini. Successivamente, fai clic su **Autorizza**.

  Per scopi di test, puoi assegnare il ruolo di accesso al servizio di **Gestore** tramite l'IU per gestire tutti i tuoi domini. Se lo fai, non devi completare il passo 5. Per gli ambienti di produzione si consiglia di assegnare il ruolo di accesso al servizio di **Lettore** ed utilizzare l'API come mostrato nel passo 5 per controllare dei domini specifici.
  {: note}
   
5. Per controllare dei domini specifici, assegna il ruolo di **Gestore** tramite l'API in modo che {{site.data.keyword.cloudcerts_short}} possa gestire i record DNS per i singoli domini presenti nella tua istanza {{site.data.keyword.cis_short_notm}}. Potresti voler copiare il comando in un file di testo per modificare facilmente i parametri richiesti.
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>Variabile</th>
      <th>Descrizione</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>Un token IAM valido. Puoi trovare il valore utilizzando la CLI {{site.data.keyword.cloud_notm}}: <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>L'ID dell'account in cui si trovano le istanze {{site.data.keyword.cloudcerts_short}} e {{site.data.keyword.cis_short_notm}}. Puoi trovare il valore andando a <b>{{site.data.keyword.cloud_notm}} > Gestisci > Account > Impostazioni account</b> o utilizzando la CLI {{site.data.keyword.cloud_notm}}: <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>L'ID basato sul GUID della tua istanza di {{site.data.keyword.cloudcerts_short}}. Per trovare il valore, utilizza la CLI {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>L'ID basato sul GUID della tua istanza di {{site.data.keyword.cis_short_notm}}. Per trovare il valore, utilizza la CLI {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>L'ID del tuo dominio come trovato in {{site.data.keyword.cis_short_notm}}. Per trovare il valore, utilizza la CLI {{site.data.keyword.cloud_notm}} per eseguire <code>ibmcloud cis domains</code>. Per gestire più domini, modifica l'array <code>resources</code>.</td>
    </tr>
  </table>

Sei ora pronto per [ordinare un certificato](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)!


### Altro provider DNS
{: #other_provider}

Per verificare che controlli un dominio quando utilizzi un provider DNS di terze parti, {{site.data.keyword.cloudcerts_short}} invia il record TXT a un canale di notifica dell'URL di callback da te fornito, che ti consente di automatizzare il processo di convalida del dominio.

Per prima cosa, implementa un'azione IBM Cloud Function per la convalida del dominio e poi fornisci il relativo endpoint a un canale di notifica dell'URL di callback. Per iniziare, vedi [configurazione di un canale di notifica dell'URL di callback](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

Per ulteriori informazioni sulla configurazione della convalida del dominio utilizzando un canale di notifica dell'URL di callback, vedi [questo post di blog](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}.
{: tip}


#### Rispondere alla verifica
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

Per visualizzare le FAQ sull'ordinazione dei certificati, [controlla la pagina delle FAQ](/docs/services/certificate-manager?topic=certificate-manager-faq).
{: tip}

## Ordinazione di certificati
{: #ordering-certificate}

Per ordinare un certificato, completa la seguente procedura:

1. Passa alla scheda Manage di {{site.data.keyword.cloudcerts_short}}.
2. Fai clic su **Order Certificate** 
3. Seleziona il tuo provider DNS - {{site.data.keyword.cis_full_notm}} o un altro provider DNS.
4. Se hai selezionato **{{site.data.keyword.cis_full_notm}}**, fornisci i seguenti dettagli:
   1. Completa le istruzioni di configurazione richieste
   2. Fornisci un nome certificato e facoltativamente una descrizione
   3. Seleziona un'autorità di certificazione (CA)
   4. Seleziona l'istanza {{site.data.keyword.cis_full_notm}} a cui hai assegnato un ruolo di accesso al servizio
   5. Seleziona il tipo di certificato di cui hai bisogno
   6. Seleziona il dominio
   7. Seleziona l'algoritmo appropriato e l'algoritmo chiave
   8. Fai clic su **Order**
5. Se hai selezionato **Another DNS Provider**, fornisci i seguenti dettagli:
   1. Completa le istruzioni di configurazione richieste
   2. Fornisci un nome certificato e facoltativamente una descrizione
   3. Seleziona un'autorità di certificazione (CA).
   4. Immetti il dominio primario e tutti i domini alternativi
   5. Seleziona l'algoritmo appropriato e l'algoritmo chiave
   6. Fai clic su **Order**

Il tuo ordine viene inserito nello stato **Pending**. Dopo che hai risposto alla verifica di convalida del dominio e {{site.data.keyword.cloudcerts_short}} verifica che gestisci il dominio richiesto, viene emesso il certificato e il suo stato verrà modificato con **Valid**. Vieni avvertito quando il tuo certificato è pronto o se si è verificato un problema, nel tuo canale di notifica Slack e/o URL di callback.

## Rinnovo dei certificati
{: #renew-certificate}

Se il tuo certificato sta per scadere, puoi richiedere di rinnovarlo tramite {{site.data.keyword.cloudcerts_short}}. Quando il tuo certificato viene rinnovato, la versione precedente del certificato viene conservata nel caso ne avessi bisogno. 

I rinnovi funzionano in modo simile all'ordinazione del certificato. Quando richiedi di rinnovare un certificato, {{site.data.keyword.cloudcerts_short}} invia le verifiche txt DNS al tuo URL di callback, in modo da poter provare nuovamente di gestire i domini per cui stai rinnovando il certificato.

Per rinnovare un certificato, completa la seguente procedura:
  1. Fai clic sul menu nella riga del certificato che vuoi rinnovare.
  2. Fai clic su **Renew Certificate**.
  3. Facoltativo: puoi scegliere di reimpostare le chiavi del tuo certificato selezionando la casella di spunta **Rekey certificate**. Questa azione rinnova il tuo certificato con una nuova coppia di chiavi. Quando reimposti le chiavi di un certificato, assicurati di distribuire i nuovi certificati e chiavi ovunque vengano utilizzati.
  4. Fai clic su **Renew**.


Puoi rinnovare solo i certificati che hai ordinato tramite {{site.data.keyword.cloudcerts_short}}.
{: note}

Il tuo rinnovo viene inserito nello stato **Renew pending**. Dopo che hai risposto alla verifica di convalida del dominio e {{site.data.keyword.cloudcerts_short}} verifica che gestisci il dominio richiesto, ricevi un certificato rinnovato e il suo stato viene modificato con **Valid**. Vieni avvertito quando il tuo certificato rinnovato è pronto o se si è verificato un problema, nel tuo canale di notifica Slack e/o URL di callback.
