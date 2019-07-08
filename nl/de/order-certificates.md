---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# Zertifikate bestellen
{: #ordering-certificates}

Sie können {{site.data.keyword.cloudcerts_long}} zum Bestellen von öffentlichen SSL/TLS-Zertifikaten für Ihre Apps und Services verwenden, die von unterstützten externen Zertifizierungsstellen signiert werden. {{site.data.keyword.cloudcerts_short}} erleichtert Ihnen die Bestellung von öffentlichen Zertifikaten und bietet Ihnen zusätzliche Sicherheit für Ihre privaten SSL/TLS-Schlüssel. Nachdem Ihr Zertifikat ausgestellt wurde, können Sie es in integrierten Services bereitstellen oder herunterladen, um es an anderer Stelle zu verwenden.  
{: shortdesc}

Wenn Sie ein Zertifikat bestellen, wird Ihr privater Schlüssel für SSL/TLS direkt in {{site.data.keyword.cloudcerts_short}} generiert und sicher gespeichert. Alle Anforderungen und der Zugriff auf ausgestellte Zertifikate können über die [Zugriffssteuerung](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) verwaltet und automatisch mithilfe von [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events) geprüft werden.   

{{site.data.keyword.cloudcerts_short}} implementiert das ACME-v2-Protokoll (Automatic Certificate Management Environment) als ACME-Client. Das ACME-Protokoll ermöglicht es, vertrauenswürdige Browser-Zertifikate ohne menschliches Eingreifen automatisch zu erhalten.

## Zertifikatmerkmale
Zertifikate, die über {{site.data.keyword.cloudcerts_short}} bestellt werden, haben die folgenden Merkmale:

- Kostenlos
- Gültigkeitsdauer - 90 Tage
- Single-Domain-, Multi-Domain (SAN)- oder Wildcard-Zertifikat
- Domäne validiert - Bevor für Sie ein Zertifikat ausgestellt wird, prüft die Zertifizierungsinstanz, ob Sie der Eigner der Domäne sind, für die Sie ein Zertifikat anfordern.

Wenn Sie Extended Validation (EV)- oder Organization Validated (OV)-Zertifikate benötigen, können Sie diese an anderer Stelle beziehen und in {{site.data.keyword.cloudcerts_short}} importieren, um ihren Lebenszyklus zu verwalten.

## Unterstützte Zertifizierungsstellen
{: #supported-certificate-authorities}

Eine Zertifizierungsstelle (Certificate Authority, CA) ist eine Entität, die digitale Zertifikate ausstellt. Die CA agiert als vertrauenswürdige dritte Partei sowohl für den Anforderer des Zertifikats als auch für den Client, der auf das Zertifikat angewiesen ist.
{: shortdesc}

### Let's Encrypt
["Let's Encrypt"](https://letsencrypt.org) ist eine kostenlose, automatisierte, ACME-basierte Zertifizierungsstelle, die über 90 Tage gültige validierte Zertifikate zur Verfügung stellt. Es handelt sich um einen Dienst, der von der Internet Security Research Group (ISRG) bereitgestellt wird.

## Zertifikatsbestellung einrichten
{: #setup}

Bevor für Sie ein Zertifikat ausgestellt werden kann, muss {{site.data.keyword.cloudcerts_short}} sicherstellen, dass Sie die Kontrolle über alle Domänen haben, die Sie in Ihrer Anforderung aufgelistet haben. {{site.data.keyword.cloudcerts_short}} verwendet eine DNS-Validierung, um Ihre Kontrolle zu überprüfen.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} sendet eine Anforderung in Form eines DNS-TXT-Datensatzes (DNS = Domain Name System), den Sie in Ihrem DNS-Service hinzufügen können. Für jede Domäne, die Sie in Ihrem Zertifikat anfordern, erhalten Sie einen separaten DNS-TXT-Datensatz. Nachdem Sie den DNS-TXT-Datensatz hinzugefügt haben, überprüfen {{site.data.keyword.cloudcerts_short}} und "Let's Encrypt", ob er in Ihrem DNS-Service enthalten ist. Wenn Sie die Anforderung erfolgreich abgeschlossen haben, wird für Sie ein "Let's Encrypt"-Zertifikat ausgegeben, das in Ihrer {{site.data.keyword.cloudcerts_short}}-Instanz verfügbar ist.

{{site.data.keyword.cloudcerts_short}} sendet den TXT-Datensatz an eine Callback-URL, die Sie in den Benachrichtigungseinstellungen angeben. Auf diese Weise können Sie den Prozess der Domänenvalidierung einfach automatisieren. 

Um das Bestellen von Zertifikaten zu starten, registrieren Sie Ihre Callback-URL als Benachrichtigungskanal in {{site.data.keyword.cloudcerts_short}}. Aktualisieren Sie anschließend Ihren Code, um die Benachrichtigungsereignisse zu bearbeiten, die die TXT-Anforderung enthalten. [Informationen zum Einrichten eines Callback-URL-Benachrichtigungskanals](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Auf eine Anforderung reagieren
{: #responding-to-challenge}

Der Benachrichtigungskanal empfängt eine Benachrichtigung mit der folgenden Struktur:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // Das erste Ereignis ist das Hinzufügen des erforderlichen TXT-Challenge-Datensatzes und das zweite das Löschen desselben TXT-Datensatzes, sobald die Abfrage beendet ist.
    "certificateCRN": "<CERTIFICATE_CRN>", // Das bestellte CRN-Zertifikat
    "userToken": "<USER_TOKEN>", /// Das IAM-Token, das die Identität des Benutzers enthält, der das Zertifikat bestellt hat
    "domain_validation_method": "dns-01", // Gibt die Domänenvalidierungsmethode an, derzeit ist nur die DNS-Überprüfung verfügbar
    "domain": "<ORDERED_DOMAIN>", // Bei der angeforderten Domäne wird für jede Domäne in der Reihenfolge (primäre und jede alternative Domäne) eine andere Anforderung gesendet.
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT-Datensatzname - wird in der Regel mit der Domäne verwendet.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT-Datensatzwert
    },
    "version": "<CHANNEL_VERSION>" // Benachrichtigungskanal-Version, die auftragsbezogene Benachrichtigungen unterstützt - 4 und höher
}
```
{: screen}

Sobald die DNS-TXT-Anforderung an Ihre Callback-URL gesendet wurde, müssen Sie die Anforderung innerhalb von 10 Minuten beantworten. {{site.data.keyword.cloudcerts_short}} prüft, ob die Anforderung abgeschlossen ist. Sobald {{site.data.keyword.cloudcerts_short}} überprüft, ob Sie die Anforderung beantwortet haben, erhalten Sie eine zweite Benachrichtigung, um Sie wissen zu lassen, dass Sie den TXT-Datensatz entfernen können.

[Überprüfen Sie die FAQ-Seite](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) für häufig gestellte Fragen zum Bestellen von Zertifikaten.
{: tip}

## Zertifikate bestellen
{: #ordering-certificate}

1. Navigieren Sie zur Registerkarte "Verwalten" der {{site.data.keyword.cloudcerts_short}}.
2. Klicken Sie auf **Order Certificate** (Zertifikat bestellen) und geben Sie die folgenden Details an:

    1. Geben Sie einen Zertifikatsnamen an.
    2. Wählen Sie eine Zertifizierungsstelle aus.
    3. Geben Sie die primäre Domäne und alle alternativen Domänen ein.
    4. Wählen Sie den entsprechenden Algorithmus und den Schlüsselalgorithmus aus.
    5. Klicken Sie auf **Bestellen**.

Ihre Bestellung wird in den Status **Anstehend** versetzt. Sobald Sie die Anforderung für die Domänenvalidierung beantwortet haben und {{site.data.keyword.cloudcerts_short}} prüft, ob Sie der Eigner der angeforderten Domäne sind, wird für Sie das Zertifikat ausgestellt. Der Status des Zertifikats wird in **Gültig** geändert. Sie werden benachrichtigt, wenn Ihr Zertifikat fertig ist oder wenn ein Problem in Ihrem Slack- und/oder Callback-URL-Kanal aufgetreten ist.

## Zertifikate verlängern
{: #renew-certificate}

Wenn Ihr Zertifikat abläuft, können Sie das Zertifikat über {{site.data.keyword.cloudcerts_short}} verlängern. Wenn Ihr Zertifikat verlängert wird, wird die vorherige Version Ihres Zertifikats beibehalten, falls Sie sie noch benötigen. 

Verlängerungen funktionieren ähnlich wie die Zertifikatsbestellung. Wenn Sie die Verlängerung eines Zertifikats anfordern, sendet {{site.data.keyword.cloudcerts_short}} DNS-TXT-Anforderungen an Ihre Callback-URL, so dass Sie erneut nachweisen können, dass Sie der Eigner der Domänen sind, für die Sie das Zertifikat verlängern.

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu verlängern:
  1. Klicken Sie auf das Menü in der Zeile des Zertifikats, das Sie verlängern möchten.
  2. Klicken Sie auf **Renew Certificate** (Zertifikat verlängern).
  3. Optional: Sie können wählen, ob Sie für Ihr Zertifikat einen neuen Schlüssel erstellen möchten, indem Sie das Kontrollkästchen **Neuen Schlüssel für Zertifikat erstellen** aktivieren. Dadurch wird Ihr Zertifikat mit einem neuen Schlüsselpaar verlängert.
  
  Wenn Sie für Ihr Zertifikat einen neuen Schlüssel erstellen, stellen Sie sicher, dass die neuen Zertifikate und Schlüssel überall dort implementiert werden, wo sie verwendet werden.
  {: note}
    
  4. Klicken Sie auf **Renew** (Verlängern).
  
  Sie können nur Zertifikate verlängern, die Sie über {{site.data.keyword.cloudcerts_short}} bestellt haben. {: note}

Ihre Verlängerung wird in den Status **Anstehend** versetzt. Sobald Sie die Anforderung für die Domänenvalidierung beantwortet haben und {{site.data.keyword.cloudcerts_short}} prüft, ob Sie der Eigner der angeforderten Domäne sind, erhalten Sie ein verlängertes Zertifikat. Der Status des Zertifikats wird in **Gültig** geändert. Sie werden benachrichtigt, wenn Ihr verlängertes Zertifikat fertig ist oder wenn ein Problem in Ihrem Slack- und/oder Callback-URL-Kanal aufgetreten ist.
