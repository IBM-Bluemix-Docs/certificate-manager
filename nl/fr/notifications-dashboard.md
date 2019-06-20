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

# Configuration des notifications
{: #configuring-notifications}

{{site.data.keyword.cloudcerts_full}} peut vous envoyer des notifications concernant les événements de cycle de vie de certificats. Ces notifications incluent des rappels de renouvellement de certificats avant leur arrivée à expiration, ainsi que des rappels de déploiement de certificats quand ceux-ci sont prêts. Pour obtenir des notifications depuis {{site.data.keyword.cloudcerts_short}}, vous pouvez configurer un canal de notification. Vous pouvez, au choix, spécifier un webhook Slack, une URL de rappel, ou toute combinaison des deux.
{: shortdesc}

La fonction de notification est également utilisée lorsque vous [commandez des certificats](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates) depuis {{site.data.keyword.cloudcerts_short}}. Pour prouver que vous possédez le domaine pour lequel vous demandez un certificat, {{site.data.keyword.cloudcerts_short}} envoie une demande d'authentification sous forme de notification à votre URL de rappel. Il s'agit d'un enregistrement texte que vous placez dans le service Domain Name System (DNS) où votre domaine est enregistré. Quand l'enregistrement texte est en place, la demande d'authentification est considérée comme terminée. Parce que la demande est envoyée sous forme de notification à votre URL de rappel, vous avez la possibilité d'automatiser le processus de validation de domaine en exécutant du code en réponse à l'événement de notification. 

## Notifications pour la surveillance de l'expiration de certificat
{: #notifications-monitoring-certificate-expiration}

Les certificats sont généralement valides pour une certaine durée. Quand un certificat que vous utilisez expire, votre application risque d'avoir à subir une période d'indisponibilité. Pour éviter cet inconvénient, vous pouvez configurer {{site.data.keyword.cloudcerts_short}} pour qu'il vous envoie des notifications relatives aux certificats qui sont sur le point d'expirer afin de vous rappeler de les renouveler à temps.

Vous êtes également alerté quand une version renouvelée de votre certificat est réimportée dans {{site.data.keyword.cloudcerts_short}} à la place de celui arrivé à expiration. Cette notification est destinée à vous rappeler de déployer le nouveau certificat sur les points de terminaison SSL/TLS. Cette notification est envoyée uniquement aux canaux à partir de la [version 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


**Quand suis-je notifié ?**  
Selon la date d'expiration du certificat que vous avez téléchargé dans {{site.data.keyword.cloudcerts_short}}, vous êtes notifié 90, 60, 30, 10 jours ou 1 jour avant l'expiration du certificat. En plus, vous recevez des notifications quotidiennes relatives aux certificats expirés. Les notifications quotidiennes commencent le premier jour qui suit l'expiration de votre certificat.

Vous devez renouveler votre certificat et le réimporter à la place de votre ancien certificat sur {{site.data.keyword.cloudcerts_short}} de manière à cesser l'envoi des notifications. Lorsque vous réimportez votre certificat, vous recevez une notification indiquant que votre certificat a été réimporté, ce afin de vous rappeler que vous devez le redéployer. 

**Quelles sont les options dont je dispose pour configurer les notifications ?**  
Vous pouvez envoyer des notifications à Slack en utilisant un webhook Slack ou vous servir de l'URL de rappel de votre choix.

## Notifications liées à la commande de certificats
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} vous notifie lorsqu'un certificat que vous aviez commandé auprès de {{site.data.keyword.cloudcerts_short}} a été émis ou renouvelé. Vous recevez également une notification en cas d'échec d'une commande ou d'un renouvellement.
{: shortdesc}

La configuration d'un canal de notification d'URL de rappel et la possibilité de gérer les événements liés à la validation de domaine constituent des prérequis à la commande et au renouvellement de certificats. Lorsque vous commandez un certificat, {{site.data.keyword.cloudcerts_short}} envoie un enregistrement TXT de demande d'authentification à votre URL de rappel. Vous devrez utiliser cet enregistrement pour prouver que vous possédez le domaine pour lequel vous demandez le certificat. Un enregistrement TXT de demande d'authentification est également envoyer lorsque vous demandez à renouveler un certificat.  


## Configuration d'un webhook Slack
{: #setup-callback}

Pour configurer un webhook Slack, procédez comme suit :

1. Inscrivez-vous à [Slack](https://slack.com/) et configurez votre espace de travail.
2. Créez un canal Slack pour y poster vos notifications.
3. [Configurez un Webhook](https://api.slack.com/incoming-webhooks) pour le canal Slack.

## Configuration d'une URL de rappel
{: #callback}

Pour déclencher le processus de renouvellement pour votre équipe, vous pouvez utiliser une URL de rappel afin de poster des notifications pour les outils que vous utilisez. Ainsi, vous pouvez envoyer des notifications pour effectuer un rapport à PagerDuty, ouvrir automatiquement un problème dans GitHub ou déclencher des scripts de renouvellement. Vous pouvez également déclencher automatiquement le déploiement de certificats en réponse aux notifications lorsque des certificats ont été réimportés ou émis.
{: shortdesc}

Une URL de rappel constitue un prérequis à la commande de certificats.
{: note}

**Important :** votre noeud final d'URL de rappel doit répondre aux exigences suivantes pour être utilisé avec {{site.data.keyword.cloudcerts_short}} :
* Le noeud final doit utiliser le protocole HTTPS.
* Le noeud final ne doit pas requérir d'en-tête HTTP. Cette condition inclut les en-têtes d'autorisation.
* Le noeud final doit renvoyer un code d'état `200 OK` pour indiquer que la remise de notification a abouti.

### Format de la notification
{: #notification_format}

La notification envoyée à votre URL de rappel est un document JSON signé avec votre clé asymétrique d'instance, au format ci-après.

```
{ "data":"<Chaîne au format JWT>" }
```
{: screen}

Après que vous avez décodé et vérifié le contenu, celui-ci est une chaîne JSON [conforme à la version de canal](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configuration d'un canal de notification
{: #adding-channel}

Une fois que vous avez créé un webhook Slack ou une URL de rappel, vous pouvez l'ajouter à {{site.data.keyword.cloudcerts_short}} pour commencer à recevoir des notifications concernant les certificats arrivant à expiration, les certificats réimportés, les certificats émis, ainsi que les demandes d'authentification pour la validation de domaine. {{site.data.keyword.cloudcerts_short}} chiffre le noeud final et le stocke en toute sécurité.
{: shortdesc}

Pour ajouter un canal de notification, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Ouvrez l'onglet **Notifications**.
3. Cliquez sur **Ajouter une entrée de notification**.
4. Choisissez le type de canal de notification que vous voulez utiliser.
5. Entrez le webhook ou l'URL de rappel spécifiant où vous souhaitez envoyer des notifications. 
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

    Lorsque vous sauvegardez un webhook Slack, {{site.data.keyword.cloudcerts_short}} envoie automatiquement une notification de confirmation au canal Slack que vous avez configuré. Contrôlez votre canal Slack pour vérifier que vous avez reçu cette notification.
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

Chaque contenu HTTP envoyé depuis {{site.data.keyword.cloudcerts_short}} vers votre URL de rappel est automatiquement signé, conformément à la norme JWT, en utilisant une paire de clés asymétriques.  
{: shortdesc}

Pour chaque instance {{site.data.keyword.cloudcerts_short}}, une clé privée et une clé publique sont générées qui ne sont pas partagées sur d'autres instances {{site.data.keyword.cloudcerts_short}}. La clé privée est utilisée pour signer le contenu HTTP et vous pouvez utiliser la clé publique pour vérifier que le contenu est généré par {{site.data.keyword.cloudcerts_short}} et n'est pas modifié par un tiers.

Pour télécharger la clé publique, procédez comme suit :

1. Dans la navigation de la page Détails du service, cliquez sur **Paramètres**.
2. Ouvrez l'onglet **Notifications**.
3. Cliquez sur le bouton **Télécharger la clé**. La clé est déchargée sous la forme d'un fichier PEM.

## Versions de canal
{: #channel-versions}

A mesure que Certificate Manager évolue, nous pouvons être amenés à modifier le format de la structure de contenu des notifications de temps à autre. Afin de garantir la compatibilité avec les versions antérieures, le contenu envoyé à vos canaux existants n'est pas modifié.    

Si vous possédez déjà des canaux de notification (Slack ou URL de rappel), pour commencer à utiliser la nouvelle version du contenu :

1. Pour une URL de rappel, assurez-vous que votre implémentation peut accepter le nouveau contenu.
2. Créez un canal de notification (les nouveaux canaux sont toujours créés avec la dernière version de canal).
3. Testez le bon fonctionnement du nouveau canal.
4. Supprimez l'ancien canal.

Pour connaître les versions de canal, consultez la [documentation d'API](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Exemples
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Apprenez comment créer des anomalies GitHub pour des notifications relatives à des certificats qui arrivent à expiration.
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Apprenez comment créer des incidents PagerDuty pour des notifications relatives à des certificats qui arrivent à expiration.
* [How to validate a domain using a Callback URL and a Cloud Function action ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
