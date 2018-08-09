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

# 証明書の有効期限に関する通知の構成
{: #configuring-notifications-for-expiring-certificates}

証明書は通常、一定の時間だけ有効です。使用する証明書の有効期限が切れると、アプリのダウン時間が発生することがあります。ダウン時間を回避するために、期限切れになりそうな証明書に関する通知を送信するように {{site.data.keyword.cloudcerts_full}} を構成して、期限前に証明書を更新できるようにします。
{: shortdesc}

**いつ通知されますか。** </br>
{{site.data.keyword.cloudcerts_full}} にアップロードした証明書の有効期限に応じて、証明書の有効期限が切れる 90 日前、60 日前、30 日前、10 日前、1 日前に、通知を受け取ります。さらに、証明書の有効期限が切れた日から毎日、期限切れの証明書に関する通知を受け取ります。 

証明書を更新し、この証明書を {{site.data.keyword.cloudcerts_full}} にアップロードし、期限切れの証明書を削除して、通知の送信が継続されないようにする必要があります。 

**通知の構成に使用できるオプションは何ですか。** </br>
Slack Web フックを使用して Slack に通知を送信するか、任意のコールバック URL を使用できます。 

## Slack Web フックのセットアップ
{: #setup-callback}

1. [Slack](https://slack.com/) に登録し、ワークスペースをセットアップします。 
2. 通知の送信先の Slack チャネルを作成します。 
3. Slack チャネルの[Web フックをセットアップします](https://api.slack.com/incoming-webhooks)。 

## コールバック URL のセットアップ
{: #callback}

チームの更新プロセスのきっかけにするために、コールバック URL を使用して、毎日使用するツールに通知されるようにすることができます。例えば、レポートする通知を PagerDuty に送信したり、Github で自動的に問題を開いたり、更新スクリプトをトリガーしたりできます。  
{: shortdesc}

**重要:** コールバック URL エンドポイントは、{{site.data.keyword.cloudcerts_short}} で使用するために以下の要件を満たす必要があります。 
* エンドポイントは HTTPS プロトコルを使用する必要がある。
* エンドポイントは HTTP ヘッダーを必要としない。この要件には許可ヘッダーが含まれます。

### コールバック URL を使用して GitHub の問題を自動的に開く 
{: #sample}

次のサンプル・コードは、{{site.data.keyword.cloudcerts_short}} 通知が送信されたときに、証明書の有効期限が切れる GitHub の問題を作成する方法を示しています。このコードは、{{site.data.keyword.openwhisk}} で実行することも、別の環境でコードを使用することもできます。   
{: shortdesc}

このコードを {{site.data.keyword.openwhisk}} で実行するには、次のようにします。

1. [{{site.data.keyword.openwhisk}} でアクション](/docs/openwhisk/index.html#getting-started)を作成します。
2. 次のコードを使用して、GitHub の問題を自動的に作成します。 

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
    
その他の REST API コマンドについては、[API 資料](https://console.bluemix.net/apidocs/cloudcerts)を参照してください。
{: tip}


## 通知チャネルの構成
{: #adding-channel}

Slack Web フックまたはコールバック URL を作成した後、それを {{site.data.keyword.cloudcerts_short}} に追加して証明書の有効期限についての通知の受信を開始します。{{site.data.keyword.cloudcerts_short}} は、エンドポイントを暗号化し、安全に保管します。
{: shortdesc}

通知チャネルを追加するには、次のようにします。

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。 
2. **「通知」**タブを開きます。
3. **「通知チャネルの追加 (Add Notification Channel)」**をクリックします。 
4. 使用する通知チャネルのタイプを選択します。 
5. 通知の送信先の Web フックまたはコールバック URL を入力します。
6. **「保存」**をクリックします。構成の要約が表示されます。 

   出力例: 
   <table>
   <caption> 通知チャネルに関する情報</caption>
   <thead>
    <th> コンポーネント </th>
    <th> 説明 </th>
   </thead>
   <tbody>
   <tr>
    <td>タイプ</td>
    <td>通知チャネルのタイプ。<i>Slack</i> または<i>コールバック URL</i></td>
   </tr>
   <tr>
    <td>エンドポイント</td>
    <td>通知の送信先の通知チャネルのエンドポイント。</td>
   </tr>
   <tr>
    <td>有効化の切り替え</td>
    <td>通知チャネルの状態。無効に設定されている場合、通知は送信されません。</td>
   </tr>
   <tr>
    <td>「テスト接続」ボタン</td>
    <td>構成したチャネルにテスト通知を送信します。</td>
   </tr>
    <tr>
      <td>ドット・メニュー</td>
      <td>チャネルで実行可能なアクション。<i>編集</i> または<i>削除</i></td>
    </tr>
    </tbody>
    </table>
   
    Slack Web フックを保存すると、{{site.data.keyword.cloudcerts_short}} によって、構成した Slack チャネルに確認通知が自動的に送信されます。Slack チャネルをチェックして、この通知を受け取ったことを確認します。
    {: tip}
7. オプション: この手順を繰り返して、通知チャネルを追加します。 

## 通知チャネルのテスト
{: #testing-channel}

通知チャネルをテストして、通知チャネルが正しく構成されていることを確認できます。
{: shortdesc}

始める前に、[通知チャネルを構成します](#adding-channel)。 

通知チャネルをテストするには、次のようにします。 

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。 
2. 通知チャネルを見つけて、**「テスト接続」**をクリックします。
3. 構成したチャネルで通知を受信したことを確認します。 


## 通知チャネルの更新
{: updating-channel}

通知チャネルの構成の更新、通知の無効化または有効化、または {{site.data.keyword.cloudcerts_short}} からの通知チャネルの削除を行うことができます。
{: shortdesc}

始める前に、[通知チャネルを構成します](#adding-channel)。 

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。 
2. **「通知」**タブを選択します。 
3. 以下のオプションから選択します。 
   - チャネルの通知を無効または有効にするには、スイッチを**「無効化」**または**「有効化」**に設定します。 
   - チャネルの設定を更新するには、「アクション」メニューから**「編集」**を選択します。
   - 通知チャネルを削除するには、「アクション」メニューから**「削除」**を選択します。 
   
   
## コールバック URL の HTTP ペイロードの検証
{: #verify-callback}

{{site.data.keyword.cloudcerts_short}} からコールバック URL に送信されるすべての HTTP ペイロードは、非対称鍵ペアを使用して、JWT 標準に従って自動的に署名されます。  
{: shortdesc}

すべての {{site.data.keyword.cloudcerts_short}} インスタンスに対して、他の {{site.data.keyword.cloudcerts_short}} インスタンス間で共有されていない秘密鍵と公開鍵が生成されます。秘密鍵は HTTP ペイロードに署名するために使用されます。公開鍵を使用して、ペイロードが {{site.data.keyword.cloudcerts_short}} によって生成され、サード・パーティーによって変更されていないことを確認できます。

公開鍵をダウンロードするには、次のようにします。

1. 「サービスの詳細」ページのナビゲーションから、**「設定」**をクリックします。
2. **「通知」**タブを開きます。
3. **「鍵のダウンロード」**ボタンをクリックします。鍵は PEM ファイルとしてダウンロードされます。
