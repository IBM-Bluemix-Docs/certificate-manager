---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理服务访问角色
{: #managing-service-access-roles}

您可以通过仅允许具有指定访问角色的用户完成特定操作，在 {{site.data.keyword.Bluemix_notm}} 中保护服务。
{: shortdesc}

### 平台访问角色
{: #platform-access-roles}

您可以使用平台访问角色以支持用户针对平台资源完成任务，例如，在 IBM Cloud 帐户中创建或删除实例。

<table>
<caption> 表 1. 映射到平台访问角色的操作</caption>
  <tr>
    <th> 操作 </th>
    <th> 角色 </th>
  </tr>
  <tr>
    <td>查看 Certificate Manager 实例</td>
    <td> 管理员、操作员、编辑者、查看者 </td>
  </tr>
  <tr>
    <td>创建 Certificate Manager 实例</td>
    <td> 管理员、编辑者 </td>
  </tr>
  <tr>
    <td>删除 Certificate Manager 实例</td>
    <td> 管理员、编辑者 </td>
  </tr>
</table>

以前平台角色还会授予有关实例中证书的特定操作的访问权。此定义已过时且很快将被移除。

### 服务访问角色
{: #service-acceess-roles}

您可以使用服务访问角色以支持用户在 Certificate Manager 实例中完成任务，例如，导入、下载、编辑或删除证书。

<table>
<caption> 表 2. 映射到服务访问角色的操作</caption>
  <tr>
    <th> 操作 </th>
    <th> 角色 </th>
  </tr>
  <tr>
    <td>列示证书 </td>
    <td> 管理员、作者和读者</td>
  </tr>
  <tr>
    <td>下载证书和专用密钥 </td>
    <td> 管理员和作者</td>
  </tr>
  <tr>
    <td>更新证书数据 </td>
    <td> 管理员和作者</td>
  </tr>
  <tr>
    <td>上传证书、专用密钥和中间证书 </td>
    <td> 管理员</td>
  </tr>
  <tr>
    <td>删除证书和专用密钥 </td>
    <td> 管理员</td>
  </tr>
</table>


有关用户角色和许可权的更多信息，请参阅[用户角色](/docs/iam/users_roles.html#userroles)。

### 分配用户访问角色
{: #assigning-user--access-roles}

要在帐户级别或资源组级别分配访问角色，请完成以下步骤。如果用户不属于组织，请从向该用户发送邀请开始。

1. 转至**管理 > 帐户 > 用户**。
2. 从**操作**菜单中，选择**分配策略**。
3. 单击**分配资源的访问权**或**在资源组中分配访问权**。
4. 在**服务**下，选择 **Certificate Manager**。
5. 可选：选择**区域**或使用缺省值**所有区域**。
6. 可选：选择**服务实例**或使用缺省值**所有实例**。
7. 在**选择角色 > 分配平台/服务访问角色**下，选择相应的访问级别。

**示例：**
* 至少将查看者角色分配给每个用户，从而使每个用户可查看服务实例。 
* 如果想要用户创建实例，那么将管理员或编辑者角色分配给此用户。 
* 如果想要用户查看实例中的证书，那么至少分配读者角色。
