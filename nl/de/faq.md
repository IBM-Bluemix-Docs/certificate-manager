---

copyright:
  years: 2018,
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
{:faq: data-hd-content-type='faq'}

# Häufig gestellte Fragen (FAQs)
{: #faq}

Häufig gestellte Fragen zu {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Welche Zertifikatstypen können in {{site.data.keyword.cloudcerts_short}} gespeichert werden?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} unterstützt ausschließlich Zertifikate im PEM-Format.

## Können kennwortgeschützte private Schlüssel hochgeladen werden?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} unterstützt das Importieren von Zertifikaten mit kennwortgeschützten privaten Schlüsseln nicht.

## Ich versuche, ein Zertifikat und einen privaten Schüssel hochzuladen, und der folgende Fehler wird angezeigt: `Fehler: Der private Schlüssel stimmt nicht mit dem Zertifikat überein, das importiert werden soll. Sicherstellen, dass eine Übereinstimmung besteht, und den Vorgang wiederholen.`
{: #import-cert-private-key}
{: faq}

Abhängig davon, ob der private Schlüssel verschlüsselt ist, eine der folgenden Optionen auswählen:

* Der private Schlüssel ist verschlüsselt. Stellen Sie sicher, dass der private Schlüssel vor dem Upload entschlüsselt wird.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* Der private Schlüssel ist nicht verschlüsselt. Stellen Sie sicher, dass das Zertifikat und der private Schlüssel übereinstimmen, indem Sie die Ergebnisse des folgenden Befehls vergleichen. Dabei gilt: `<certificate-file>` ist der Name der Zertifikatsdatei und `<key-file>` ist der Name der Datei mit dem privaten Schlüssel:

   ```
   openssl x509 -modulus -noout -in <Zertifikatsdatei>.pem | openssl md5; openssl rsa -modulus -noout -in <Schlüsseldatei>.key | openssl md5
   ```
   {: pre}

## Kann ich E-Mail-Benachrichtigungen zu ablaufenden Zertifikaten erhalten?
{: #email-notifications}
{: faq}

Nur Callback- und Slack-Benachrichtigungen werden unterstützt.

## Ist eine Versionssteuerung der Zertifikate möglich?
{: #certificate-versioning}
{: faq}

Sie können ein Zertifikat aktualisieren, indem Sie eine neue Version des Zertifikats mit derselben Domäne wie das vorhandene Zertifikat, jedoch einem neuen Ablaufdatum, importieren. Beim erneuten Importieren eines Zertifikats wird die vorhandene Version des Zertifikats als Sicherungskopie beibehalten. Weitere Informationen finden Sie in [Zertifikat erneut importieren](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

## Kann ich dafür sorgen, dass bestimmte Zertifikate nur für bestimmte Benutzer sichtbar sind?
{: #access-policies}
{: faq}

Zertifikate können durch IAM-Zugriffsrichtlinien geschützt werden, um eine differenzierte Zugriffssteuerung zu ermöglichen. Informationen hierzu finden Sie in [Servicezugriffsrollen verwalten](access-management.html).
