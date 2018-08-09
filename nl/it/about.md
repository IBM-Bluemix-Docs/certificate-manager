---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-21"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni sul Gestore certificato
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}} ti aiuta a gestire i certificati SSL per i tuoi servizi e applicazioni basati sul cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Puoi importare i certificati SSL che ottieni per i tuoi servizi e applicazioni, archiviarli in modo sicuro e ottenere una vista centrale dei certificati che stai utilizzando.

Puoi gestire i tuoi certificati nei seguenti modi:

* Ricevi una notifica prima della scadenza dei certificati per assicurarti di rinnovarli in tempo
* Visualizza i tipi di certificati nelle tue distribuzioni e assicurati che soddisfino le politiche dell'organizzazione
* Trova i certificati che devono essere sostituiti quando vengono emessi nuovi requisiti di sicurezza o conformità
* Configura i controlli su chi può accedere e gestire i tuoi certificati

## Sicurezza chiave privata
{: #private-key-security}

Quando importi un certificato e la rispettiva chiave privata in {{site.data.keyword.cloudcerts_short}}, il servizio utilizza un algoritmo Advanced Encryption Standard (AES) 256 per codificare la chiave privata. {{site.data.keyword.cloudcerts_short}} salva questa chiave codificata univoca da utilizzare con la tua istanza del servizio.

## Disponibilità
{: #availability}

{{site.data.keyword.cloudcerts_short}} è disponibile solo nella regione Stati Uniti Sud.

## Integrazioni
{: #integrations}
<table>
<caption> Tabella 1. Servizi IBM Cloud che utilizzano il Gestore certificato</caption>
  <tr>
    <th> Servizio </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Archivia i tuoi certificati del dominio personalizzato del cluster Kubernetes nel Gestore certificato, poi distribuiscili utilizzando i [comandi del plugin del servizio Kubernetes](/docs/containers/cs_cli_reference.html) della CLI IBM Cloud. [Ulteriori informazioni su questa integrazione](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>IBM Cloud Security Advisor</td>
    <td>Security Advisor centralizza le informazioni approfondite dei servizi IBM Cloud, inclusa l'indicazione dei certificati scaduti o quasi scaduti nelle istanze del Gestore certificato nel tuo account IBM Cloud. [Ulteriori informazioni su Security Advisor](/docs/services/security-advisor/index.html#index)</td>
  </tr><tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui gli utenti e le applicazioni interagiscono con il servizio {{site.data.keyword.cloudcerts_long}} in {{site.data.keyword.Bluemix}}. [Ulteriori informazioni su {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).
    <p>Per ottenere l'elenco delle azioni che generano un evento, vedi [Eventi di {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager/at_events.html#at_events).</p></td>
  </tr>
</table>
