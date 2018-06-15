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

# 使用 API 管理证书
{: #managing-certificates-by-using-api}

{{site.data.keyword.cloudcerts_full}} 服务提供 REST 端点以导入、获取和删除证书。使用 {{site.data.keyword.iamshort}}，您还可以[为特定证书分配策略](#assigning-advanced-policies)。
{: shortdesc}

## 测试 API
{: #testing}

您可以使用 Swagger 或在命令行中运行 cURL 请求来测试 REST 端点。  
Swagger 仅在美国南部 {{site.data.keyword.Bluemix_notm}} 区域提供。
{: shortdesc}

## 先决条件
{: #prereq-api}

您必须完成以下任务才能使用 {{site.data.keyword.cloudcerts_full}}。
{: shortdesc}

* 安装 [{{site.data.keyword.Bluemix_notm}}CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) 以获取所需数据。

* 当您使用 {{site.data.keyword.cloudcerts_short}} API 时，您可以在调用中使用以下变量。


<table>
<caption> 表 1. 解释的命令组件 </caption>
  <tr>
    <th> 组件</th>
    <th> 解释 </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> 您可以登录到 {{site.data.keyword.Bluemix_notm}} 并运行 <code>bx iam oauth-tokens</code> 命令，以获取 {{site.data.keyword.iamshort}} (IAM) 访问令牌。</td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> [基于云资源名称 (CRN) 的证书标识](/docs/overview/crn.html#format)，导入后分配给证书。您可以使用以下其中一个选项来查找证书标识：<ul><li> 在服务的“管理”选项卡中，通过在“证书”表中进行选择查看证书信息。<li> 通过 API：[列示可用证书](/docs/services/certificate-manager/rest-api.html#list-certificates)。</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> [基于云资源名称 (CRN) 的实例标识](/docs/overview/crn.html#format)，创建后会分配给服务实例。您可以通过以下方式检索实例标识：
    <ul>
      <li>在服务的“管理”页面中。</li>
      <li>运行 <code>bx resource service-instance</code> 命令，将 <i>&lt;Instance_Name&gt;</i> 替换为您服务实例的名称。
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>调用 {{site.data.keyword.Bluemix_notm}} 资源控制器 <code>[GET/resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code> REST 端点，其需要具有帐户管理员 IAM 令牌的 <code>Authorization</code> 头。</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> 管理 {{site.data.keyword.Bluemix_notm}} 帐户的用户的帐户标识。您可以运行 <code>bx info</code> 命令来查找帐户标识。</td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> 创建服务的 {{site.data.keyword.Bluemix_notm}} 区域中该服务的 URL。您可以在 Swagger UI 中查找 URL。</td>
  </tr>
  <tr>
    <td>  <code> name（可选）</code> </td>
    <td> 已导入证书的显示名称。 </td>
  </tr>
  <tr>
    <td> <code> description（可选）</code> </td>
    <td> 已导入证书的描述。 </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> 已转义的证书数据。 </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> 已转义的专用密钥数据。 </td>
  </tr>
  <tr>
    <td> <code> intermediate（可选）</code> </td>
    <td> 已转义的中间证书数据。 </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>您要向其分配访问策略的用户的标识。要查找用户标识，请参阅[检索用户标识](#retrieve-user-id)。 </td>
  </tr>
</table>

## 导入证书
{: #import-certificate}  

以隐私加强电子邮件 (PEM) 格式导入证书及其专用密钥。您还可以导入中间证书。
{: shortdesc}


运行以下 `curl` 命令：

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/<instanceId>/certificates/import \
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

将 _&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_、_&lt;description&gt;_、_&lt;certificate&gt;_、_&lt;privateKey&gt;_ 和 _&lt;intermediate&gt;_ 替换为相应的值。_&lt;name&gt;_、_&lt;description&gt;_ 和 _&lt;intermediate&gt;_ 值是可选的。

## 更新证书元数据
{: #update-certificate-metadata}  

更新证书的可选 `name` 和/或 `description` 属性。

**注**：更新操作限制为每分钟五个操作。  
{: shortdesc}

运行以下 `curl` 命令：

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/certificate/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```

{: pre}

将 _&lt;cluster-url&gt;_、_&lt;instanceId&gt;_、_&lt;certificateId&gt;_、_&lt;IAM-token&gt;_、_&lt;name&gt;_ 和 _&lt;description&gt;_ 替换为相应的值。

## 列示所有证书
{: #list-certificates}  

检索所有可用证书的列表。
{: shortdesc}

运行以下 `curl` 命令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```

  {: pre}

将 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_ 和 _&lt;instanceId&gt;_ 替换为相应的值。

## 下载证书
{: #get-certificate}  

使用检索到的证书标识下载证书数据。
{: shortdesc}

运行以下 `curl` 命令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

{: pre}

将 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_ 和 _&lt;certificateId&gt;_ 替换为相应的值。

## 删除证书
{: #delete-certificate}  

使用检索到的证书标识删除证书及其数据。
{: shortdesc}

运行以下 `curl` 命令：

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

  {: pre}

将 _&lt;IAM-token&gt;_、_&lt;cluster-url&gt;_、_&lt;instanceId&gt;_ 和 _&lt;certificateId&gt;_ 替换为相应的值。

## 分配高级策略
{: #assigning-advanced-policies}

您可以选择允许特定用户对特定证书执行特定操作。您可能想要允许用户仅可以查看可用服务实例证书的子集。
{: shortdesc}

要分配策略，请运行以下 `curl` 命令，以向 {{site.data.keyword.iamshort}} 发送请求。针对每个证书重复该命令。

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

将 _&lt;account-id&gt;_、_&lt;user-id&gt;_、_&lt;instanceId&gt;_ 和 _&lt;certificateId&gt;_ 替换为相应的值。
将 _&lt;Account-Admin-IAM-token&gt;_ 替换为帐户管理员的 IAM 令牌。将 _&lt;region&gt;_ 替换为您的区域，例如美国南部为 `ng`。

**注**：在之前的 cURL 请求中，<code>instanceId</code> 和 <code>certificateId</code> 不是基于 CRN，而是基于 GUID。  
例如，在以下 <code>certificateId</code> CRN 中，instanceId 值为 **58866f34-55ca-4477-8c32-fda435f01f97** 且 certificateId 值为 **e20cb664efcbfa2c2f57801230d246a6**。

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97:certificate:e20cb664efcbfa2c2f57801230d246a6
```

### 检索用户标识
{: #retrieve-user-id}

检索用户标识。
{: shortdesc}

要检索用户标识，请完成以下步骤：

1. 要求用户[提供 IAM 令牌](/docs/services/certificate-manager/rest-api.html#prereq-api)。IAM 令牌结构格式如下：`<value_1>.<value_2>.<value_3>`
2. 复制 _&lt;value_2&gt;_ 的值并运行以下 `echo` 命令：

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   结果为类似以下输出的 JSON 对象：

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

3. 复制 `id` 属性的值。
