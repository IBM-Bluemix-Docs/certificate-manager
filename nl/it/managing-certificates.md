---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione dei certificati dal dashboard
{: #managing-certificates-from-the-dashboard}

Puoi utilizzare il dashboard del servizio {{site.data.keyword.cloudcerts_full}} per gestire i certificati che ottieni da emittenti di terze parti da utilizzare con i tuoi servizi e applicazioni basati sul cloud {{site.data.keyword.IBM_notm}}. Dopo aver importato i certificati e le chiavi, vengono codificati e archiviati nel servizio.
{: shortdesc}

## Importazione di un certificato
{: #importing-a-certificate}

Per aiutarti a gestire i tuoi certificati, puoi caricarli.
{: shortdesc}

Prima di iniziare:

* Crea un certificato non scaduto e valido con un chiave privata corrispondente.
* Converti i file nel formato Privacy-enhanced Electronic Mail (PEM).
* Lascia la chiave privata non codificata per assicurarti che possa essere importata.

Per importare un certificato, fai clic su **Importa certificato** e fornisci i seguenti dettagli: 
1. Facoltativo: immetti un nome di visualizzazione
2. Fai clic su **Sfoglia**, seleziona il file del certificato nel formato PEM.
3. Fai clic su **Sfoglia**, seleziona la chiave privata del certificato nel formato PEM.
4. Se applicabile, fornisci il file del certificato intermedio nel formato PEM.
5. Facoltativo: immetti una descrizione.
6. Fai clic su **Importa**.  

**Nota**: per rinnovare un certificato importato, ottieni un nuovo certificato dalla tua autorità di certificazione (CA) e importalo in {{site.data.keyword.cloudcerts_short}}. Dopo la distribuzione del nuovo certificato, puoi eliminare quello vecchio.

Dopo aver importato un certificato, vengono visualizzate le seguenti informazioni nella tabella Certificati. Per visualizzare ulteriori informazioni sul certificato, puoi selezionare il certificato nella riga della tabella.

<table>
<caption> Tabella 1. Informazioni sul certificato importato </caption>
  <tr>
    <th> Componente </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Facoltativo: un nome di visualizzazione significativo. Lunghezza massima 256 caratteri. </td>
    
  </tr>
  <tr>
    <td>Descrizione</td>
    <td>Facoltativo: il testo descrittivo del certificato. Lunghezza massima 1024 caratteri.</td>
  </tr>
  <tr>
    <td>Dominio</td>
    <td>Il dominio o i domini per cui il certificato è valido. </td>
  </tr>
  <tr>
    <td>Emittente</td>
    <td>La CA che ha emesso il certificato.</td>
  </tr>
  <tr>
    <td>Algoritmo</td>
    <td>Il tipo di codifica da cui il certificato viene creato. </td>
  </tr>
  <tr>
    <td>Algoritmo chiave</td>
    <td>La dimensione e il tipo di chiave utilizzati dall'algoritmo. </td>
  </tr>
  <tr>
    <td>Scade in </td>
    <td>Il numero di giorni rimanenti prima che il certificato non sia più valido. </td>
  </tr>
  <tr>
    <td>Data di emissione</td>
    <td>La data in cui è stato emesso il certificato. </td>
  </tr>
  <tr>
    <td>Valido da</td>
    <td>La data in cui il certificato diventa valido. </td>
  </tr>
  <tr>
    <td>Scade il</td>
    <td>La data da cui il certificato non è più valido. </td>
  </tr>
  <tr>
    <td>ID certificato</td>
    <td>L'ID generato fornito al certificato all'importazione. </td>
  </tr>
</table>

## Ricerca dei certificati
{: #searching-certificates}
 
Se gestisci molti certificati, puoi utilizzare la barra di ricerca per individuare il certificato necessario.
{: shortdesc}
 
-   Per eseguire la ricerca per il nome, il dominio o l'emittente del certificato, immetti il tuo termine di ricerca nella barra di ricerca e premi Invio.
-   Per visualizzare tutti i tuoi certificati, fai clic sull'icona **X** nella barra di ricerca.

## Scaricamento dei certificati
{: #downloading-certificates}

Quando sei pronto per distribuire il tuo certificato al tuo servizio o applicazione, puoi scaricare il certificato e la chiave privata associata.
{: shortdesc}

Per scaricare un certificato:

1. Seleziona la casella di spunta del certificato che desideri scaricare.
2. Fai clic su **Scarica certificato**. A seconda di cosa hai importato nel servizio, ricevi un file compresso che contiene il file PEM del certificato, una chiave associata e un certificato intermedio associato.


## Eliminazione dei certificati
{: #deleting-certificates}

Se desideri smettere di tracciare un certificato, puoi eliminarlo.
{: shortdesc}  

Per eliminare un certificato:

1. Seleziona la casella di spunta del certificato che desideri eliminare.
2. Fai clic sull'icona **Cestino**.

## Aggiornamento dei metadati del certificato
{: #updating-certificates-metadata}

Puoi anche aggiornare il nome e la descrizione di un certificato.
{: shortdesc}

Per aggiornare un certificato:

1. Seleziona una riga per aprire i dettagli di quel certificato.
2. Aggiorna il nome o la descrizione.
3. Salva le tue modifiche.

**Nota**: puoi eseguire fino a 5 azioni di aggiornamento al minuto.
