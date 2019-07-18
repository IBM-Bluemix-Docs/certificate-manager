---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: certificates, SSL, TLS, activity tracker,

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

# Activity Tracker イベント  
{: #at_events}

{{site.data.keyword.at_full}} サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud_notm}} の {{site.data.keyword.cloudcerts_long}} サービスとどのように対話するかをトラッキングします。{:shortdesc}

{{site.data.keyword.at_short}} サービスは、{{site.data.keyword.cloud_notm}} 内のサービスの状態を変更するユーザー開始アクティビティーを記録します。例えば、証明書をインポートすると、イベントが生成されます。 詳しくは、[{{site.data.keyword.at_short}} の資料](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)を参照してください。

次の表に、呼び出されるとイベントを生成する API メソッドをリストします。

<table>
  <caption>表 1. イベントを生成するアクション</caption>
  <tr>
    <th>アクション</th>
	  <th>説明</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>証明書をインポートします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>証明書を再インポートします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>証明書を注文します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.renew`</td>
	  <td>発行された証明書を更新します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>証明書メタデータを取得します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>証明書をダウンロードします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>証明書をリストします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>証明書メタデータをリストします。 証明書の詳細を表示します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>証明書を検索します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>証明書メタデータを検索します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>証明書を削除します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>証明書メタデータを更新します。例えば、証明書の説明を変更します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>リスト通知チャネル</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>通知チャネルを作成します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>通知チャネルを無効または有効にします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>通知チャネルのエンドポイントを更新します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>通知チャネルを削除します。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>通知チャネルをテストします。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>通知は通知チャネルのエンドポイントに送信されました。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>公開鍵が要求されました。</td>
  </tr>
</table>

## イベントの検索先
{: #at_ui}

ご使用の {{site.data.keyword.cloudcerts_short}} インスタンスと同じ場所に {{site.data.keyword.at_short}} インスタンスをプロビジョンします。

以下の手順を実行してください。

1. [「{{site.data.keyword.cloud_notm}} プログラム識別情報」](https://cloud.ibm.com/observe/){: external}に移動します。
2. ご使用の {{site.data.keyword.cloudcerts_short}} インスタンスと同じ場所に {{site.data.keyword.at_short}} インスタンスをプロビジョンします。

イベントは、{{site.data.keyword.cloudcerts_short}} サービスがプロビジョンされているのと同じ場所にある {{site.data.keyword.at_short}} サービス・インスタンスに自動的に転送されます。

## 追加情報
{: #info}

* 「*requestData_str*」フィールドには、証明書の、人が判読できる名前が含まれます。

## 可用性
{: #at-availability}

{{site.data.keyword.at_short}} サポートは、**ダラス**、**フランクフルト**、**東京**、および**ロンドン**で利用できます。
