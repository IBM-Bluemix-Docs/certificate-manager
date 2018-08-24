---

copyright:
  years: 2018
lastupdated: "2018-08-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse  
{: #at_events}

Mit dem {{site.data.keyword.cloudaccesstrailfull}}-Service können Sie die Interaktionen von Benutzern und Anwendungen mit dem {{site.data.keyword.cloudcerts_long}}-Service in {{site.data.keyword.Bluemix}} verfolgen.
{:shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}}-Service zeichnet vom Benutzer initiierte Aktivitäten auf, die den Status eines Service in {{site.data.keyword.Bluemix_notm}} ändern. Weitere Informationen finden Sie in [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Beispiel: Beim Importieren eines Zertifikats wird ein {{site.data.keyword.cloudaccesstrailshort}}-Ereignis generiert.

In der folgenden Tabelle sind die API-Methoden aufgeführt, bei deren Aufruf ein Ereignis generiert wird:

<table>
  <caption>Aktionen, die Ereignisse generieren</caption>
  <tr>
    <th>Aktion</th>
	  <th>Beschreibung</th>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>Von einer unabhängige Zertifizierungsstelle ausgestelltes Zertifikat importieren.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>Zertifikat herunterladen.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>Zertifikate auflisten.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>Metadaten für Zertifikate auflisten. Details zu einem Zertifikat anzeigen.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>Zertifikate durchsuchen.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>Metadaten für Zertifikate durchsuchen.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>Zertifikat löschen.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>Zertifikat aktualisieren, z. B. Beschreibung eines Zertifikats ändern.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channels.list</td>
	  <td>Benachrichtigungskanäle auflisten.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.create</td>
	  <td>Benachrichtigungskanal erstellen.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.state</td>
	  <td>Benachrichtigungskanal inaktivieren oder aktivieren.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.update</td>
	  <td>Endpunkt für einen Benachrichtigungskanal aktualisieren.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.delete</td>
	  <td>Benachrichtigungskanal löschen.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications-channel.test</td>
	  <td>Benachrichtigungskanal testen.</td>
  </tr>
  <tr>
    <td>cloudcerts.notification.sent</td>
	  <td>Benachrichtigung wurde an den Endpunkt eines Benachrichtigungskanals gesendet.</td>
  </tr>
  <tr>
    <td>cloudcerts.notifications.publickey</td>
	  <td>Öffentlicher Schlüssel wurde angefordert.</td>
  </tr>
</table>

## Position der Ereignisse
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse befinden sich in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** in der {{site.data.keyword.Bluemix_notm}}-Region, in der die Ereignisse generiert werden.

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse werden automatisch an den {{site.data.keyword.cloudaccesstrailshort}}-Service in derselben Region weitergeleitet, in der der {{site.data.keyword.cloudcerts_short}}-Service bereitgestellt wird.

## Zusätzliche Informationen
{: #info}

Das Feld *requestData_str* enthält den lesbaren Namen des Zertifikats.
