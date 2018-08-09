---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-05"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 配置到期憑證的通知
{: #configuring-notifications-for-expiring-certificates}

憑證通常只會在一段設定的時間量內有效。當您使用的憑證到期時，您可能會遇到應用程式的關閉時間。若要避免關閉時間，您可以配置 {{site.data.keyword.cloudcerts_full}}，針對即將到期的憑證傳送通知，以便您可以準時更新憑證。
{: shortdesc}

**我何時會收到通知？** </br>
根據您上傳至 {{site.data.keyword.cloudcerts_full}} 的憑證的到期日，您會在憑證到期之前 90、60、30、10 和 1 天收到通知。此外，您也會在憑證到期之後的第一天開始，收到關於到期憑證的每日通知。 

您必須更新憑證、將此憑證上傳至 {{site.data.keyword.cloudcerts_full}}，然後刪除到期憑證，才能停止繼續傳送通知。 

**我有哪些配置通知的選項？** </br>
您可以使用 Slack Webhook 或使用您喜歡的任何回呼 URL 傳送通知給 Slack。 

## 設定 Slack Webhook
{: #setup-callback}

1. 註冊 [Slack](https://slack.com/) 並設定工作區。 
2. 建立 Slack 頻道，您可以在這裡張貼通知。 
3. 為 Slack 頻道[設定 Webhook](https://api.slack.com/incoming-webhooks)。 

## 設定回呼 URL
{: #callback}

建議您使用回呼 URL 張貼通知到您日常使用的工具，以便為您的團隊觸發更新處理程序。例如，您可以傳送通知以便報告至 PagerDuty、自動在 GitHub 開啟問題，或是觸發更新 Script。  
{: shortdesc}

**重要事項：**您的回呼 URL 端點必須符合下列需求，才能與 {{site.data.keyword.cloudcerts_short}} 搭配使用： 
* 端點必須使用 HTTPS 通訊協定。
* 端點不得要求 HTTP 標頭。這項需求包含授權標頭。

### 使用回呼 URL 自動開啟 GitHub 問題 
{: #sample}

下列範例程式碼顯示在傳送 {{site.data.keyword.cloudcerts_short}} 通知時，如何針對到期的憑證建立 GitHub 問題。您可以在 {{site.data.keyword.openwhisk}} 執行此程式碼，或在不同環境使用程式碼。   
{: shortdesc}

若要在 {{site.data.keyword.openwhisk}} 執行此程式碼，請執行下列動作：

1. [在 {{site.data.keyword.openwhisk}} 建立動作](/docs/openwhisk/index.html#getting-started)。
2. 使用下列程式碼自動建立 GitHub 問題： 

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "<PERSONAL_GITHUB_TOKEN>";

    /**
     * Returns the expiration data as short date string
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Creates the issue body string
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Gets the notification body and creates a Github issue
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Decode message to get information
        const data = jwtDecode(params.data);
        try {
            // Create request options to get the public key for verification
            const keysOptions = {
                method: 'GET',
                url: `https://<CERTIFICATE_MANAGER_CLUSTER_BASE_URL>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Send request to get the public key
            const keysResponse = await request(keysOptions);

            // Verify the data using the acquired public key
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Create request options to send a new issue to Github
            // Based on Github API - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<REPO_OWNER>/<REPO_NAME>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Certificates about to expire",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Send request to Github
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}
    
如需其他 REST API 指令，請參閱 [API 文件](https://console.bluemix.net/apidocs/cloudcerts)
{: tip}


## 配置通知頻道
{: #adding-channel}

建立 Slack Webhook 或回呼 URL 之後，請將它新增至 {{site.data.keyword.cloudcerts_short}} 以開始接收關於到期憑證的通知。{{site.data.keyword.cloudcerts_short}} 會加密端點並安全地儲存它。
{: shortdesc}

若要新增通知頻道，請執行下列動作：

1. 在服務詳細資料頁面上的導覽，按一下**設定**。 
2. 開啟**通知**標籤。
3. 按一下**新增通知頻道**。 
4. 選擇您要使用的通知頻道類型。 
5. 輸入您要傳送通知到該處的 Webhook 或回呼 URL。
6. 按一下**儲存**。會顯示配置的摘要。 

   輸出範例： 
   <table>
   <caption> 通知頻道的相關資訊</caption>
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
7. 選用項目：重複這些步驟以新增其他通知頻道。 

## 測試通知頻道
{: #testing-channel}

您可以測試通知頻道，以確保您的通知頻道配置正確。
{: shortdesc}

開始之前，請[配置通知頻道](#adding-channel)。 

若要測試通知頻道，請執行下列動作： 

1. 在服務詳細資料頁面上的導覽，按一下**設定**。 
2. 找到通知頻道，然後按一下**測試連線**。
3. 驗證您已在配置的頻道中收到通知。 


## 更新通知頻道
{: updating-channel}

您可以更新通知頻道配置、停用或啟用通知，或從 {{site.data.keyword.cloudcerts_short}} 刪除通知頻道。
{: shortdesc}

開始之前，請[配置通知頻道](#adding-channel)。 

1. 在服務詳細資料頁面上的導覽，按一下**設定**。 
2. 選取**通知**標籤。 
3. 從下列選項中進行選擇。 
   - 若要停用或啟用頻道的通知，請將開關設為**停用**或**啟用**。 
   - 若要更新頻道的設定，請從動作功能表選取**編輯**。
   - 若要刪除通知頻道，請從動作功能表選取**刪除**。 
   
   
## 驗證回呼 URL 的 HTTP 有效負載
{: #verify-callback}

從 {{site.data.keyword.cloudcerts_short}} 傳送到回呼 URL 的每個 HTTP 有效負載，會根據 JWT 標準，使用非對稱金鑰配對自動進行簽署。  
{: shortdesc}

對於每個 {{site.data.keyword.cloudcerts_short}} 實例，會產生私密和公開金鑰，不會在其他 {{site.data.keyword.cloudcerts_short}} 實例之間共用。私密金鑰用來簽署 HTTP 有效負載，而您可以使用公開金鑰驗證有效負載確實是由 {{site.data.keyword.cloudcerts_short}} 產生，且未遭到第三方變更。

若要下載公開金鑰，請執行下列動作：

1. 從服務詳細資料頁面上的導覽，按一下**設定**。
2. 開啟**通知**標籤。
3. 按一下**下載金鑰**圖示。金鑰會下載為 PEM 檔案。
