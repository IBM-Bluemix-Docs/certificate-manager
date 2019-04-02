---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

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

# Configuration des notifications
{: #configuring-notifications}

Les certificats ne sont généralement valides que pour une durée définie. Quand un certificat que vous utilisez expire, votre application risque d'avoir à subir une période d'indisponibilité. Pour éviter cet inconvénient, vous pouvez configurer {{site.data.keyword.cloudcerts_full}} pour qu'il vous envoie des notifications relatives aux certificats qui sont sur le point d'expirer afin de vous rappeler de les renouveler à temps.

Vous recevez également une alerte lorsqu'une version renouvelée de votre certificat est réimportée dans {{site.data.keyword.cloudcerts_short}} à la place de celle qui a expiré, cela fin de vous rappeler que vous devez la déployer également sur les points de terminaison SSL/TLS. Cette notification relative aux certificats réimportés est envoyée uniquement aux canaux à partir du [canal version 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).
{: shortdesc}

**Quand suis-je notifié ?**  
Selon la date d'expiration du certificat que vous avez téléchargé dans {{site.data.keyword.cloudcerts_full_notm}}, vous êtes notifié 90, 60, 30, 10 jours ou 1 jour avant l'expiration du certificat. En plus, vous recevez des notifications quotidiennes relatives aux certificats expirés. Les notifications quotidiennes commencent le premier jour qui suit l'expiration de votre certificat.

Vous devez renouveler votre certificat et le réimporter à la place de votre ancien certificat sur {{site.data.keyword.cloudcerts_full_notm}} de manière à cesser l'envoi des notifications. Lorsque vous réimportez votre certificat, vous recevez une notification indiquant que votre certificat a été réimporté, cela afin de vous rappeler que vous devez le redéployer. 

**Quelles sont les options dont je dispose pour configurer les notifications ?**  
Vous pouvez envoyer des notifications à Slack en utilisant un webhook Slack ou vous servir de l'URL de rappel de votre choix.

## Configuration d'un webhook Slack
{: #setup-callback}

Pour configurer un webhook Slack, procédez comme suit :

1. Inscrivez-vous à [Slack](https://slack.com/) et configurez votre espace de travail.
2. Créez un canal Slack pour y poster vos notifications.
3. [Configurez un webhook](https://api.slack.com/incoming-webhooks) pour le canal Slack.

## Configuration d'une URL de rappel
{: #callback}

Pour déclencher le processus de renouvellement pour votre équipe, vous pouvez utiliser une URL de rappel afin de poster des notifications pour les outils que vous utilisez. Ainsi, vous pouvez envoyer des notifications pour effectuer un rapport à PagerDuty, ouvrir automatiquement un problème dans GitHub ou déclencher des scripts de renouvellement.  
{: shortdesc}

**Important :** votre noeud final d'URL de rappel doit répondre aux exigences suivantes pour être utilisé avec {{site.data.keyword.cloudcerts_short}} :
* Le noeud final doit utiliser le protocole HTTPS.
* Le noeud final ne doit pas requérir d'en-tête HTTP. Cette condition inclut les en-têtes d'autorisation.
* Le noeud final doit renvoyer un code d'état `200 OK` pour indiquer que la remise de notification a abouti.

### Format de la notification
{: #notification_format}

La notification envoyée à votre URL de rappel est un document JSON signé avec votre clé asymétrique d'instance au format suivant :

```
{ "data":"<Chaîne au format JWT>" }
```
{: screen}

Après que vous avez décodé et vérifié le contenu, celui-ci est une chaîne JSON [conforme à la version de canal](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Configuration d'un canal de notification
{: #adding-channel}

Après avoir créé un webhook Slack ou une URL de rappel, vous pouvez l'ajouter à {{site.data.keyword.cloudcerts_short}} pour commencer à recevoir des notifications relatives aux certificats sur le point d'expirer et aux certificats réimportés. {{site.data.keyword.cloudcerts_short}} chiffre le noeud final et le stocke en toute sécurité.
{: shortdesc}

Pour ajouter un canal de notification, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Ouvrez l'onglet **Notifications**.
3. Cliquez sur **Ajouter une entrée de notification**.
4. Choisissez le type de canal de notification que vous voulez utiliser.
5. Entrez le webhook ou l'URL de rappel spécifiant l'endroit où vous voulez envoyer les notifications.
6. Cliquez sur **Sauvegarder**. Un récapitulatif de votre configuration s'affiche.

   **Exemple de sortie**

   <table>
   <caption>Tableau 1. Informations sur le canal de notification </caption>
   <thead>
    <th> Composant </th>
    <th> Description </th>
   </thead>
   <tbody>
   <tr>
    <td>Type</td>
    <td>Type de canal de notification : <i>Slack</i> ou <i>URL de rappel</i></td>
   </tr>
   <tr>
    <td>Noeud final</td>
    <td>Noeud final du canal de notification où sont envoyées les notifications.</td>
   </tr>
   <tr>
    <td>Bascule d'activation</td>
    <td>Etat du canal de notification. S'il est défini sur désactivé, aucune notification n'est envoyée.</td>
   </tr>
   <tr>
    <td>Bouton Tester la connexion</td>
    <td>Envoie une notification test au canal que vous avez configuré. </td>
   </tr>
    <tr>
      <td>Menu Points</td>
      <td>Actions disponibles que vous pouvez exécuter sur le canal : <i>éditer</i> ou <i>supprimer</i></td>
    </tr>
    </tbody>
    </table>

    Quand vous sauvegardez un webhook Slack, {{site.data.keyword.cloudcerts_short}} envoie automatiquement une notification de confirmation au canal Slack que vous avez configuré. Contrôlez votre canal Slack pour vérifier que vous avez reçu cette notification.
    {: tip}
7. (Facultatif) Répétez cette procédure pour ajouter d'autres canaux de notification.

## Test d'un canal de notification
{: #testing-channel}

Vous pouvez tester un canal de notification pour vous assurer qu'il est configuré correctement.
{: shortdesc}

Avant de commencer, [configurez un canal de notification](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Pour tester un canal de notification, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Trouvez votre canal de notification puis cliquez sur **Tester la connexion**.
3. Vérifiez que vous avez reçu une notification dans le canal que vous avez configuré.

## Mise à jour d'un canal de notification
{: #updating-channel}

Vous pouvez mettre à jour la configuration de votre canal de notification, activer ou désactiver les notifications ou supprimer des canaux de notification de {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Avant de commencer, [configurez un canal de notification](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Pour mettre à jour un canal de notification, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Sélectionnez l'onglet **Notifications**.
3. Sélectionnez l'une des options suivantes :
   * Pour désactiver ou activer des notifications pour un canal, paramétrez le commutateur à **Désactiver** ou **Activer**.
   * Pour mettre à jour les paramètres pour un canal, sélectionnez **Editer** dans le menu d'actions.
   * Pour supprimer un canal de notification, sélectionnez **Supprimer** dans le menu d'actions.

## Vérification du contenu HTTP pour une URL de rappel
{: #verify-callback}

Chaque contenu HTTP qui est envoyé depuis {{site.data.keyword.cloudcerts_short}} vers votre URL de rappel est automatiquement signé selon le standard JWT en utilisant une paire de clés asymétriques.  
{: shortdesc}

Pour chaque instance {{site.data.keyword.cloudcerts_short}}, une clé privée et une clé publique sont générées qui ne sont pas partagées sur d'autres instances {{site.data.keyword.cloudcerts_short}}. La clé privée est utilisée pour signer le contenu HTTP et vous pouvez utiliser la clé publique pour vérifier que le contenu est généré par {{site.data.keyword.cloudcerts_short}} et n'est pas modifié par un tiers.

Pour télécharger la clé publique, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Ouvrez l'onglet **Notifications**.
3. Cliquez sur le bouton **Télécharger la clé**. La clé est déchargée sous la forme d'un fichier PEM.

## Versions de canal
{: #channel-versions}

A mesure que Certificate Manager évolue, nous pouvons être amenés à modifier le format de la structure de contenu des notifications de temps à autre. Pour garantir la compatibilité avec les versions antérieures, le contenu envoyé à vos canaux existants n'est pas modifié.    

Si vous possédez déjà des canaux de notification (Slack ou URL de rappel), pour commencer à utiliser la nouvelle version du contenu :
1. Pour une URL de rappel, assurez-vous que votre implémentation peut accepter le nouveau contenu. 
2. Créez un canal de notification (les nouveaux canaux sont toujours créés avec la dernière version de canal).
3. Testez le bon fonctionnement du nouveau canal.
4. Supprimez l'ancien canal.

Pour les versions de canal, consultez la [documentation d'API](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Exemples
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Apprenez comment créer des anomalies GitHub pour des notifications relatives à des certificats qui arrivent à expiration.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Apprenez comment créer des anomalies PagerDuty pour des notifications relatives à des certificats qui arrivent à expiration.
