---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Informazioni
{: #about-cloud-certs}

Scopri ulteriori informazioni su {{site.data.keyword.cloudcerts_full}}.

## Cosa è {{site.data.keyword.cloudcerts_short}}
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} ti aiuta a gestire i certificati SSL per i tuoi servizi e applicazioni basati sul cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Puoi importare i certificati SSL che ottieni per i tuoi servizi e applicazioni, archiviarli in modo sicuro e ottenere una vista centrale dei certificati che stai utilizzando.

Puoi gestire i tuoi certificati nei seguenti modi:

* Monitora le date di scadenza dei tuoi certificati per assicurarti di rinnovarli in tempo
* Visualizza i tipi di certificati nelle tue distribuzioni e assicurati che soddisfino le politiche dell'organizzazione
* Trova i certificati che devono devono essere sostituiti quando vengono emessi nuovi requisiti di sicurezza o conformità
* Configura i controlli su chi può accedere e gestire i tuoi certificati

## Disponibilità
{: #availability}

{{site.data.keyword.cloudcerts_short}} è disponibile solo nella regione Stati Uniti Sud.

## Sicurezza chiave privata 
{: #private-key-security}

Quando importi un certificato e la rispettiva chiave privata in {{site.data.keyword.cloudcerts_short}}, il servizio utilizza un algoritmo Advanced Encryption Standard (AES) 256 per codificare la chiave privata. {{site.data.keyword.cloudcerts_short}} salva questa chiave codificata univoca da utilizzare con la tua istanza del servizio.

## Identity and Access Management
{: #identity-access-management}

Puoi proteggere i servizi in {{site.data.keyword.Bluemix_notm}} consentendo soltanto gli utenti con i ruoli specificati per il completamento di alcune azioni.
{: shortdesc}

<table>
<caption> Tabella 1. Azioni che vengono associate ai ruoli utente</caption>
  <tr>
    <th> Azione</th>
    <th> Ruolo </th>
  </tr>
  <tr>
    <td>Elenca i certificati</td>
    <td> Amministratore, operatore, editor, visualizzatore </td>
  </tr>
  <tr>
    <td>Scarica un certificato e la chiave privata </td>
    <td> Amministratore, operatore </td>
  </tr>
  <tr>
    <td>Aggiorna i dati del certificato</td>
    <td> Amministratore, editor </td>
  </tr>
  <tr>
    <td>Carica i certificati, le chiavi private e i certificati intermedi </td>
    <td> Amministratore, editor </td>
  </tr>
  <tr>
    <td>Elimina un certificato e la chiave privata </td>
    <td> Amministratore, editor </td>
  </tr>
</table>

Per ulteriori informazioni sui ruoli e le autorizzazioni utente, consulta [Ruoli utente](/docs/admin/patterns.html#userroles).

### Assegnazione dei ruoli utente
{: #assigning-user-roles}

Per assegnare un ruolo utente al livello dell'account o al livello del gruppo di risorse, completa la seguente procedura.
Se l'utente non fa parte della tua organizzazione, inizia inviando un invito a tale utente.

1. Vai a **Gestisci > Account > Utenti**.
2. Dal menu **Azioni**, seleziona **Assegna politica**.
3. Fai clic su **Assegna l'accesso alle risorse** o su **Assegna l'accesso in un gruppo di risorse**.
4. In **Servizi**, seleziona **Gestore certificato**.
5. Facoltativo: seleziona una **Regione** o utilizza il valore predefinito, **Tutte le regioni**.
6. Facoltativo: seleziona un'**Istanza del servizio** o utilizza il valore predefinito, **Tutte le istanze**.
7. In **Seleziona ruoli > Assegna i ruoli di accesso alla piattaforma**, seleziona il livello di accesso appropriato.
