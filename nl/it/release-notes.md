
---
copyright:
  years: 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Note sulla release
{: #release-notes}

Sono disponibili le seguenti funzioni e modifiche al servizio {{site.data.keyword.cloudcerts_long}}.

## 12 settembre 2018
{: 12September2018}

- **Il nome del certificato è obbligatorio**  
  È obbligatorio fornire un valore per il nome del certificato quando lo importi.  
  Inoltre, le API v2 **Import a certificate** e **Update a certificate's metadata** sono obsolete e saranno rimosse il primo novembre 2018. Devi eseguire l'upgrade alle API v3. Per ulteriori informazioni, vedi [Documentazione API](https://console.bluemix.net/apidocs/certificate-manager).

- **Notifiche Slack raggruppate**  
  Le notifiche in Slack sono raggruppare per data di scadenza.

## 2 settembre 2018
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} è generalmente disponibile**  
  Il servizio {{site.data.keyword.cloudcerts_short}} è generalmente disponibile (GA) in {{site.data.keyword.cloud_notm}}.

## 22 agosto 2018
{: 22August2018}

- **Live nel Regno Unito**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta è disponibile nella regione Regno Unito (Regno Unito Sud).

## 15 agosto 2018
{: 15August2018}

- **Rimosse le API v1 obsolete**  
  Le API versione 1 non sono più disponibili. Se non hai ancora aggiornato la tua API, devi farlo il prima possibile. [Review the API documentation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.bluemix.net/apidocs/).

- **I ruoli della piattaforma sono stati sostituiti con i ruoli del servizio**  
  Puoi controllare l'accesso alle istanze di {{site.data.keyword.cloudcerts_short}} utilizzando i ruoli del servizio. [Ulteriori informazioni sulla gestione dell'accesso](access-management.html).

## 12 luglio 2018
{: 12July2018}

- **Callback delle notifiche**  
  È stato aggiunto il supporto di callback alle notifiche. Puoi scegliere se inviare le notifiche allo slack o di utilizzare un qualsiasi URL di callback per inviare le notifiche. Ad esempio, puoi inviare notifiche a PagerDuty, aprire automaticamente un problema in GitHub o attivare gli script di rinnovo. [Ulteriori informazioni sulle notifiche](notifications-dashboard.html).

## 12 giugno 2018
{: 12June2018}

- **Notifiche slack**  
  Sono state aggiunte le notifiche slack in modo che non perderai mai un certificato in scadenza. [Ulteriori informazioni sulle notifiche](notifications-dashboard.html).

## 19 dicembre 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} è disponibile come un servizio beta**  
  Il servizio {{site.data.keyword.cloudcerts_short}} è disponibile come un servizio beta in {{site.data.keyword.cloud_notm}}.
