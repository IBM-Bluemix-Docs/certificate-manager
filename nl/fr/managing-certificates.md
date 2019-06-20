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

# Gestion des certificats depuis le tableau de bord
{: #managing-certificates-from-the-dashboard}

Vous pouvez utiliser le tableau de bord du service {{site.data.keyword.cloudcerts_full}} pour gérer des certificats que vous vous procurez auprès d'émetteurs tiers afin de les utiliser avec vos services ou applications cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

## Formats de certificat et algorithmes de clé publique pris en charge
{: supported-formats-and-algorithms}

### Formats de certificat
* PEM

### Algorithmes de clé publique
* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Protocole d'accord de clé Elliptic Curve with Diffie-Hellman

## Importation d'un certificat
{: #importing-a-certificate}

Importez vos certificats afin de pouvoir les gérer.
{: shortdesc}

**Avant de commencer**

* Créez un certificat valide non arrivé à expiration avec une clé privée correspondante (la clé est facultative).
* Convertissez les fichiers au format PEM (Privacy-enhanced Electronic Mail).
* Gardez la clé privée non chiffrée pour vous assurer qu'il peut être importé.

Pour importer un certificat, cliquez sur **Importer le certificat** et indiquez les détails suivants :

1. Indiquez un nom de certificat.
2. Sélectionnez le fichier certificat au format PEM en cliquant sur **Parcourir**.
3. Facultatif : sélectionnez la clé privée du nouveau certificat au format PEM en cliquant sur **Parcourir**.
4. Si applicable, indiquez le fichier certificat intermédiaire au format PEM.
5. Facultatif : entrez une description.
6. Cliquez sur **Importer**.

Une fois que vous avez importé un certificat, les informations ci-après sont affichées dans le tableau Certificats. Pour afficher d'autres informations sur le certificat, vous pouvez développer la ligne correspondant à celui-ci dans le tableau Certificats.

<table>
<caption> Tableau 1. Informations sur le certificat importé </caption>
  <tr>
    <th> Composant </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Nom</td>
    <td>Nom d'affichage descriptif. La longueur maximale est de 256 caractères. </td>
  </tr>
  <tr>
    <td>Description</td>
    <td>(Facultatif) Texte descriptif relatif au certificat. La longueur maximale est de 1024 caractères.</td>
  </tr>
  <tr>
    <td>Domaine</td>
    <td>Domaine ou domaines pour lesquels le certificat est valide. </td>
  </tr>
  <tr>
    <td>Emetteur</td>
    <td>Autorité de certification ayant émis le certificat.</td>
  </tr>
  <tr>
    <td>Algorithme</td>
    <td>Algorithme de signature de certificat</td>
  </tr>
  <tr>
    <td>Algorithme de clé</td>
    <td>Algorithme de clé publique</td>
  </tr>
  <tr>
    <td>Expire dans</td>
    <td>Nombre jours avant l'expiration du certificat. </td>
  </tr>
  <tr>
    <td>Valide à partir du</td>
    <td>Date à laquelle le certificat est devenu valide (fuseau horaire UTC). </td>
  </tr>
  <tr>
    <td>Expire le</td>
    <td>Date à laquelle le certificat n'est plus valide (fuseau horaire UTC). </td>
  </tr>
  <tr>
    <td>Statut</td>
    <td>Statut de votre certificat. </td>
  </tr>
  <tr>
    <td>ID certificat</td>
    <td>ID généré pour le certificat lors de l'importation.</td>
  </tr>
</table>

</br>

## Réimportation d'un certificat
{: #reimport-certificate}

Si votre certificat est sur le point d'expirer, vous pouvez le mettre à jour en important une nouvelle version avec le même domaine que le certificat existant, mais avec une nouvelle date d'expiration. Lorsqu'un certificat est réimporté, la version existante de celui-ci est conservée en tant que sauvegarde qui peut être téléchargée en cas de besoin.
{: shortdesc}

### Réimportation de votre certificat
{: #reimporting-certificate}

Pour réimporter un certificat, procédez comme suit :

1. Développez la ligne correspondant au certificat.
2. Cliquez sur **Réimporter le certificat**.
3. Sélectionnez le nouveau fichier certificat au format PEM en cliquant sur **Parcourir**.
4. (Facultatif) Sélectionnez la clé privée du nouveau certificat au format PEM en cliquant sur **Parcourir**.
5. (Facultatif) Indiquez un nouveau fichier certificat intermédiaire au format PEM en cliquant sur **Parcourir**.
6. Cliquez sur **Réimporter**, puis sur **Terminé**.

Les opérations de réimportation de certificats sont limitées à cinq actions par minute.
{: note}

### Téléchargement d'une version précédente de votre certificat
{: #downloading-certificate}

Pour télécharger la version précédente d'un certificat, procédez comme suit :

1. Développez la ligne correspondant au certificat.
2. Cliquez sur le lien **Version précédente**.

## Commande de certificats
{: #order-certificates}

Avant de commander un certificat, [commencez par effectuer la configuration obligatoire](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates).

1. Indiquez un nom de certificat.
2. Sélectionnez une autorité de certification.
3. Indiquez le domaine principal ainsi que tout domaine de remplacement.
4. Sélectionnez l'algorithme et l'algorithme de clé appropriés. 
5. Cliquez sur **Commander**.

La commande de certificats est limitée à cinq commandes/minute par instance {{site.data.keyword.cloudcerts_short}}, 100 commandes/heure par compte utilisateur IBM, et cinq certificats pour les mêmes domaines par semaine.
{: note}

## Renouvellement de certificats
{: #renew-certificates}

Pour renouveler un certificat, procédez comme suit :
  1. Cliquez sur le menu sur la ligne du certificat à renouveler.
  2. Cliquez sur **Renouveler le certificat**.
  3. Facultatif : Vous pouvez choisir de recomposer votre certificat en cochant la case **Recomposer le certificat**. Le certificat sera alors renouvelé avec une nouvelle paire de clés. 
  
  Lorsque vous recomposez un certificat, veillez à déployer les nouveaux certificats et clés partout où ils sont utilisés. {: note}
    
  4. Cliquez sur **Renouveler**
  
  Vous pouvez uniquement renouveler des certificats commandés via {{site.data.keyword.cloudcerts_short}}.
  {: note}

Le renouvellement de certificat est limité à cinq demandes de renouvellement par certificat par minute, 100 renouvellements/heure par compte utilisateur IBM.
{: note}


## Recherche de certificats
{: #searching-certificates}

Si vous gérez un grand nombre de certificats, vous pouvez utiliser la barre de recherche pour localiser le certificat requis.
{: shortdesc}

* Pour rechercher un nom de certificat, un domaine de certificat ou un émetteur de certificat, tapez le terme recherché dans la barre de recherche et appuyez sur Entrée.
* Pour afficher tous vos certificats, cliquez sur l'icône **X** dans la barre de recherche.

## Téléchargement de certificats
{: #downloading-certificates}

Lorsque vous êtes prêt à déployer votre certificat sur votre application ou service, vous pouvez le télécharger, ainsi que la clé privée qui lui est associée.
{: shortdesc}

Pour télécharger un certificat, procédez comme suit :

1. Cochez la case correspondant au certificat que vous souhaitez télécharger.
2. Cliquez sur **Télécharger le certificat**. Selon ce que vous avez importé dans le service, vous recevez un fichier compressé contenant des fichiers PEM pour le certificat, une clé privée associée et un certificat intermédiaire associé.

Vous ne pouvez pas télécharger des certificats arrivés à expiration.
{: note}

## Suppression de certificats
{: #deleting-certificates}

Si vous souhaitez arrêter le suivi d'un certificat, vous pouvez supprimer celui-ci.
{: shortdesc}  

Pour supprimer un certificat, procédez comme suit :

1. Cochez la case correspondant au certificat que vous souhaitez supprimer.
2. Cliquez sur l'icône **Corbeille**.

## Mise à jour des métadonnées de certificat
{: #updating-certificates-metadata}

Vous pouvez également mettre à jour le nom et la description d'un certificat.
{: shortdesc}

Pour mettre à jour un certificat, procédez comme suit :

1. Sélectionnez une ligne afin d'ouvrir les détails de ce certificat.
2. Mettez à jour le nom ou la description.
3. Sauvegardez vos modifications.

Vous pouvez effectuer jusqu'à cinq actions de mise à jour par minute.
{: note}
