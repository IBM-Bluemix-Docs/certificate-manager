---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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
{:faq: data-hd-content-type='faq'}

# Häufig gestellte Fragen (FAQs)
{: #faq}

Häufig gestellte Fragen zu {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Welches Format müssen die Zertifikate aufweisen?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} unterstützt ausschließlich Zertifikate im PEM-Format.

## Welcher Typ von Algorithmus mit öffentlichem Schlüssel wird unterstützt?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} unterstützt Zertifikate mit öffentlichen Schlüsseln, die mithilfe der folgenden Algorithmen mit öffentlichem Schlüssel generiert werden:

* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA), Algorithmus für digitale Signaturen
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman Key Agreement Protocol (ECDH)


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

* Der private Schlüssel ist nicht verschlüsselt. Stellen Sie sicher, dass das Zertifikat und der private Schlüssel übereinstimmen, indem Sie die Ergebnisse des folgenden Befehls vergleichen. Dabei gilt: `<certificate-file>` ist der Name Ihrer Zertifikatsdatei und `<key-file>` ist der Name Ihrer Datei mit privatem Schlüssel:

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

Sie können ein Zertifikat aktualisieren, indem Sie eine neue Version des Zertifikats mit derselben Domäne wie das vorhandene Zertifikat, jedoch einem neuen Ablaufdatum, importieren. Beim erneuten Importieren eines Zertifikats wird die vorhandene Version des Zertifikats als Sicherungskopie beibehalten. Weitere Informationen finden Sie in [Zertifikat erneut importieren](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).



## Kann ich dafür sorgen, dass bestimmte Zertifikate nur für bestimmte Benutzer sichtbar sind?
{: #access-policies}
{: faq}

Zertifikate können durch IAM-Zugriffsrichtlinien geschützt werden, um eine differenzierte Zugriffssteuerung zu ermöglichen. Informationen hierzu finden Sie in [Servicezugriffsrollen verwalten](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).



## Wie widerrufe ich ein ausgestelltes Zertifikat?
{: #revoke-certificate}
{: faq}

{{site.data.keyword.cloudcerts_short}} verfügt derzeit über keine Widerrufs-API, die Sie verwenden können. Sie können jedoch die "Let's Encrypt"-API verwenden, um Zertifikate mithilfe des privaten Zertifikatsschlüssels zu widerrufen. Informationen darüber, wie "Let's Encrypt"-Zertifikate widerrufen werden, finden Sie in der ["Let's Encrypt"-Dokumentation](https://letsencrypt.org/docs/revoking/).



## Der Status meiner Zertifikatsbestellung befindet sich sehr lange im Status 'Anstehend'.
{: #certificate-order-status}
{: faq}

Bei langsamen DNS-Netzen kann eine Bestellung bis zu 20 Minuten dauern, bis sie erfolgreich abgeschlossen werden kann.

## Wie lange dauert der Zeitraum, in dem der Service überprüft, ob ich die Domänen besitze, die ich in meiner Bestellung angefordert habe?
{: #certificate-order-validation}
{: faq}

Nach dem Senden der Anforderung zur Domänenüberprüfung versucht {{site.data.keyword.cloudcerts_short}} in 10 Minuten zu prüfen, ob Ihnen die Domänen gehören, die Sie angefordert haben. Wenn Ihr DNS nicht innerhalb von 10 Minuten mit der TXT-Datensatzanforderung aktualisiert wird, schlägt Ihre Bestellung fehl.

## Wie überprüfe ich den Status meiner Zertifikatsbestellung mit der öffentlichen {{site.data.keyword.cloudcerts_short}}-API?
{: #certificate-order-status-api}
{: faq}

Verwenden Sie die API `Get certificate metadata`, um den Bestellstatus des Zertifikats abzufragen.

## Kann ich benachrichtigt werden, sobald meine Bestellung abgeschlossen ist?
{: #certificate-order-notification}
{: faq}

Wenn Sie einen Benachrichtigungskanal konfiguriert haben, werden Sie benachrichtigt, sobald Ihr Zertifikat ausgestellt wurde oder falls Ihre Bestellung fehlgeschlagen ist. Beachten Sie, dass die Version Ihres Benachrichtigungskanals die Version 4 oder höher sein muss.

## Meine Bestellung ist fehlgeschlagen. Warum?
{: #certificate-order-failure}
{: faq}

Sie finden einen Fehlercode und eine Nachricht in den Zertifikatsmetadaten, in der Benutzerschnittstelle und in der Benachrichtigung, die Sie erhalten, falls Ihre Bestellung fehlgeschlagen ist.

## Warum erhalte ich in meinem vorhandenen Slack-Benachrichtigungskanal keine Zertifikatsbestellungsereignisse?
{: #missing-notification-for-ordered-certificate}
{: faq}

Führen Sie auf der Registerkarte für die Certificate Manager-Einstellungen ein Upgrade Ihres Slack-Benachrichtigungskanals auf die neueste Version durch.
