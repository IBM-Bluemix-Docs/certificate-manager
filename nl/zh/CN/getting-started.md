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

# 入门教程
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} 可帮助您为 {{site.data.keyword.IBM_notm}} 基于云的应用程序获取、存储和管理 SSL 证书。
  
首先，完成以下步骤来创建新的 {{site.data.keyword.cloudcerts_short}} 服务实例。
{: shortdesc}

要通过 {{site.data.keyword.cloud_notm}} 控制台来创建实例，请执行以下操作：

1.	在 {{site.data.keyword.cloud_notm}} 目录中，选择 **{{site.data.keyword.cloudcerts_short}}**。
2.	为服务实例提供名称或使用预设名称。
3.	单击**创建**。
4.	要将组织证书导入到 **{{site.data.keyword.cloudcerts_short}}**，请单击**导入证书**。
5.	要订购新证书，请单击**订购证书**。

<br/>
要通过 [{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli) 来创建实例，请执行以下操作：

1. 登录到 {{site.data.keyword.cloud_notm}}，然后按照屏幕上的指示信息进行操作。

   ```
   ibmcloud login
   ```

2. 创建实例。

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - 将 **My Certificate Manager instance** 替换为您选择的实例名称。
   - 将 **us-south** 替换为 **us-south**（达拉斯）、**eu-gb**（伦敦）、**eu-de**（法兰克福）或 **jp-tok**（东京）。

<br/>
[了解更多](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager)有关可从 {{site.data.keyword.cloudcerts_short}} 获取的功能的信息，并[在 {{site.data.keyword.IBM_notm}} Developer 中提供用户反馈](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support)，以随着 {{site.data.keyword.cloudcerts_short}} 的不断演化而对其进行增强。要了解有关服务中新增内容的信息，请参阅[发行说明](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes)。
{: note}
