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

# 入門指導教學
{: #getting-started}

{{site.data.keyword.cloudcerts_full}} 可協助您為 {{site.data.keyword.cloud_notm}} 應用程式取得、儲存和管理 SSL 憑證。  
若要開始使用，請完成下列步驟來建立新的 {{site.data.keyword.cloudcerts_short}} 服務實例。
{: shortdesc}

若要透過 {{site.data.keyword.cloud_notm}} 主控台來建立實例，請執行下列動作：

1.	在 {{site.data.keyword.cloud_notm}} 型錄中，選取 **{{site.data.keyword.cloudcerts_short}}**。
2.	提供服務實例名稱，或使用預設名稱。
3.	按一下**建立**。
4.	若要將您組織的憑證匯入至 **{{site.data.keyword.cloudcerts_short}}**，請按一下**匯入憑證**。
5.	若要訂購新憑證，請按一下**訂購憑證**。

<br/>
若要透過 [{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli) 來建立實例，請執行下列動作：

1. 登入到 {{site.data.keyword.cloud_notm}}，然後按照螢幕上的指示進行操作。

   ```
   ibmcloud login
   ```

2. 建立實例。

   ```
   ibmcloud resource service-instance-create "My Certificate Manager instance" cloudcerts free us-south
   ```

   - 將 **My Certificate Manager instance** 取代為您選擇的實例名稱。
   - 將 **us-south** 取代為 **us-south**（達拉斯）、**eu-gb**（倫敦）、**eu-de**（法蘭克福）或 **jp-tok**（東京）。

<br/>
[進一步瞭解](/docs/services/certificate-manager?topic=certificate-manager-about-certificate-manager#about-certificate-manager)有關可從 {{site.data.keyword.cloudcerts_short}} 取得的功能的資訊，並[在 {{site.data.keyword.IBM_notm}} Developer 中提供使用者意見](/docs/services/certificate-manager?topic=certificate-manager-troubleshooting#getting-help-and-support)，以隨著 {{site.data.keyword.cloudcerts_short}} 的不斷演化而對其進行增強。若要瞭解有關服務中新增內容的資訊，請參閱[版本注意事項](/docs/services/certificate-manager?topic=certificate-manager-release-notes#release-notes)。
{: note}
