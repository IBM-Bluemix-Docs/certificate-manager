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

# リリース・ノート
{: #release-notes}

{{site.data.keyword.cloudcerts_long}} サービスには、以下のフィーチャーおよび変更があります。

## 2019 年 7 月 8 日
{: 8July2019}

- **DNS プロバイダーとしての IBM Cloud Internet Services**  
  IBM Cloud Internet Services を DNS プロバイダーとして使用できるようになりました。これにより、証明書の注文が簡単になります。[証明書の注文の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-order-certificates)を参照してください。

## 2019 年 6 月 10 日
{: 10June2019}

- **注文した Let's Encrypt 証明書の更新**  
  {{site.data.keyword.cloudcerts_short}} を使用して注文した Let's Encrypt 証明書を更新できるようになりました。 [証明書の注文の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-order-certificates)を参照してください。

## 2019 年 5 月 6 日
{: 6May2019}

- **Let's Encrypt 証明書の注文**  
  Let's Encrypt 証明書を注文できるようになりました。 [証明書の注文の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-order-certificates)を参照してください。

## 2019 年 2 月 18 日
{: 18February2019}

- **東京で使用可能**  
  {{site.data.keyword.cloudcerts_long_notm}} は東京のロケーションで使用可能です。

## 2019 年 1 月 13 日
{: 13January2019}
- **コールバック・ペイロード バージョン 3**  
  [API 資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/certificate-manager)を参照してください。

## 2019 年 1 月 6 日
{: 6January2019}
- **非推奨 API**  
  **証明書のリスト**と**検索証明書リポジトリー** v2 API は非推奨となり、 将来削除されます。 v3 API にアップグレードする必要があります。 詳しくは、[API 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") ](https://cloud.ibm.com/apidocs/certificate-manager)を参照してください。

## 2018 年 12 月 9 日
{: 9December2018}
- **その他の証明書形式**    
{{site.data.keyword.cloudcerts_short}} は、以下の証明書形式をサポートします: RSA、DSA、ECDSA、ECDH。

## 2018 年 12 月 5 日
{: 5December2018}
- **再インポート通知**    
有効期限が切れる証明書の代わりに更新された証明書を再インポートすると、証明書が再インポートされたことの通知を受け取ることがあります。 この通知は、更新された証明書を SSL/TLS 終端ポイントにデプロイするよう自分とチームに思い出させるものとなります。 この通知は、新しく作成された通知チャネルにのみ利用可能です。

- **{{site.data.keyword.cloudcerts_short}} はフランクフルトのロケーションで使用可能です。**     
このサービスは EU の要件に準拠しています。

## 2018 年 12 月 2 日
{: 2December2018}
- **コールバックおよび Slack ペイロード バージョン 2**  
  [API 資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/certificate-manager)を参照してください。

## 2018 年 11 月 14 日
{: 14November2018}

- **再インポート**  
  証明書は、既存の証明書と同じドメインの、新たな有効期限日付を持つ新しいバージョンを再インポートすることで更新できます。 証明書が再インポートされると、証明書の既存のバージョンはバックアップとして保存されます。[証明書の再インポート](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)を参照してください。

- **1 インスタンスにつき 1000 の証明書**  
  1 インスタンスにつき最大 1000 の証明書をインポートできます。

## 2018 年 10 月 28 日
{: 28October2018}

- **発表バナー**  
  非推奨になった API やその他のニュースなどのサービス発表は、**「管理」**タブに表示されます。

## 2018 年 9 月 12 日
{: 12September2018}

- **証明書名は必須**  
  証明書をインポートするときに、証明書の名前の値を指定することは必須です。  

- **非推奨 API**  
  v2 API の**「証明書のインポート」**と**「証明書のメタデータの更新」**は非推奨で、2018 年 12 月 1 日に削除されます。 v3 API にアップグレードする必要があります。 詳しくは、[API 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") ](https://cloud.ibm.com/apidocs/certificate-manager)を参照してください。

- **Slack 通知のグループ化**  
  Slack での通知は、有効期限日によってグループ化されます。

## 2018 年 9 月 2 日
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} は一般出荷可能**  
  {{site.data.keyword.cloudcerts_short}} サービスは、{{site.data.keyword.cloud_notm}} で、一般出荷可能 (GA) です。

## 2018 年 8 月 22 日
{: 22August2018}

- **ロンドンで使用可能**  
  {{site.data.keyword.cloudcerts_long_notm}} ベータは、ロンドンのロケーションで使用できます。

## 2018 年 8 月 15 日
{: 15August2018}

- **非推奨の v1 API の削除**  
  バージョン 1 の API は、使用できなくなりました。 まだ API を更新していない場合は、できるだけ早く更新する必要があります。 詳しくは、[API 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") ](https://cloud.ibm.com/apidocs/)を参照してください。

- **プラットフォーム役割はサービス役割に置き換えられる**  
  サービス役割を使用して、{{site.data.keyword.cloudcerts_short}} インスタンスへのアクセスを制御できます。 [アクセス管理の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)を参照してください。

## 2018 年 7 月 12 日
{: 12July2018}

- **コールバック通知**  
  通知に対してコールバック・サポートが追加されました。 通知を Slack に送信するか、任意のコールバック URL を使用して通知をポストするかを選択できます。 例えば、通知を PagerDuty に送信したり、GitHub で自動的に問題を開いたり、更新スクリプトをトリガーしたりできます。 [通知の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback)を参照してください。

## 2018 年 6 月 12 日
{: 12June2018}

- **Slack 通知**  
  証明書の期限切れを見逃さないために、Slack 通知が追加されました。 [通知の詳細はこちら](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback)を参照してください。

## 2018 年 1 月 8 日
{: 8January2018}

- **非推奨 API**  
  v1 API は、非推奨となり、2018 年 9 月 8 日に削除されます。 v2 API にアップグレードする必要があります。 詳しくは、[API 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") ](https://cloud.ibm.com/apidocs/certificate-manager)を参照してください。

## 2017 年 12 月 19 日
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} はベータ版サービスとして使用可能**  
  {{site.data.keyword.cloudcerts_short}} サービスは、{{site.data.keyword.cloud_notm}} 内のベータ版サービスとして使用可能です。
