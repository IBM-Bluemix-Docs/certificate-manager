---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 製品情報
{: #about-cloud-certs}

{{site.data.keyword.cloudcerts_full}} について説明します。

## {{site.data.keyword.cloudcerts_short}} の概要
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} は、{{site.data.keyword.IBM_notm}} Cloud ベースのアプリおよびサービス用の SSL 証明書の管理を支援します。
{: shortdesc}

アプリおよびサービス用に取得する SSL 証明書をインポートし、それらを安全に保管し、使用している証明書を集中して表示することができます。

証明書は、以下の方法で管理できます。

* 証明書の更新が予定どおりに行われるように、証明書の有効期限日付をモニターする
* 複数のデプロイメントにわたって証明書のタイプを表示し、それらが組織のポリシーに一致していることを確認する
* 新しいコンプライアンス要件またはセキュリティー要件が出されたときに置き換える必要がある証明書を見つける
* 証明書のアクセスおよび管理を行えるユーザーについて制御を設定する

## 可用性
{: #availability}

{{site.data.keyword.cloudcerts_short}} は、米国南部地域でのみ使用可能です。

## 秘密鍵のセキュリティー
{: #private-key-security}

証明書と、対応する秘密鍵を {{site.data.keyword.cloudcerts_short}} にインポートすると、サービスは Advanced Encryption Standard (AES) 256 アルゴリズムを使用して秘密鍵を暗号化します。{{site.data.keyword.cloudcerts_short}} は、サービス・インスタンスで使用するために、この暗号化された固有鍵を保存します。

## ID およびアクセス権の管理
{: #identity-access-management}

指定された役割のユーザーのみに、特定のアクションの実行を許可することにより、{{site.data.keyword.Bluemix_notm}} 内のサービスを保護することができます。
{: shortdesc}

<table>
<caption> 表 1. ユーザーの役割にマップされているアクション</caption>
  <tr>
    <th> アクション </th>
    <th> 役割</th>
  </tr>
  <tr>
    <td>証明書のリスト</td>
    <td> 管理者、オペレーター、エディター、ビューアー </td>
  </tr>
  <tr>
    <td>証明書と秘密鍵のダウンロード </td>
    <td> 管理者、オペレーター </td>
  </tr>
  <tr>
    <td>証明書データの更新</td>
    <td> 管理者、エディター</td>
  </tr>
  <tr>
    <td>証明書、秘密鍵、および中間証明書のアップロード </td>
    <td> 管理者、エディター</td>
  </tr>
  <tr>
    <td>証明書および秘密鍵の削除 </td>
    <td> 管理者、エディター</td>
  </tr>
</table>

ユーザーの役割と許可について詳しくは、『[ユーザーの役割](/docs/admin/patterns.html#userroles)』を参照してください。

### ユーザーの役割の割り当て
{: #assigning-user-roles}

アカウント・レベルまたはリソース・グループ・レベルでユーザーの役割を割り当てるには、以下のステップを実行してください。ユーザーが組織の一員でない場合は、そのユーザーに招待状を送信して開始します。

1. **「管理」>「アカウント」>「ユーザー」**に移動します。
2. **「アクション」**メニューから、**「ポリシーの割り当て」**を選択します。
3. **「リソースへのアクセス権の割り当て (Assign access to resources)」**または**「リソース・グループ内のアクセス権の割り当て (Assign access within a resource group)」**をクリックします。
4. **「サービス」**の下から、**「Certificate Manager」**を選択します。
5. オプション: **「地域」**を選択するか、デフォルトの**「すべての地域」**を使用します。
6. オプション: **「サービス・インスタンス」**を選択するか、デフォルトの**「すべてのインスタンス (All instances)」**を使用します。
7. **「役割の選択 (Select roles)」>「プラットフォーム・アクセス役割の割り当て (Assign platform access roles)」**の下から、適切なアクセス・レベルを選択します。
