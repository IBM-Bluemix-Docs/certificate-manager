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

# Guía de aprendizaje de iniciación
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} le ayuda a obtener, almacenar y gestionar certificados SSL para las apps basadas en nube de {{site.data.keyword.IBM_notm}}.  
Para empezar, cree una nueva instancia de servicio de {{site.data.keyword.cloudcerts_short}} siguiendo estos pasos.
{: shortdesc}

Para crear una instancia desde la consola de {{site.data.keyword.cloud_notm}}:

1.	En el catálogo de {{site.data.keyword.cloud_notm}}, seleccione **{{site.data.keyword.cloudcerts_short}}**.
2.	Dé un nombre a la instancia de servicio, o utilice el nombre preestablecido.
3.	Pulse **Crear**.
4.	Para importar los certificados de la organización en **{{site.data.keyword.cloudcerts_short}}**, pulse **Importar certificado**.
5.	Para solicitar un nuevo certificado, pulse **Solicitar certificado**.

<br/>
Para crear una instancia desde la [CLI de {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli):

1. Inicie una sesión en {{site.data.keyword.cloud_notm}} y siga las instrucciones de la pantalla.

   ```
   ibmcloud login
   ```

2. Cree una instancia.

   ```
   ibmcloud resource service-instance-create "Mi instancia del gestor de certificados" cloudcerts free us-south
   ```

   - Sustituya **Mi instancia del gestor de certificados** por el nombre de instancia que elija.
   - Sustituya **us-south** por **us-south** (Dallas), **eu-gb** (Londres), **eu-de** (Frankfurt) o **jp-tok** (Tokio).

<br/>
Puede [obtener más información](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) sobre lo que ofrece {{site.data.keyword.cloudcerts_short}}, y [enviar comentarios de los usuarios en {{site.data.keyword.IBM_notm}} Developer](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) para mejorar {{site.data.keyword.cloudcerts_short}} a medida que se desarrolla. Para ver las novedades en el servicio, consulte [Notas del release](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}
