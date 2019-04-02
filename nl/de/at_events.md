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

# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse  
{: #at_events}

Mit dem {{site.data.keyword.cloudaccesstrailfull}}-Service können Sie die Interaktionen von Benutzern und Anwendungen mit dem {{site.data.keyword.cloudcerts_long_notm}}-Service in {{site.data.keyword.Bluemix_notm}} verfolgen.
{:shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}}-Service zeichnet vom Benutzer initiierte Aktivitäten auf, die den Status eines Service in {{site.data.keyword.Bluemix_notm}} ändern. Weitere Informationen finden Sie in [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started). Beispiel: Beim Importieren eines Zertifikats wird ein {{site.data.keyword.cloudaccesstrailshort}}-Ereignis generiert.

In der folgenden Tabelle sind die API-Methoden aufgeführt, bei deren Aufruf ein Ereignis generiert wird.

<table>
  <caption>Tabelle 1. Aktionen, die Ereignisse generieren</caption>
  <tr>
    <th>Aktion</th>
	  <th>Beschreibung</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Zertifikat importieren.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Zertifikat erneut importieren.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Zertifikat herunterladen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>Zertifikate auflisten.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>Metadaten für Zertifikate auflisten. Details zu einem Zertifikat anzeigen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Zertifikate durchsuchen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Metadaten für Zertifikate durchsuchen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Zertifikat löschen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Zertifikatsmetadaten aktualisieren, z. B. Beschreibung eines Zertifikats ändern.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>Benachrichtigungskanäle auflisten.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Benachrichtigungskanal erstellen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Benachrichtigungskanal inaktivieren oder aktivieren.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Endpunkt für einen Benachrichtigungskanal aktualisieren.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Benachrichtigungskanal löschen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Benachrichtigungskanal testen.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>Benachrichtigung wurde an den Endpunkt eines Benachrichtigungskanals gesendet.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>Öffentlicher Schlüssel wurde angefordert.</td>
  </tr>
</table>

## Position der Ereignisse
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse befinden sich in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** an dem {{site.data.keyword.Bluemix_notm}}-Standort, an dem die Ereignisse generiert werden.

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse werden automatisch an den {{site.data.keyword.cloudaccesstrailshort}}-Service am selben Standort weitergeleitet, an dem der {{site.data.keyword.cloudcerts_short}}-Service bereitgestellt wird.

## Zusätzliche Informationen
{: #info}

Das Feld *requestData_str* enthält den lesbaren Namen des Zertifikats.
