---
copyright:
  years: 2017, 2018
lastupdated: "2018-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# API を使用した証明書の管理
{: #managing-certificates-by-using-api}

{{site.data.keyword.cloudcerts_full}} サービスは、証明書をインポート、取得、および削除するための REST エンドポイントを提供します。 {{site.data.keyword.iamshort}} を使用して、[特定の証明書のポリシーを割り当てる](#assigning-advanced-policies)こともできます。
{: shortdesc}

## API のテスト
{: #testing}

REST エンドポイントのテストは、Swagger を使用するか、コマンド・ラインで cURL 要求を実行して行うことができます。  
Swagger は、米国南部の {{site.data.keyword.Bluemix_notm}} 地域でのみ使用可能です。
{: shortdesc}

## 前提条件
{: #prereq-api}

{{site.data.keyword.cloudcerts_full}} を使用する前に、以下のタスクを実行する必要があります。
{: shortdesc}

* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) をインストールして、必要なデータを取得します。

* {{site.data.keyword.cloudcerts_short}} API で作業する際、呼び出しで以下の変数を使用できます。


<table>
<caption> 表 1. コマンドのコンポーネントの説明 </caption>
  <tr>
    <th> コンポーネント </th>
    <th> 説明 </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> {{site.data.keyword.iamshort}} (IAM) アクセス・トークンを取得するには、{{site.data.keyword.Bluemix_notm}} にログインし、<code>bx iam oauth-tokens</code> コマンドを実行します。 </td>
  </tr>
  <tr>
    <td> <code>certificateId</code> </td>
    <td> インポート後に証明書に割り当てられる[クラウド・リソース名 (CRN、Cloud Resource Name) ベースの証明書 ID](/docs/overview/crn.html#format)。証明書 ID は、次のいずれかの選択方法を使用して見つけることができます。 <ul><li> サービスの「管理」タブの「証明書」テーブルで、証明書の情報を選択して表示します。<li> API を通して、[使用可能な証明書をリストします](/docs/services/certificate-manager/rest-api.html#list-certificates)。</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> 作成後にサービス・インスタンスに割り当てられる [Cloud Resource Name (CRN) ベースのインスタンス ID](/docs/overview/crn.html#format)。 インスタンス ID は、次のいずれかの方法で取得できます。
    <ul>
      <li>サービスの「管理」ページで取得します。</li>
      <li><i>&lt;Instance_Name&gt;</i> をサービス・インスタンスの名前に置き換えて、<code>bx resource service-instance</code> コマンドを実行します。
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>{{site.data.keyword.Bluemix_notm}} Resource Controller の <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST エンドポイントを呼び出します。これには、アカウント管理者の IAM トークンに <code>Authorization</code> ヘッダーが必要です。</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> {{site.data.keyword.Bluemix_notm}} アカウントを管理するユーザーのアカウント ID。 アカウント ID を検出するには、<code>bx info</code> コマンドを実行します。 </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> サービスが作成された {{site.data.keyword.Bluemix_notm}} 地域内のサービスの URL。 この URL は、Swagger UI で検出できます。 </td>
  </tr>
  <tr>
    <td>  <code> name (Optional) </code> </td>
    <td> インポートされた証明書の表示名。 </td>
  </tr>
  <tr>
    <td> <code> description (Optional) </code> </td>
    <td> インポートされた証明書の説明。 </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> 証明書データ、エスケープ。 </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> 秘密鍵データ、エスケープ。 </td>
  </tr>
  <tr>
    <td> <code> intermediate (Optional) </code> </td>
    <td> 中間証明書データ、エスケープ。 </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>アクセス・ポリシーを割り当てる対象のユーザーの ID。 ユーザー ID を見つけるには、[ユーザー ID の取得](#retrieve-user-id)を参照してください。 </td>
  </tr>
</table>

## 証明書のインポート
{: #import-certificate}  

証明書を Privacy-enhanced Electronic Mail (PEM) フォーマットで秘密鍵とともにインポートします。 また、中間証明書もインポートできます。
{: shortdesc}


以下の `curl` コマンドを実行します。

  ```
  curl -X POST &#xa5;
  https://<cluster-url>/api/v2/<instanceId>/certificates/import &#xa5;
  -H 'authorization: Bearer <IAM-token>' &#xa5;
  -H 'content-type: application/json' &#xa5;
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
    {: pre}

_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_、_&lt;description&gt;_、_&lt;certificate&gt;_、 _&lt;privateKey&gt;_、および _&lt;intermediate&gt;_ は、適切な値に置き換えてください。 _&lt;name&gt;_、_&lt;description&gt;_、および _&lt;intermediate&gt;_ の各値はオプションです。

## 証明書メタデータの更新
{: #update-certificate-metadata}  

証明書のオプションの `name`、`description`、または両方のプロパティーを更新します。

**注**: 更新操作は、1 分当たり 5 アクションに制限されています。  
{: shortdesc}

以下の `curl` コマンドを実行します。

  ```
  curl -X POST &#xa5;
  https://<cluster-url>/api/v2/certificate/<certificateId> &#xa5;
  -H 'authorization: Bearer <IAM-token>' &#xa5;
  -H 'content-type: application/json' &#xa5;
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```

{: pre}

_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;certificateId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_、および _&lt;description&gt;_ は、適切な値に置き換えてください。

## すべての証明書をリスト
{: #list-certificates}  

使用可能なすべての証明書のリストを取得します。
{: shortdesc}

以下の `curl` コマンドを実行します。

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```

  {: pre}

_&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、および _&lt;instanceId&gt;_ は、適切な値に置き換えてください。

## 証明書のダウンロード
{: #get-certificate}  

取得した証明書 ID を使用して、証明書のデータをダウンロードします。
{: shortdesc}

以下の `curl` コマンドを実行します。

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

{: pre}

_&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、および _&lt;certificateId&gt;_ は、適切な値に置き換えてください。

## 証明書の削除
{: #delete-certificate}  

取得した証明書 ID を使用して、証明書とそのデータを削除します。
{: shortdesc}

以下の `curl` コマンドを実行します。

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

  {: pre}

_&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、および _&lt;certificateId&gt;_ は、適切な値に置き換えてください。

## 拡張ポリシーの割り当て
{: #assigning-advanced-policies}

特定のユーザーが特定の証明書に対して特定のアクションを実行することを許可することを選択できます。 ユーザーに対して、使用可能なサービス・インスタンス証明書のサブセットのみを表示することを許可することもできます。
{: shortdesc}

ポリシーを割り当てるには、以下の `curl` コマンドを実行して {{site.data.keyword.iamshort}} に要求を送信します。 このコマンドは、それぞれの証明書について繰り返してください。

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<account-id>/users/<user-id>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <Account-Admin-IAM-token>' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{
        "roles": [
        {
            "id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }
    ],
    "resources": [
        {
            "serviceName”: "cloudcerts",
            "serviceInstance": "<instanceId>",
            "resourceType": "certificate",
            "resource": "<certificateId>"
        }
    ]
}'
```
{: pre}

_&lt;account-id&gt;_、_&lt;user-id&gt;_、_&lt;instanceId&gt;_、および _&lt;certificateId&gt;_ は、適切な値に置き換えてください。
_&lt;Account-Admin-IAM-token&gt;_ は、アカウント管理者の IAM トークンに置き換えます。
_&lt;region&gt;_ は、ユーザーの地域に置き換えます。例えば、米国南部であれば `ng` に置き換えます。

**注**: 前の cURL 要求で、<code>instanceId</code> と <code>certificateId</code> は CRN ベースではなく、GUID ベースです。  
例えば、次の <code>certificateId</code> CRN では、instanceId 値は **58866f34-55ca-4477-8c32-fda435f01f97** で、certificateId 値は **e20cb664efcbfa2c2f57801230d246a6** です。

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97:certificate:e20cb664efcbfa2c2f57801230d246a6
```

### ユーザー ID の取得
{: #retrieve-user-id}

ユーザー ID を取得します。
{: shortdesc}

ユーザー ID を取得するには、以下のステップを実行します。

1. ユーザーに、[IAM トークンを提供](/docs/services/certificate-manager/rest-api.html#prereq-api)するよう依頼します。 IAM トークンの構造は、次のフォーマットになります。`<value_1>.<value_2>.<value_3>`
2. _&lt;value_2&gt;_ の値をコピーし、次の `echo` コマンドを実行します。

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   結果として、以下の出力に似た JSON オブジェクトが表示されます。

   ```
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

3. `id` プロパティーの値をコピーします。
