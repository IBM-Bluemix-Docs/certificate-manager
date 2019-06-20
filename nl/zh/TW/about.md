---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

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

# 關於 {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_full}} 可協助您為 {{site.data.keyword.IBM_notm}} 雲端型應用程式取得、儲存和管理 SSL 憑證。
{: shortdesc}

您可以匯入針對應用程式及服務取得的 SSL 憑證、安全地儲存它們，以及取得所要使用憑證的中央視圖。或者，您可以透過 Certificate Manager 向支援的 CA 訂購公用憑證。

您可以使用下列方式管理憑證：

* 在憑證到期之前收到通知，以確保您準時更新  
* 使用通知觸發憑證自動更新  
* 檢視部署中的憑證類型，並確定它們符合組織原則  
* 尋找在發出新相符性或安全需求時需要取代的憑證  
* 設定您可存取及管理憑證的控制項
* 訂購新的公用憑證


![高階服務架構圖](images/high-level-architecture.png)
<caption>圖 1. 高階服務架構。</caption>


## 私密金鑰安全
{: #private-key-security}

將憑證匯入到 {{site.data.keyword.cloudcerts_short}} 或在其中訂購憑證時，該服務將使用進階加密標準 (AES) 256 演算法來加密私密金鑰。{{site.data.keyword.cloudcerts_short}} 會儲存這個唯一加密金鑰，以與服務實例搭配使用。

## 整合
{: #integrations}

<table>
<caption>表 1. 使用 {{site.data.keyword.cloudcerts_short}} 的 {{site.data.keyword.cloud_notm}} 服務</caption>
  <tr>
    <th> 服務</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>您可以輕鬆又安全地將 {{site.data.keyword.cloudcerts_short}} 的自訂網域 TLS 憑證部署至您的 Kubernetes 叢集。叢集管理者可以使用 [Kubernetes 服務外掛程式指令](/docs/containers?topic=containers-cs_cli_reference)以新憑證將 TLS 憑證更新為 Kubernetes 密碼，而不會造成運作中斷。若要開始使用，請查閱[文件中的 Ingress 註釋](/docs/containers?topic=containers-ingress_annotation#https-auth)。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) 會集中 {{site.data.keyword.cloud_notm}} 服務的相關資訊。資訊會指出在您的 {{site.data.keyword.cloud_notm}} 帳戶中，{{site.data.keyword.cloudcerts_short}} 實例的已過期憑證和即將過期憑證。[進一步瞭解 {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started)。
    </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>您可以使用 [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) 來追蹤使用者和應用程式如何與 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.cloudcerts_long_notm}} 服務互動。
    <p>若要取得產生事件的動作清單，請參閱 [{{site.data.keyword.at_short}} 事件](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events)。</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>請將您的自訂網域憑證儲存在 {{site.data.keyword.cloudcerts_short}} 服務，然後使用憑證 CRN 在 {{site.data.keyword.apiconnect_short}} 中與自訂網域連結。[進一步瞭解 {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index)。
    </p></td>
  </tr>
</table>

## 可用性
{: #availability}

{{site.data.keyword.cloudcerts_short}} 在達拉斯、倫敦、法蘭克福和東京位置中可用。



## 限制
{: #limits}

每個實例可以上傳最多 1000 個憑證。

## 合規性與標準
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} 已順利完成多項憑證和審核，並符合多種重要標準。

### HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} 符合必要的 IBM 控制措施，這些措施與 1996 年頒佈的醫療保險轉移和責任法 (HIPAA) 中的安全和隱私權規則要求相一致。

### 國際標準組織 (ISO)
{: #compliance-iso}

* {{site.data.keyword.IBM_notm}} 服務（PaaS 和 SaaS）憑證 - ISO 27001

### 一般資料保護規範 (GDPR)
{: #compliance-gdpr}

GDPR 嘗試建立跨歐盟的協調資料保護法律架構，而且目的是將居民的個人資料控制權返還給居民，同時對於在全球任何位置管理及「處理」此資料的人員強制施行嚴格的規則。此「規範」也會建立與在歐盟內外部自由移動個人資料有關的規則。如需相關資訊，請參閱 [IBM 隱私權聲明](https://www.ibm.com/privacy/)。
