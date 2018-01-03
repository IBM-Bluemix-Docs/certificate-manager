---
copyright:
  years: 2017
lastupdated: "2017-12-13"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestion des certificats dans l'interface graphique
{: #managing-certificates-ui}

Vous pouvez utiliser l'interface graphique du service {{site.data.keyword.cloudcerts_full}} pour gérer des certificats que vous vous procurez auprès d'émetteurs tiers afin de les utiliser avec vos services ou applications cloud {{site.data.keyword.IBM_notm}}. Une fois importés, vos certificats et vos clés sont chiffrés et stockés par le service.
{: shortdesc}

## Importation d'un certificat
{: #importing-a-certificate}

Pour vous aider à gérer vos certificats, vous pouvez les télécharger.
{: shortdesc}

Avant de commencer :

* Créez un certificat valide non arrivé à expiration avec une clé privée correspondante.
* Convertissez les fichiers au format PEM (Privacy-enhanced Electronic Mail). 
* Gardez la clé privée non chiffrée pour vous assurer qu'il peut être importé. 

Pour importer un certificat, cliquez sur **Importer le certificat** et indiquez les détails suivants :

1. Facultatif : entrez un nom d'affichage.
2. Cliquez sur **Parcourir** et sélectionnez le fichier certificat au format PEM. 
3. Cliquez sur **Parcourir** et sélectionnez la clé privée du certificat au format PEM. 
4. Si applicable, indiquez le fichier certificat intermédiaire au format PEM. 
5. Facultatif : entrez une description.
6. Cliquez sur **Importer**.  

**Remarque** : pour renouveler un certificat importé, procurez-vous un nouveau certificat auprès de votre autorité de certification et importez le nouveau certificat dans {{site.data.keyword.cloudcerts_short}}. Une fois le nouveau certificat déployé, vous pouvez supprimer l'ancien. 

Une fois que vous avez importé un certificat, les informations ci-après sont affichées dans le tableau Certificats. Pour visualiser d'autres informations sur le certificat, vous pouvez sélectionner le certificat dans la ligne de tableau. 

<table>
<caption> Tableau 1. Informations sur le certificat importé </caption>
  <tr>
    <th> Composant </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>Nom</td>
    <td>Facultatif : nom d'affichage. </td>
  </tr>
  <tr>
    <td>Description </td>
    <td>Facultatif : texte descriptif relatif au certificat. </td>
  </tr>
  <tr>
    <td>Domaine</td>
    <td>Domaine ou domaines pour lesquels le certificat est valide. </td>
  </tr>
  <tr>
    <td>Emetteur</td>
    <td>Autorité de certification ayant émis le certificat. </td>
  </tr>
  <tr>
    <td>Algorithme</td>
    <td>Type de chiffrement par lequel le certificat est créé. </td>
  </tr>
  <tr>
    <td>Algorithme de clé</td>
    <td>Type et taille de clé utilisés par l'algorithme. </td>
  </tr>
  <tr>
    <td>Expire dans </td>
    <td>Nombre jours avant l'expiration du certificat. </td>
  </tr>
  <tr>
    <td>Date de publication</td>
    <td>Date à laquelle le certificat a été émis. </td>
  </tr>
  <tr>
    <td>Valide à partir du</td>
    <td>Date à laquelle le certificat est devenu valide. </td>
  </tr>
  <tr>
    <td>Expire le  </td>
    <td>Date à laquelle le certificat n'est plus valide. </td>
  </tr>
  <tr>
    <td>ID certificat</td>
    <td>ID généré pour le certificat lors de l'importation. </td>
  </tr>
</table>

## Recherche de certificats
{: #searching-certificates}
 
Si vous gérez un grand nombre de certificats, vous pouvez utiliser la barre de recherche pour localiser le certificat requis.
{: shortdesc}
 
-   Pour rechercher un nom de certificat, un domaine de certificat ou un émetteur de certificat, tapez le terme recherché dans la barre de recherche et appuyez sur Entrée. 
-   Pour afficher tous vos certificats, cliquez sur l'icône **X** dans la barre de recherche. 

## Téléchargement de certificats
{: #downloading-certificates}

Lorsque vous êtes prêt à déployer votre certificat sur votre application ou service, vous pouvez le télécharger, ainsi que la clé privée qui lui est associée.
{: shortdesc}

Pour télécharger un certificat : 

1. Cochez la case correspondant au certificat que vous souhaitez télécharger. 
2. Cliquez sur **Télécharger le certificat**. Selon ce que vous avez importé dans le service, vous recevez un fichier compressé contenant des fichiers PEM pour le certificat, une clé privée associée et un certificat intermédiaire associé. 


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

**Remarque** : vous pouvez effectuer jusqu'à 5 actions de mise à jour par minute.
