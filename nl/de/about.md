---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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

{{site.data.keyword.cloudcerts_long}} unterstützt Sie bei der Verwaltung der SSL-Zertifikate für Ihre {{site.data.keyword.IBM_notm}} Cloud-basierten Apps und Services.
{: shortdesc}

Sie können SSL-Zertifikate, die Sie von Ihren Apps und Services empfangen, importieren und sicher speichern und Sie erhalten eine zentrale Übersicht über die Zertifikate, die Sie verwenden.

Sie können Ihre Zertifikate auf folgende Art und Weise verwalten:

* Benachrichtigung vor dem Ablauf von Zertifikaten erhalten und so eine rechtzeitige Verlängerung sicherstellen
* Zertifikatstypen über verschiedene Bereitstellungen hinweg anzeigen und die Einhaltung der Richtlinien der Organisation sicherstellen
* Zertifikate suchen, die ersetzt werden müssen, wenn neue Konformitäts- und Sicherheitsanforderungen in Kraft treten
* Mechanismen einrichten, die steuern, wer auf Ihre Zertifikate zugreifen und wer sie verwalten kann

![Diagramm der allgemeinen Servicearchitektur](images/high-level-architecture.png)
<caption>Abbildung 1. Allgemeine Servicearchitektur</caption>

## Schutz privater Schlüssel
{: #private-key-security}

Wenn Sie ein Zertifikat und den entsprechenden privaten Schlüssel in {{site.data.keyword.cloudcerts_short}} importieren, verwendet der Service einen AES 256-Algorithmus zum Verschlüsseln des privaten Schlüssels (AES = Advanced Encryption Standard). {{site.data.keyword.cloudcerts_short}} speichert diesen eindeutigen verschlüsselten Schlüssel zur Verwendung mit Ihrer Serviceinstanz.

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
    <td>Mit [{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index) werden die Informationen zu den {{site.data.keyword.cloud_notm}}-Services zentral erfasst. Zu diesen Informationen gehört die Angabe von Zertifikaten in {{site.data.keyword.cloudcerts_short}}-Instanzen des {{site.data.keyword.cloud_notm}}-Kontos, die abgelaufen sind oder demnächst ablaufen werden. [Weitere Informationen zu {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Mit [dem {{site.data.keyword.cloudaccesstrailfull_notm}}-Service](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started) können Sie die Interaktionen von Benutzern und Anwendungen mit dem {{site.data.keyword.cloudcerts_long_notm}}-Service in {{site.data.keyword.cloud_notm}} verfolgen. [Weitere Informationen zu {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).
    <p>Eine Liste der Aktionen, die ein Ereignis generieren, finden Sie in [{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Speichern Sie die angepassten Domänenzertifikate im {{site.data.keyword.cloudcerts_short}}-Service und verwenden Sie dann Zertifikats-CRNs für die Bindung mit angepassten Domänen in {{site.data.keyword.apiconnect_short}}. [Weitere Informationen {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index).</p></td>
  </tr>
</table>

## Standorte
{: #availability}

{{site.data.keyword.cloudcerts_short}} ist an den Standorten Dallas, London, Frankfurt und Tokio verfügbar.



## Grenzwerte
{: #limits}

Es können maximal 1000 Zertifikate pro Instanz hochgeladen werden.
