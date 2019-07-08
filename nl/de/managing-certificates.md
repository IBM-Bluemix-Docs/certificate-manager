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

# Zertifikate über das Dashboard verwalten
{: #managing-certificates-from-the-dashboard}

Sie können das Dashboard des {{site.data.keyword.cloudcerts_full}}-Service verwenden, um Zertifikate zu verwalten, die Sie von unabhängigen Ausstellern erhalten, um Ihre {{site.data.keyword.IBM_notm}} Cloud-basierten Apps oder Services verwenden zu können.
{: shortdesc}

## Unterstützte Zertifikatsformate und Algorithmen mit öffentlichem Schlüssel
{: supported-formats-and-algorithms}

### Zertifikatsformate
* PEM

### Algorithmen mit öffentlichem Schlüssel
* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA), Algorithmus für digitale Signaturen
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman Key Agreement Protocol (ECDH)

## Zertifikat importieren
{: #importing-a-certificate}

Importieren Sie die Zertifikate, damit Sie diese verwalten können.
{: shortdesc}

**Vorbereitungen**

* Erstellen Sie ein gültiges, nicht abgelaufenes Zertifikat mit einem passenden privaten Schlüssel (Schlüssel ist optional).
* Konvertieren Sie die Dateien in das PEM-Format (PEM = Privacy-enhanced Electronic Mail).
* Lassen Sie den privaten Schlüssel unverschlüsselt, um sicherzustellen, dass er importiert werden kann.

Um ein Zertifikat zu importieren, klicken Sie auf **Zertifikat importieren** und machen Sie folgende Angaben:

1. Geben Sie einen Zertifikatsnamen an.
2. Wählen Sie die Zertifikatsdatei im PEM-Format aus, indem Sie auf **Durchsuchen** klicken.
3. Optional: Wählen Sie den privaten Schlüssel des Zertifikats im PEM-Format aus, indem Sie auf **Durchsuchen** klicken.
4. Falls zutreffend: Geben Sie die Zwischenzertifikatsdatei im PEM-Format an.
5. Optional: Geben Sie eine Beschreibung ein.
6. Klicken Sie auf **Importieren**.

Wenn Sie ein Zertifikat importiert haben, werden die folgenden Informationen in der Tabelle 'Zertifikate' angezeigt. Weitere Informationen zum Zertifikat können Sie aufrufen, indem Sie die Zeile des betreffenden Zertifikats in der Zertifikatstabelle erweitern.

<table>
<caption> Tabelle 1. Informationen über das importierte Zertifikat </caption>
  <tr>
    <th> Komponente </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Ein aussagekräftiger Anzeigename. Maximal zulässige Länge: 256 Zeichen. </td>
  </tr>
  <tr>
    <td>Beschreibung</td>
    <td>(Optional) Beschreibender Text für das Zertifikat. Maximal zulässige Länge: 1024 Zeichen.</td>
  </tr>
  <tr>
    <td>Domäne</td>
    <td>Die Domäne(n), für die das Zertifikat gültig ist/sind. </td>
  </tr>
  <tr>
    <td>Aussteller</td>
    <td>Die Zertifizierungsstelle (CA), die das Zertifikat ausgestellt hat.</td>
  </tr>
  <tr>
    <td>Algorithmus</td>
    <td>Der Zertifikatssignaturalgorithmus.</td>
  </tr>
  <tr>
    <td>Schlüsselalgorithmus</td>
    <td>Der Algorithmus mit öffentlichem Schlüssel.</td>
  </tr>
  <tr>
    <td>Ablauf nach</td>
    <td>Die Anzahl der verbleibenden Tage, bevor das Zertifikat seine Gültigkeit verliert. </td>
  </tr>
  <tr>
    <td>Gültig ab</td>
    <td>Das Datum, an dem das Zertifikat gültig wurde (in UTC-Zeit). </td>
  </tr>
  <tr>
    <td>Läuft ab am</td>
    <td>Das Datum, ab dem das Zertifikat nicht mehr gültig ist (in UTC-Zeit). </td>
  </tr>
  <tr>
    <td>Status</td>
    <td>Der Status Ihres Zertifikats. </td>
  </tr>
  <tr>
    <td>Zertifikat-ID</td>
    <td>Die generierte ID, die dem Zertifikat beim Import zugeordnet wird.</td>
  </tr>
</table>

</br>

## Zertifikat erneut importieren
{: #reimport-certificate}

Wenn das Zertifikat demnächst abläuft, können Sie es aktualisieren, indem Sie eine neue Version des Zertifikats mit derselben Domäne wie das vorhandene Zertifikat, jedoch einem neuen Ablaufdatum, importieren. Beim erneuten Importieren eines Zertifikats wird die vorhandene Version des Zertifikats als Sicherungskopie beibehalten, die bei Bedarf heruntergeladen werden kann.
{: shortdesc}

### Zertifikat erneut importieren
{: #reimporting-certificate}

Führen Sie die folgenden Schritte aus, um ein Zertifikat erneut zu importieren:

1. Erweitern Sie die Zeile für das Zertifikat.
2. Klicken Sie auf **Zertifikat erneut importieren**.
3. Wählen Sie die neue Zertifikatsdatei im PEM-Format aus, indem Sie auf **Durchsuchen** klicken.
4. (Optional) Wählen Sie den privaten Schlüssel des neuen Zertifikats im PEM-Format aus, indem Sie auf **Durchsuchen** klicken.
5. (Optional) Geben Sie eine neue Zwischenzertifikatsdatei im PEM-Format an, indem Sie auf **Durchsuchen** klicken.
6. Klicken Sie auf **Erneut importieren** und dann auf **Fertig**.

Das erneute Importieren von Zertifikaten ist auf fünf Aktionen pro Minute begrenzt.
{: note}

### Vorhergehende Version des Zertifikats herunterladen
{: #downloading-certificate}

Führen Sie die folgenden Schritte aus, um die vorhergehende Version eines Zertifikats herunterzuladen:

1. Erweitern Sie die Zeile für das Zertifikat.
2. Klicken Sie auf den Link **Vorherige Version**.

## Zertifikate bestellen
{: #order-certificates}

Bevor Sie ein Zertifikat bestellen, [müssen Sie zuerst die erforderliche Konfiguration durchführen](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates).

1. Geben Sie einen Zertifikatsnamen an.
2. Wählen Sie eine Zertifizierungsstelle aus.
3. Geben Sie die primäre Domäne und alle alternativen Domänen ein.
4. Wählen Sie den entsprechenden Algorithmus und den Schlüsselalgorithmus aus.
5. Klicken Sie auf **Bestellen**.

Das Bestellen von Zertifikaten ist auf fünf Bestellungen/Minute pro {{site.data.keyword.cloudcerts_short}}-Instanz, 100 Bestellungen/Stunde pro IBM Benutzerkonto und fünf Zertifikate für dieselben Domänen pro Woche beschränkt.
{: note}

## Zertifikate verlängern
{: #renew-certificates}

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu verlängern:
  1. Klicken Sie auf das Menü in der Zeile des Zertifikats, das Sie verlängern möchten.
  2. Klicken Sie auf **Renew Certificate** (Zertifikat verlängern).
  3. Optional: Sie können wählen, ob Sie für Ihr Zertifikat einen neuen Schlüssel erstellen möchten, indem Sie das Kontrollkästchen **Neuen Schlüssel für Zertifikat erstellen** aktivieren. Dadurch wird Ihr Zertifikat mit einem neuen Schlüsselpaar verlängert.
  
  Wenn Sie für Ihr Zertifikat einen neuen Schlüssel erstellen, stellen Sie sicher, dass die neuen Zertifikate und Schlüssel überall dort implementiert werden, wo sie verwendet werden.
  {: note}
    
  4. Klicken Sie auf **Renew** (Verlängern).
  
  Sie können nur Zertifikate verlängern, die Sie über {{site.data.keyword.cloudcerts_short}} bestellt haben.
  {: note}

Die Verlängerung von Zertifikaten ist auf fünf Verlängerungsanforderungen pro Zertifikat pro Minute und 100 Verlängerungen/Stunde pro IBM Benutzerkonto beschränkt.
{: note}


## Zertifikate suchen
{: #searching-certificates}

Wenn Sie viele Zertifikate verwalten, können Sie die Suchleiste verwenden, um das erforderliche Zertifikat zu finden.
{: shortdesc}

* Um nach dem Zertifikatsnamen, der Zertifikatsdomäne oder dem Zertifikatsaussteller zu suchen, geben Sie Ihren Suchbegriff in der Suchleiste ein und drücken Sie die Eingabetaste.
* Um alle Ihre Zertifikate anzuzeigen, klicken Sie auf das Symbol **X** in der Suchleiste.

## Zertifikate herunterladen
{: #downloading-certificates}

Wenn Sie bereit sind, Ihr Zertifikat für Ihre App oder Ihren Service bereitzustellen, können Sie das Zertifikat und den zugehörigen privaten Schlüssel herunterladen.
{: shortdesc}

Führen Sie die folgenden Schritte aus, um ein Zertifikat herunterzuladen:

1. Wählen Sie das Kontrollkästchen für das Zertifikat aus, das Sie herunterladen wollen.
2. Klicken Sie auf **Zertifikat herunterladen**. Abhängig davon, was Sie in den Service importiert haben, erhalten Sie eine komprimierte Datei, die PEM-Dateien für das Zertifikat enthält, einen zugehörigen privaten Schlüssel und ein zugehöriges Zwischenzertifikat.

Abgelaufene Zertifikate können nicht heruntergeladen werden.
{: note}

## Zertifikate löschen
{: #deleting-certificates}

Wenn Sie ein Zertifikat nicht mehr überwachen wollen, können Sie es löschen.
{: shortdesc}  

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu löschen:

1. Wählen Sie das Kontrollkästchen für das Zertifikat aus, das Sie löschen wollen.
2. Klicken Sie auf das Symbol **Papierkorb**.

## Zertifikatsmetadaten aktualisieren
{: #updating-certificates-metadata}

Sie haben außerdem die Möglichkeit, den Namen und die Beschreibung eines Zertifikats zu aktualisieren.
{: shortdesc}

Führen Sie die folgenden Schritte aus, um ein Zertifikat zu aktualisieren:

1. Wählen Sie eine Zeile aus, um die Details für dieses Zertifikat zu öffnen.
2. Aktualisieren Sie den Namen oder die Beschreibung.
3. Speichern Sie Ihre Änderungen.

Sie können bis zu fünf Aktualisierungsaktionen pro Minute ausführen.
{: note}
