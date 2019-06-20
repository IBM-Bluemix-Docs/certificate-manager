---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

keywords: certificates, SSL, TLS, activity tracker,

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

# Activity Tracker 事件  
{: #at_events}

使用 {{site.data.keyword.at_full}} 服務可追蹤使用者及應用程式與 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.cloudcerts_long}} 服務互動的情形。
{:shortdesc}

{{site.data.keyword.at_short}} 服務記錄了由使用者起始且變更 {{site.data.keyword.cloud_notm}} 中服務狀態的活動。例如，匯入憑證時，會產生事件。如需相關資訊，請參閱 [{{site.data.keyword.at_short}} 文件](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)。

下表列出在呼叫時會產生事件的 API 方法。

<table>
  <caption>表 1. 可產生事件的動作</caption>
  <tr>
    <th>動作</th>
	  <th>說明</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>匯入憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>訂購憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>重新匯入憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>取得憑證 meta 資料。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>下載憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>列出憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>列出憑證 meta 資料。顯示憑證的詳細資料。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>搜尋憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>搜尋憑證 meta 資料。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>刪除憑證。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>更新憑證 meta 資料，例如，變更憑證的說明。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>列出通知頻道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>建立通知頻道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>停用或啟用通知頻道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>更新通知頻道的端點。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>刪除通知頻道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>測試通知頻道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>已傳送通知到通知頻道端點。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>已要求公開金鑰。</td>
  </tr>
</table>

## 尋找事件的位置
{: #at_ui}

在 {{site.data.keyword.cloudcerts_short}} 實例所在位置佈建 {{site.data.keyword.at_short}} 實例。

系統會自動將事件轉遞給佈建 {{site.data.keyword.cloudcerts_short}} 服務的相同位置中的 {{site.data.keyword.at_short}} 服務實例。

## 相關資訊
{: #info}

* *requestData_str* 欄位包含人類可讀的憑證名稱。

## 可用性
{: #at-availability}

* 目前，在**達拉斯**和**法蘭克福**位置有提供 {{site.data.keyword.at_short}} 支援。
* 對於其他位置，請佈建已淘汰之 Activity Tracker 服務的實例，直到 {{site.data.keyword.at_short}} 可用為止。
