---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestion des rôles d'accès aux services
{: #managing-service-access-roles}

Vous pouvez sécuriser des services dans {{site.data.keyword.Bluemix_notm}} en autorisant uniquement les utilisateurs dotés de rôles d'accès spécifiés à exécuter certaines actions.
{: shortdesc}

### Rôles d'accès à la plateforme
{: #platform-access-roles}

Vous pouvez utiliser des rôles d'accès à la plateforme pour permettre aux utilisateurs d'effectuer des tâches sur des ressources de plateforme telles que la création ou la suppression d'instances dans votre compte IBM Cloud.

<table>
<caption> Tableau 1. Actions mappées aux rôles d'accès à la plateforme</caption>
  <tr>
    <th> Action </th>
    <th> Rôle </th>
  </tr>
  <tr>
    <td>Afficher des instances de Certificate Manager</td>
    <td> Administrateur, Opérateur, Editeur, Afficheur </td>
  </tr>
  <tr>
    <td>Créer une instance de Certificate Manager</td>
    <td> Administrateur, Editeur </td>
  </tr>
  <tr>
    <td>Supprimer une instance de Certificate Manager</td>
    <td> Administrateur, Editeur </td>
  </tr>
</table>

Historiquement, les rôles de plateforme donnent également accès à certaines actions sur les certificats au sein des instances. Cette définition est obsolète et sera retirée dans un futur proche.

### Rôles d'accès au service
{: #service-acceess-roles}

Vous pouvez utiliser des rôles d'accès au service afin de permettre aux utilisateurs d'effectuer des tâches dans des instances Certificate Manager telles que l'importation, le téléchargement, l'édition ou la suppression de certificats.

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
    <td>Mettre à jour des données de certificat</td>
    <td> Gestionnaire, Rédacteur </td>
  </tr>
  <tr>
    <td>Télécharger des certificats, des clés privées et des certificats intermédiaires </td>
    <td> Gestionnaire </td>
  </tr>
  <tr>
    <td>Supprimer un certificat et une clé privée </td>
    <td> Gestionnaire </td>
  </tr>
</table>


Pour plus d'informations sur les rôles et les droits utilisateur, voir [Rôles utilisateur](/docs/iam/users_roles.html#userroles).

### Affectation de rôles d'accès utilisateur
{: #assigning-user--access-roles}

Pour affecter un rôle d'accès au niveau compte ou au niveau groupe de ressources, procédez comme indiqué ci-après.
Si l'utilisateur ne fait pas partie de votre organisation, commencez par envoyer une invitation à cet utilisateur.

1. Accédez à **Gérer > Compte > Utilisateur**.
2. Dans le menu **Actions**, sélectionnez **Affecter une règle**.
3. Cliquez sur **Affecter l'accès aux ressources** ou **Affecter l'accès au sein d'un groupe de ressources**.
4. Sous **Services**, sélectionnez **Gestionnaire de certificat**.
5. Facultatif : sélectionnez une **région** ou utilisez la valeur par défaut, **Toutes les régions**.
6. Facultatif : sélectionnez une **instance de service** ou utilisez la valeur par défaut, **Toutes les instances**.
7. Sous **Sélectionner les rôles > Affecter des rôles d'accès à une plateforme/un service**, sélectionnez le niveau d'accès approprié.

**Exemples :**
* Affectez au moins le rôle Visualiseur à chaque utilisateur pour qu'il puisse voir les instances de service. 
* Affichez le rôle Administrateur ou Editeur à un utilisateur si vous souhaitez que celui-ci puisse créer des instances. 
* Affectez au moins le rôle Lecteur si vous souhaitez qu'un utilisateur puisse afficher les certificats au sein d'une instance.
