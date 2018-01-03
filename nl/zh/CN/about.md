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

# 关于
{: #about-cloud-certs}

了解 {{site.data.keyword.cloudcerts_full}}。

## 什么是 {{site.data.keyword.cloudcerts_short}}
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} 可帮助您管理基于 {{site.data.keyword.IBM_notm}} 云的应用程序和服务的 SSL 证书。
{: shortdesc}

您可以导入为应用程序和服务获取的 SSL 证书，安全地存储它们并集中查看正在使用的证书。

您可以通过以下方式来管理您的证书：

* 监视证书的到期日期，以确保准时更新证书
* 跨部署查看证书的类型并确保它们满足组织策略
* 发出新合规性或安全性需求时，查找需要替换的证书
* 控制谁可以访问和管理证书

## 可用性
{: #availability}

{{site.data.keyword.cloudcerts_short}} 仅在美国南部区域提供。

## 专用密钥安全性
{: #private-key-security}

当您将证书及相应专用密钥导入到 {{site.data.keyword.cloudcerts_short}} 时，该服务将使用高级加密标准 (AES) 256 算法来加密专用密钥。{{site.data.keyword.cloudcerts_short}} 会保存此唯一加密密钥以使用服务实例。

## 身份与访问管理
{: #identity-access-management}

您可以通过仅允许具有指定角色的用户完成特定操作，在 {{site.data.keyword.Bluemix_notm}} 中保护服务。
{: shortdesc}

<table>
<caption> 表 1. 映射到用户角色的操作</caption>
  <tr>
    <th> 操作 </th>
    <th> 角色 </th>
  </tr>
  <tr>
    <td>列示证书 </td>
    <td> 管理员、操作员、编辑者、查看者 </td>
  </tr>
  <tr>
    <td>下载证书和专用密钥 </td>
    <td> 管理员、操作员 </td>
  </tr>
  <tr>
    <td>更新证书数据 </td>
    <td> 管理员、编辑者 </td>
  </tr>
  <tr>
    <td>上传证书、专用密钥和中间证书 </td>
    <td> 管理员、编辑者 </td>
  </tr>
  <tr>
    <td>删除证书和专用密钥 </td>
    <td> 管理员、编辑者 </td>
  </tr>
</table>

有关用户角色和许可权的更多信息，请参阅[用户角色](/docs/admin/patterns.html#userroles)。

### 分配用户角色
{: #assigning-user-roles}

要在帐户级别或资源组级别分配用户角色，请完成以下步骤。如果用户不属于组织，请从向该用户发送邀请开始。

1. 转至**管理 > 帐户 > 用户**。
2. 从**操作**菜单中，选择**分配策略**。
3. 单击**分配资源的访问权**或**在资源组中分配访问权**。
4. 在**服务**下，选择 **Certificate Manager**。
5. 可选：选择**区域**或使用缺省值**所有区域**。
6. 可选：选择**服务实例**或使用缺省值**所有实例**。
7. 在**选择角色 > 分配平台访问角色**下，选择相应的访问级别。
