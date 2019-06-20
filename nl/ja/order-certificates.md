---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# 証明書の注文
{: #ordering-certificates}

{{site.data.keyword.cloudcerts_long}} を使用して、サポートされている外部の認証局によって署名されたアプリおよびサービス用の公開 SSL/TLS 証明書を注文できます。{{site.data.keyword.cloudcerts_short}} を使用すると、SSL/TLS 秘密鍵のセキュリティーが強化されるだけでなく、公開証明書を簡単に注文できるようになります。証明書が発行された後、それを統合サービスにデプロイするか、ダウンロードして他の場所で使用できるようになります。  
{: shortdesc}

証明書を注文すると、SSL/TLS の秘密鍵は {{site.data.keyword.cloudcerts_short}} に直接生成され、安全に保管されます。要求、および発行された証明書へのアクセスはすべて、[アクセス制御](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)によって管理でき、[{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events)を使用して自動的に監査できます。  

{{site.data.keyword.cloudcerts_short}} は、ACME クライアントとして Automatic Certificate Management Environment (ACME) v2 プロトコルを実装します。ACME プロトコルにより、人手を介さずにブラウザーの信頼できる証明書を自動的に取得することができます。

## 証明書の特徴
{{site.data.keyword.cloudcerts_short}} を通して注文された証明書には、次の特徴があります。

- 無料
- 有効期間 - 90 日間
- シングル・ドメイン、マルチ・ドメイン (SAN)、またはワイルドカードの証明書
- ドメインの検証 - 証明書を発行する前に、証明書を要求しているドメインを所有しているかどうか認証局が確認します。

Extended Validation (EV) 証明書または Organization Validated (OV) 証明書が必要な場合は、別の場所からそれらを取得して {{site.data.keyword.cloudcerts_short}} にインポートし、それらのライフサイクルを管理できます。

## サポートされている認証局
{: #supported-certificate-authorities}

認証局 (CA) はデジタル証明書を発行するエンティティーです。CA は、証明書の要求者と証明書に依存するクライアントの両方にとって信頼できるサード・パーティーとして機能します。
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) は、無料の自動化された ACME ベースの CA で、90 日間有効なドメイン検証済み証明書を提供します。このサービスは、Internet Security Research Group (ISRG) によって提供されています。

## 証明書の注文のセットアップ
{: #setup}

{{site.data.keyword.cloudcerts_short}} は証明書を発行する前に、
要求にリストされているすべてのドメインがユーザーによって制御されていることを確認する必要があります。{{site.data.keyword.cloudcerts_short}} は DNS 検証を使用して、ユーザーが持つ制御を検証します。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} は、ドメイン・ネーム・システム (DNS) TXT レコードの形式でチャレンジを送信し、ユーザーが DNS サービスに追加できるようにします。証明書で要求したドメインごとに、個別の DNS TXT レコードをユーザーが受け取ります。DNS TXT レコードを追加した後、{{site.data.keyword.cloudcerts_short}} および Let’s Encrypt は、そのレコードが DNS サービスにあるかどうかを確認します。チャレンジを正常に完了すると、{{site.data.keyword.cloudcerts_short}} インスタンスで使用可能な Let's Encrypt 証明書が発行されます。

{{site.data.keyword.cloudcerts_short}} は、通知設定で指定したコールバック URL に TXT レコードを送信するので、ドメイン検証プロセスを簡単に自動化することができます。

証明書の注文を開始するには、{{site.data.keyword.cloudcerts_short}} にコールバック URL を通知チャネルとして登録します。その後、コードを更新して、TXT チャレンジを含む通知イベントを処理するようにします。[コールバック URL 通知チャネルのセットアップ方法については、こちらを参照してください](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)。

## チャレンジへの応答
{: #responding-to-challenge}

通知チャネルは、次の構造を持つ通知を受け取ります。

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

DNS TXT チャレンジがコールバック URL に送信された後、10 分以内にチャレンジに応答しなければなりません。{{site.data.keyword.cloudcerts_short}} は、チャレンジが完了したかどうかを確認します。チャレンジに応答したことが {{site.data.keyword.cloudcerts_short}} によって確認されると、TXT レコードを削除できることを知らせる 2 回目の通知が送信されます。

証明書の注文に関するよくある質問については、[FAQ のページを確認してください](/docs/services/certificate-manager?topic=certificate-manager-faq#faq)。
{: tip}

## 証明書の注文
{: #ordering-certificate}

1. {{site.data.keyword.cloudcerts_short}} の「管理」タブにナビゲートします。
2. **「証明書の注文 (Order Certificate)」**をクリックし、以下の詳細を指定してください。

    1. 証明書名を指定します。
    2. 認証局を選択します。
    3. 1 次ドメイン、および代替ドメインがあれば代替ドメインを入力します。
    4. 適切なアルゴリズムと鍵アルゴリズムを選択します。
    5. **「注文」**をクリックします。

注文は**「保留中」**状態になります。ユーザーがドメイン検証チャレンジに応答し、要求したドメインをユーザーが所有していることを {{site.data.keyword.cloudcerts_short}} が確認すると、証明書が発行され、その状態が**「有効 (Valid)」**に変わります。証明書の準備が整ったとき、または問題が発生したときは、Slack および/またはコールバック URL チャネルで通知されます。

## 証明書の更新
{: #renew-certificate}

証明書が期限切れになりそうな場合は、{{site.data.keyword.cloudcerts_short}} で証明書の更新を要求できます。証明書が更新された後、以前のバージョンの証明書は、必要に応じて保持されます。 

更新は、証明書の注文と同じような仕組みです。ユーザーが証明書の更新を要求すると、{{site.data.keyword.cloudcerts_short}} は DNS txt チャレンジをコールバック URL に送信します。これによりユーザーは、証明書が更新されているドメインを所有していることを再び証明することができます。

証明書を更新するには、以下のステップを実行します。
  1. 更新する証明書の行のメニューをクリックします。
  2. **「証明書の更新 (Renew Certificate)」**をクリックします。
  3. オプション:**「証明書の鍵の再設定 (Rekey certificate)」**チェック・ボックスをオンにすることで、
証明書の鍵を再設定できます。この操作により、証明書が新しい鍵ペアで更新されます。
  
  証明書の鍵を再設定するときは、それが使用されているすべての場所に新しい証明書と鍵を配置してください。
  {: note}
    
  4. **「更新 (Renew)」**をクリックします。
  
  更新できるのは、{{site.data.keyword.cloudcerts_short}} 経由で注文した証明書だけです。
  {: note}

注文は**「更新保留中 (Renew Pending)」**状態になります。ユーザーがドメイン検証チャレンジに応答し、要求したドメインをユーザーが所有していることを {{site.data.keyword.cloudcerts_short}} が確認すると、ユーザーは更新された証明書を取得し、その状態が**「有効 (Valid)」**に変わります。更新された証明書の準備が整ったとき、または問題が発生したときは、Slack および/またはコールバック URL チャネルで通知されます。
