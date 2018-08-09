---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Benachrichtigungen für ablaufende Zertifikate konfigurieren
{: #configuring-notifications-for-expiring-certificates}

Zertifikate sind normalerweise nur für einen bestimmten Zeitraum gültig. Wenn ein von Ihnen verwendetes Zertifikat abläuft, kommt es möglicherweise zu Ausfallzeiten für Ihre App. Sie können Ausfallzeiten vermeiden, indem Sie {{site.data.keyword.cloudcerts_full}} so konfigurieren, dass Benachrichtigungen für Zertifikate gesendet werden, deren Gültigkeitszeitraum demnächst abläuft, sodass Sie die Zertifikate rechtzeitig verlängern können.
{: shortdesc}

**Wann werde ich benachrichtigt?** </br>
Abhängig vom Ablaufdatum des Zertifikats, das Sie in {{site.data.keyword.cloudcerts_full}} hochgeladen haben, werden Sie 90, 60, 30 und 10 Tage sowie 1 Tag vor dem Ablaufen des Zertifikats benachrichtigt. Darüber hinaus erhalten Sie tägliche Benachrichtigungen zu abgelaufenen Zertifikaten, beginnend mit dem ersten Tag nach dem Ablaufen des Zertifikats. 

Sie müssen das Zertifikat verlängern, dieses Zertifikat in {{site.data.keyword.cloudcerts_full}} hochladen und das abgelaufene Zertifikat löschen, damit keine weiteren Benachrichtigungen gesendet werden. 

**Welche Optionen zur Konfiguration der Benachrichtigungen stehen zur Verfügung?** </br>
Sie können Benachrichtigung an Slack senden, indem Sie einen Slack-Webhook verwenden, oder Sie können eine beliebige Callback-URL verwenden. 

## Slack-Webhook einrichten
{: #setup-callback}

1. Melden Sie sich bei [Slack](https://slack.com/) an und richten Sie einen Arbeitsbereich ein. 
2. Erstellen Sie einen Slack-Kanal, an den Ihre Benachrichtigungen gesendet werden sollen. 
3. Richten Sie einen [Webhook](https://api.slack.com/incoming-webhooks) für den Slack-Kanal ein. 

## Callback-URL einrichten
{: #callback}

Sie können eine Callback-URL verwenden, um Benachrichtigungen an täglich genutzte Tools zu senden und so den Verlängerungsprozess für das Team auszulösen. So können Sie zum Beispiel Benachrichtigungen senden, um Berichte für PagerDuty zu erstellen, automatisch eine Problemmeldung in GitHub zu öffnen oder Verlängerungsscripts auszulösen.  
{: shortdesc}

**Wichtig:** Der Endpunkt der Callback-URL muss die folgenden Anforderungen erfüllen, damit er in {{site.data.keyword.cloudcerts_short}} verwendet werden kann: 
* Der Endpunkt muss das HTTPS-Protokoll verwenden.
* Für den Endpunkt dürfen keine HTTP-Header erforderlich sein. Diese Anforderung schließt Berechtigungsheader ein.

### Callback-URL verwenden, um automatisch eine GitHub-Problemmeldung zu öffnen 
{: #sample}

Der folgende Beispielcode veranschaulicht, wie eine GitHub-Problemmeldung für ablaufende Zertifikate beim Senden einer {{site.data.keyword.cloudcerts_short}}-Benachrichtigung erstellt wird. Sie können diesen Code in {{site.data.keyword.openwhisk}} ausführen oder in einer anderen Umgebung verwenden.   
{: shortdesc}

Gehen Sie wie folgt vor, um diesen Code in {{site.data.keyword.openwhisk}} auszuführen:

1. Erstellen Sie eine [Aktion in {{site.data.keyword.openwhisk}}](/docs/openwhisk/index.html#getting-started).
2. Verwenden Sie den folgenden Code, um automatisch eine GitHub-Problemmeldung zu erstellen: 

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "<Persönliches GitHub-Token>";

    /**
     * Gibt das Ablaufdatum als kurze Datumszeichenfolge zurück.
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Erstellt die Zeichenfolge für den Hauptteil der Problemmeldung.
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Ruft den Benachrichtigungshauptteil ab und erstellt eine Github-Problemmeldung.
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Zum Abrufen der Informationen Nachricht decodieren.
        const data = jwtDecode(params.data);
        try {
            // Anforderungsoptionen erstellen, um den öffentlichen Schlüssel zur Verifizierung abzurufen.
            const keysOptions = {
                method: 'GET',
                url: `https://<Basis-URL für Zertifikatsmanagercluster>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Anforderung zum Abrufen des öffentlichen Schlüssels senden.
            const keysResponse = await request(keysOptions);

            // Daten mithilfe des abgerufenden öffentlichen Schlüssels verifizieren.
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Anforderungsoptionen zum Senden einer neuen Problemmeldung an GitHub erstellen.
            // GitHub-API-basiert - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<Repository-Eigner>/<Repositoryname>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Zertifikat läuft demnächst ab",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Anforderung an GitHub senden.
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}
    
Informationen zu anderen REST-API-Befehlen finden Sie in der [API-Dokumentation](https://console.bluemix.net/apidocs/cloudcerts).
{: tip}


## Benachrichtigungskanal konfigurieren
{: #adding-channel}

Nach dem Erstellen eines Slack-Webhooks oder einer Callback-URL fügen Sie diesen bzw. diese zu {{site.data.keyword.cloudcerts_short}} hinzu, damit Sie Benachrichtigungen zu ablaufenden Zertifikaten erhalten. {{site.data.keyword.cloudcerts_short}} verschlüsselt den Endpunkt und speichert ihn sicher.
{: shortdesc}

Gehen Sie wie folgt vor, um einen Benachrichtigungskanal hinzuzufügen:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**. 
2. Öffnen Sie die Registerkarte **Benachrichtigungen**.
3. Klicken Sie auf **Benachrichtigungskanal hinzufügen**. 
4. Wählen Sie den Benachrichtigungskanaltyp aus, der verwendet werden soll. 
5. Geben Sie den Webhook oder die Callback-URL ein, an den bzw. die Benachrichtigungen gesendet werden sollen.
6. Klicken Sie auf **Speichern**. Eine Zusammenfassung Ihrer Konfiguration wird angezeigt. 

   Beispielausgabe: 
   <table>
   <caption> Informationen zum Benachrichtigungskanal </caption>
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
7. Optional: Wiederholen Sie diese Schritte, um weitere Benachrichtigungskanäle hinzuzufügen. 

## Benachrichtigungskanal testen
{: #testing-channel}

Sie können einen Benachrichtigungskanal testen, um sicherzustellen, dass er korrekt konfiguriert ist.
{: shortdesc}

Zuerst müssen Sie [einen Benachrichtigungskanal konfigurieren](#adding-channel). 

Gehen Sie wie folgt vor, um einen Benachrichtigungskanal zu testen: 

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**. 
2. Suchen Sie Ihren Benachrichtigungskanal und klicken Sie auf **Verbindung testen**.
3. Vergewissern Sie sich, dass Sie im konfigurierten Kanal eine Benachrichtigung erhalten haben. 


## Benachrichtigungskanal aktualisieren
{: updating-channel}

Sie können die Benachrichtigungskanalkonfiguration aktualisieren, Benachrichtigungen aktivieren oder inaktivieren oder Benachrichtigungskanäle aus {{site.data.keyword.cloudcerts_short}} löschen.
{: shortdesc}

Zuerst müssen Sie [einen Benachrichtigungskanal konfigurieren](#adding-channel). 

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**. 
2. Wählen Sie die Registerkarte **Benachrichtigungen** aus. 
3. Wählen Sie eine der folgenden Optionen aus. 
   - Zum Inaktivieren oder Aktivieren von Benachrichtigungen für einen Kanal legen Sie **Inaktivieren** oder **Aktivieren** fest. 
   - Zum Aktualisieren der Einstellungen für einen Kanal wählen Sie **Bearbeiten** im Aktionsmenü aus.
   - Zum Löschen eines Benachrichtigungskanals wählen Sie **Löschen** im Aktionsmenü aus. 
   
   
## HTTP-Nutzdaten für eine Callback-URL verifizieren
{: #verify-callback}

Alle HTTP-Nutzdaten, die von {{site.data.keyword.cloudcerts_short}} an Ihre Callback-URL gesendet werden, werden automatisch dem JWT-Standard entsprechend mithilfe eines asymmetrischen Schlüsselpaars signiert.  
{: shortdesc}

Für jede {{site.data.keyword.cloudcerts_short}}-Instanz werden ein privater und ein öffentlicher Schlüssel generiert, die in anderen {{site.data.keyword.cloudcerts_short}}-Instanzen nicht verwendet werden. Der private Schlüssel wird zum Signieren der HTTP-Nutzdaten verwendet; der öffentliche Schlüssel kann verwendet werden, um sicherzustellen, dass die Nutzdaten von {{site.data.keyword.cloudcerts_short}} generiert und nicht durch Dritte geändert wurden.

Gehen Sie wie folgt vor, um den öffentlichen Schlüssel herunterzuladen:

1. Klicken Sie im Navigationsbereich der Servicedetailseite auf **Einstellungen**.
2. Öffnen Sie die Registerkarte **Benachrichtigungen**.
3. Klicken Sie auf die Schaltfläche **Schlüssel herunterladen**. Der Schlüssel wird als PEM-Datei heruntergeladen.
