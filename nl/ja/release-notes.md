
---
copyright:
  years: 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# リリース・ノート
{: #release-notes}

{{site.data.keyword.cloudcerts_long}} サービスには、以下のフィーチャーおよび変更があります。

## 2018 年 9 月 12 日
{: 12September2018}

- **証明書名は必須**  
  証明書をインポートするときに、証明書の名前の値を指定することは必須です。  
  さらに、v2 API の**「証明書のインポート」**と**「証明書のメタデータの更新」**は非推奨で、2018 年 11 月 1 日に削除されます。v3 API にアップグレードする必要があります。詳しくは、[API 資料](https://console.bluemix.net/apidocs/certificate-manager)を参照してください。

- **Slack 通知のグループ化**  
  Slack での通知は、有効期限日によってグループ化されます。

## 2018 年 9 月 2 日
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} は一般出荷可能**  
  {{site.data.keyword.cloudcerts_short}} サービスは、{{site.data.keyword.cloud_notm}} で、一般出荷可能 (GA) です。

## 2018 年 8 月 22 日
{: 22August2018}

- **英国で使用可能**  
  {{site.data.keyword.cloudcerts_long_notm}} ベータが英国地域 (英国南部) で使用可能です。

## 2018 年 8 月 15 日
{: 15August2018}

- **非推奨の v1 API の削除**  
  バージョン 1 の API は、使用できなくなりました。 まだ API を更新していない場合は、できるだけ早く更新する必要があります。 [API 資料 (API documentation) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/apidocs/) を検討してください。

- **プラットフォーム役割はサービス役割に置き換えられる**  
  サービス役割を使用して、{{site.data.keyword.cloudcerts_short}} インスタンスへのアクセスを制御できます。 [アクセス管理の詳細はこちら](access-management.html)を参照してください。

## 2018 年 7 月 12 日
{: 12July2018}

- **コールバック通知**  
  通知に対してコールバック・サポートが追加されました。 通知を Slack に送信するか、任意のコールバック URL を使用して通知をポストするかを選択できます。 例えば、通知を PagerDuty に送信したり、GitHub で自動的に問題を開いたり、更新スクリプトをトリガーしたりできます。 [通知の詳細はこちら](notifications-dashboard.html)を参照してください。

## 2018 年 6 月 12 日
{: 12June2018}

- **Slack 通知**  
  証明書の期限切れを見逃さないために、Slack 通知が追加されました。 [通知の詳細はこちら](notifications-dashboard.html)を参照してください。

## 2017 年 12 月 19 日
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} はベータ版サービスとして使用可能**  
  {{site.data.keyword.cloudcerts_short}} サービスは、{{site.data.keyword.cloud_notm}} 内のベータ版サービスとして使用可能です。
