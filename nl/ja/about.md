---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Certificate Manager 製品情報
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}} は、{{site.data.keyword.IBM_notm}} Cloud ベースのアプリおよびサービス用の SSL 証明書の管理を支援します。
{: shortdesc}

アプリおよびサービス用に取得する SSL 証明書をインポートし、それらを安全に保管し、使用している証明書を集中して表示することができます。

証明書は、以下の方法で管理できます。

* 証明書の更新が予定どおりに行われるように、証明書の有効期限日付をモニターする
* 複数のデプロイメントにわたって証明書のタイプを表示し、それらが組織のポリシーに一致していることを確認する
* 新しいコンプライアンス要件またはセキュリティー要件が出されたときに置き換える必要がある証明書を見つける
* 証明書のアクセスおよび管理を行えるユーザーについて制御を設定する

## 秘密鍵のセキュリティー
{: #private-key-security}

証明書と、対応する秘密鍵を {{site.data.keyword.cloudcerts_short}} にインポートすると、サービスは Advanced Encryption Standard (AES) 256 アルゴリズムを使用して秘密鍵を暗号化します。 {{site.data.keyword.cloudcerts_short}} は、サービス・インスタンスで使用するために、この暗号化された固有鍵を保存します。

## 可用性
{: #availability}

{{site.data.keyword.cloudcerts_short}} は、米国南部地域でのみ使用可能です。

## 統合
{: #integrations}
<table>
<caption> 表 1. Certificate Manager を活用する IBM Cloud サービス</caption>
  <tr>
    <th> サービス</th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Kubernetes クラスターのカスタム・ドメイン証明書を Certificate Manager に保管し、それを IBM Cloud CLI の [Kubernetes サービス・プラグイン・コマンド](/docs/containers/cs_cli_reference.html)を使用してデプロイします。[この統合の詳細はこちら](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/)</td>
  </tr>
  <tr>
    <td>IBM Cloud セキュリティー・アドバイザー</td>
    <td>セキュリティー・アドバイザーは、IBM Cloud アカウントの Certificate Manager のインスタンスで、期限切れか期限切れ間近の証明書を表示するなど、IBM Cloud サービスによる洞察を一元化します。[セキュリティー・アドバイザーの詳細はこちら](/docs/services/security-advisor/index.html#index)</td>
  </tr>
</table>
