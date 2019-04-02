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

# Foire aux questions
{: #faq}

Foire aux questions concernant {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Quel format dois-je utiliser pour mes certificats ?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} ne prend en charge que des certificats au format PEM.

## Quels sont les types d'algorithme de clé publique pris en charge ?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} prend en charge des certificats avec des clés publiques générées à l'aide des algorithmes de clé publique suivants :

* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Protocole d'accord de clé Elliptic Curve with Diffie-Hellman


## Puis-je télécharger des clés privées protégées par mot de passe ?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} ne prend pas en charge l'importation de certificats avec des clés privées protégées par mot de passe.

## J'essaie de télécharger un certificat et une clé privée et j'obtiens le message d'erreur suivant : `Erreur: La clé privée ne correspond pas au certificat que vous essayez d'importer. Assurez-vous qu'ils correspondent et réessayez.`
{: #import-cert-private-key}
{: faq}

Selon que votre clé privée est chiffrée ou non, choisissez l'une des options suivantes :

* La clé privée est chiffrée. Prenez soin de déchiffrer la clé privée avant de la télécharger.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* La clé privée n'est pas chiffrée. Assurez-vous que le certificat et la clé chiffrée correspondent en comparant les résultats de la commande suivante, où `<certificate-file>` est le nom de votre fichier certificat et `<key-file>` est le nom de votre fichier de clé privée :

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## Puis-je recevoir des notifications par courrier électronique concernant des certificats qui arrivent à expiration ?
{: #email-notifications}
{: faq}

Seules les notifications Callback et Slack sont prises en charge.

## Puis-je contrôler les versions de mes certificats ?
{: #certificate-versioning}
{: faq}

Vous pouvez mettre à jour un certificat en réimportant une nouvelle version avec le même domaine que le certificat existant, mais avec une nouvelle date d'expiration. Lorsqu'un certificat est réimporté, la version existante de celui-ci est conservée en tant que sauvegarde. Voir [Réimportation d'un certificat](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

## Puis-je faire en sorte que certains certificats ne soient visibles que pour certains utilisateurs ?
{: #access-policies}
{: faq}

Les certificats peuvent être protégés à l'aide de politiques d'accès IAM pour obtenir un contrôle d'accès granulaire. Voir [Gestion des rôles d'accès aux services](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).
