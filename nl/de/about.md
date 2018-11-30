---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
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
    <td>Speichern Sie Ihre angepassten Domänenzertifikate für Kubernetes-Cluster in {{site.data.keyword.cloudcerts_short}} und stellen Sie sie dann mithilfe der [Kubernetes-Service-Plug-in-Befehle](/docs/containers/cs_cli_reference.html) für die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle bereit. [Weitere Informationen zu dieser Integration finden Sie hier ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>Mit {{site.data.keyword.security-advisor_short}} werden die Informationen zu den {{site.data.keyword.cloud_notm}}-Services zentral erfasst. Zu diesen Informationen gehört die Angabe von Zertifikaten in {{site.data.keyword.cloudcerts_short}}-Instanzen des {{site.data.keyword.cloud_notm}}-Kontos, die abgelaufen sind oder demnächst ablaufen werden. [Weitere Informationen zu {{site.data.keyword.security-advisor_short}} finden Sie hier](/docs/services/security-advisor/index.html#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Mit dem {{site.data.keyword.cloudaccesstrailfull_notm}}-Service können Sie die Interaktionen von Benutzern und Anwendungen mit dem {{site.data.keyword.cloudcerts_long_notm}}-Service in {{site.data.keyword.cloud_notm}} verfolgen. [Weitere Informationen zu {{site.data.keyword.cloudaccesstrailshort}} finden Sie hier](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).
    <p>Eine Liste der Aktionen, die ein Ereignis generieren, finden Sie in [{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse](/docs/services/certificate-manager/at_events.html#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Speichern Sie die angepassten Domänenzertifikate im {{site.data.keyword.cloudcerts_short}}-Service und verwenden Sie dann Zertifikats-CRNs für die Bindung mit angepassten Domänen in {{site.data.keyword.apiconnect_short}}. [Weitere Informationen zu {{site.data.keyword.apiconnect_short}} finden Sie hier](/docs/api-management/index.html#index).</p></td>
  </tr>
</table>

## Standorte
{: #availability}

{{site.data.keyword.cloudcerts_short}} steht an den Standorten Dallas und London zur Verfügung.



## Grenzwerte
{: #limits}

Es können maximal 1000 Zertifikate pro Instanz hochgeladen werden.
