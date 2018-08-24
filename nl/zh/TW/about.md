---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 關於 Certificate Manager
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}} 可協助您管理 {{site.data.keyword.IBM_notm}} 雲端型應用程式及服務的 SSL 憑證。
{: shortdesc}

您可以匯入針對應用程式及服務取得的 SSL 憑證、安全地儲存它們，以及取得所要使用憑證的中央視圖。

您可以使用下列方式管理憑證：

* 在憑證到期之前收到通知，以確保您準時更新
* 檢視部署中的憑證類型，並確定它們符合組織原則
* 尋找在發出新相符性或安全需求時需要取代的憑證
* 設定您可存取及管理憑證的控制項

![高階服務架構圖](images/high-level-architecture.png)
<caption>高階服務架構。</caption>

## 私密金鑰安全
{: #private-key-security}

當您將憑證及對應私密金鑰匯入至 {{site.data.keyword.cloudcerts_short}} 時，服務會使用「進階加密標準 (AES) 256」演算法來加密私密金鑰。{{site.data.keyword.cloudcerts_short}} 會儲存這個唯一加密金鑰，以與服務實例搭配使用。

## 整合
{: #integrations}
<table>
<caption>使用 Certificate Manager 的 IBM Cloud 服務</caption>
  <tr>
    <th> 服務</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>將您的 Kubernetes 叢集自訂網域憑證儲存在 Certificate Manager 中，然後使用 IBM Cloud CLI 的 [Kubernetes 服務外掛程式指令](/docs/containers/cs_cli_reference.html)部署它們。[進一步瞭解此整合](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/)。</td>
  </tr>
  <tr>
    <td>IBM Cloud Security Advisor</td>
    <td>Security Advisor 將 IBM Cloud 服務的見解集中化，包括指出您 IBM Cloud 帳戶中，Certificate Manager 實例裡已過期和即將過期的憑證。[進一步瞭解 Security Advisor](/docs/services/security-advisor/index.html#index)</td>
  </tr><tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>使用 {{site.data.keyword.cloudaccesstrailfull}} 服務可追蹤使用者及應用程式與 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.cloudcerts_long}} 服務互動的情形。[進一步瞭解 {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。
    <p>若要取得產生事件的動作清單，請參閱 [{{site.data.keyword.cloudaccesstrailshort}} 事件](/docs/services/certificate-manager/at_events.html#at_events)。</p></td>
  </tr>
</table>

## 地區
{: #availability}

只有在美國南部地區才能使用 {{site.data.keyword.cloudcerts_short}}。

