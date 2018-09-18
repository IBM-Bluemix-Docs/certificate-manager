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

# 管理服务访问角色
{: #managing-service-access-roles}

您可以通过仅允许具有指定访问角色的用户完成特定操作，在 {{site.data.keyword.Bluemix_notm}} 中保护服务。
{: shortdesc}


## 平台访问角色
{: #platform-access-roles}

您可以使用平台访问角色以支持用户针对平台资源完成任务，例如，在 {{site.data.keyword.Bluemix_notm}} 帐户中创建或删除实例。

<table>
<caption> 表 1. 映射到平台访问角色的操作</caption>
  <tr>
    <th> 操作 </th>
    <th> 角色 </th>
  </tr>
  <tr>
    <td>查看 {{site.data.keyword.cloudcerts_short}} 实例</td>
    <td> 管理员、操作员、编辑者、查看者 </td>
  </tr>
  <tr>
    <td>创建 {{site.data.keyword.cloudcerts_short}} 实例</td>
    <td> 管理员、编辑者 </td>
  </tr>
  <tr>
    <td>删除 {{site.data.keyword.cloudcerts_short}} 实例</td>
    <td> 管理员、编辑者 </td>
  </tr>
</table>


## 服务访问角色
{: #service-access-roles}

您可以使用服务访问角色以支持用户在 {{site.data.keyword.cloudcerts_short}} 实例中完成任务，例如，导入、下载、编辑或删除证书。

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
      <tr>
        <td>列出所有通知通道</td>
        <td> 管理员、作者和读者</td>
      </tr>
   <tr>
     <td>添加、更新或删除通知通道</td>
     <td> 管理员</td>
   </tr>
     <tr>
       <td>测试通知通道</td>
       <td> 管理员、作者和读者</td>
     </tr>
</table>


有关用户角色和许可权的更多信息，请参阅[用户角色](/docs/iam/users_roles.html#userroles)。


## 配置用户的访问策略
{: #configuring-access-policies}

您可以为 {{site.data.keyword.cloudcerts_short}} 实例配置访问策略（因此也可以为该实例中的所有证书配置访问策略），也可以为实例中的单个证书（资源）设置策略。
{: shortdesc}

1.  导航至**管理 > 帐户 > 用户**。这将显示有权访问 {{site.data.keyword.Bluemix_notm}} 帐户的用户的列表。
2.  单击要向其分配访问策略的用户的名称。如果未显示用户，请单击**邀请用户**以[将用户添加到 {{site.data.keyword.Bluemix_notm}} 帐户](/docs/iam/iamuserinv.html#iamuserinv)。
3.  单击**分配访问权**。
4.  单击**分配对资源的访问权**。
5.  从**服务**下拉菜单中，选择 **Certificate Manager**。
6.  从**服务实例**菜单中，选择 {{site.data.keyword.cloudcerts_short}} 实例，或者使用缺省值`所有实例`。
7.  可选：配置对特定证书的访问权。
    1. [检索证书标识](#get-certificate-id)。
    2. 在**资源类型**字段中，输入`证书`。
    3. 在**资源标识**字段中，输入证书标识。
8.  向用户分配[平台访问角色](#platform-access-roles)。
9.  向用户分配[服务访问角色](#service-access-roles)。
10. 单击**分配**以便为用户分配访问策略。

**角色分配的示例：**
* 至少将查看者角色分配给每个用户，从而使每个用户可查看服务实例。
* 如果想要用户创建/删除实例，那么将管理员或编辑者角色分配给此用户。
* 如果想要用户查看实例中的证书，那么至少分配读者角色。

### 检索证书标识
{: #get-certificate-id}

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，选择 {{site.data.keyword.cloudcerts_short}} 实例。
2. 在“服务详细信息”页面上的导航中，选择**管理**。
3. 选择证书。
4. 在证书详细信息中，找到证书 CRN。
5. 复制证书标识。CRN 包含不同的值，所有值之间均用冒号 (`:`) 分隔。证书标识是 CRN 中的最新值；例如：`e20cb664efcbfa2c2f57801230d246a6)`
