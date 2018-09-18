---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# A propos de Certificate Manager
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}} vous permet de gérer les certificats SSL pour vos applications et vos services cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Vous pouvez importer des certificats SSL que vous obtenez pour vos applications et vos services, les stocker en toute sécurité et centraliser l'affichage des certificats que vous utilisez.

Vous pouvez gérer vos certificats en procédant comme suit :

* Soyez averti avant l'expiration de vos certificats pour être sûr de pouvoir les renouveler à temps.
* Affichez les types de certificats sur vos déploiements et assurez-vous qu'ils répondent aux politiques de l'organisation.
* Recherchez les certificats que vous devez remplacer lorsque de nouvelles exigences de conformité ou de sécurité sont émises.
* Définissez les contrôles qui déterminent qui peut accéder à et gérer vos certificats.

![Diagramme d'architecture de haut niveau du service](images/high-level-architecture.png)
<caption>Architecture de haut niveau du service.</caption>

## Sécurité de clé privée
{: #private-key-security}

Lorsque vous importez un certificat et la clé privée correspondante dans {{site.data.keyword.cloudcerts_short}}, le service utilise un algorithme AES (Advanced Encryption Standard) 256 pour chiffrer la clé privée. {{site.data.keyword.cloudcerts_short}} sauvegarde cette clé chiffrée unique à utiliser avec votre instance de service.

## Intégrations
{: #integrations}
<table>
<caption>Services IBM Cloud utilisant Certificate Manager</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Stockez vos certificats de domaine personnalisé de cluster Kubernetes dans Certificate Manager, puis déployez-les à l'aide de [commandes du plug-in Kubernetes Service](/docs/containers/cs_cli_reference.html) pour l'interface CLI IBM Cloud. [En savoir plus sur cette intégration](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>IBM Cloud Security Advisor</td>
    <td>Security Advisor centralise les analyses des services IBM Cloud, notamment l'indication des certificats arrivés ou sur le point d'arriver à expiration dans des instances de Certificate Manager dans votre compte IBM Cloud. [En savoir plus sur Security Advisor](/docs/services/security-advisor/index.html#index)</td>
  </tr><tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour suivre comment les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long}} dans {{site.data.keyword.Bluemix}}. [En savoir plus sur {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).
    <p>Pour obtenir une liste des actions qui génère un événement, voir [Evénements {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager/at_events.html#at_events).</p></td>
  </tr>
</table>

## Régions
{: #availability}
{{site.data.keyword.cloudcerts_short}} est disponible dans le Sud des Etats-Unis et au Royaume-Uni.

