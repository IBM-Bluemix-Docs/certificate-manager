---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

subcollection: certificate-manager

---

{:external: target="_blank" .external}
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

# Zertifikate bestellen
{: #ordering-certificates}

Sie können {{site.data.keyword.cloudcerts_long}} zum Bestellen von öffentlichen SSL/TLS-Zertifikaten für Ihre Apps und Services verwenden, die von unterstützten externen Zertifizierungsstellen signiert werden. {{site.data.keyword.cloudcerts_short}} erleichtert Ihnen die Bestellung von öffentlichen Zertifikaten und bietet Ihnen zusätzliche Sicherheit für Ihre privaten SSL/TLS-Schlüssel. Nachdem Ihr Zertifikat ausgestellt wurde, können Sie es in integrierten Services bereitstellen oder herunterladen, um es an anderer Stelle zu verwenden.  
{: shortdesc}

Wenn Sie ein Zertifikat bestellen, wird Ihr privater Schlüssel für SSL/TLS direkt in {{site.data.keyword.cloudcerts_short}} generiert und sicher gespeichert. Alle Anforderungen und der Zugriff auf ausgestellte Zertifikate können über die [Zugriffssteuerung](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles) verwaltet und automatisch mithilfe von [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events) geprüft werden.  

{{site.data.keyword.cloudcerts_short}} implementiert das ACME-v2-Protokoll (Automatic Certificate Management Environment) als ACME-Client. Das ACME-Protokoll ermöglicht es, vertrauenswürdige Browser-Zertifikate ohne menschliches Eingreifen automatisch zu erhalten.

## Zertifikatmerkmale
{: #certificate-characteristics}

Für die Bestellung von Zertifikaten über {{site.data.keyword.cloudcerts_short}} gilt Folgendes:

- Sie sind kostenfrei. 
- Sie sind für einen Zeitraum von 90 Tagen gültig. 
- Single-Domain-, Multi-Domain- (SAN) oder Wildcard-Zertifikate sind möglich. 
- Sie verwenden eine Domänenvalidierung. 

Im Rahmen der Domänenvalidierung wird verifiziert, dass Sie der Eigner der Domäne sind, für die Sie ein Zertifikat anfordern. Wenn Sie Extended Validation (EV)- oder Organization Validated (OV)-Zertifikate benötigen, können Sie diese an anderer Stelle beziehen und in {{site.data.keyword.cloudcerts_short}} importieren, um ihren Lebenszyklus zu verwalten.


## Unterstützte Zertifizierungsstellen
{: #supported-certificate-authorities}

Eine Zertifizierungsstelle (Certificate Authority, CA) ist eine Entität, die digitale Zertifikate ausstellt. Die CA agiert als vertrauenswürdige dritte Partei sowohl für den Anforderer des Zertifikats als auch für den Client, der auf das Zertifikat angewiesen ist.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
["Let's Encrypt"](https://letsencrypt.org) ist eine kostenlose, automatisierte, ACME-basierte Zertifizierungsstelle, die über 90 Tage gültige validierte Zertifikate zur Verfügung stellt. Es handelt sich um einen Service, der von der Internet Security Research Group (ISRG) bereitgestellt wird.

## Zertifikatsbestellung einrichten
{: #setup}

Bevor für Sie ein Zertifikat ausgestellt werden kann, muss {{site.data.keyword.cloudcerts_short}} sicherstellen, dass Sie die Kontrolle über alle Domänen haben, die Sie in Ihrer Anforderung aufführen. Hierfür verwendet {{site.data.keyword.cloudcerts_short}} die DNS-Validierung.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} sendet eine Abfrage in Form eines DNS-TXT-Datensatzes (DNS = Domain Name System), den Sie in Ihrem DNS-Service hinzufügen können. Für jede Domäne, die Sie in Ihrem Zertifikat anfordern, erhalten Sie einen separaten DNS-TXT-Datensatz. Nachdem Sie den DNS-TXT-Datensatz hinzugefügt haben, überprüfen {{site.data.keyword.cloudcerts_short}} und "Let's Encrypt", ob er in Ihrem DNS-Service enthalten ist. Wenn Sie die Abfrage erfolgreich abgeschlossen haben, wird für Sie ein "Let's Encrypt"-Zertifikat ausgegeben, das in Ihrer {{site.data.keyword.cloudcerts_short}}-Instanz verfügbar ist.

Die Vorgehensweise bei der Verifizierung des Domäneneigners ist davon abhängig, ob Sie {{site.data.keyword.cis_full_notm}} oder einen anderen DNS-Provider verwenden. 


### {{site.data.keyword.cis_full_notm}}
{: #cis}

Wenn Sie Ihre Domänen in {{site.data.keyword.cis_short}} verwalten, führen Sie die folgenden Schritte aus, um den Eigner zu verifizieren: 

1. Navigieren Sie zu **{{site.data.keyword.cloud_notm}} >Verwalten > Zugriff (IAM) > Berechtigungen**. 
2. Klicken Sie auf **Erstellen** und weisen Sie einen Quellen- und Zielservice zu. Dem Quellenservice wird auf der Basis der im nächsten Schritt festgelegten Rollen Zugriff auf den Zielservice erteilt. 
  * Quelle: {{site.data.keyword.cloudcerts_short}}
  * Ziel: Internet Services
3. Geben Sie sowohl für die Quelle als auch für das Ziel eine Serviceinstanz an. 
4. Weisen Sie die Rolle eines **Leseberechtigten** zu, um es {{site.data.keyword.cloudcerts_short}} zu ermöglichen, die {{site.data.keyword.cis_short_notm}}-Instanz und die zugehörigen Domänen anzuzeigen. Klicken Sie dann auf **Berechtigen**.

  Zu Testzwecken können Sie die Servicezugriffsrolle **Manager** für die Verwaltung aller Domänen über die Benutzerschnittstelle zuweisen. In diesem Fall müssen Sie Schritt 5 nicht ausführen. Für Produktionsumgebungen wird empfohlen, die Servicezugriffsrolle **Leseberechtigter** zuzuweisen und die API wie in Schritt 5 beschrieben zu verwenden, um bestimmte Domänen zu kontrollieren.
{: note}
   
5. Zur Kontrolle bestimmter Domänen weisen Sie die Rolle **Manager** über die API zu, sodass {{site.data.keyword.cloudcerts_short}} die DNS-Datensätze für die einzelnen Domänen verwalten kann, die in Ihrer Instanz von {{site.data.keyword.cis_short_notm}} vorhanden sind. Sie können den Befehl in eine Textdatei kopieren, um die Bearbeitung der erforderlichen Parameter zu vereinfachen. 
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <Token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<Konto-ID>" }, { "name": "serviceInstance", "value": "<Instanz-ID auf der Basis der Certificate Manager-GUID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<Konto-ID>" }, { "name": "serviceInstance", "value": "<Instanz-ID auf der Basis der Cloud Internet Services-GUID>" }, { "name": "domainId", "value": "<Domänen-ID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>Variable</th>
      <th>Beschreibung</th>
    </tr>
    <tr>
      <td><code>Token</code></td>
      <td>Ein gültiges IAM-Token. Sie können den Wert über die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle ermitteln: <code>ibmcloud iam oauth-tokens</code>. </td>
    </tr>
    <tr>
      <td><code>Konto-ID</code></td>
      <td>Die ID für das Konto, in dem sich die Instanzen von {{site.data.keyword.cloudcerts_short}} und {{site.data.keyword.cis_short_notm}} befinden. Sie können den Wert ermitteln, indem Sie zu <b>{{site.data.keyword.cloud_notm}} > Verwalten > Konto > Kontoeinstellungen</b> navigieren oder indem Sie die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle verwenden: <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><code>Instanz-ID auf der Basis der Certificate Manager-GUID</code></td>
      <td>Die GUID-basierte ID für Ihre Instanz von {{site.data.keyword.cloudcerts_short}}. Sie können den Wert über die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle ermitteln: <code>ibmcloud resource service-instance "Instanzname"</code>. </td>
    </tr>
    <tr>
      <td><code>Instanz-ID auf der Basis der Cloud Internet Services-GUID</code></td>
      <td>Die GUID-basierte ID für Ihre Instanz von {{site.data.keyword.cis_short_notm}}. Sie können den Wert über die {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle ermitteln: <code>ibmcloud resource service-instance "Instanzname"</code>. </td>
    </tr>
    <tr>
      <td><code>Domänen-ID</code></td>
      <td>Die ID Ihrer Domäne wie in {{site.data.keyword.cis_short_notm}} angegeben. Sie können den Wert ermitteln, indem Sie in der {{site.data.keyword.cloud_notm}}-Befehlszeilenschnittstelle den Befehl <code>ibmcloud cis domains</code> ausführen. Wenn Sie mehrere Domänen verwalten möchten, ändern Sie das Array <code>resources</code> entsprechend. </td>
    </tr>
  </table>

Nun können Sie ein [Zertifikat bestellen](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate). 


### Anderer DNS-Provider
{: #other_provider}

Wenn Sie Ihre Kontrolle einer Domäne verifizieren möchten und einen anderen DNS-Provider (Drittanbieter) verwenden, sendet {{site.data.keyword.cloudcerts_short}} den TXT-Datensatz an einen von Ihnen angegebenen Callback-URL-Benachrichtigungskanal. Auf diese Weise können Sie den Domänenvalidierungsprozess automatisieren. 

Zuerst implementieren Sie eine IBM Cloud Function-Aktion für die Domänenvalidierung und anschließend geben Sie einem Callback-URL-Benachrichtigungskanal den entsprechenden Endpunkt an. Lesen Sie zum Einstieg die Informationen in [Callback-URL-Benachrichtigungskanal einrichten](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions). 

Weitere Informationen zum Einrichten der Domänenvalidierung mithilfe eines Callback-URL-Benachrichtigungskanals finden Sie in [diesem Blogbeitrag](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}.
{: tip}


#### Auf eine Abfrage antworten
{: #responding-to-challenge}

Der Benachrichtigungskanal empfängt eine Benachrichtigung mit der folgenden Struktur:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // Das erste Ereignis ist das Hinzufügen des erforderlichen TXT-Abfragedatensatzes und das zweite das Löschen desselben TXT-Datensatzes, sobald die Abfrage beendet ist.
    "certificateCRN": "<CERTIFICATE_CRN>", // Das bestellte CRN-Zertifikat
    "userToken": "<USER_TOKEN>", /// Das IAM-Token, das die Identität des Benutzers enthält, der das Zertifikat bestellt hat
    "domain_validation_method": "dns-01", // Gibt die Domänenvalidierungsmethode an, derzeit ist nur die DNS-Überprüfung verfügbar
    "domain": "<ORDERED_DOMAIN>", // Bei der angeforderten Domäne wird für jede Domäne in der Reihenfolge (primäre und jede alternative Domäne) eine andere Abfrage gesendet.
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT-Datensatzname - wird in der Regel mit der Domäne verwendet.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT-Datensatzwert
    },
    "version": "<CHANNEL_VERSION>" // Benachrichtigungskanal-Version, die auftragsbezogene Benachrichtigungen unterstützt - 4 und höher
}
```
{: screen}

Sobald die DNS-TXT-Abfrage an Ihre Callback-URL gesendet wurde, müssen Sie die Abfrage innerhalb von 10 Minuten beantworten. {{site.data.keyword.cloudcerts_short}} prüft, ob die Abfrage abgeschlossen ist. Sobald {{site.data.keyword.cloudcerts_short}} verifiziert hat, ob Sie die Abfrage beantwortet haben, erhalten Sie eine zweite Benachrichtigung, um Sie zu informieren, dass Sie den TXT-Datensatz entfernen können.

Häufig gestellte Fragen zur Bestellung von Zertifikaten finden Sie auf [dieser Seite](/docs/services/certificate-manager?topic=certificate-manager-faq).
{: tip}

## Zertifikate bestellen
{: #ordering-certificate}

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu bestellen: 

1. Navigieren Sie zur Registerkarte "Verwalten" der {{site.data.keyword.cloudcerts_short}}.
2. Klicken Sie auf **Zertifikat bestellen** 
3. Wählen Sie den DNS-Provider aus - entweder {{site.data.keyword.cis_full_notm}} oder einen anderen DNS-Provider. 
4. Wenn Sie **{{site.data.keyword.cis_full_notm}}** ausgewählt haben, geben Sie die folgenden Details an: 
   1. Führen Sie erforderlichen Einrichtungsschritte aus. 
   2. Geben Sie einen Zertifikatsnamen und eine optionale Beschreibung an. 
   3. Wählen Sie eine Zertifizierungsstelle (CA) aus. 
   4. Wählen Sie die {{site.data.keyword.cis_full_notm}}-Instanz aus, für die Sie eine Servicezugriffsrolle zugewiesen haben. 
   5. Wählen Sie den gewünschten Zertifikatstyp aus. 
   6. Wählen Sie die Domäne aus. 
   7. Wählen Sie den entsprechenden Algorithmus und Schlüsselalgorithmus aus. 
   8. Klicken Sie auf **Bestellen**. 
5. Wenn Sie **Anderer DNS-Provider** ausgewählt haben, geben Sie die folgenden Details an:
   1. Führen Sie erforderlichen Einrichtungsschritte aus. 
   2. Geben Sie einen Zertifikatsnamen und eine optionale Beschreibung an. 
   3. Wählen Sie eine Zertifizierungsstelle (CA) aus.
   4. Geben Sie die primäre Domäne und alle alternativen Domänen ein.
   5. Wählen Sie den entsprechenden Algorithmus und Schlüsselalgorithmus aus. 
   6. Klicken Sie auf **Bestellen**. 

Ihre Bestellung wird in den Status **Anstehend** versetzt. Nachdem Sie die Abfrage für die Domänenvalidierung beantwortet haben und {{site.data.keyword.cloudcerts_short}} verifiziert hat, ob Sie der Eigner der angeforderten Domäne sind, wird für Sie das Zertifikat ausgestellt. Der Status des Zertifikats wird in **Gültig** geändert. Wenn Ihr Zertifikat bereit ist oder wenn ein Problem aufgetreten ist, werden Sie über Ihren Slack- und/oder Callback-URL-Benachrichtigungskanal informiert. 

## Zertifikate verlängern
{: #renew-certificate}

Wenn Ihr Zertifikat abläuft, können Sie das Zertifikat über {{site.data.keyword.cloudcerts_short}} verlängern. Wenn Ihr Zertifikat verlängert wird, wird die vorherige Version Ihres Zertifikats beibehalten, falls Sie sie noch benötigen. 

Verlängerungen funktionieren ähnlich wie die Zertifikatsbestellung. Wenn Sie die Verlängerung eines Zertifikats anfordern, sendet {{site.data.keyword.cloudcerts_short}} DNS-TXT-Abfragen an Ihre Callback-URL, so dass Sie erneut nachweisen können, dass Sie der Eigner der Domänen sind, für die Sie das Zertifikat verlängern.

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu verlängern:
  1. Klicken Sie auf das Menü in der Zeile des Zertifikats, das Sie verlängern möchten.
  2. Klicken Sie auf **Zertifikat verlängern**. 
  3. Optional: Sie können wählen, ob Sie für Ihr Zertifikat einen neuen Schlüssel erstellen möchten, indem Sie das Kontrollkästchen **Neuen Schlüssel für Zertifikat erstellen** aktivieren. Dadurch wird Ihr Zertifikat mit einem neuen Schlüsselpaar verlängert. Wenn Sie für Ihr Zertifikat einen neuen Schlüssel erstellen, stellen Sie sicher, dass die neuen Zertifikate und Schlüssel überall dort implementiert werden, wo sie verwendet werden.
  4. Klicken Sie auf **Verlängern**.


Sie können nur Zertifikate verlängern, die Sie über {{site.data.keyword.cloudcerts_short}} bestellt haben.
{: note}

Ihre Verlängerung wird in den Status **Verlängerung anstehend** versetzt. Sobald Sie die Abfrage für die Domänenvalidierung beantwortet haben und {{site.data.keyword.cloudcerts_short}} verifziert hat, dass Sie der Eigner der angeforderten Domäne sind, erhalten Sie ein verlängertes Zertifikat. Der Status des Zertifikats wird in **Gültig** geändert. Wenn Ihr verlängertes Zertifikat bereit ist oder wenn ein Problem aufgetreten ist, werden Sie über Ihren Slack- und/oder Callback-URL-Benachrichtigungskanal informiert. 
