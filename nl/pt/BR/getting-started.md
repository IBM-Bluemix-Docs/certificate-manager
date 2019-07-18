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

# Tutorial de Introdução
{: #getting-started}

O {{site.data.keyword.cloudcerts_full}} o ajuda a obter, armazenar e gerenciar certificados SSL para seus apps baseados em {{site.data.keyword.cloud_notm}}.  
Comece criando uma nova instância de serviço do {{site.data.keyword.cloudcerts_short}} concluindo as etapas a seguir.
{: shortdesc}

Para criar uma instância por meio do console do {{site.data.keyword.cloud_notm}}:

1.	No catálogo do {{site.data.keyword.cloud_notm}}, selecione **{{site.data.keyword.cloudcerts_short}}**.
2.	Dê à sua instância de serviço um nome ou use o nome predefinido.
3.	Clique em **Criar**.
4.	Para importar certificados de sua organização em **{{site.data.keyword.cloudcerts_short}}**, clique em
**Importar certificado**.
5.	Para pedir um novo certificado, clique em **Pedir certificado**.

<br/>
Para criar uma instância por meio da [CLI do {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli):

1. Efetue login no {{site.data.keyword.cloud_notm}} e siga as instruções na tela.

   ```
   ibmcloud login
   ```

2. Criar uma instância.

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - Substitua **Minha instância do Certificate Manager** pela sua opção de nome da instância.
   - Substitua **us-south** por **us-south** (Dallas), **eu-gb** (Londres), **eu-de** (Frankfurt) ou **jp-tok** (Tóquio).

<br/>
[Saiba mais](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager) sobre o que o {{site.data.keyword.cloudcerts_short}} oferece para você e [forneça feedback de usuário no {{site.data.keyword.IBM_notm}} Developer](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support) para aprimorar o {{site.data.keyword.cloudcerts_short}} conforme ele se desenvolve. Para descobrir o que há de novo no serviço, consulte as [Notas sobre a liberação](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes).
{: note}
