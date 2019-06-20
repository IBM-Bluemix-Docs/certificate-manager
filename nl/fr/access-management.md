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

# Gestion des rôles d'accès aux services
{: #managing-service-access-roles}

Vous pouvez sécuriser des services dans {{site.data.keyword.cloud_notm}} en autorisant uniquement les utilisateurs dotés de rôles d'accès spécifiés à exécuter certaines actions.
{: shortdesc}

## Rôles d'accès à la plateforme
{: #platform-access-roles}

Vous pouvez utiliser des rôles d'accès à la plateforme pour permettre aux utilisateurs d'effectuer des tâches sur des ressources de plateforme, telles que la création ou la suppression d'instances dans votre compte {{site.data.keyword.cloud_notm}}.

<table>
<caption> Tableau 1. Actions mappées aux rôles d'accès à la plateforme</caption>
  <tr>
    <th> Action </th>
    <th> Rôle </th>
  </tr>
  <tr>
    <td>Afficher des instances de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrateur, Opérateur, Editeur, Afficheur </td>
  </tr>
  <tr>
    <td>Créer une instance de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrateur, Editeur </td>
  </tr>
  <tr>
    <td>Supprimer une instance de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrateur, Editeur </td>
  </tr>
</table>

## Rôles d'accès au service
{: #service-access-roles}

Vous pouvez utiliser des rôles d'accès au service afin de permettre aux utilisateurs d'effectuer des tâches dans des instances {{site.data.keyword.cloudcerts_short}}, telles que l'importation, le téléchargement, l'édition ou la suppression de certificats.

<table>
<caption> Tableau 2. Actions mappées aux rôles d'accès au service</caption>
  <tr>
    <th> Action </th>
    <th> Rôle </th>
  </tr>
  <tr>
    <td>Répertorier des certificats</td>
    <td> Gestionnaire, Rédacteur, Lecteur </td>
  </tr>
  <tr>
    <td>Télécharger un certificat et une clé privée </td>
    <td> Gestionnaire, Rédacteur </td>
  </tr>
  <tr>
     <td>Obtenir des métadonnées de certificat </td>
     <td> Gestionnaire, Rédacteur, Lecteur </td>
  </tr>      
  <tr>
    <td>Mettre à jour des métadonnées de certificat</td>
    <td> Gestionnaire, Rédacteur </td>
  </tr>
  <tr>
    <td>Importer ou réimporter des certificats, des clés privées et des certificats intermédiaires </td>
    <td> Gestionnaire </td>
  </tr>
  <tr>
    <td>Commander un certificat </td>
    <td> Gestionnaire </td>
  </tr>
  <tr>
    <td>Supprimer un certificat et une clé privée </td>
    <td> Gestionnaire </td>
  </tr>
      <tr>
        <td>Répertorier tous les canaux de notification </td>
        <td> Gestionnaire, Rédacteur, Lecteur </td>
      </tr>
   <tr>
     <td>Ajouter, mettre à jour ou supprimer un canal de notification </td>
     <td> Gestionnaire </td>
   </tr>
     <tr>
       <td>Tester un canal de notification </td>
       <td> Gestionnaire, Rédacteur, Lecteur </td>
     </tr>

</table>

Pour plus d'informations sur les rôles et les droits utilisateur, voir [Rôles utilisateur](/docs/iam?topic=iam-userroles#userroles).

## Configuration des politiques d'accès pour les utilisateurs
{: #configuring-access-policies}

Vous pouvez configurer des politiques d'accès pour une instance {{site.data.keyword.cloudcerts_short}} (et, de ce fait, pour tous les certificats de cette instance), ou vous pouvez définir des politiques pour les certificats individuels (ressources) dans une instance.

**Exemples d'affectation de rôles**

* Affectez au moins le rôle Visualiseur à chaque utilisateur pour qu'il puisse voir les instances de service.
* Affectez le rôle Administrateur ou Editeur à un utilisateur si vous voulez que cet utilisateur crée/supprime des instances.
* Affectez au moins le rôle Lecteur si vous souhaitez qu'un utilisateur puisse afficher les certificats au sein d'une instance.

{: shortdesc}

### Configuration de politiques d'accès 
{: #configuring-access}

Pour configurer des politiques d'accès, procédez comme suit :

1. Accédez à **Gérer > Accès (IAM) > Utilisateurs**. Une liste des utilisateurs ayant un accès à votre compte {{site.data.keyword.cloud_notm}} s'affiche.
2. Cliquez sur le nom de l'utilisateur auquel vous voulez affecter une politique d'accès. Si l'utilisateur ne s'affiche pas, cliquez sur **Inviter des utilisateurs** pour [ajouter l'utilisateur à votre compte {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Cliquez sur **Politiques d'accès** puis sur **Affecter un accès**.
4. Cliquez **Affecter l'accès aux ressources**.
5. Dans le menu **Services**, sélectionnez **Certificate Manager**.
6. Dans le menu **Instance de service**, sélectionnez une instance {{site.data.keyword.cloudcerts_short}}, ou utilisez la valeur par défaut `Toutes les instances`.
7. Affectez un [rôle d'accès à une plateforme](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) à l'utilisateur.
8. Affectez un [rôle d'accès à un service](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) à l'utilisateur.
9. Cliquez sur **Affecter** pour affecter la politique d'accès à l'utilisateur.

### Autorisation de l'accès à un certificat spécifique
{: #allow-access-to-specific-certificate}

Pour accéder à un certificat particulier, exécutez la procédure suivante :

1. [Extrayez votre ID certificat](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Créez deux politiques d'accès :
   - Première politique : Affectez au moins le rôle d'accès plateforme **Afficheur** pour l'instance de service. 
   - Seconde politique : Affectez au moins le rôle d'accès service **Lecteur**.
     - Entrez `certificate` dans la zone **Type de ressource**.
     - Entrez l'ID certificat dans la zone **ID de ressource**.

### Extraction de l'ID d'un certificat
{: #get-certificate-id}

Pour récupérer l'ID d'un certificat, procédez comme suit :

1. Depuis le tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez votre instance {{site.data.keyword.cloudcerts_short}}.
2. Dans la navigation de la page Détails du service, sélectionnez **Gérer**.
3. Sélectionnez un certificat.
4. Dans les détails du certificat, trouvez le certificat CRN (Cloud Resource Name).
5. Copiez l'ID de certificat. Le certificat CRN contient différentes valeurs qui sont séparées par le signe deux points (`:`). L'ID de certificat est la dernière valeur de votre certificat CRN, par exemple `e20cb664efcbfa2c2f57801230d246a6`
