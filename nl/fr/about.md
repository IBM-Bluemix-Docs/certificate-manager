---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

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

# A propos de {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_full}} vous aide à obtenir, stocker et gérer les certificats SSL que vous utilisez pour des déploiements {{site.data.keyword.cloud_notm}} ou d'autres déploiements cloud ou sur site.
{: shortdesc}

Vous pouvez importer des certificats SSL que vous obtenez pour vos applications et vos services, les stocker en toute sécurité et centraliser l'affichage des certificats que vous utilisez. Ou bien, vous pouvez commander des certificats publics via Certificate Manager auprès d'autorités de certification prises en charge.

Vous pouvez gérer vos certificats en procédant comme suit :

* Soyez averti avant l'expiration de vos certificats pour être sûr de pouvoir les renouveler à temps.  
* Utilisez des notifications pour déclencher le renouvellement automatique de certificat.  
* Affichez les types de certificats sur vos déploiements et assurez-vous qu'ils répondent aux politiques de l'organisation.  
* Recherchez les certificats que vous devez remplacer lorsque de nouvelles exigences de conformité ou de sécurité sont émises.  
* Définissez les contrôles qui déterminent qui peut accéder à et gérer vos certificats.
* Commandez de nouveaux certificats publics


![Diagramme d'architecture de haut niveau du service](images/high-level-architecture.png)
<caption>Figure 1. Architecture de haut niveau du service.</caption>


## Sécurité de clé privée
{: #private-key-security}

Lorsque vous importez ou commandez un certificat dans {{site.data.keyword.cloudcerts_short}}, le service utilise un algorithme AES (Advanced Encryption Standard) 256 pour chiffrer la clé privée. {{site.data.keyword.cloudcerts_short}} sauvegarde cette clé chiffrée unique à utiliser avec votre instance de service.

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
    <td>Vous pouvez facilement déployer des certificats TLS de domaine personnalisé en toute sécurité depuis {{site.data.keyword.cloudcerts_short}} vers votre cluster Kubernetes. Les administrateurs de cluster peuvent utiliser les [commandes de plug-in Kubernetes Service](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) pour mettre à jour des certificats TLS en tant que secrets Kubernetes avec un nouveau certificat sans provoquer d'interruption. Pour commencer, vérifiez les [annotations Ingress dans la documentation](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) centralise les informations relatives aux services {{site.data.keyword.cloud_notm}}. Ces informations incluent notamment l'indication des certificats ayant expiré et des certificats sur le point d'expirer dans des instances de {{site.data.keyword.cloudcerts_short}} dans votre compte {{site.data.keyword.cloud_notm}}. [En savoir plus sur {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>Vous pouvez utiliser [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) pour suivre la façon dont utilisateurs et applications interagissent avec le service {{site.data.keyword.cloudcerts_long_notm}} dans {{site.data.keyword.cloud_notm}}.
    <p>Pour obtenir la liste des actions qui génèrent un événement, voir [Evénements {{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Stockez vos certificats de domaine personnalisé dans le service {{site.data.keyword.cloudcerts_short}}, puis utilisez des CRN de certificat à lier à des domaines personnalisés dans {{site.data.keyword.apiconnect_short}}. [En savoir plus sur {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index).</p></td>
  </tr>
</table>

## Disponibilité
{: #availability}

{{site.data.keyword.cloudcerts_short}} est disponible à Dallas, Londres, Francfort et Tokyo.



## Limites
{: #limits}

Vous pouvez télécharger un maximum de 1 000 certificats par instance.

## Conformité et normes
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} terminé avec succès plusieurs certifications et audits, et satisfait plusieurs normes importantes.

### Loi HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} satisfait les contrôles IBM requis qui sont équivalents à la loi Health Insurance Portability and Accountability Act (HIPAA) de 1996 ainsi que les exigences Security and Privacy Rule.

### Organisation internationale de normalisation (ISO)
{: #compliance-iso}

* Certificat {{site.data.keyword.IBM_notm}} Services (PaaS et SaaS) - ISO 27001

### Règlement général sur la protection des données (RGPD)
{: #compliance-gdpr}

Le RGPD cherche à créer un cadre législatif harmonisé sur la protection des données dans l'Union européenne et vise à redonner aux citoyens le contrôle de leurs données personnelles, tout en imposant des règles strictes à ceux chargés d'héberger et de "traiter" ces données, partout dans le monde. Ce règlement introduit également des règles en matière de libre circulation des données personnelles au sein et en dehors de l'UE. Pour plus d'informations, voir la [déclaration de confidentialité d'IBM](https://www.ibm.com/privacy/).
