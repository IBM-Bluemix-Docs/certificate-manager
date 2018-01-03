---
copyright:
  years: 2017
lastupdated: "2017-12-14"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 使用 API 管理憑證
{: #managing-certificates-api}

{{site.data.keyword.cloudcerts_full}} 服務提供 REST 端點來匯入、取得及刪除憑證。使用 {{site.data.keyword.iamshort}}，您也可以[指派特定憑證的原則](#assigning-advanced-policies)。
{: shortdesc}

## 測試 API
{: #testing}

您可以使用 Swagger 或在指令行中執行 cURL 要求，來測試 REST 端點。  
只有在美國南部 {{site.data.keyword.Bluemix_notm}} 地區才能使用 Swagger。
{: shortdesc}

## 必要條件
{: #prereq-api}

您必須先完成下列作業，才能使用 {{site.data.keyword.cloudcerts_full}}。
{: shortdesc}

* 安裝 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started)，以取得必要資料。

* 當您使用 {{site.data.keyword.cloudcerts_short}} API 時，可以在呼叫中使用下列變數。


<table>
<caption> 表 1. 說明的指令元件</caption>
  <tr>
    <th> 元件</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> 您可以登入 {{site.data.keyword.Bluemix_notm}} 並執行 <code>bx iam oauth-tokens</code> 指令，來取得 {{site.data.keyword.iamshort}} (IAM) 存取記號。</td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> 您可以使用下列其中一個選項，來找到憑證 ID：<ul><li> 在 GUI 中，從「憑證」表格的列中選取憑證。<li> 從 API，[列出您可用的憑證](/docs/services/certificate-manager/rest-api.html#list-certificates)。</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> 在建立後指派給服務實例的[雲端資源名稱 (CRN) 型實例 ID](/docs/overview/crn.html#format)。您可以使用下列方式擷取實例 ID：
    <ul>
      <li>在服務的「管理」頁面中。</li>
      <li>執行 <code>bx resource service-instance</code> 指令，並將 <i>&lt;Instance_Name&gt;</i> 取代為您服務實例的名稱。
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>呼叫 {{site.data.keyword.Bluemix_notm}} 資源控制器 <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST 端點，這需要含帳戶管理者 IAM 記號的 <code>Authorization</code> 標頭。</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> 管理 {{site.data.keyword.Bluemix_notm}} 帳戶的使用者帳戶 ID。您可以執行 <code>bx info</code> 指令來找到帳戶 ID。</td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> 服務在建立它的 {{site.data.keyword.Bluemix_notm}} 地區中的 URL。您可以在 Swagger 使用者介面中找到 URL。</td>
  </tr>
  <tr>
    <td>  <code> name（選用）</code> </td>
    <td> 所匯入憑證的顯示名稱。</td>
  </tr>
  <tr>
    <td> <code> description（選用）</code> </td>
    <td> 所匯入憑證的說明。</td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> 憑證資料（已跳出）。</td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> 私密金鑰資料（已跳出）。</td>
  </tr>
  <tr>
    <td> <code> intermediate（選用）</code> </td>
    <td> 中繼憑證資料（已跳出）。</td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>要獲指派存取原則的使用者 ID。若要找到使用者 ID，請參閱[擷取使用者 ID](#retrieve-user-id)。</td>
  </tr>
</table>

## 匯入憑證
{: #import-certificate}  

使用憑證的私密金鑰，以「隱私權加強電子郵件 (PEM)」格式匯入憑證。您也可以匯入中繼憑證。
{: shortdesc}


執行下列 `curl` 指令：

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
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

將 _&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_、_&lt;description&gt;_、_&lt;certificate&gt;_、_&lt;privateKey&gt;_ 及 _&lt;intermediate&gt;_ 取代為適當值。_&lt;name&gt;_、_&lt;description&gt;_ 及 _&lt;intermediate&gt;_ 是選用值。

## 更新憑證 meta 資料
{: #update-certificate-metadata}  

更新憑證的選用 `name` 及（或）`description` 內容。

**附註**：更新作業每分鐘只能執行五個動作。  
{: shortdesc}


執行下列 `curl` 指令：

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```
  {: pre}

將 _&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;certificateId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_ 及 _&lt;description&gt;_ 取代為適當值。

## 列出所有憑證
{: #list-certificates}  

擷取所有可用憑證的清單。
{: shortdesc}

執行下列 `curl` 指令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/
  ```
  {: pre}

將 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_ 及 _&lt;instanceId&gt;_ 取代為適當值。

## 下載憑證
{: #get-certificate}  

使用所擷取的憑證 ID 來下載憑證資料。
{: shortdesc}

執行下列 `curl` 指令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

將 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_ 及 _&lt;certificateId&gt;_ 取代為適當值。

## 刪除憑證
{: #delete-certificate}  

使用所擷取的憑證 ID 來刪除憑證及其資料。
{: shortdesc}

執行下列 `curl` 指令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

將 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_ 及 _&lt;certificateId&gt;_ 取代為適當值。

## 指派進階原則
{: #assigning-advanced-policies}

您可以選擇容許特定使用者對特定憑證執行特定動作。您可能要容許使用者只檢視一小部分的可用服務實例憑證。
{: shortdesc}

若要指派原則，請執行下列 `curl` 指令，以將要求傳送至 {{site.data.keyword.iamshort}}。請針對每一個憑證重複此指令。

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

將 _&lt;account-id&gt;_、_&lt;user-id&gt;_、_&lt;instanceId&gt;_ 及 _&lt;certificateId&gt;_ 取代為適當值。
將 _&lt;Account-Admin-IAM-token&gt;_ 取代為帳戶管理者的 IAM 記號。
將 _&lt;region&gt;_ 取代為您的地區（例如，`ng` 表示美國南部）。

**附註**：在前面的 cURL 要求中，<code>instanceId</code> 不是 CRN 型，而是 GUID 型。  
例如，在下列 <code>instanceId</code> CRN 中，實例值是 **58866f34-55ca-4477-8c32-fda435f01f97**。

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97::
```

### 擷取使用者 ID
{: #retrieve-user-id}

擷取使用者 ID。
{: shortdesc}

若要擷取使用者 ID，請完成下列步驟：

1. 要求使用者[提供 IAM 記號](/docs/services/certificate-manager/rest-api.html#prereq-api)。IAM 記號結構的格式如下：`<value_1>.<value_2>.<value_3>`
2. 複製 _&lt;value_2&gt;_ 的值，並執行下列 `echo` 指令：

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   結果是與下列輸出類似的 JSON 物件：

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

3. 複製 `id` 內容的值。
