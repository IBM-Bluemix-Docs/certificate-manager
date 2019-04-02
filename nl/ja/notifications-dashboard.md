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

# 通知の構成
{: #configuring-notifications}

証明書は通常、一定の時間だけ有効です。 使用する証明書の有効期限が切れると、アプリのダウン時間が発生することがあります。 ダウン時間を回避するために、期限切れになりそうな証明書に関する通知を送信するように {{site.data.keyword.cloudcerts_full}} を構成して、期限前に証明書を更新するよう思い出させるようにします。

期限切れになる証明書の代わりに、更新されたバージョンの証明書が {{site.data.keyword.cloudcerts_short}} に再インポートされる際にもアラートが出るので、その証明書を SSL/TLS 終端点にデプロイすることを思い出すこともできます。再インポートされた証明書に関するこの通知は、[チャネル・バージョン 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) からチャネルにのみ送信されます。
{: shortdesc}

**いつ通知されますか?**  
{{site.data.keyword.cloudcerts_full_notm}} にアップロードした証明書の有効期限に応じて、証明書の有効期限が切れる 90 日前、60 日前、30 日前、10 日前、1 日前に、通知を受け取ります。 さらに、期限切れの証明書に関する通知を毎日受け取ります。 毎日の通知は、証明書の有効期限が切れた次の日から始まります。

証明書を更新し、古い証明書の代わりにこの証明書を  {{site.data.keyword.cloudcerts_full_notm}} に再インポートして、通知が送信されないようにします。証明書を再インポートすると、証明書が再インポートされたことの通知が送信され、再デプロイするように思い出させてくれます。

**通知の構成に使用できるオプションは何ですか?**  
Slack Web フックを使用して Slack に通知を送信するか、任意のコールバック URL を使用できます。

## Slack Web フックのセットアップ
{: #setup-callback}

Slack Web フックをセットアップするには、以下のステップを実行します。

1. [Slack](https://slack.com/) に登録し、ワークスペースをセットアップします。
2. 通知の送信先の Slack チャネルを作成します。
3. Slack チャネルの[Web フックをセットアップします](https://api.slack.com/incoming-webhooks)。

## コールバック URL のセットアップ
{: #callback}

チームの更新プロセスのきっかけにするために、コールバック URL を使用して、使用するツールに通知されるようにすることができます。例えば、レポートする通知を PagerDuty に送信したり、GitHub で自動的に問題を開いたり、更新スクリプトをトリガーしたりできます。  
{: shortdesc}

**重要:** コールバック URL エンドポイントは、{{site.data.keyword.cloudcerts_short}} で使用するために以下の要件を満たす必要があります。
* エンドポイントは HTTPS プロトコルを使用する必要がある。
* エンドポイントは HTTP ヘッダーを必要としない。 この要件には許可ヘッダーが含まれます。
* エンドポイントは、通知配信が正常に終了したことを示す `200 OK` 状況コードを返す必要があります。

### 通知形式
{: #notification_format}

コールバック URL に送信される通知は、インスタンス非対称鍵で署名された以下の形式の JSON 文書 です。

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

ペイロードをデコードして確認した後のコンテンツは、[チャネル・バージョンによる](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) JSON 文字列です。

## 通知チャネルの構成
{: #adding-channel}

Slack Web フックまたはコールバック URL を作成した後、それを {{site.data.keyword.cloudcerts_short}} に追加して有効期限が切れる証明書と再インポートされた証明書についての通知の受信を開始します。{{site.data.keyword.cloudcerts_short}} は、エンドポイントを暗号化し、安全に保管します。
{: shortdesc}

通知チャネルを追加するには、以下のステップを実行します。

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。
2. **「通知」**タブを開きます。
3. **「通知チャネルの追加 (Add Notification Channel)」**をクリックします。
4. 使用する通知チャネルのタイプを選択します。
5. 通知の送信先の Web フックまたはコールバック URL を入力します。
6. **「保存」**をクリックします。 構成の要約が表示されます。

   **出力例**

   <table>
   <caption>表 1. 通知チャネルに関する情報 </caption>
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
    <td>通知チャネルの状態。 無効に設定されている場合、通知は送信されません。</td>
   </tr>
   <tr>
    <td>「テスト接続」ボタン</td>
    <td>構成したチャネルにテスト通知を送信します。 </td>
   </tr>
    <tr>
      <td>ドット・メニュー</td>
      <td>チャネルで実行可能なアクション。<i>編集</i> または<i>削除</i></td>
    </tr>
    </tbody>
    </table>

    Slack Web フックを保存すると、{{site.data.keyword.cloudcerts_short}} によって、構成した Slack チャネルに確認通知が自動的に送信されます。 Slack チャネルをチェックして、この通知を受け取ったことを確認します。
    {: tip}
7. (オプション) このステップを繰り返して、通知チャネルを追加します。

## 通知チャネルのテスト
{: #testing-channel}

通知チャネルをテストして、通知チャネルが正しく構成されていることを確認できます。
{: shortdesc}

始める前に、[通知チャネルを構成します](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

通知チャネルをテストするには、以下のステップを実行します。

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。
2. 通知チャネルを見つけて、**「テスト接続」**をクリックします。
3. 構成したチャネルで通知を受信したことを確認します。

## 通知チャネルの更新
{: #updating-channel}

通知チャネルの構成の更新、通知の無効化または有効化、または {{site.data.keyword.cloudcerts_short}} からの通知チャネルの削除を行うことができます。
{: shortdesc}

始める前に、[通知チャネルを構成します](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

通知チャネルを更新するには、以下のステップを実行します。

1. 「サービスの詳細」ページのナビゲーションで、**「設定」**をクリックします。
2. **「通知」**タブを選択します。
3. 以下のオプションから選択します。
   * チャネルの通知を無効または有効にするには、スイッチを**「無効化」**または**「有効化」**に設定します。
   * チャネルの設定を更新するには、「アクション」メニューから**「編集」**を選択します。
   * 通知チャネルを削除するには、「アクション」メニューから**「削除」**を選択します。

## コールバック URL の HTTP ペイロードの検証
{: #verify-callback}

{{site.data.keyword.cloudcerts_short}} からコールバック URL に送信されるすべての HTTP ペイロードは、非対称鍵ペアを使用して、JWT 標準に従って自動的に署名されます。  
{: shortdesc}

すべての {{site.data.keyword.cloudcerts_short}} インスタンスに対して、他の {{site.data.keyword.cloudcerts_short}} インスタンス間で共有されていない秘密鍵と公開鍵が生成されます。 秘密鍵は HTTP ペイロードに署名するために使用されます。公開鍵を使用して、ペイロードが {{site.data.keyword.cloudcerts_short}} によって生成され、サード・パーティーによって変更されていないことを確認できます。

公開鍵をダウンロードするには、以下のステップを実行します。

1. 「サービスの詳細」ページのナビゲーションから、**「設定」**をクリックします。
2. **「通知」**タブを開きます。
3. **「鍵のダウンロード」**ボタンをクリックします。 鍵は PEM ファイルとしてダウンロードされます。

## チャネル・バージョン
{: #channel-versions}

証明書マネージャーが更新されるのに応じて、通知ペイロード構造の形式を時々変更することがあります。
後方互換性を保証するために、既存のチャネルに送信されるペイロードは変更されません。   

既存の通知チャネルがある場合は (Slack またはコールバック URL)、新しいバージョンのペイロードの取得を開始するには、以下のようにします。
1. コールバック URL の場合、実装環境が新しいペイロードを受け入れることができることを確認します。
2. 新しい通知チャネルを作成します (新しいチャネルは常に最新チャネル・バージョンを使用して作成されます)。
3. 新しいチャネルが正しく動作することをテストします。
4. 古いチャネルを削除します。

チャネル・バージョンの場合は、[API 資料](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions)を確認してください。

## 例
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   期限切れが近い証明書に関する通知のための GitHub 問題を作成する方法を説明します。
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   期限切れが近い証明書に関する通知のための PagerDuty インシデント問題を作成する方法を説明します。
