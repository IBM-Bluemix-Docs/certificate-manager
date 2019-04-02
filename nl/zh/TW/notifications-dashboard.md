---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-07"

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

# 配置通知
{: #configuring-notifications}

憑證通常只會在一段設定的時間量內有效。當您使用的憑證到期時，您可能會遇到應用程式的關閉時間。若要避免運作中斷，您可以配置 {{site.data.keyword.cloudcerts_full}}，以將即將過期的憑證相關通知傳送給您，以便提醒您及時更新憑證。

當您將憑證的更新版本重新匯入至 {{site.data.keyword.cloudcerts_short}} 以取代到期的憑證時，您將會收到警示，以讓您記得同時也將其部署至 SSL/TLS 終止點。有關重新匯入憑證的此項通知將僅傳送至[頻道第 2 版](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)的頻道。
{: shortdesc}

**我何時會收到通知？**   根據您上傳至 {{site.data.keyword.cloudcerts_full_notm}} 的憑證的到期日，您會在憑證到期之前 90、60、30、10 和 1 天收到通知。此外，您也會收到關於到期憑證的每日通知。每日通知會從您的憑證到期之後的第一天開始。

您必須更新憑證，並將此憑證重新匯入至 {{site.data.keyword.cloudcerts_full_notm}} 取代舊有憑證，才能停止傳送通知。重新匯入憑證時，會收到已重新匯入憑證的通知，提醒您重新部署該憑證。

**我有哪些配置通知的選項？**   您可以使用 Slack Webhook 或使用您喜歡的任何回呼 URL 傳送通知給 Slack。

## 設定 Slack Webhook
{: #setup-callback}

若要設定 Slack Webhook，請完成下列步驟：

1. 註冊 [Slack](https://slack.com/) 並設定工作區。
2. 建立 Slack 頻道，您可以在這裡張貼通知。
3. 為 Slack 頻道[設定 Webhook](https://api.slack.com/incoming-webhooks)。

## 設定回呼 URL
{: #callback}

若要觸發您團隊的更新處理程序，您可以使用回呼 URL，將通知張貼至您使用的工具。例如，您可以傳送通知以便報告至 PagerDuty、自動在 GitHub 開啟問題，或是觸發更新 Script。  
{: shortdesc}

**重要事項：**您的回呼 URL 端點必須符合下列需求，才能與 {{site.data.keyword.cloudcerts_short}} 搭配使用：
* 端點必須使用 HTTPS 通訊協定。
* 端點不得要求 HTTP 標頭。這項需求包含授權標頭。
* 端點必須傳回 `200 OK` 狀態碼，以指出成功遞送通知。

### 通知格式
{: #notification_format}

傳送到回呼 URL 的通知，是使用下列格式的實例非對稱金鑰所簽署的 JSON 文件。

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

在您解碼並驗證有效負載之後，內容是[根據頻道版本](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)的 JSON 字串。

## 配置通知頻道
{: #adding-channel}

在建立 Slack Webhook 或回呼 URL 之後，請將它新增至 {{site.data.keyword.cloudcerts_short}} 以開始接收關於到期憑證和重新匯入之憑證的通知。{{site.data.keyword.cloudcerts_short}} 會加密端點並安全地儲存它。
{: shortdesc}

若要新增通知頻道，請完成下列步驟：

1. 在服務詳細資料頁面上的導覽，按一下**設定**。
2. 開啟**通知**標籤。
3. 按一下**新增通知頻道**。
4. 選擇您要使用的通知頻道類型。
5. 輸入您要傳送通知到該處的 Webhook 或回呼 URL。
6. 按一下**儲存**。會顯示配置的摘要。

   **輸出範例**

   <table>
   <caption>表 1. 通知頻道的相關資訊</caption>
   <thead>
    <th> 元件</th>
    <th> 說明</th>
   </thead>
   <tbody>
   <tr>
    <td>類型</td>
    <td>通知頻道類型：<i>Slack</i> 或<i>回呼 URL</i></td>
   </tr>
   <tr>
    <td>端點</td>
    <td>通知傳送至的通知頻道端點。</td>
   </tr>
   <tr>
    <td>啟用切換</td>
    <td>通知頻道狀態。如果設為已停用，則不會傳送任何通知。</td>
   </tr>
   <tr>
    <td>測試連線按鈕</td>
    <td>傳送測試通知到您配置的頻道。</td>
   </tr>
    <tr>
      <td>點功能表</td>
      <td>您可以對頻道執行的可用動作：<i>編輯</i> 或<i>刪除</i></td>
    </tr>
    </tbody>
    </table>

    當您儲存 Slack Webhook 時，{{site.data.keyword.cloudcerts_short}} 會自動傳送確認通知到您配置的 Slack 頻道。請檢查您的 Slack 頻道，以驗證您已收到此通知。
    {: tip}
7. （選用）重複這些步驟以新增其他通知頻道。

## 測試通知頻道
{: #testing-channel}

您可以測試通知頻道，以確保您的通知頻道配置正確。
{: shortdesc}

開始之前，請[配置通知頻道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

若要測試通知頻道，請完成下列步驟：

1. 在服務詳細資料頁面上的導覽，按一下**設定**。
2. 找到通知頻道，然後按一下**測試連線**。
3. 驗證您已在配置的頻道中收到通知。

## 更新通知頻道
{: #updating-channel}

您可以更新通知頻道配置、停用或啟用通知，或從 {{site.data.keyword.cloudcerts_short}} 刪除通知頻道。
{: shortdesc}

開始之前，請[配置通知頻道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

若要更新通知頻道，請完成下列步驟：

1. 在服務詳細資料頁面上的導覽，按一下**設定**。
2. 選取**通知**標籤。
3. 從下列選項進行選擇：
   * 若要停用或啟用頻道的通知，請將開關設為**停用**或**啟用**。
   * 若要更新頻道的設定，請從動作功能表選取**編輯**。
   * 若要刪除通知頻道，請從動作功能表選取**刪除**。

## 驗證回呼 URL 的 HTTP 有效負載
{: #verify-callback}

從 {{site.data.keyword.cloudcerts_short}} 傳送到回呼 URL 的每個 HTTP 有效負載，會根據 JWT 標準，使用非對稱金鑰配對自動進行簽署。  
{: shortdesc}

對於每個 {{site.data.keyword.cloudcerts_short}} 實例，會產生私密和公開金鑰，不會在其他 {{site.data.keyword.cloudcerts_short}} 實例之間共用。私密金鑰用來簽署 HTTP 有效負載，而您可以使用公開金鑰驗證有效負載確實是由 {{site.data.keyword.cloudcerts_short}} 產生，且未遭到第三方變更。

若要下載公開金鑰，請完成下列步驟：

1. 從服務詳細資料頁面上的導覽，按一下**設定**。
2. 開啟**通知**標籤。
3. 按一下**下載金鑰**圖示。金鑰會下載為 PEM 檔案。

## 頻道版本
{: #channel-versions}

隨著 Certificate Manager 的發展，我們可能會不定期修改通知有效負載結構的格式。為了確保舊版相容性，傳送至現有頻道的有效負載將不會改變。   

如果您有現有的通知頻道（Slack 或回呼 URL），若要開始取得新版本的有效負載，請：
1. 確定您的實作可以接受回呼 URL 的新有效負載。
2. 建立新的通知頻道（一律會使用最新的頻道版本建立新頻道）。
3. 測試新頻道運作正確。
4. 刪除舊頻道。

針對「頻道版本」，請參閱 [API 文件](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions)。

## 範例
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   了解如何為到期憑證通知建立 GitHub 問題。
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   了解如何為到期憑證通知建立 PagerDuty 突發事件問題。
