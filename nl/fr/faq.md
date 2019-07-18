---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL,

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

* La clé privée n'est pas chiffrée. Assurez-vous que le certificat et la clé privée correspondent en comparant les résultats de la commande suivante, où `<certificate-file>` est le nom de votre fichier certificat et `<key-file>` est le nom de votre fichier de clé privée :

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



## Comment révoquer un certificat émis ?
{: #revoke-certificate}
{: faq}

{{site.data.keyword.cloudcerts_short}} ne dispose actuellement d'aucune API de révocation que vous pourriez utiliser. Toutefois, vous pouvez utiliser l'API Let's Encrypt pour révoquer des certificats en utilisant la clé privée du certificat. Pour apprendre comment révoquer des certificats Let's Encrypt, voir la [documentation Let's Encrypt](https://letsencrypt.org/docs/revoking/).



## Le statut de ma commande de certificat est à l'état en attente depuis un long moment
{: #certificate-order-status}
{: faq}

Sur les réseaux DNS lents, une commande peut prendre jusqu'à environ 20 minutes pour aboutir.

## Combien de temps le service prend-il pour valider que vous possédez les domaines demandés dans ma commande ?
{: #certificate-order-validation}
{: faq}

Après que je service a envoyé la demande d'authentification de la validation de domaine, {{site.data.keyword.cloudcerts_short}} tente de valider le fait que vous possédez les domaines demandés (pendant 10 minutes maximum). Si votre DNS n'est pas mis à jour avec la demande d'authentification de l'enregistrement TXT record sous 10 minutes, votre commande échoue.

## Comment vérifier le statut de ma commande de certificat via l'API publique {{site.data.keyword.cloudcerts_short}} ?
{: #certificate-order-status-api}
{: faq}

Utilisez l'API `Get certificate metadata` (obtenir des métadonnées de certificat) pour interroger le statut de la commande de certificat.

## Puis-je être notifié quand ma commande est terminée ?
{: #certificate-order-notification}
{: faq}

Si vous avez configuré un canal de notification, vous recevez une notification lorsque votre certificat est émis, ou si votre commande échoue. Notez que votre canal de notification doit être à la version 4 ou ultérieure.

## Ma commande a échoué. Pourquoi ?
{: #certificate-order-failure}
{: faq}

Vous trouverez un code et un message d'erreur dans les métadonnées de certificat, l'interface utilisateur, ainsi que dans la notification que vous avez reçu lorsque votre commande a échoué.

## Pourquoi est-ce que je ne reçois pas les événements de commande de certificat dans mon canal de notification Slack existant ?
{: #missing-notification-for-ordered-certificate}
{: faq}

Mettez votre canal de notification Slack à niveau vers la version la plus récente dans l'onglet des paramètres de Certificate Manager.
