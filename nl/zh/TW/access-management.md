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

# 管理服務存取角色
{: #managing-service-access-roles}

您可以保護 {{site.data.keyword.Bluemix_notm}} 內的服務，方法是只容許具有指定存取角色的使用者來完成特定動作。
{: shortdesc}

### 平台存取角色
{: #platform-access-roles}

您可以使用平台存取角色，讓使用者能對平台資源完成作業，例如在您的 IBM Cloud 帳戶中建立或刪除實例。

<table>
<caption> 表 1. 對映至平台存取角色的動作</caption>
  <tr>
    <th> 動作</th>
    <th> 角色</th>
  </tr>
  <tr>
    <td>檢視 Certificate Manager 的實例</td>
    <td> 管理者、操作員、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>建立 Certificate Manager 的實例</td>
    <td> 管理者、編輯者</td>
  </tr>
  <tr>
    <td>刪除 Certificate Manager 的實例</td>
    <td> 管理者、編輯者</td>
  </tr>
</table>

在過去，平台角色也提供對實例內之憑證的特定動作存取權。此定義已作廢，且將在不久的將來移除。

### 服務存取角色
{: #service-acceess-roles}

您可以使用服務存取角色，讓使用者能在 Certificate Manager 實例中完成作業，例如匯入、下載、編輯或刪除憑證。

<table>
<caption> 表 2. 對映至服務存取角色的動作</caption>
  <tr>
    <th> 動作</th>
    <th> 角色</th>
  </tr>
  <tr>
    <td>列出認證</td>
    <td> 管理員、撰寫者、讀者</td>
  </tr>
  <tr>
    <td>下載憑證及私密金鑰</td>
    <td> 管理員、撰寫者</td>
  </tr>
  <tr>
    <td>更新憑證資料</td>
    <td> 管理員、撰寫者</td>
  </tr>
  <tr>
    <td>上傳憑證、私密金鑰及中繼憑證</td>
    <td> 管理員</td>
  </tr>
  <tr>
    <td>刪除憑證及私密金鑰</td>
    <td> 管理員</td>
  </tr>
</table>


如需使用者角色及許可權的相關資訊，請參閱[使用者角色](/docs/iam/users_roles.html#userroles)。

### 指派使用者存取角色
{: #assigning-user--access-roles}

若要指派帳戶層次或資源群組層次的存取角色，請完成下列步驟。如果使用者不屬於您的組織，請從將邀請傳送至該使用者開始。

1. 移至**管理 > 帳戶 > 使用者**。
2. 從**動作**功能表中，選取**指派原則**。
3. 按一下**指派資源的存取權**或**指派資源群組內的存取權**。
4. 在**服務**下方，選取**憑證管理員**。
5. 選用項目：選取**地區**，或使用預設值：**所有地區**。
6. 選用項目：選取**服務實例**，或使用預設值：**所有實例**。
7. 在**選取角色 > 指派平台/服務存取角色**下方，選取適當的存取層次。

**範例：**
* 至少指派「檢視者」角色給每個使用者，以便每個使用者能看到服務實例。 
* 如果您要讓使用者建立實例，請指派「管理者」或「編輯者」角色給該名使用者。 
* 如果您要讓使用者在實例內檢視憑證，請至少指派「讀者」角色。
