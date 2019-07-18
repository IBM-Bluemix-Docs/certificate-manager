---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

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

# Tutoriel d'initiation
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} vous aide à obtenir, stocker et gérer des certificats SSL pour vos applications basées {{site.data.keyword.cloud_notm}}.   
Commencez par la création d'une instance de service {{site.data.keyword.cloudcerts_short}} en effectuant les tâches suivantes.
{: shortdesc}

Pour créer une instance depuis la console {{site.data.keyword.cloud_notm}} :

1.	Dans le catalogue {{site.data.keyword.cloud_notm}}, sélectionnez **{{site.data.keyword.cloudcerts_short}}**.
2.	Attribuez un nom à votre instance de service ou utilisez le nom prédéfini.
3.	Cliquez sur **Créer**.
4.	Pour importer les certificats de votre organisation dans **{{site.data.keyword.cloudcerts_short}}**, cliquez sur **Importer le certificat**.
5.	Pour commander un nouveau certificat, cliquez sur **Demander un certificat**.

<br/>
Pour créer une instance depuis l'[interface CLI {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli) :

1. Connectez-vous à {{site.data.keyword.cloud_notm}} et suivez les instructions à l'écran.

   ```
   ibmcloud login
   ```

2. Créez une instance.

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - Remplacez **My Certificate Manager instance** par le nom d'instance de votre choix.
   - Remplacez **us-south** par **us-south** (Dallas), **eu-gb** (Londres), **eu-de** (Francfort), ou **jp-tok** (Tokyo).

<br/>
[Apprenez-en davantage](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) sur ce que {{site.data.keyword.cloudcerts_short}} peut vous apporter et [apportez vos commentaires dans {{site.data.keyword.IBM_notm}} Developer](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) afin d'améliorer le développement de {{site.data.keyword.cloudcerts_short}}. Pour découvrir les nouveautés du service, voir les [Notes sur l'édition](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}
