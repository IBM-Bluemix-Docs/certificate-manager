---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione dei ruoli di accesso al servizio
{: #managing-service-access-roles}

Puoi proteggere i servizi in {{site.data.keyword.Bluemix_notm}} consentendo soltanto gli utenti con i ruoli di accesso specificati per il completamento di alcune azioni.
{: shortdesc}

### Ruoli di accesso alla piattaforma
{: #platform-access-roles}

Puoi utilizzare i ruoli di accesso alla piattaforma per consentire agli utenti di completare le attività sulle risorse della piattaforma, come la creazione o l'eliminazione delle istanze nel tuo account IBM Cloud.

<table>
<caption> Tabella 1. Azioni che vengono associate ai ruoli di accesso alla piattaforma</caption>
  <tr>
    <th> Azione </th>
    <th> Ruolo </th>
  </tr>
  <tr>
    <td>Visualizza le istanze del Gestore certificato</td>
    <td> Amministratore, operatore, editor, visualizzatore </td>
  </tr>
  <tr>
    <td>Crea un'istanza del Gestore certificato</td>
    <td> Amministratore, editor </td>
  </tr>
  <tr>
    <td>Elimina un'istanza del Gestore certificato</td>
    <td> Amministratore, editor </td>
  </tr>
</table>

I ruoli della piattaforma storicamente forniscono anche l'accesso ad alcune azioni sui certificati all'interno delle istanze. Questa definizione è obsoleta e sarà rimossa nel prossimo futuro.

### Ruoli di accesso al servizio
{: #service-acceess-roles}

Puoi utilizzare i ruoli di accesso al servizio per consentire agli utenti di completare le attività nelle istanze del Gestore certificato, come l'importazione, lo scaricamento, la modifica o l'eliminazione dei certificati.

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
    <td>Aggiorna i dati del certificato</td>
    <td> Gestore, scrittore </td>
  </tr>
  <tr>
    <td>Carica i certificati, le chiavi private e i certificati intermedi </td>
    <td> Gestore  </td>
  </tr>
  <tr>
    <td>Elimina un certificato e la chiave privata </td>
    <td> Gestore  </td>
  </tr>
</table>


Per ulteriori informazioni sui ruoli e le autorizzazioni utente, consulta [Ruoli utente](/docs/iam/users_roles.html#userroles).

### Assegnazione dei ruoli di accesso utente
{: #assigning-user--access-roles}

Per assegnare un ruolo di accesso al livello dell'account o al livello del gruppo di risorse, completa la seguente procedura.
Se l'utente non fa parte della tua organizzazione, inizia inviando un invito a tale utente.

1. Vai a **Gestisci > Account > Utenti**.
2. Dal menu **Azioni**, seleziona **Assegna politica**.
3. Fai clic su **Assegna l'accesso alle risorse** o su **Assegna l'accesso in un gruppo di risorse**.
4. In **Servizi**, seleziona **Gestore certificato**.
5. Facoltativo: seleziona una **Regione** o utilizza il valore predefinito, **Tutte le regioni**.
6. Facoltativo: seleziona un'**Istanza del servizio** o utilizza il valore predefinito, **Tutte le istanze**.
7. In **Seleziona ruoli > Assegna i ruoli di accesso alla piattaforma/servizio**, seleziona il livello di accesso appropriato.

**Esempi:**
* Assegna almeno un ruolo di visualizzatore ad ogni utente in modo che possa visualizzare le istanze del servizio. 
* Assegna il ruolo di amministratore o editor a un utente se vuoi che crei le istanze. 
* Assegna almeno un ruolo di lettore se vuoi che un utente visualizzi i certificati in un'istanza.
