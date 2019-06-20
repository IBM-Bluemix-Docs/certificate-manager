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

# Esercitazione introduttiva 
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} ti aiuta ad ottenere, archiviare e gestire i certificati SSL per le tue applicazioni basate sul cloud {{site.data.keyword.IBM_notm}}.  
Inizia creando una nuova istanza del servizio {{site.data.keyword.cloudcerts_short}} completando la seguente procedura.
{: shortdesc}

Per creare un'istanza dalla console {{site.data.keyword.cloud_notm}}:

1.	Nel catalogo {{site.data.keyword.cloud_notm}}, seleziona **{{site.data.keyword.cloudcerts_short}}**.
2.	Fornisci un nome alla tua istanza del servizio o utilizza il nome predefinito.
3.	Fai clic su **Crea**.
4.	Per importare i certificati della tua organizzazione in **{{site.data.keyword.cloudcerts_short}}**, fai clic su **Importa certificati**.
5.	Per ordinare un nuovo certificato, fai clic su **Ordina certificato**.

<br/>
Per creare un'istanza dalla [CLI {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli):

1. Accedi a {{site.data.keyword.cloud_notm}} e segui le istruzioni a schermo.

   ```
   ibmcloud login
   ```

2. Crea un'istanza.

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - Sostituisci **My Certificate Manager instance** con il nome dell'istanza di tua scelta.
   - Sostituisci **us-south** con **us-south** (Dallas), **eu-gb** (Londra), **eu-de** (Francoforte) o **jp-tok** (Tokyo).

<br/>
[Ulteriori informazioni](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) su cosa ricevi da {{site.data.keyword.cloudcerts_short}} e [fornisci il feedback utente in {{site.data.keyword.IBM_notm}} Developer](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) per migliorare {{site.data.keyword.cloudcerts_short}} e il suo sviluppo. Per informazioni sulle novità nel servizio, consulta le [Note sulla release](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}
