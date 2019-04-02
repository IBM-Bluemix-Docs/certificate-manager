---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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
    <td>カスタム・ドメイン TLS 証明書を {{site.data.keyword.cloudcerts_short}} から Kubernetes クラスターに簡単かつ安全にデプロイできます。クラスター管理者は [Kubernetes サービス・プラグイン・コマンド](/docs/containers?topic=containers-cs_cli_reference)を使用して、ダウン時間を発生させることなく TLS 証明書を Kubernetes secret として新しい証明書で更新することができます。開始するには、
[ドキュメンテーションの入口コメント](/docs/containers?topic=containers-ingress_annotation#https-auth)をチェックアウトします。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index) は、{{site.data.keyword.cloud_notm}} サービスに関する情報を一元化します。 これには、{{site.data.keyword.cloud_notm}} アカウント内の {{site.data.keyword.cloudcerts_short}} のインスタンスで期限切れになった証明書と有効期限が近づいた証明書についての情報が含まれます。 [{{site.data.keyword.security-advisor_short}}の詳細はこちら](/docs/services/security-advisor?topic=security-advisor-index#index)を参照してください。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>[{{site.data.keyword.cloudaccesstrailfull_notm}} サービス](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)を使用して、{{site.data.keyword.cloud_notm}} でユーザーとアプリケーションが {{site.data.keyword.cloudcerts_long_notm}} サービスと対話する方法を追跡できます。[{{site.data.keyword.cloudaccesstrailshort}}の詳細はこちら](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)を参照してください。
    <p>イベントを生成するアクションのリストを取得するには、[{{site.data.keyword.cloudaccesstrailshort}} イベント](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events)を参照してください。</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>カスタム・ドメイン証明書を {{site.data.keyword.cloudcerts_short}} サービスに保管し、証明書 CRN を使用して {{site.data.keyword.apiconnect_short}} のカスタム・ドメインにバインドします。 [{{site.data.keyword.apiconnect_short}} の詳細はこちら](/docs/services/apiconnect?topic=apiconnect-index)を参照してください。</p></td>
  </tr>
</table>

## ロケーション
{: #availability}

{{site.data.keyword.cloudcerts_short}} は、ダラス、ロンドン、フランクフルト、東京のロケーションで使用可能です。



## 制限
{: #limits}

1 インスタンスにつき最大 1000 の証明書をアップロードできます。
