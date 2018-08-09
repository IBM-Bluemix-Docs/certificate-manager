---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Zertifikate über das Dashboard verwalten
{: #managing-certificates-from-the-dashboard}

Sie können das Dashboard des {{site.data.keyword.cloudcerts_full}}-Service verwenden, um Zertifikate zu verwalten, die Sie von unabhängigen Ausstellern erhalten, um Ihre {{site.data.keyword.IBM_notm}} Cloud-basierten Apps oder Services verwenden zu können. Wenn Sie die Zertifikate und Schlüssel importiert haben, werden sie von dem Service verschlüsselt und gespeichert.
{: shortdesc}

## Zertifikat importieren
{: #importing-a-certificate}

Sie können die Zertifikate hochladen, um sie verwalten zu können.
{: shortdesc}

Führen Sie zunächst folgende Schritte aus:

* Erstellen Sie ein gültiges, nicht abgelaufenes Zertifikat mit einem passenden privaten Schlüssel.
* Konvertieren Sie die Dateien in das PEM-Format (PEM = Privacy-enhanced Electronic Mail).
* Lassen Sie den privaten Schlüssel unverschlüsselt, um sicherzustellen, dass er importiert werden kann.

Um ein Zertifikat zu importieren, klicken Sie auf **Zertifikat importieren** und machen Sie folgende Angaben:

1. Optional: Geben Sie einen Anzeigename ein.
2. Klicken Sie auf **Durchsuchen** und wählen Sie die Zertifikatsdatei im PEM-Format aus.
3. Klicken Sie auf **Durchsuchen** und wählen Sie den privaten Schlüssel des Zertifikats im PEM-Format aus.
4. Falls zutreffend: Geben Sie die Zwischenzertifikatsdatei im PEM-Format an.
5. Optional: Geben Sie eine Beschreibung ein.
6. Klicken Sie auf **Importieren**.  

**Hinweis**: Um ein importiertes Zertifikat zu verlängern, fordern Sie ein neues Zertifikat bei Ihrer Zertifizierungsstelle (Certificate Authority, CA) an und importieren Sie das neue Zertifikat in {{site.data.keyword.cloudcerts_short}}. Wenn das neue Zertifikat bereitgestellt wurde, können Sie das alte löschen.

Wenn Sie ein Zertifikat importiert haben, werden die folgenden Informationen in der Tabelle 'Zertifikate' angezeigt. Wenn Sie weitere Zertifikatsinformationen anzeigen wollen, können Sie das Zertifikat in der Tabellenzeile auswählen.

<table>
<caption> Tabelle 1. Informationen über das importierte Zertifikat </caption>
  <tr>
    <th> Komponente </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td>Name</td>
    <td>Optional: Aussagekräftiger Anzeigename. Maximal zulässige Länge: 256 Zeichen. </td>
  </tr>
  <tr>
    <td>Beschreibung</td>
    <td>Optional: Beschreibender Text für das Zertifikat. Maximal zulässige Länge: 1024 Zeichen.</td>
  </tr>
  <tr>
    <td>Domäne</td>
    <td>Die Domäne(n), für die das Zertifikat gültig ist. </td>
  </tr>
  <tr>
    <td>Aussteller</td>
    <td>Die Zertifizierungsstelle, die das Zertifikat ausgestellt hat.</td>
  </tr>
  <tr>
    <td>Algorithmus</td>
    <td>Der Verschlüsselungstyp, mit dem das Zertifikat erstellt wird. </td>
  </tr>
  <tr>
    <td>Schlüsselalgorithmus</td>
    <td>Der Typ und die Größe des Schlüssels, der von dem Algorithmus verwendet wird. </td>
  </tr>
  <tr>
    <td>Ablauf nach </td>
    <td>Die Anzahl der verbleibenden Tage, bevor das Zertifikat seine Gültigkeit verliert. </td>
  </tr>
  <tr>
    <td>Ausgestellt am</td>
    <td>Das Datum, an dem das Zertifikat ausgestellt wurde. </td>
  </tr>
  <tr>
    <td>Gültig ab</td>
    <td>Das Datum, an dem das Zertifikat gültig wurde. </td>
  </tr>
  <tr>
    <td>Läuft ab am</td>
    <td>Das Datum, ab dem das Zertifikat nicht mehr gültig ist. </td>
  </tr>
  <tr>
    <td>Zertifikat-ID</td>
    <td>Die generierte ID, die dem Zertifikat beim Import zugeordnet wird. </td>
  </tr>
</table>

## Zertifikate suchen
{: #searching-certificates}
 
Wenn Sie viele Zertifikate verwalten, können Sie die Suchleiste verwenden, um das erforderliche Zertifikat zu finden.
{: shortdesc}
 
-   Um nach dem Zertifikatsnamen, der Zertifikatsdomäne oder dem Zertifikatsaussteller zu suchen, geben Sie Ihren Suchbegriff in der Suchleiste ein und drücken Sie die Eingabetaste.
-   Um alle Ihre Zertifikate anzuzeigen, klicken Sie auf das Symbol **X** in der Suchleiste.

## Zertifikate herunterladen
{: #downloading-certificates}

Wenn Sie bereit sind, Ihr Zertifikat für Ihre App oder Ihren Service bereitzustellen, können Sie das Zertifikat und den zugehörigen privaten Schlüssel herunterladen.
{: shortdesc}

Gehen Sie wie folgt vor, um ein Zertifikat herunterzuladen:

1. Wählen Sie das Kontrollkästchen für das Zertifikat aus, das Sie herunterladen wollen.
2. Klicken Sie auf **Zertifikat herunterladen**. Abhängig davon, was Sie in den Service importiert haben, erhalten Sie eine komprimierte Datei, die PEM-Dateien für das Zertifikat enthält, einen zugehörigen privaten Schlüssel und ein zugehöriges Zwischenzertifikat.


## Zertifikate löschen
{: #deleting-certificates}

Wenn Sie ein Zertifikat nicht mehr überwachen wollen, können Sie es löschen.
{: shortdesc}  

Gehen Sie wie folgt vor, um ein Zertifikat zu löschen:

1. Wählen Sie das Kontrollkästchen für das Zertifikat aus, das Sie löschen wollen.
2. Klicken Sie auf das Symbol **Papierkorb**.

## Zertifikatsmetadaten aktualisieren
{: #updating-certificates-metadata}

Sie haben außerdem die Möglichkeit, den Namen und die Beschreibung eines Zertifikats zu aktualisieren.
{: shortdesc}

Gehen Sie wie folgt vor, um ein Zertifikat zu aktualisieren:

1. Wählen Sie eine Zeile aus, um die Details für dieses Zertifikat zu öffnen.
2. Aktualisieren Sie den Namen oder die Beschreibung.
3. Speichern Sie Ihre Änderungen.

**Hinweis**: Sie können bis zu fünf Aktualisierungsaktionen pro Minute ausführen.
