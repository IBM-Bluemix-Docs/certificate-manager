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

# 管理服务访问角色
{: #managing-service-access-roles}

您可以通过仅允许具有指定访问角色的用户完成特定操作，在 {{site.data.keyword.cloud_notm}} 中保护服务。
{: shortdesc}

## 平台访问角色
{: #platform-access-roles}

您可以使用平台访问角色以支持用户针对平台资源完成任务，例如，在 {{site.data.keyword.cloud_notm}} 帐户中创建或删除实例。

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
    <td> 管理者、写入者和读取者</td>
  </tr>
  <tr>
    <td>下载证书和专用密钥 </td>
    <td> 管理者和写入者</td>
  </tr>
  <tr>
     <td>获取证书元数据</td>
     <td> 管理者、写入者和读取者</td>
  </tr>      
  <tr>
    <td>更新证书的元数据</td>
    <td> 管理者和写入者</td>
  </tr>
  <tr>
    <td>导入或重新导入证书、专用密钥和中间证书</td>
    <td> 管理者</td>
  </tr>
  <tr>
    <td>订购证书</td>
    <td> 管理者</td>
  </tr>
  <tr>
    <td>删除证书和专用密钥 </td>
    <td> 管理者</td>
  </tr>
      <tr>
        <td>列出所有通知通道</td>
        <td> 管理者、写入者和读取者</td>
      </tr>
   <tr>
     <td>添加、更新或删除通知通道</td>
     <td> 管理者</td>
   </tr>
     <tr>
       <td>测试通知通道</td>
       <td> 管理者、写入者和读取者</td>
     </tr>

</table>

有关用户角色和许可权的更多信息，请参阅[用户角色](/docs/iam?topic=iam-userroles#userroles)。

## 配置用户的访问策略
{: #configuring-access-policies}

您可以为 {{site.data.keyword.cloudcerts_short}} 实例配置访问策略（因此也可以为该实例中的所有证书配置访问策略），也可以为实例中的单个证书（资源）设置策略。


**角色分配的示例**

* 至少将查看者角色分配给每个用户，从而使每个用户都可查看服务实例。
* 如果想要用户创建和删除实例，那么将管理员或编辑者角色分配给该用户。
* 如果想要用户查看实例中的证书，那么至少分配读取者角色。

{: shortdesc}

### 配置访问策略
{: #configuring-access}

要配置访问策略，请完成以下步骤：

1. 转至**管理 > 访问权 (IAM) > 用户**。这将显示有权访问 {{site.data.keyword.cloud_notm}} 帐户的用户的列表。
2. 单击要向其分配访问策略的用户的名称。如果未显示用户，请单击**邀请用户**以[将用户添加到 {{site.data.keyword.cloud_notm}} 帐户](/docs/iam?topic=iam-iamuserinv#iamuserinv)。
3. 单击**访问策略**，然后单击**分配访问权**。
4. 单击**分配对资源的访问权**。
5. 从**服务**菜单中，选择 **Certificate Manager**。
6. 从**服务实例**菜单中，选择 {{site.data.keyword.cloudcerts_short}} 实例，或者使用缺省值`所有实例`。
7. 向用户分配[平台访问角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles)。
8. 向用户分配[服务访问角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles)。
9. 单击**分配**以便为用户分配访问策略。

### 允许访问特定证书
{: #allow-access-to-specific-certificate}

要允许访问特定证书，请完成以下步骤：

1. [检索证书标识](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id)。
2. 创建两个访问策略：
   - 第一个策略：至少分配对服务实例的**查看者**平台访问角色
   - 第二个策略：至少分配**读取者**服务访问角色
     - 在**资源类型**字段中，输入`证书`。
     - 在**资源标识**字段中，输入证书标识。

### 检索证书标识
{: #get-certificate-id}

要检索证书的标识，请完成以下步骤：

1. 在 {{site.data.keyword.cloud_notm}}“仪表板”中，选择 {{site.data.keyword.cloudcerts_short}} 实例。
2. 在“服务详细信息”页面上的导航中，选择**管理**。
3. 选择证书。
4. 在证书详细信息中，找到证书 CRN。
5. 复制证书标识。CRN 包含不同的值，所有值之间均用冒号 (`:`) 分隔。证书标识是 CRN 中的最后一个值；例如：`e20cb664efcbfa2c2f57801230d246a6`
