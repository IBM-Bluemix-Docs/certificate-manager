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

# 在 GUI 中管理证书
{: #managing-certificates-ui}

您可以使用 {{site.data.keyword.cloudcerts_full}} 服务 GUI 来管理您从第三方签发者获取的证书，以使用基于 {{site.data.keyword.IBM_notm}} 云的应用程序或服务。在导入证书和密钥后，该服务即会对它们进行加密和存储。
{: shortdesc}

## 导入证书
{: #importing-a-certificate}

为了帮助您管理证书，您可以将它们上传。
{: shortdesc}

开始之前：

* 使用匹配的专用密钥，创建有效的未到期证书。
* 将文件转换为隐私加强电子邮件 (PEM) 格式。
* 使专用密钥保持未加密状态以确保可以导入该密钥。

要导入证书，请单击**导入证书**并提供以下详细信息：

1. 可选：输入显示名称。
2. 单击**浏览**，选择 PEM 格式的证书文件。
3. 单击**浏览**，选择 PEM 格式的证书专用密钥。
4. 如果适用的话，以 PEM 格式提供中间证书文件。
5. 可选：输入描述。
6. 单击**导入**。  

**注**：要更新已导入的证书，请从您的认证中心 (CA) 获取新证书，并将新证书导入到 {{site.data.keyword.cloudcerts_short}}。在部署新证书后，您可以删除旧的证书。

导入证书后，以下信息会显示在证书表中。要查看更多证书信息，您可以在表行中选择证书。

<table>
<caption> 表 1. 已导入证书的信息</caption>
  <tr>
    <th> 组件</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td>名称</td>
    <td>可选：显示名称。</td>
  </tr>
  <tr>
    <td>描述</td>
    <td>可选：证书的描述性文本。</td>
  </tr>
  <tr>
    <td>域</td>
    <td>证书有效的域。</td>
  </tr>
  <tr>
    <td>签发者</td>
    <td>签发证书的 CA。</td>
  </tr>
  <tr>
    <td>算法</td>
    <td>创建证书所使用的加密类型。</td>
  </tr>
  <tr>
    <td>密钥算法</td>
    <td>算法所使用的密钥类型和大小。</td>
  </tr>
  <tr>
    <td>离到期日还有 </td>
    <td>证书到期的剩余天数。</td>
  </tr>
  <tr>
    <td>签发日期</td>
    <td>签发证书的日期。</td>
  </tr>
  <tr>
    <td>有效开始日期</td>
    <td>证书开始有效的日期。</td>
  </tr>
  <tr>
    <td>到期日期</td>
    <td>证书不再有效的日期。</td>
  </tr>
  <tr>
    <td>证书标识</td>
    <td>导入时为证书提供的生成标识。</td>
  </tr>
</table>

## 搜索证书
{: #searching-certificates}
 
如果您管理许多证书，那么您可以使用搜索栏来查找所需证书。
{: shortdesc}
 
-   要搜索证书名称、证书域或证书签发者，请在搜索栏中输入搜索项并按 Enter。
-   要查看所有证书，请单击搜索栏中的 **X** 图标。

## 下载证书
{: #downloading-certificates}

当您准备好向应用程序或服务部署证书时，您可以下载证书和关联的专用密钥。
{: shortdesc}

要下载证书，请执行以下操作：

1. 选择要下载的证书的复选框。
2. 单击**下载证书**。根据导入到服务中的项目，您会收到压缩文件，其中包含证书的 PEM 文件、关联的专用密钥和关联的中间证书。


## 删除证书
{: #deleting-certificates}

如果您想要停止跟踪证书，可以将其删除。
{: shortdesc}  

要删除证书，请执行以下操作：

1. 选择要删除的证书的复选框。
2. 单击**废纸篓**图标。

## 更新证书元数据
{: #updating-certificates-metadata}

您还可以更新证书的名称和描述。
{: shortdesc}

要更新证书，请执行以下操作：

1. 选择某行以打开该证书的详细信息。
2. 更新名称或描述。
3. 保存更改。

**注**：每分钟最多可以执行 5 个更新操作。
