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

# Benachrichtigungen konfigurieren
{: #configuring-notifications}

Zertifikate sind normalerweise nur für einen bestimmten Zeitraum gültig. Wenn ein von Ihnen verwendetes Zertifikat abläuft, kommt es möglicherweise zu Ausfallzeiten für Ihre App. Sie können Ausfallzeiten vermeiden, indem Sie {{site.data.keyword.cloudcerts_full}} so konfigurieren, dass Benachrichtigungen für Zertifikate an Sie gesendet werden, deren Gültigkeitszeitraum demnächst abläuft, sodass Sie die Zertifikate rechtzeitig verlängern können.

Sie werden außerdem benachrichtigt, wenn eine verlängerte Version Ihres Zertifikats für das ablaufende erneut in {{site.data.keyword.cloudcerts_short}} importiert wird, damit Sie wissen, dass es auch für die SSL/TLS-Abschlusspunkte bereitgestellt werden muss. Diese Benachrichtigung zu erneut importierten Zertifikaten wird an Kanäle ausschließlich über [Kanal Version 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) gesendet.
{: shortdesc}

**Wann werde ich benachrichtigt?**  
Abhängig vom Ablaufdatum des Zertifikats, das Sie in {{site.data.keyword.cloudcerts_full_notm}} hochgeladen haben, werden Sie 90, 60, 30 und 10 Tage sowie 1 Tag vor dem Ablaufen des Zertifikats benachrichtigt. Darüber hinaus erhalten Sie tägliche Benachrichtigungen zu abgelaufenen Zertifikaten. Die täglichen Benachrichtigungen beginnen am ersten Tag nach dem Ablaufen des Zertifikats.

Sie müssen Ihr Zertifikat verlängern und dieses Zertifikat für das alte erneut in {{site.data.keyword.cloudcerts_full_notm}} importieren, damit keine Benachrichtigungen mehr gesendet werden. Wenn Sie Ihr Zertifikat erneut importieren, erhalten Sie eine Benachrichtigung darüber, dass Ihr Zertifikat erneut importiert wurde, damit Sie es wieder bereitstellen können.

**Welche Optionen zur Konfiguration der Benachrichtigungen stehen zur Verfügung?**  
Sie können Benachrichtigungen an Slack senden, indem Sie einen Slack-Webhook verwenden, oder Sie können eine beliebige Callback-URL verwenden.

## Slack-Webhook einrichten
{: #setup-callback}

Führen Sie die folgenden Schritte aus, um einen Slack-Webhook einzurichten:

1. Melden Sie sich bei [Slack](https://slack.com/) an und richten Sie einen Arbeitsbereich ein.
2. Erstellen Sie einen Slack-Kanal, an den Ihre Benachrichtigungen gesendet werden sollen.
3. Richten Sie einen [Webhook](https://api.slack.com/incoming-webhooks) für den Slack-Kanal ein.

## Callback-URL einrichten
{: #callback}

Um den Verlängerungsprozess für das Team auszulösen, können Sie eine Callback-URL verwenden, um Benachrichtigungen an die von Ihnen genutzten Tools zu senden. So können Sie zum Beispiel Benachrichtigungen senden, um Berichte für PagerDuty zu erstellen, automatisch eine Problemmeldung in GitHub zu öffnen oder Verlängerungsscripts auszulösen.  
{: shortdesc}

**Wichtig:** Der Endpunkt der Callback-URL muss die folgenden Anforderungen erfüllen, damit er in {{site.data.keyword.cloudcerts_short}} verwendet werden kann:
* Der Endpunkt muss das HTTPS-Protokoll verwenden.
* Für den Endpunkt dürfen keine HTTP-Header erforderlich sein. Diese Anforderung schließt Berechtigungsheader ein.
* Der Endpunkt muss den Statuscode `200 OK` zurückgeben, der eine erfolgreiche Benachrichtigungszustellung angibt.

### Benachrichtigungsformat
{: #notification_format}

Bei der Benachrichtigung, die an Ihre Callback-URL gesendet wird, handelt es sich um ein JSON-Dokument im folgenden Format, das mit Ihrem asymmetrischen Instanzschlüssel signiert wurde:

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Nach dem Decodieren und Verifizieren der Nutzdaten ist der Inhalt eine JSON-Zeichenfolge nach den [Gesetzmäßigkeiten der Kanalversion](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Benachrichtigungskanal konfigurieren
{: #adding-channel}

Nach dem Erstellen eines Slack-Webhooks oder einer Callback-URL fügen Sie diesen bzw. diese zu {{site.data.keyword.cloudcerts_short}} hinzu, damit Sie Benachrichtigungen zu ablaufenden und erneut importierten Zertifikaten erhalten. {{site.data.keyword.cloudcerts_short}} verschlüsselt den Endpunkt und speichert ihn sicher.
{: shortdesc}

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal hinzuzufügen:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**.
2. Öffnen Sie die Registerkarte **Benachrichtigungen**.
3. Klicken Sie auf **Benachrichtigungskanal hinzufügen**.
4. Wählen Sie den Benachrichtigungskanaltyp aus, der verwendet werden soll.
5. Geben Sie den Webhook oder die Callback-URL ein, an den bzw. die Benachrichtigungen gesendet werden sollen.
6. Klicken Sie auf **Speichern**. Eine Zusammenfassung Ihrer Konfiguration wird angezeigt.

   **Beispielausgabe**

   <table>
   <caption>Tabelle 1. Informationen zum Benachrichtigungskanal </caption>
   <thead>
    <th> Komponente </th>
    <th> Beschreibung </th>
   </thead>
   <tbody>
   <tr>
    <td>Typ</td>
    <td>Benachrichtigungskanaltyp: <i>Slack</i> oder <i>Callback-URL</i>.</td>
   </tr>
   <tr>
    <td>Endpunkt</td>
    <td>Endpunkt des Benachrichtigungskanals, an den die Benachrichtigungen gesendet werden.</td>
   </tr>
   <tr>
    <td>Schaltfläche zum Ein-/Ausschalten der Aktivierung</td>
    <td>Status des Benachrichtigungskanals. Lautet er 'inaktiviert', werden keine Benachrichtigungen gesendet.</td>
   </tr>
   <tr>
    <td>Schaltfläche zum Testen der Verbindung</td>
    <td>Sendet eine Testbenachrichtigung an den konfigurierten Kanal. </td>
   </tr>
    <tr>
      <td>Menü mit Auslassungspunkten</td>
      <td>Verfügbare Aktionen, die für den Kanal ausgeführt werden können: <i>Bearbeiten</i> oder <i>Löschen</i>.</td>
    </tr>
    </tbody>
    </table>

    Wenn Sie einen Slack-Webhook speichern, sendet {{site.data.keyword.cloudcerts_short}} automatisch eine Bestätigungsbenachrichtigung an den konfigurierten Slack-Kanal. Überprüfen Sie den Slack-Kanal, um sicherzustellen, dass Sie diese Benachrichtigung erhalten haben.
    {: tip}
7. (Optional) Wiederholen Sie diese Schritte, um weitere Benachrichtigungskanäle hinzuzufügen.

## Benachrichtigungskanal testen
{: #testing-channel}

Sie können einen Benachrichtigungskanal testen, um sicherzustellen, dass er korrekt konfiguriert ist.
{: shortdesc}

Zuerst müssen Sie [einen Benachrichtigungskanal konfigurieren](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Führen Sie die folgenden Schritte aus, um einen Benachrichtigungskanal zu testen:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**.
2. Suchen Sie Ihren Benachrichtigungskanal und klicken Sie auf **Verbindung testen**.
3. Vergewissern Sie sich, dass Sie im konfigurierten Kanal eine Benachrichtigung erhalten haben.

## Benachrichtigungskanal aktualisieren
{: #updating-channel}

Sie können die Benachrichtigungskanalkonfiguration aktualisieren, Benachrichtigungen aktivieren oder inaktivieren oder Benachrichtigungskanäle aus {{site.data.keyword.cloudcerts_short}} löschen.
{: shortdesc}

Zuerst müssen Sie [einen Benachrichtigungskanal konfigurieren](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Führen Sie die folgenden Schritte aus, um den Benachrichtigungskanal zu aktualisieren:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**.
2. Wählen Sie die Registerkarte **Benachrichtigungen** aus.
3. Wählen Sie eine der folgenden Optionen aus:
   * Zum Inaktivieren oder Aktivieren von Benachrichtigungen für einen Kanal legen Sie **Inaktivieren** oder **Aktivieren** fest.
   * Zum Aktualisieren der Einstellungen für einen Kanal wählen Sie **Bearbeiten** im Aktionsmenü aus.
   * Zum Löschen eines Benachrichtigungskanals wählen Sie **Löschen** im Aktionsmenü aus.

## HTTP-Nutzdaten für eine Callback-URL verifizieren
{: #verify-callback}

Alle HTTP-Nutzdaten, die von {{site.data.keyword.cloudcerts_short}} an Ihre Callback-URL gesendet werden, werden automatisch dem JWT-Standard entsprechend mithilfe eines asymmetrischen Schlüsselpaars signiert.  
{: shortdesc}

Für jede {{site.data.keyword.cloudcerts_short}}-Instanz werden ein privater und ein öffentlicher Schlüssel generiert, die in anderen {{site.data.keyword.cloudcerts_short}}-Instanzen nicht verwendet werden. Der private Schlüssel wird zum Signieren der HTTP-Nutzdaten verwendet; der öffentliche Schlüssel kann verwendet werden, um sicherzustellen, dass die Nutzdaten von {{site.data.keyword.cloudcerts_short}} generiert und nicht durch Dritte geändert wurden.

Führen Sie die folgenden Schritte aus, um den öffentlichen Schlüssel herunterzuladen:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**.
2. Öffnen Sie die Registerkarte **Benachrichtigungen**.
3. Klicken Sie auf die Schaltfläche **Schlüssel herunterladen**. Der Schlüssel wird als PEM-Datei heruntergeladen.

## Kanalversionen
{: #channel-versions}

Certificate Manager wird immer weiterentwickelt und so wird das Format der Nutzdatenstruktur für Benachrichtigungen möglicherweise von Zeit zu Zeit geändert. Für die Abwärtskompatibilität werden die an Ihre vorhandenen Kanäle gesendeten Nutzdaten nicht geändert.   

Gehen Sie wie folgt vor, wenn Sie über bereits vorhandene Benachrichtigungskanäle (Slack oder Callback-URL) verfügen und die neue Version der Nutzdaten abrufen möchten:
1. Stellen Sie bei der Callback-URL sicher, dass Ihre Implementierung die neuen Nutzdaten akzeptieren kann.
2. Erstellen Sie einen neuen Benachrichtigungskanal (neue Kanäle werden immer mit der aktuellen Kanalversion erstellt).
3. Testen Sie, ob der neue Kanal ordnungsgemäß funktioniert.
4. Löschen Sie den alten Kanal.

Informationen zu den Kanalversionen finden Sie in der [API-Dokumentation](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Beispiele
{: #examples}

* [Verwendung des Zertifikatsmanagers mit Callback-URLs zur Vermeidung von Ausfällen - Teil 1 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Hier finden Sie Informationen zum Generieren von GitHub Issues für Benachrichtigungen über ablaufende Zertifikate.
* [Verwendung des Zertifikatsmanagers mit Callback-URLs zur Vermeidung von Ausfällen - Teil 2 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Hier finden Sie Informationen zum Generieren von PagerDuty Incidents Issues für Benachrichtigungen über ablaufende Zertifikate.
