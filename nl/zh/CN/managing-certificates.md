---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL,

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

# 从仪表板管理证书
{: #managing-certificates-from-the-dashboard}

您可以使用 {{site.data.keyword.cloudcerts_full}} 服务仪表板来管理从第三方签发者获取的证书，以使用基于 {{site.data.keyword.IBM_notm}} 云的应用程序或服务。
{: shortdesc}

## 支持的证书格式和公用密钥算法
{: supported-formats-and-algorithms}

### 证书格式
* PEM

### 公用密钥算法
* Rivest-Shamir-Adleman (RSA)
* 数字签名算法 (DSA)
* 椭圆曲线数字签名算法 (ECDSA)
* 使用 Diffie-Hellman 的椭圆曲线密钥协商协议 (ECDH)

## 导入证书
{: #importing-a-certificate}

导入证书以便对它们进行管理。
{: shortdesc}

**开始之前**

* 使用匹配的专用密钥（密钥为可选），创建有效的未到期证书。
* 将文件转换为隐私加强电子邮件 (PEM) 格式。
* 使专用密钥保持未加密状态以确保可以导入该密钥。

要导入证书，请单击**导入证书**并提供以下详细信息：

1. 提供证书名称。
2. 单击**浏览**，选择 PEM 格式的证书文件。
3. 可选：单击**浏览**，选择 PEM 格式的证书专用密钥。
4. 如果适用的话，以 PEM 格式提供中间证书文件。
5. 可选：输入描述。
6. 单击**导入**。

导入证书后，以下信息会显示在证书表中。要查看有关证书的更多信息，可以在“证书”表中展开证书所在的行。

<table>
<caption> 表 1. 已导入证书的信息</caption>
  <tr>
    <th> 组件</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td>名称</td>
    <td>有意义的显示名称。最大长度为 256 个字符。</td>
  </tr>
  <tr>
    <td>描述</td>
    <td>（可选）证书的描述性文本。最大长度为 1024 个字符。</td>
  </tr>
  <tr>
    <td>域</td>
    <td>证书有效的域。</td>
  </tr>
  <tr>
    <td>签发者</td>
    <td>签发证书的认证中心 (CA)。</td>
  </tr>
  <tr>
    <td>算法</td>
    <td>证书签名算法。</td>
  </tr>
  <tr>
    <td>密钥算法</td>
    <td>公用密钥算法</td>
  </tr>
  <tr>
    <td>离到期日还有 </td>
    <td>证书到期的剩余天数。</td>
  </tr>
  <tr>
    <td>有效开始日期</td>
    <td>证书开始有效的日期（采用全球标准时间时区）。</td>
  </tr>
  <tr>
    <td>到期日期</td>
    <td>证书不再有效的日期（采用全球标准时间时区）。</td>
  </tr>
  <tr>
    <td>状态</td>
    <td>证书的状态。</td>
  </tr>
  <tr>
    <td>证书标识</td>
    <td>导入时为证书提供的生成标识。</td>
  </tr>
</table>

</br>

## 重新导入证书
{: #reimport-certificate}

如果证书即将到期，可以导入与现有证书具有相同域但到期日期为新日期的新证书版本来更新证书。重新导入证书时，会保留现有版本的证书作为备份，您可以根据需要进行下载。
{: shortdesc}

### 重新导入证书
{: #reimporting-certificate}

要重新导入证书，请完成以下步骤：

1. 展开证书所在的行。
2. 单击**重新导入证书**。
3. 单击**浏览**，选择 PEM 格式的新证书文件。
4. （可选）单击**浏览**，选择 PEM 格式的新证书专用密钥。
5. （可选）单击**浏览**，选择 PEM 格式的新中间证书文件。
6. 单击**重新导入**，然后单击**完成**。

重新导入证书限制为每分钟五个操作。
{: note}

### 下载先前版本的证书
{: #downloading-certificate}

要下载先前版本的证书，请完成以下步骤：

1. 展开证书所在的行。
2. 单击**先前版本**链接。

## 订购证书
{: #order-certificates}

订购证书之前，请[首先完成必需的设置](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates)。  
要订购证书，请单击**订购证书**，选择 **{{site.data.keyword.cis_full_notm}}** 或**其他 DNS 提供者**，然后提供以下详细信息：

1. 证书名称。
2. 认证中心。
3. 必需的域。
4. 适当的算法和密钥算法。
5. 单击**订购**。

订购证书限制为每个 {{site.data.keyword.cloudcerts_short}} 实例每分钟 5 个订购请求，每个 IBM 用户帐户每小时 100 个订购请求，每周对于相同域只能订购 5 个证书。
{: note}

## 更新证书
{: #renew-certificates}

要更新证书，请完成以下步骤：
  1. 单击要更新的证书所在行中的菜单。
  2. 单击**更新证书**。
  3. 可选：可以通过选中**再加密证书**复选框来选择对证书再加密。这将使用新密钥对来更新证书。
  
    对证书再加密后，请确保将新的证书和密钥部署到使用它们的所有位置。
  {: note}
    
  4. 单击**更新**。
  
  只能更新通过 {{site.data.keyword.cloudcerts_short}} 订购的证书。
  {: note}

更新证书限制为每分钟每个证书 5 个更新请求，每个 IBM 用户帐户每小时 100 个更新请求。
{: note}


## 搜索证书
{: #searching-certificates}

如果您管理许多证书，那么您可以使用搜索栏来查找所需证书。
{: shortdesc}

* 要搜索证书名称、证书域或证书签发者，请在搜索栏中输入搜索项并按 Enter。
* 要查看所有证书，请单击搜索栏中的 **X** 图标。

## 下载证书
{: #downloading-certificates}

当您准备好向应用程序或服务部署证书时，您可以下载证书和关联的专用密钥。
{: shortdesc}

要下载证书，请完成以下步骤：

1. 选择要下载的证书的复选框。
2. 单击**下载证书**。根据导入到服务中的项目，您会收到压缩文件，其中包含证书的 PEM 文件、关联的专用密钥和关联的中间证书。

无法下载到期的证书。
{: note}

## 删除证书
{: #deleting-certificates}

如果您想要停止跟踪证书，可以将其删除。
{: shortdesc}  

要删除证书，请完成以下步骤：

1. 选择要删除的证书的复选框。
2. 单击**废纸篓**图标。

## 更新证书元数据
{: #updating-certificates-metadata}

您还可以更新证书的名称和描述。
{: shortdesc}

要更新证书，请完成以下步骤：

1. 选择某行以打开该证书的详细信息。
2. 更新名称或描述。
3. 保存更改。

每分钟最多可执行五个更新操作。
{: note}
