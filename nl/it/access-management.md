---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL,

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

# Gestione dei ruoli di accesso al servizio
{: #managing-service-access-roles}

Puoi proteggere i servizi in {{site.data.keyword.cloud_notm}} consentendo soltanto gli utenti con i ruoli di accesso specificati per il completamento di alcune azioni.
{: shortdesc}

## Ruoli di accesso alla piattaforma
{: #platform-access-roles}

Puoi utilizzare i ruoli di accesso alla piattaforma per consentire agli utenti di completare attività sulle risorse della piattaforma, come la creazione o l'eliminazione delle istanze nel tuo account {{site.data.keyword.cloud_notm}}.

<table>
<caption> Tabella 1. Azioni che vengono associate ai ruoli di accesso alla piattaforma</caption>
  <tr>
    <th> Azione </th>
    <th> Ruolo </th>
  </tr>
  <tr>
    <td>Visualizza le istanze di {{site.data.keyword.cloudcerts_short}}</td>
    <td> Amministratore, operatore, editor, visualizzatore </td>
  </tr>
  <tr>
    <td>Crea un'istanza di {{site.data.keyword.cloudcerts_short}}</td>
    <td> Amministratore, editor </td>
  </tr>
  <tr>
    <td>Elimina un'istanza di {{site.data.keyword.cloudcerts_short}}</td>
    <td> Amministratore, editor </td>
  </tr>
</table>

## Ruoli di accesso al servizio
{: #service-access-roles}

Puoi utilizzare i ruoli di accesso al servizio per consentire agli utenti di completare attività nelle istanze di {{site.data.keyword.cloudcerts_short}}, come l'importazione, lo scaricamento, la modifica o l'eliminazione dei certificati.

<table>
<caption> Tabella 2. Azioni che vengono associate ai ruoli di accesso al servizio</caption>
  <tr>
    <th> Azione </th>
    <th> Ruolo </th>
  </tr>
  <tr>
    <td>Elenca i certificati</td>
    <td> Gestore, scrittore, lettore </td>
  </tr>
  <tr>
    <td>Scarica un certificato e la chiave privata </td>
    <td> Gestore, scrittore </td>
  </tr>
  <tr>
     <td>Ottieni i metadati del certificato </td>
     <td> Gestore, scrittore, lettore </td>
  </tr>      
  <tr>
    <td>Aggiorna i metadati del certificato</td>
    <td> Gestore, scrittore </td>
  </tr>
  <tr>
    <td>Importa o reimporta certificati, chiavi private e certificati intermedi. </td>
    <td> Gestore </td>
  </tr>
  <tr>
    <td>Ordina un certificato </td>
    <td> Gestore </td>
  </tr>
  <tr>
    <td>Elimina un certificato e la chiave privata </td>
    <td> Gestore </td>
  </tr>
      <tr>
        <td>Elenca tutti i canali di notifica </td>
        <td> Gestore, scrittore, lettore </td>
      </tr>
   <tr>
     <td>Aggiunge, aggiorna o elimina un canale di notifica </td>
     <td> Gestore </td>
   </tr>
     <tr>
       <td>Verifica un canale di notifica </td>
       <td> Gestore, scrittore, lettore </td>
     </tr>

</table>

Per ulteriori informazioni sui ruoli e le autorizzazioni utente, consulta [Ruoli utente](/docs/iam?topic=iam-userroles#userroles).

## Configurazione delle politiche di accesso per gli utenti
{: #configuring-access-policies}

Puoi configurare le politiche di accesso per un'istanza di {{site.data.keyword.cloudcerts_short}}, tutti i certificati in tale istanza oppure puoi impostare le politiche per i singoli certificati (risorse) all'interno di un'istanza.

**Esempi di assegnazione del ruolo**

* Assegna almeno un ruolo di visualizzatore ad ogni utente in modo che possa visualizzare le istanze del servizio.
* Assegna il ruolo di amministratore o editor a un utente se vuoi che crei ed elimini le istanze.
* Assegna almeno un ruolo di lettore se vuoi che un utente visualizzi i certificati in un'istanza.

{: shortdesc}

### Configurazione delle politiche di accesso
{: #configuring-access}

Per configurare le politiche di accesso, completa la seguente procedura:

1. Vai a **Gestisci > Accesso (IAM) > Utenti**. Viene visualizzato un elenco di utenti con accesso al tuo account {{site.data.keyword.cloud_notm}}.
2. Fai clic sul nome dell'utente a cui desideri assegnare una politica di accesso. Se l'utente non è visualizzato, fai clic su **Invita utenti** per [aggiungere l'utente al tuo account {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Fai clic su **Politiche di accesso** e poi su **Assegna accesso**.
4. Fai clic su **Assegna l'accesso alle risorse**.
5. Dal menu **Servizi**, seleziona **Gestore certificato**.
6. Dal menu **Istanza del servizio**, seleziona un'istanza di {{site.data.keyword.cloudcerts_short}} o utilizza il valore predefinito `Tutte le istanze`.
7. Assegna all'utente un [ruolo di accesso alla piattaforma](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles).
8. Assegna all'utente un [ruolo di accesso al servizio](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles).
9. Fai clic su **Assegna** per assegnare la politica di accesso all'utente.

### Concedere l'accesso a uno specifico certificato
{: #allow-access-to-specific-certificate}

Per consentire l'accesso a uno specifico certificato, completa la seguente procedura:

1. [Richiama l'ID del tuo certificato](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Crea due politiche di accesso:
   - La prima politica: assegna almeno un ruolo di accesso alla piattaforma **Visualizzatore** all'istanza del servizio.
   - La seconda politica: assegna almeno un ruolo di accesso al servizio **Lettore**
     - Immetti `certificate` nel campo **Tipo di risorsa**.
     - Immetti l'ID del certificato nel campo **ID risorsa**.

### Richiamo dell'ID di un certificato
{: #get-certificate-id}

Per richiamare l'ID di un certificato, completa la seguente procedura:

1. Dal dashboard {{site.data.keyword.cloud_notm}}, seleziona la tua istanza di {{site.data.keyword.cloudcerts_short}}.
2. Dalla navigazione nella pagina dei dettagli del servizio, seleziona **Gestisci**.
3. Seleziona un certificato.
4. Nei dettagli del certificato, trova il CRN del certificato.
5. Copia l'ID del certificato. Il CRN contiene diversi valori, tutti separati da due punti (`:`). L'ID del certificato è l'ultimo valore nel tuo CRN; ad esempio: `e20cb664efcbfa2c2f57801230d246a6`
