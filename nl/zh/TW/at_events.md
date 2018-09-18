---

copyright:
  years: 2018
lastupdated: "2018-08-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}} 事件  
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服務可追蹤使用者及應用程式與 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.cloudcerts_long}} 服務互動的情形。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服務記錄了由使用者起始且變更 {{site.data.keyword.Bluemix_notm}} 中服務狀態的活動。如需相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。例如，當您匯入憑證時，會產生 {{site.data.keyword.cloudaccesstrailshort}} 事件。

下表列出在呼叫時會產生事件的 API 方法：

<table>
  <caption>產生事件的動作</caption>
  <tr>
    <th>動作</th>
	  <th>說明</th>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>匯入由第三方憑證管理中心發出的憑證。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.download</td>
	  <td>下載憑證。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.read</td>
	  <td>列出憑證。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.read</td>
	  <td>列出憑證 meta 資料。顯示憑證的詳細資料。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>搜尋憑證。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>搜尋憑證 meta 資料。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>刪除憑證。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate-metadata.update</td>
	  <td>更新憑證 meta 資料，例如，變更憑證的說明。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channels.list</td>
	  <td>列出通知頻道。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channel.create</td>
	  <td>建立通知頻道。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channel.state</td>
	  <td>停用或啟用通知頻道。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channel.update</td>
	  <td>更新通知頻道的端點。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channel.delete</td>
	  <td>刪除通知頻道。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channel.test</td>
	  <td>測試通知頻道。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification.sent</td>
	  <td>已傳送通知到通知頻道端點。</td>
  </tr>
  <tr>
    <td>cloudcerts.notification-channels-publickey.read</td>
	  <td>已要求公開金鑰。</td>
  </tr>
</table>

## 尋找事件的位置
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件提供於 {{site.data.keyword.cloudaccesstrailshort}} **帳戶網域**中，後者提供於產生事件的 {{site.data.keyword.Bluemix_notm}} 地區。

{{site.data.keyword.cloudaccesstrailshort}} 事件會自動轉遞給佈建 {{site.data.keyword.cloudcerts_short}} 服務之相同地區的 {{site.data.keyword.cloudaccesstrailshort}} 服務。

## 相關資訊
{: #info}

*requestData_str* 欄位包含人類可讀的憑證名稱。
