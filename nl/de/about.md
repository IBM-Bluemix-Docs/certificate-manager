---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

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

# Informationen zu {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_full}} unterstützt Sie beim Abrufen, Speichern und Verwalten von SSL-Zertifikaten für Ihre cloudbasierten {{site.data.keyword.IBM_notm}}-Apps.
{: shortdesc}

Sie können SSL-Zertifikate, die Sie von Ihren Apps und Services empfangen, importieren und sicher speichern und Sie erhalten eine zentrale Übersicht über die Zertifikate, die Sie verwenden. Oder Sie können öffentliche Zertifikate über Certificate Manager von unterstützten CAs bestellen.

Sie können Ihre Zertifikate auf folgende Art und Weise verwalten:

* Benachrichtigung vor dem Ablauf von Zertifikaten erhalten und so eine rechtzeitige Verlängerung sicherstellen  
* Benachrichtigungen verwenden, um die automatische Zertifikatsverlängerung auszulösen  
* Zertifikatstypen über verschiedene Bereitstellungen hinweg anzeigen und die Einhaltung der Richtlinien der Organisation sicherstellen  
* Zertifikate suchen, die ersetzt werden müssen, wenn neue Konformitäts- und Sicherheitsanforderungen in Kraft treten  
* Mechanismen einrichten, die steuern, wer auf Ihre Zertifikate zugreifen und wer sie verwalten kann
* Neue öffentliche Zertifikate bestellen


![Diagramm der allgemeinen Servicearchitektur](images/high-level-architecture.png)
<caption>Abbildung 1. Allgemeine Servicearchitektur</caption>


## Schutz privater Schlüssel
{: #private-key-security}

Wenn Sie ein Zertifikat in {{site.data.keyword.cloudcerts_short}} importieren oder ein Zertifikat bestellen, verwendet der Service einen AES 256-Algorithmus (AES = Advanced Encryption Standard) zum Verschlüsseln des privaten Schlüssels. {{site.data.keyword.cloudcerts_short}} speichert diesen eindeutigen verschlüsselten Schlüssel zur Verwendung mit Ihrer Serviceinstanz.

## Integrationen
{: #integrations}

<table>
<caption>Tabelle 1. {{site.data.keyword.cloud_notm}}-Services, die {{site.data.keyword.cloudcerts_short}} verwenden</caption>
  <tr>
    <th> Service </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Sie können TLS-Zertifikate für angepasste Domänen sicher und ohne großen Aufwand von {{site.data.keyword.cloudcerts_short}} aus in Ihrem Kubernetes-Cluster bereitstellen. Clusteradministratoren können mithilfe der [Befehle für das Kubernetes-Service-Plug-in](/docs/containers?topic=containers-cs_cli_reference) TLS-Zertifikate als geheime Kubernetes-Schlüssel mit einem neuen Zertifikat aktualisieren, ohne dass es zu Ausfallzeiten kommt. Einen Einstieg in dieses Thema vermittelt der Abschnitt zu den [Ingress-Annotationen in der Dokumentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>Mit [{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) werden die Informationen zu den {{site.data.keyword.cloud_notm}}-Services zentral erfasst. Zu diesen Informationen gehört die Angabe von Zertifikaten in {{site.data.keyword.cloudcerts_short}}-Instanzen des {{site.data.keyword.cloud_notm}}-Kontos, die abgelaufen sind oder demnächst ablaufen werden. [Weitere Informationen zu {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>Mit dem [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) können Sie die Interaktionen von Benutzern und Anwendungen mit dem {{site.data.keyword.cloudcerts_long_notm}}-Service in {{site.data.keyword.cloud_notm}} verfolgen.
    <p>Eine Liste der Aktionen, die ein Ereignis generieren, finden Sie in [{{site.data.keyword.at_short}}-Ereignisse](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Speichern Sie die angepassten Domänenzertifikate im {{site.data.keyword.cloudcerts_short}}-Service und verwenden Sie dann Zertifikats-CRNs für die Bindung mit angepassten Domänen in {{site.data.keyword.apiconnect_short}}. [Weitere Informationen zu {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index).</p></td>
  </tr>
</table>

## Verfügbarkeit
{: #availability}

{{site.data.keyword.cloudcerts_short}} ist an den Standorten Dallas, London, Frankfurt und Tokio verfügbar.



## Grenzwerte
{: #limits}

Es können maximal 1000 Zertifikate pro Instanz hochgeladen werden.

## Compliance und Standards
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} hat mehrere Zertifizierungen und Audits erfolgreich abgeschlossen und erfüllt mehrere wichtige Standards.

### HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} erfüllt die erforderlichen IBM Kontrollmechanismen, die den Anforderungen der Sicherheits- und Datenschutzregeln des Health Insurance Portability and Accountability Act (HIPAA) von 1996 entsprechen.

### International Organization for Standardization (ISO)
{: #compliance-iso}

* Zertifikat für {{site.data.keyword.IBM_notm}} Services (PaaS und SaaS) - ISO 27001

### Datenschutz-Grundverordnung (DSGVO)
{: #compliance-gdpr}

Mit der DSGVO (Datenschutz-Grundverordnung) soll in der gesamten EU ein harmonisierter Rechtsrahmen für den Datenschutz geschaffen werden, in dem Bürger wieder die Kontrolle über ihre personenbezogenen Daten übernehmen, während gleichzeitig denen, die diese Daten an einem beliebigen Standort weltweit hosten und verarbeiten, strikte Regeln auferlegt werden. Mit der Verordnung werden auch Vorschriften für den freien Verkehr personenbezogener Daten innerhalb und außerhalb der EU eingeführt. Weitere Informationen finden Sie unter [IBM Datenschutzerklärung](https://www.ibm.com/privacy/).
