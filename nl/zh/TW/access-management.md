---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

keywords: certificates, SSL,

subcollection: certificate-manager

---

{:new_window: target="_blank"}
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

# 管理服務存取角色
{: #managing-service-access-roles}

您可以保護 {{site.data.keyword.cloud_notm}} 內的服務，方法是只容許具有指定存取角色的使用者來完成特定動作。
{: shortdesc}

## 平台存取角色
{: #platform-access-roles}

您可以使用平台存取角色，讓使用者能對平台資源完成作業，例如在您的 {{site.data.keyword.cloud_notm}} 帳戶中建立或刪除實例。

<table>
<caption> 表 1. 對映至平台存取角色的動作</caption>
  <tr>
    <th> 動作</th>
    <th> 角色</th>
  </tr>
  <tr>
    <td>檢視 {{site.data.keyword.cloudcerts_short}} 的實例</td>
    <td> 管理者、操作員、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>建立 {{site.data.keyword.cloudcerts_short}} 的實例</td>
    <td> 管理者、編輯者</td>
  </tr>
  <tr>
    <td>刪除 {{site.data.keyword.cloudcerts_short}} 的實例</td>
    <td> 管理者、編輯者</td>
  </tr>
</table>

## 服務存取角色
{: #service-access-roles}

您可以使用服務存取角色，讓使用者能在 {{site.data.keyword.cloudcerts_short}} 實例中完成作業，例如匯入、下載、編輯或刪除憑證。

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
     <td>取得憑證 meta 資料</td>
     <td> 管理員、撰寫者、讀者</td>
  </tr>      
  <tr>
    <td>更新憑證的 meta 資料</td>
    <td> 管理員、撰寫者</td>
  </tr>
  <tr>
    <td>匯入或重新匯入憑證、私密金鑰及中繼憑證</td>
    <td> 管理員</td>
  </tr>
  <tr>
    <td>訂購憑證</td>
    <td> 管理員</td>
  </tr>
  <tr>
    <td>刪除憑證及私密金鑰</td>
    <td> 管理員</td>
  </tr>
      <tr>
        <td>列出所有通知頻道</td>
        <td> 管理員、撰寫者、讀者</td>
      </tr>
   <tr>
     <td>新增、更新或刪除通知頻道</td>
     <td> 管理員</td>
   </tr>
     <tr>
       <td>測試通知頻道</td>
       <td> 管理員、撰寫者、讀者</td>
     </tr>

</table>

如需使用者角色及許可權的相關資訊，請參閱[使用者角色](/docs/iam?topic=iam-userroles#userroles)。

## 配置使用者的存取原則
{: #configuring-access-policies}

您可以配置 {{site.data.keyword.cloudcerts_short}} 實例（以及該實例中所有憑證）的存取原則，也可以為實例內的個別憑證（資源）設定原則。


**角色配置的範例**

* 至少指派「檢視者」角色給每個使用者，以便每個使用者能看到服務實例。
* 如果您要讓使用者建立及刪除實例，請指派「管理者」或「編輯者」角色給該名使用者。
* 如果您要讓使用者在實例內檢視憑證，請至少指派「讀者」角色。

{: shortdesc}

### 配置存取原則
{: #configuring-access}

若要配置存取原則，請完成下列步驟：

1. 導覽至**管理 > 存取權 (IAM) > 使用者**。會顯示能存取您 {{site.data.keyword.cloud_notm}} 帳戶的使用者清單。
2. 按一下要獲指派存取原則的使用者名稱。如果未顯示使用者，請按一下**邀請使用者**，以[將使用者新增至 {{site.data.keyword.cloud_notm}} 帳戶](/docs/iam?topic=iam-iamuserinv#iamuserinv)。
3. 按一下**存取原則**，然後按一下**指派存取權**。
4. 按一下**指派對資源的存取權**。
5. 從**服務**功能表，選取 **Certificate Manager**。
6. 從**服務實例**功能表，選取 {{site.data.keyword.cloudcerts_short}} 實例，或使用預設值`所有實例`。
7. 指派[平台存取角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles)給使用者。
8. 指派[服務存取角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles)給使用者。
9. 按一下**指派**，以將存取原則指派給使用者。

### 容許存取特定憑證
{: #allow-access-to-specific-certificate}

若要容許存取特定憑證，請完成下列步驟：

1. [擷取憑證 ID](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id)。
2. 建立兩個存取原則：
   - 第一個原則：至少指派對服務實例的**檢視者**平台存取角色
   - 第二個原則：至少指派**讀者**服務存取角色
     - 在**資源類型**欄位中，輸入 `certificate`。
     - 在**資源 ID** 欄位中，輸入憑證 ID。

### 擷取憑證的 ID
{: #get-certificate-id}

若要擷取憑證的 ID，請完成下列步驟：

1. 從 {{site.data.keyword.cloud_notm}} 儀表板，選取 {{site.data.keyword.cloudcerts_short}} 實例。
2. 從服務詳細資料頁面上的導覽，選取**管理**。
3. 選取憑證。
4. 在憑證詳細資料中，找到憑證 CRN。
5. 複製憑證 ID。CRN 包含不同的值，全都以冒號 (`:`) 區隔。憑證 ID 是 CRN 中的最後一個值，例如 `e20cb664efcbfa2c2f57801230d246a6`
