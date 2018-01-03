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
{:tip: .tip}

# À propos de
{: #about-cloud-certs}

Découvrez {{site.data.keyword.cloudcerts_full}}.

## Présentation de {{site.data.keyword.cloudcerts_short}}
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} vous permet de gérer les certificats SSL pour vos applications et vos services cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Vous pouvez importer des certificats SSL que vous obtenez pour vos applications et vos services, les stocker en toute sécurité et centraliser l'affichage des certificats que vous utilisez. 

Vous pouvez gérer vos certificats en procédant comme suit :

* Surveillez les dates d'expiration de vos certificats afin de les renouveler à temps. 
* Affichez les types de certificats sur vos déploiements et assurez-vous qu'ils répondent aux règles de l'organisation.
* Recherchez les certificats que vous devez remplacer lorsque de nouvelles exigences de conformité ou de sécurité sont émises.
* Définissez les contrôles qui déterminent qui peut accéder à et gérer vos certificats.

## Disponibilité
{: #availability}

{{site.data.keyword.cloudcerts_short}} est disponible uniquement dans la région du Sud des Etats-Unis. 

## Sécurité de clé privée
{: #private-key-security}

Lorsque vous importez un certificat et la clé privée correspondante dans {{site.data.keyword.cloudcerts_short}}, le service utilise un algorithme AES (Advanced Encryption Standard) 256 pour chiffrer la clé privée. {{site.data.keyword.cloudcerts_short}} sauvegarde cette clé chiffrée unique à utiliser avec votre instance de service.

## Identity and Access Management
{: #identity-access-management}

Vous pouvez sécuriser des services dans {{site.data.keyword.Bluemix_notm}} en autorisant uniquement les utilisateurs dotés de rôles spécifiés à exécuter certaines actions.
{: shortdesc}

<table>
<caption> Tableau 1. Actions mappées aux rôles utilisateur</caption>
  <tr>
    <th> Action </th>
    <th> Rôle </th>
  </tr>
  <tr>
    <td>Répertorier des certificats</td>
    <td> Administrateur, Opérateur, Editeur, Afficheur </td>
  </tr>
  <tr>
    <td>Télécharger un certificat et une clé privée </td>
    <td> Administrateur, Opérateur </td>
  </tr>
  <tr>
    <td>Mettre à jour des données de certificat </td>
    <td> Administrateur, Editeur </td>
  </tr>
  <tr>
    <td>Télécharger des certificats, des clés privées et des certificats intermédiaires </td>
    <td> Administrateur, Editeur  </td>
  </tr>
  <tr>
    <td>Supprimer un certificat et une clé privée </td>
    <td> Administrateur, Editeur </td>
  </tr>
</table>

Pour plus d'informations sur les rôles et les droits utilisateur, voir [Rôles utilisateur](/docs/admin/patterns.html#userroles).

### Affectation de rôles utilisateur
{: #assigning-user-roles}

Pour affecter un rôle utilisateur au niveau compte ou au niveau groupe de ressources, procédez comme indiqué ci-après.
Si l'utilisateur ne fait pas partie de votre organisation, commencez par envoyer une invitation à cet utilisateur. 

1. Accédez à **Gérer > Compte > Utilisateur**.
2. Dans le menu **Actions**, sélectionnez **Affecter une règle**.
3. Cliquez sur **Affecter l'accès aux ressources** ou **Affecter l'accès au sein d'un groupe de ressources**.
4. Sous **Services**, sélectionnez **Gestionnaire de certificat**.
5. Facultatif : sélectionnez une **région** ou utilisez la valeur par défaut, **Toutes les régions**.
6. Facultatif : sélectionnez une **instance de service** ou utilisez la valeur par défaut, **Toutes les instances**.
7. Sous **Sélectionner les rôles > Affecter des rôles d'accès à une plateforme**, sélectionnez le niveau d'accès approprié.
