---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

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

# Gestione dei certificati dal dashboard
{: #managing-certificates-from-the-dashboard}

Puoi utilizzare il dashboard del servizio {{site.data.keyword.cloudcerts_full}} per gestire i certificati che ottieni da emittenti di terze parti da utilizzare con i tuoi servizi e applicazioni basati sul cloud {{site.data.keyword.IBM_notm}}. Dopo che ne hai eseguito l'importazione, i certificati e le chiavi vengono crittografati e memorizzati dal servizio.
{: shortdesc}

## Importazione di un certificato
{: #importing-a-certificate}

Importa i tuoi certificati in modo da poterli gestire.
{: shortdesc}

## Formati dei certificati e algoritmi chiave pubblica supportati
{: supported-formats-and-algorithms}

### Formati dei certificati
* PEM

### Algoritmi chiave pubblica
* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman key agreement protocol (ECDH)

**Prima di iniziare**

* Crea un certificato non scaduto e valido con una chiave privata corrispondente (la chiave è facoltativa).
* Converti i file nel formato Privacy-enhanced Electronic Mail (PEM).
* Lascia la chiave privata non codificata per assicurarti che possa essere importata.

Per importare un certificato, fai clic su **Importa certificato** e fornisci i seguenti dettagli:

1. Immetti un nome di visualizzazione
2. Seleziona il file del certificato in formato PEM facendo clic su **Browse**.
3. Facoltativo: seleziona la chiave privata del certificato nel formato PEM facendo clic su **Browse**.
4. Se applicabile, fornisci il file del certificato intermedio nel formato PEM.
5. Facoltativo: immetti una descrizione.
6. Fai clic su **Importa**.

Dopo aver importato un certificato, vengono visualizzate le seguenti informazioni nella tabella Certificati. Per visualizzare ulteriori informazioni sul certificato, puoi espandere la riga del certificato nella tabella Certificati.

<table>
<caption> Tabella 1. Informazioni sul certificato importato </caption>
  <tr>
    <th> Componente </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Un nome di visualizzazione significativo. La lunghezza massima è di 256 caratteri. </td>
  </tr>
  <tr>
    <td>Descrizione</td>
    <td>(Facoltativo) Testo descrittivo per il certificato. La lunghezza massima è di 1024 caratteri.</td>
  </tr>
  <tr>
    <td>Dominio</td>
    <td>Il dominio o i domini per cui il certificato è valido. </td>
  </tr>
  <tr>
    <td>Emittente</td>
    <td>L'Autorità di certificazione (o CA, Certificate Authority) che ha emesso il certificato.</td>
  </tr>
  <tr>
    <td>Algoritmo</td>
    <td>L'algoritmo della firma del certificato</td>
  </tr>
  <tr>
    <td>Algoritmo chiave</td>
    <td>L'algoritmo chiave pubblica</td>
  </tr>
  <tr>
    <td>Scade in</td>
    <td>Il numero di giorni rimanenti prima che il certificato non sia più valido. </td>
  </tr>
  <tr>
    <td>Valido da</td>
    <td>La data in cui il certificato diventa valido (nel fuso orario UTC). </td>
  </tr>
  <tr>
    <td>Scade il</td>
    <td>La data da cui il certificato non è più valido (nel fuso orario UTC). </td>
  </tr>
  <tr>
    <td>ID certificato</td>
    <td>L'ID generato fornito al certificato all'importazione.</td>
  </tr>
</table>

</br>

## Reimportazione di un certificato
{: #reimport-certificate}

Se il tuo certificato sta per scadere, puoi aggiornare il certificato importando una nuova versione del certificato che ha lo stesso dominio del certificato esistente ma che ha una nuova data di scadenza. Quando un certificato viene reimportato, la versione esistente del certificato viene conservata come un backup che può essere scaricato, se necessario.
{: shortdesc}

### Reimportazione del tuo certificato
{: #reimporting-certificate}

Per reimportare un certificato, completa la seguente procedura:

1. Espandi la riga per il certificato.
2. Fai clic su **Reimport certificate**.
3. Seleziona il nuovo file di certificato in formato PEM facendo clic su **Browse**.
4. (Facoltativo) Seleziona la chiave privata del nuovo certificato in formato PEM facendo clic su **Browse**.
5. (Facoltativo) Fornisci un nuovo file di certificato intermedio in formato PEM facendo clic su **Browse**.
6. Fai clic su **Reimport** e quindi su **Done**.

La reimportazione dei certificati è limitata a cinque azioni al minuto.
{: note}

### Download di una versione precedente del tuo certificato
{: #downloading-certificate}

Per scaricare la versione precedente di un certificato, completa la seguente procedura:

1. Espandi la riga per il certificato.
2. Fai clic sul link **Previous version**.

## Ricerca dei certificati
{: #searching-certificates}

Se gestisci molti certificati, puoi utilizzare la barra di ricerca per individuare il certificato necessario.
{: shortdesc}

* Per eseguire la ricerca per il nome, il dominio o l'emittente del certificato, immetti il tuo termine di ricerca nella barra di ricerca e premi Invio.
* Per visualizzare tutti i tuoi certificati, fai clic sull'icona **X** nella barra di ricerca.

## Scaricamento dei certificati
{: #downloading-certificates}

Quando sei pronto per distribuire il tuo certificato al tuo servizio o applicazione, puoi scaricare il certificato e la chiave privata associata.
{: shortdesc}

Per scaricare un certificato, completa la seguente procedura:

1. Seleziona la casella di spunta del certificato che desideri scaricare.
2. Fai clic su **Scarica certificato**. A seconda di cosa hai importato nel servizio, ricevi un file compresso che contiene il file PEM del certificato, una chiave associata e un certificato intermedio associato.

## Eliminazione dei certificati
{: #deleting-certificates}

Se desideri smettere di tracciare un certificato, puoi eliminarlo.
{: shortdesc}  

Per eliminare un certificato, completa la seguente procedura:

1. Seleziona la casella di spunta del certificato che desideri eliminare.
2. Fai clic sull'icona **Cestino**.

## Aggiornamento dei metadati del certificato
{: #updating-certificates-metadata}

Puoi anche aggiornare il nome e la descrizione di un certificato.
{: shortdesc}

Per aggiornare un certificato, completa la seguente procedura:

1. Seleziona una riga per aprire i dettagli di quel certificato.
2. Aggiorna il nome o la descrizione.
3. Salva le tue modifiche.

Puoi eseguire fino a cinque azioni di aggiornamento al minuto.
{: note}
