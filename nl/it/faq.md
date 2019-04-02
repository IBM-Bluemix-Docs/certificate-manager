---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-12"

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

# Domande frequenti (FAQ, Frequently Asked Questions)
{: #faq}

Domande frequenti (FAQ, Frequently Asked Questions) su {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Quale formato devono avere i miei certificati?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} supporta solo certificati in formato PEM.

## Quale tipo di algoritmi chiave pubblica sono supportati?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} supporta i certificati con chiavi pubbliche generate utilizzando i seguenti algoritmi chiave pubblica: 

* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Elliptic Curve with Diffie-Hellman key agreement protocol (ECDH)


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

Puoi aggiornare un certificato reimportando una nuova versione del certificato che ha lo stesso dominio del certificato esistente ma che ha una nuova data di scadenza. Quando un certificato viene reimportato, la versione esistente del certificato viene conservata come un backup; vedi [Reimportazione di un certificato](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

## Posso rendere visibili degli specifici certificati solo a specifici utenti?
{: #access-policies}
{: faq}

I certificati possono essere protetti utilizzando le politiche di accesso IAM per ottenere un controllo degli accessi granulare; vedi [Gestione dei ruoli di accesso al servizio](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).
