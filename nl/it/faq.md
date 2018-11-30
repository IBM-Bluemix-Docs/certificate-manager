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

# Domande frequenti (FAQ, Frequently Asked Questions)
{: #faq}

Domande frequenti (FAQ, Frequently Asked Questions) su {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Che tipo di certificati posso memorizzare in {{site.data.keyword.cloudcerts_short}}?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} supporta solo certificati in formato PEM.

## Posso caricare chiavi private protette da password?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} non supporta l'importazione di certificati con chiavi private protette da password.

## Sto provando a caricare un certificato e una chiave privata e ottengo questo errore: `Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}
{: faq}

A seconda che la tua chiave privata sia crittografata o meno, scegli una delle seguenti opzioni:

* La chiave privata è crittografata. Assicurati di decrittografare la chiave privata prima di caricarla.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* La chiave privata non è crittografata. Assicurati che il certificato e la chiave privata corrispondano confrontando i risultati del seguente comando, dove `<certificate-file>` è il nome del tuo file del certificato e `<key-file>` è il nome del tuo file di chiave privata:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## Posso ricevere notifiche email per i certificati in scadenza?
{: #email-notifications}
{: faq}

Sono supportate solo le notifiche Callback e Slack.

## Posso controllare la versione dei miei certificati?
{: #certificate-versioning}
{: faq}

Puoi aggiornare un certificato reimportando una nuova versione del certificato che ha lo stesso dominio del certificato esistente ma che ha una nuova data di scadenza. Quando un certificato viene reimportato, la versione esistente del certificato viene conservata come un backup; vedi [Reimportazione di un certificato](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

## Posso rendere visibili degli specifici certificati solo a specifici utenti?
{: #access-policies}
{: faq}

I certificati possono essere protetti utilizzando le politiche di accesso IAM per ottenere un controllo degli accessi granulare; vedi [Gestione dei ruoli di accesso al servizio](access-management.html).
