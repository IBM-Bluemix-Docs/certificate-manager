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

# 配置通知
{: #configuring-notifications}

{{site.data.keyword.cloudcerts_full}} 可以向您傳送有關憑證生命週期事件的通知。這包括在憑證到期之前更新憑證的提醒，以及在憑證備妥時部署憑證的提醒。若要取得 {{site.data.keyword.cloudcerts_short}} 傳送的通知，可以設定通知頻道。可以指定 Slack Webhook、回呼 URL 或這兩者的任意組合。
{: shortdesc}

向 {{site.data.keyword.cloudcerts_short}} [訂購憑證](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates)時，也會使用通知特性。若要證明您擁有要為其要求憑證的網域，{{site.data.keyword.cloudcerts_short}} 會將盤查作為通知傳送到回呼 URL。盤查是一種文字記錄，應將其放入在其中登錄網域的網域名稱系統 (DNS) 服務中。文字記錄準備妥當後，盤查被視為是完整的。由於盤查是作為通知傳送到回呼 URL 的，因此您能夠透過執行程式碼來使網域驗證處理程序自動化，以回應通知事件。

## 用於監視憑證到期的通知
{: #notifications-monitoring-certificate-expiration}

憑證通常在設定的時間內有效。當您使用的憑證到期時，您可能會遇到應用程式的關閉時間。為避免產生關閉時間，您可以配置 {{site.data.keyword.cloudcerts_short}} 以傳送有關憑證即將到期的通知，以便提醒您按時更新憑證。

在將更新版本的憑證重新匯入到 {{site.data.keyword.cloudcerts_short}} 以代替即將到期的憑證時，您也將收到警示。這是為了提醒您將其部署到 SSL/TLS 終止點。有關重新匯入憑證的此通知僅傳送到[頻道 V2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) 中的頻道。


**何時會收到通知？**   
根據您上傳至 {{site.data.keyword.cloudcerts_short}} 的憑證的到期日，您會在憑證到期之前 90、60、30、10 和 1 天收到通知。此外，您也會收到關於到期憑證的每日通知。每日通知會從您的憑證到期之後的第一天開始。

您必須更新憑證，並將此憑證重新匯入至 {{site.data.keyword.cloudcerts_short}} 取代舊有憑證，才能停止傳送通知。在重新匯入憑證時，您將收到重新匯入憑證的通知以提醒您重新部署憑證。

**我有哪些配置通知的選項？**   您可以使用 Slack Webhook 或使用您喜歡的任何回呼 URL 向 Slack 傳送通知。

## 與訂購憑證相關的通知
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} 會在您向 {{site.data.keyword.cloudcerts_short}} 訂購的憑證簽發時或順利更新時通知您。如果訂購失敗或更新失敗，也會通知您。
{: shortdesc}

設定回呼 URL 通知頻道，並能夠處理與網域驗證相關的事件是訂購和更新憑證的必要條件。訂購憑證時，{{site.data.keyword.cloudcerts_short}} 會向回呼 URL 傳送盤查 TXT 記錄，用於證明您擁有要為其要求憑證的網域。要求更新憑證時，也會傳送盤查 TXT 記錄。 


## 設定 Slack Webhook
{: #setup-callback}

若要設定 Slack Webhook，請完成下列步驟：

1. 註冊 [Slack](https://slack.com/) 並設定工作區。
2. 建立 Slack 頻道，您可以在這裡張貼通知。
3. [設定 Webhook](https://api.slack.com/incoming-webhooks) 以用於 Slack 頻道。

## 設定回呼 URL
{: #callback}

若要觸發團隊的更新處理程序，您可以使用回呼 URL 以將通知公佈到使用的工具。例如，您可以傳送通知以便報告至 PagerDuty、自動在 GitHub 開啟問題，或是觸發更新 Script。您還可以自動觸發憑證部署，以回應在成功重新匯入或簽發憑證時傳送的通知。
{: shortdesc}

回呼 URL 是訂購憑證的先決條件。
{: note}

**重要事項：**回呼 URL 端點必須符合下列需求才能用於 {{site.data.keyword.cloudcerts_short}}：
* 端點必須使用 HTTPS 通訊協定。
* 端點不得要求 HTTP 標頭。這項需求包含授權標頭。
* 端點必須傳回 `200 OK` 狀態碼，以指出成功遞送通知。

### 通知格式
{: #notification_format}

傳送到回呼 URL 的通知是使用下列格式的實例非對稱金鑰簽署的 JSON 文件。

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

在您解碼並驗證有效負載之後，內容是[根據頻道版本](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)的 JSON 字串。


## 配置通知頻道
{: #adding-channel}

建立 Slack Webhook 或回呼 URL 後，可以將其新增到 {{site.data.keyword.cloudcerts_short}} 以開始接收有關憑證到期、已重新匯入憑證、已簽發憑證以及網域驗證盤查的通知。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} 會將您配置的端點加密，以便安全地儲存它們。
{: important}

若要新增通知頻道，請完成下列步驟：

1. 在服務詳細資料頁面上的導覽，按一下**設定**。
2. 開啟**通知**標籤。
3. 按一下**新增通知頻道**。
4. 選擇您要使用的通知頻道類型。
5. 輸入要向其傳送通知的 Webhook 或回呼 URL。
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

    儲存 Slack Webhook 時，{{site.data.keyword.cloudcerts_short}} 會自動向已配置的 Slack 頻道傳送確認通知。請檢查您的 Slack 頻道，以驗證您已收到此通知。
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

從 {{site.data.keyword.cloudcerts_short}} 傳送到回呼 URL 的每個 HTTP 有效負載都會根據 JWT 標準使用非對稱金鑰組自動簽署。  
{: shortdesc}

對於每個 {{site.data.keyword.cloudcerts_short}} 實例，會產生私密和公開金鑰，不會在其他 {{site.data.keyword.cloudcerts_short}} 實例之間共用。私密金鑰用來簽署 HTTP 有效負載，而您可以使用公開金鑰驗證有效負載確實是由 {{site.data.keyword.cloudcerts_short}} 產生，且未遭到第三方變更。

若要下載公開金鑰，請完成下列步驟：

1. 從服務詳細資料頁面上的導覽，按一下**設定**。
2. 開啟**通知**標籤。
3. 按一下**下載金鑰**圖示。金鑰會下載為 PEM 檔案。

## 頻道版本
{: #channel-versions}

隨著 Certificate Manager 的發展，我們可能會不定期修改通知有效負載結構的格式。為確保與更早版本的相容性，傳送到現有頻道的有效負載不會進行變更。   

如果您有現有的通知頻道（Slack 或回呼 URL），若要開始取得新版本的有效負載，請：

1. 確定您的實作可以接受回呼 URL 的新有效負載。
2. 建立新的通知頻道（一律會使用最新的頻道版本建立新頻道）。
3. 測試新頻道運作正確。
4. 刪除舊頻道。

如需頻道版本的資訊，請參閱 [API 文件](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions)。

## 範例
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   了解如何為到期憑證通知建立 GitHub 問題。
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   瞭解如何建立 PagerDuty 突發事件以獲取憑證到期通知。
* [如何使用回呼 URL 和 Cloud Functions 動作驗證網域 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
