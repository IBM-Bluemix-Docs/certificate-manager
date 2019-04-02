---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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


# A propos de {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_long}} vous permet de gérer les certificats SSL pour vos applications et vos services cloud {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Vous pouvez importer des certificats SSL que vous obtenez pour vos applications et vos services, les stocker en toute sécurité et centraliser l'affichage des certificats que vous utilisez.

Vous pouvez gérer vos certificats en procédant comme suit :

* Soyez averti avant l'expiration de vos certificats pour être sûr de pouvoir les renouveler à temps.
* Affichez les types de certificats sur vos déploiements et assurez-vous qu'ils répondent aux politiques de l'organisation.
* Recherchez les certificats que vous devez remplacer lorsque de nouvelles exigences de conformité ou de sécurité sont émises.
* Définissez les contrôles qui déterminent qui peut accéder à et gérer vos certificats.

![Diagramme d'architecture de haut niveau du service](images/high-level-architecture.png)
<caption>Figure 1. Architecture de haut niveau du service.</caption>

## Sécurité de clé privée
{: #private-key-security}

Lorsque vous importez un certificat et la clé privée correspondante dans {{site.data.keyword.cloudcerts_short}}, le service utilise un algorithme AES (Advanced Encryption Standard) 256 pour chiffrer la clé privée. {{site.data.keyword.cloudcerts_short}} sauvegarde cette clé chiffrée unique à utiliser avec votre instance de service.

## Intégrations
{: #integrations}

<table>
<caption>Tableau 1. Services {{site.data.keyword.cloud_notm}} qui utilisent {{site.data.keyword.cloudcerts_short}}</caption>
  <tr>
    <th> Service </th>
    <th> Description </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Vous pouvez facilement déployer des certificats TLS de domaine personnalisé en toute sécurité depuis {{site.data.keyword.cloudcerts_short}} vers votre cluster Kubernetes. Les administrateurs de cluster peuvent utiliser les [commandes de plug-in Kubernetes Service](/docs/containers?topic=containers-cs_cli_reference) pour mettre à jour des certificats TLS en tant que secrets Kubernetes avec un nouveau certificat sans provoquer d'interruption. Pour commencer, vérifiez les [annotations Ingress dans la documentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index) centralise les informations relatives aux services {{site.data.keyword.cloud_notm}}. Ces informations incluent notamment l'indication des certificats ayant expiré et des certificats sur le point d'expirer dans des instances de {{site.data.keyword.cloudcerts_short}} dans votre compte {{site.data.keyword.cloud_notm}}. [En savoir plus sur {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Vous pouvez utiliser [le service {{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started) pour suivre la façon dont les utilisateurs et les applications interagissent avec le service {{site.data.keyword.cloudcerts_long_notm}} dans {{site.data.keyword.cloud_notm}}. [En savoir plus sur {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).
    <p>Pour obtenir une liste des actions qui génère un événement, voir [Evénements {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Stockez vos certificats de domaine personnalisé dans le service {{site.data.keyword.cloudcerts_short}}, puis utilisez des CRN de certificat à lier à des domaines personnalisés dans {{site.data.keyword.apiconnect_short}}. [En savoir plus sur {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index).</p></td>
  </tr>
</table>

## Emplacements
{: #availability}

{{site.data.keyword.cloudcerts_short}} est disponible à Dallas, Londres, Francfort et Tokyo.



## Limites
{: #limits}

Vous pouvez télécharger un maximum de 1 000 certificats par instance.
