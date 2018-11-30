---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
# {{site.data.keyword.cloudcerts_short}} の概要
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_long}} は、{{site.data.keyword.IBM_notm}} Cloud ベースのアプリおよびサービス用の SSL 証明書の管理を支援します。
{: shortdesc}

アプリおよびサービス用に取得する SSL 証明書をインポートし、それらを安全に保管し、使用している証明書を集中して表示することができます。

証明書は、以下の方法で管理できます。

* 証明書の有効期限が切れる前に通知を受け取り、期限前に更新するようにする
* 複数のデプロイメントにわたって証明書のタイプを表示し、それらが組織のポリシーに一致していることを確認する
* 新しいコンプライアンス要件またはセキュリティー要件が出されたときに置き換える必要がある証明書を見つける
* 証明書のアクセスおよび管理を行えるユーザーについて制御を設定する

![上位サービス・アーキテクチャー・ダイアグラム](images/high-level-architecture.png)
<caption>図 1. 上位サービス・アーキテクチャー。</caption>

## 秘密鍵のセキュリティー
{: #private-key-security}

証明書と、対応する秘密鍵を {{site.data.keyword.cloudcerts_short}} にインポートすると、サービスは Advanced Encryption Standard (AES) 256 アルゴリズムを使用して秘密鍵を暗号化します。 {{site.data.keyword.cloudcerts_short}} は、サービス・インスタンスで使用するために、この暗号化された固有鍵を保存します。

## 統合
{: #integrations}

<table>
<caption>表 1. {{site.data.keyword.cloudcerts_short}} を使用する{{site.data.keyword.cloud_notm}} サービス</caption>
  <tr>
    <th> サービス </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Kubernetes クラスターのカスタム・ドメイン証明書を {{site.data.keyword.cloudcerts_short}} に保管し、それを {{site.data.keyword.cloud_notm}} CLI の [Kubernetes サービス・プラグイン・コマンド](/docs/containers/cs_cli_reference.html)を使用してデプロイします。[この統合の詳細はこちら ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/)を参照してください。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>{{site.data.keyword.security-advisor_short}} は、{{site.data.keyword.cloud_notm}} サービスに関する情報を一元化します。これには、{{site.data.keyword.cloud_notm}} アカウント内の {{site.data.keyword.cloudcerts_short}} のインスタンスで期限切れになった証明書と有効期限が近づいた証明書についての情報が含まれます。[{{site.data.keyword.security-advisor_short}} の詳細はこちら](/docs/services/security-advisor/index.html#index)を参照してください。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>ユーザーおよびアプリケーションが {{site.data.keyword.cloud_notm}} 内の {{site.data.keyword.cloudcerts_long_notm}} サービスとどのように対話するのかを {{site.data.keyword.cloudaccesstrailfull_notm}} サービスを使用してトラッキングします。 [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla) についての詳細。
    <p>イベントを生成するアクションのリストを取得するには、[{{site.data.keyword.cloudaccesstrailshort}} イベント](/docs/services/certificate-manager/at_events.html#at_events)を参照してください。</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>カスタム・ドメイン証明書を {{site.data.keyword.cloudcerts_short}} サービスに保管し、証明書 CRN を使用して {{site.data.keyword.apiconnect_short}} のカスタム・ドメインにバインドします。[{{site.data.keyword.apiconnect_short}} の詳細はこちら](/docs/api-management/index.html#index)を参照してください。</p></td>
  </tr>
</table>

## ロケーション
{: #availability}

{{site.data.keyword.cloudcerts_short}} は、ダラスとロンドンのロケーションで使用可能です。



## 制限
{: #limits}

1 インスタンスにつき最大 1000 の証明書をアップロードできます。
