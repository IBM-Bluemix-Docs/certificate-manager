---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# 証明書の注文
{: #ordering-certificates}

{{site.data.keyword.cloudcerts_long}} を使用して、サポートされている外部の認証局によって署名されたアプリおよびサービス用の公開 SSL/TLS 証明書を注文できます。 {{site.data.keyword.cloudcerts_short}} を使用すると、SSL/TLS 秘密鍵のセキュリティーが強化されるだけでなく、公開証明書を簡単に注文できるようになります。 証明書が発行された後、それを統合サービスにデプロイするか、ダウンロードして他の場所で使用できるようになります。  
{: shortdesc}

証明書を注文すると、SSL/TLS の秘密鍵は {{site.data.keyword.cloudcerts_short}} に直接生成され、安全に保管されます。 要求、および発行された証明書へのアクセスはすべて、[アクセス制御](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles)によって管理でき、[{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events)を使用して自動的に監査できます。  

{{site.data.keyword.cloudcerts_short}} は、ACME クライアントとして Automatic Certificate Management Environment (ACME) v2 プロトコルを実装します。 ACME プロトコルにより、人手を介さずにブラウザーの信頼できる証明書を自動的に取得することができます。

## 証明書の特徴
{: #certificate-characteristics}

{{site.data.keyword.cloudcerts_short}} を介して証明書を注文する場合:

- 証明書は無料です
- 証明書の有効期間は 90 日間です
- 証明書はシングル・ドメイン、マルチ・ドメイン (SAN)、またはワイルドカードになります
- 証明書はドメイン検証されています

ドメイン検証には、証明書を要求しているドメインを所有しているかどうかの確認が含まれます。Extended Validation (EV) 証明書または Organization Validated (OV) 証明書が必要な場合は、別の場所からそれらを取得して {{site.data.keyword.cloudcerts_short}} にインポートし、それらのライフサイクルを管理できます。


## サポートされている認証局
{: #supported-certificate-authorities}

認証局 (CA) はデジタル証明書を発行するエンティティーです。 CA は、証明書の要求者と証明書に依存するクライアントの両方にとって信頼のおける第三者機関として機能します。
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) は、無料の自動化された ACME ベースの CA で、90 日間有効なドメイン検証済み証明書を提供します。 このサービスは、Internet Security Research Group (ISRG) によって提供されています。

## 証明書の注文のセットアップ
{: #setup}

{{site.data.keyword.cloudcerts_short}} は証明書を発行する前に、要求にリストされているすべてのドメインがユーザーによって制御されていることを確認する必要があります。これを行うために、{{site.data.keyword.cloudcerts_short}} は DNS 検証を使用します。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} は、ドメイン・ネーム・システム (DNS) TXT レコードの形式でチャレンジを送信し、ユーザーが DNS サービスに追加できるようにします。 証明書で要求したドメインごとに、個別の DNS TXT レコードをユーザーが受け取ります。 DNS TXT レコードを追加した後、{{site.data.keyword.cloudcerts_short}} および Let’s Encrypt は、そのレコードが DNS サービスにあるかどうかを確認します。チャレンジを正常に完了すると、{{site.data.keyword.cloudcerts_short}} インスタンスで使用可能な Let's Encrypt 証明書が発行されます。

ドメインの所有権を確認する方法は、{{site.data.keyword.cis_full_notm}} を使用するか、別の DNS プロバイダーを使用するかによって異なります。


### {{site.data.keyword.cis_full_notm}}
{: #cis}

{{site.data.keyword.cis_short}} でドメインを管理する場合、以下のステップを実行して所有権を検証します。

1. **{{site.data.keyword.cloud_notm}} >「管理」>「アクセス (IAM)」>「許可」**に移動します。
2. **「作成」**をクリックして、ソース・サービスおよびターゲット・サービスを割り当てます。ソース・サービスには、次のステップで設定する役割に基づいてターゲット・サービスへのアクセスが付与されます。
  * ソース: {{site.data.keyword.cloudcerts_short}}
  * ターゲット: インターネット・サービス
3. ソースとターゲットの両方にサービス・インスタンスを指定します。
4. **「リーダー」**役割を割り当てて、{{site.data.keyword.cloudcerts_short}} が {{site.data.keyword.cis_short_notm}} インスタンスとそのドメインを表示できるようにします。次に、**「許可」**をクリックします。

  テスト目的で、UI を介して**「管理者」**サービス・アクセス役割を割り当てて、すべてのドメインを管理できます。その場合、ステップ 5 を実行する必要はありません。実稼働環境では、**「リーダー」**サービス・アクセス役割を割り当てて、ステップ 5 に示すように API を使用して特定のドメインを制御することをお勧めします。
　{: note}
   
5. 特定のドメインを制御するには、API を使用して**「管理者」**役割を割り当てて、{{site.data.keyword.cloudcerts_short}} が {{site.data.keyword.cis_short_notm}} インスタンスに存在する個々のドメインの DNS レコードを管理できるようにします。必須パラメーターを編集しやすくするために、コマンドをテキスト・ファイルにコピーすることもできます。
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>有効な IAM トークン。{{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud iam oauth-tokens</code> を使用してこの値を見つけることができます。</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} および {{site.data.keyword.cis_short_notm}} インスタンスが存在するアカウントの ID。値を検索するには、<b>「{{site.data.keyword.cloud_notm}}」>「管理」>「アカウント」>「アカウント設定」</b>にナビゲートするか、{{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud account show</code> を使用します。</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} のインスタンスの GUID ベースの ID。値を検索するには、{{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code> を使用します。</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} のインスタンスの GUID ベースの ID。値を検索するには、{{site.data.keyword.cloud_notm}} CLI: <code>ibmcloud resource service-instance "Instance name"</code> を使用します。</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} で見つかったドメインの ID。値を検索するには、{{site.data.keyword.cloud_notm}} CLI を使用して <code>ibmcloud cis domains</code> を実行します。複数のドメインを管理するには、<code>resources</code> 配列を変更します。</td>
    </tr>
  </table>

これで、[証明書を注文する](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)準備ができました。


### 別の DNS プロバイダー
{: #other_provider}

サード・パーティーの DNS プロバイダーを使用しているときにドメインに対するコントロールを確認するために、{{site.data.keyword.cloudcerts_short}} は、指定したコールバック URL 通知チャネルに TXT レコードを送信するので、ドメイン検証プロセスを自動化することができます。

最初に、ドメイン検証用の IBM Cloud Function アクションを実装してから、そのエンドポイントをコールバック URL 通知チャネルに指定します。開始するには、「[コールバック URL 通知チャネルを設定する](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)」を参照してください。

コールバック URL 通知チャネルを使用してドメイン検証を設定する方法の詳細については、[このブログ投稿](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}を参照してください。
{: tip}


#### チャレンジへの応答
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

DNS TXT チャレンジがコールバック URL に送信された後、10 分以内にチャレンジに応答しなければなりません。 {{site.data.keyword.cloudcerts_short}} は、チャレンジが完了したかどうかを確認します。 チャレンジに応答したことが {{site.data.keyword.cloudcerts_short}} によって確認されると、TXT レコードを削除できることを知らせる 2 回目の通知が送信されます。

証明書の注文に関するよくあるご質問については、[FAQ ページを確認してください](/docs/services/certificate-manager?topic=certificate-manager-faq)。
{: tip}

## 証明書の注文
{: #ordering-certificate}

証明書を注文するには、以下のステップを完了します。

1. {{site.data.keyword.cloudcerts_short}} の「管理」タブにナビゲートします。
2. **「証明書の注文 (Order Certificate)」**をクリックします。 
3. DNS プロバイダー ({{site.data.keyword.cis_full_notm}}、または別の DNS プロバイダー) を選択します。
4. **{{site.data.keyword.cis_full_notm}}** を選択した場合、以下の詳細を指定します。
   1. 必要なセットアップ手順を実行します。
   2. 証明書の名前と説明 (任意指定) を入力します。
   3. 認証局を選択します。
   4. サービス・アクセス役割を割り当てた {{site.data.keyword.cis_full_notm}} インスタンスを選択します。
   5. 必要な証明書タイプを選択します。
   6. ドメインを選択します。
   7. 適切なアルゴリズムと鍵アルゴリズムを選択します。
   8. **「オーダー」**をクリックします。
5. **「別の DNS プロバイダー (Another DNS Provider)」**を選択した場合、以下の詳細を指定します。
   1. 必要なセットアップ手順を実行します。
   2. 証明書の名前と説明 (任意指定) を入力します。
   3. 認証局を選択します。
   4. 1 次ドメイン、および代替ドメインがあれば代替ドメインを入力します。
   5. 適切なアルゴリズムと鍵アルゴリズムを選択します。
   6. **「オーダー」**をクリックします。

注文は**「保留中」**状態になります。 ユーザーがドメイン検証チャレンジに応答し、要求したドメインをユーザーが所有していることを {{site.data.keyword.cloudcerts_short}} が確認すると、証明書が発行され、その状態が**「有効 (Valid)」**に変わります。証明書の準備が整ったとき、または問題が発生したときは、Slack またはコールバック URL 通知チャネル (あるいは両方) で通知されます。

## 証明書の更新
{: #renew-certificate}

証明書が期限切れになりそうな場合は、{{site.data.keyword.cloudcerts_short}} で証明書の更新を要求できます。 証明書が更新された後、以前のバージョンの証明書は、必要に応じて保持されます。 

更新は、証明書の注文と同じような仕組みです。 ユーザーが証明書の更新を要求すると、{{site.data.keyword.cloudcerts_short}} は DNS txt チャレンジをコールバック URL に送信します。これによりユーザーは、証明書が更新されているドメインを所有していることを再び証明することができます。

証明書を更新するには、以下のステップを実行します。
  1. 更新する証明書の行のメニューをクリックします。
  2. **「証明書の更新 (Renew Certificate)」**をクリックします。
  3. オプション:**「証明書の鍵の再設定 (Rekey certificate)」**チェック・ボックスをオンにすることで、
証明書の鍵を再設定できます。 この操作により、証明書が新しい鍵ペアで更新されます。証明書を鍵再設定するときは、それが使用されているすべての場所に新しい証明書と鍵を配置してください。
  
  4. **「更新」**をクリックします。


更新できるのは、{{site.data.keyword.cloudcerts_short}} 経由で注文した証明書だけです。
{: note}

注文は**「更新保留中 (Renew pending)」**状態になります。ユーザーがドメイン検証チャレンジに応答し、要求したドメインをユーザーが所有していることを {{site.data.keyword.cloudcerts_short}} が確認すると、ユーザーは更新された証明書を取得し、その状態が**「有効 (Valid)」**に変わります。更新された証明書の準備が整ったとき、または問題が発生したときは、Slack またはコールバック URL 通知チャネル (あるいは両方) で通知されます。
