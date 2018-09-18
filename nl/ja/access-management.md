---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# サービス・アクセス役割の管理
{: #managing-service-access-roles}

指定されたアクセス役割を持つユーザーのみに、特定のアクションの実行を許可することにより、{{site.data.keyword.Bluemix_notm}} 内のサービスを保護することができます。
{: shortdesc}


## プラットフォーム・アクセス役割
{: #platform-access-roles}

プラットフォーム・アクセス役割を使用して、ユーザーが {{site.data.keyword.Bluemix_notm}} アカウントのインスタンスの作成や削除など、プラットフォーム・リソースに関するタスクを完了できるようにすることができます。

<table>
<caption> 表 1. プラットフォーム・アクセス役割にマップされているアクション</caption>
  <tr>
    <th> アクション </th>
    <th> 役割 </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}} のインスタンスの表示</td>
    <td> 管理者、オペレーター、エディター、ビューアー </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}} のインスタンスの作成</td>
    <td> 管理者、エディター </td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudcerts_short}} のインスタンスの削除</td>
    <td> 管理者、エディター </td>
  </tr>
</table>


## サービス・アクセス役割
{: #service-access-roles}

サービス・アクセス役割を使用して、証明書のインポート、ダウンロード、編集、削除など、ユーザーが {{site.data.keyword.cloudcerts_short}} インスタンスでタスクを完了できるようにすることができます。

<table>
<caption> 表 2. サービス・アクセス役割にマップされているアクション</caption>
  <tr>
    <th> アクション </th>
    <th> 役割 </th>
  </tr>
  <tr>
    <td>証明書のリスト</td>
    <td> 管理者、ライター、リーダー </td>
  </tr>
  <tr>
    <td>証明書と秘密鍵のダウンロード </td>
    <td> 管理者、ライター </td>
  </tr>
  <tr>
    <td>証明書データの更新</td>
    <td> 管理者、ライター </td>
  </tr>
  <tr>
    <td>証明書、秘密鍵、および中間証明書のアップロード </td>
    <td> 管理者  </td>
  </tr>
  <tr>
    <td>証明書および秘密鍵の削除 </td>
    <td> 管理者 </td>
  </tr>
      <tr>
        <td>すべての通知チャネルのリスト </td>
        <td> 管理者、ライター、リーダー </td>
      </tr>
   <tr>
     <td>通知チャネルの追加、更新、または削除 </td>
     <td> 管理者 </td>
   </tr>
     <tr>
       <td>通知チャネルのテスト </td>
       <td> 管理者、ライター、リーダー </td>
     </tr>
</table>


ユーザーの役割と許可について詳しくは、『[ユーザーの役割](/docs/iam/users_roles.html#userroles)』を参照してください。


## ユーザーのアクセス・ポリシーの構成
{: #configuring-access-policies}

{{site.data.keyword.cloudcerts_short}} インスタンス (および、結果的にそのインスタンス内のすべての証明書) のアクセス・ポリシーを構成したり、インスタンス内の個々の証明書 (リソース) のポリシーを設定したりできます。
{: shortdesc}

1.  **「管理」>「アカウント」>「ユーザー」**に移動します。 {{site.data.keyword.Bluemix_notm}} アカウントにアクセスできるユーザーのリストが表示されます。
2.  アクセス・ポリシーを割り当てる対象のユーザーの名前をクリックします。 ユーザーが表示されていない場合は、**「ユーザーの招待」**をクリックして、[{{site.data.keyword.Bluemix_notm}} アカウントにユーザーを追加します](/docs/iam/iamuserinv.html#iamuserinv)。
3.  **「アクセス権限の割り当て」**をクリックします。
4.  **「リソースへのアクセス権限の割り当て」**をクリックします。
5.  **「サービス」**ドロップダウン・メニューから、**「Certificate Manager」**を選択します。
6.  **「サービス・インスタンス」**メニューから、{{site.data.keyword.cloudcerts_short}} インスタンスを選択するか、デフォルト値の`「すべてのインスタンス」`を使用します。
7.  オプション: 特定の証明書へのアクセスを構成します。
    1. [証明書 ID を取得します](#get-certificate-id)。
    2. **「リソース・タイプ」**フィールドに「`certificate`」と入力します。
    3. **「リソース ID」**フィールドに証明書 ID を入力します。
8.  ユーザーに[プラットフォーム・アクセス役割](#platform-access-roles)を割り当てます。
9.  ユーザーに[サービス・アクセス役割](#service-access-roles)を割り当てます。
10. **「割り当て」**をクリックして、ユーザーにアクセス・ポリシーを割り当てます。

**役割の割り振りの例:**
* すべてのユーザーがサービス・インスタンスを表示できるように、すべてのユーザーに少なくともビューアー役割を割り当てます。
* ユーザーがインスタンスを作成したり削除したりできるようにするには、ユーザーに管理者役割またはエディター役割を割り当てます。
* ユーザーがインスタンス内の証明書を表示できるようにするには、少なくともリーダー役割を割り当てます。

### 証明書の ID の取得
{: #get-certificate-id}

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.cloudcerts_short}} インスタンスを選択します。
2. 「サービスの詳細」ページのナビゲーションから、**「管理」**を選択します。
3. 証明書を選択します。
4. 証明書の詳細で、証明書の CRN を見つけます。
5. 証明書 ID をコピーします。 CRN には、すべてコロン (`:`) で区切られた異なる値が含まれています。 証明書 ID は、CRN の最後の値です。例: `e20cb664efcbfa2c2f57801230d246a6)`
