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

# 關於
{: #about-cloud-certs}

了解 {{site.data.keyword.cloudcerts_full}}。

## 何謂 {{site.data.keyword.cloudcerts_short}}
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} 可協助您管理 {{site.data.keyword.IBM_notm}} 雲端型應用程式及服務的 SSL 憑證。
{: shortdesc}

您可以匯入針對應用程式及服務取得的 SSL 憑證、安全地儲存它們，以及取得所要使用憑證的中央視圖。

您可以使用下列方式管理憑證：

* 監視憑證的到期日，確定及時進行更新
* 檢視部署中的憑證類型，並確定它們符合組織原則
* 尋找在發出新相符性或安全需求時需要取代的憑證
* 設定您可存取及管理憑證的控制項

## 可用性
{: #availability}

只有在美國南部地區才能使用 {{site.data.keyword.cloudcerts_short}}。

## 私密金鑰安全
{: #private-key-security}

當您將憑證及對應私密金鑰匯入至 {{site.data.keyword.cloudcerts_short}} 時，服務會使用「進階加密標準 (AES) 256」演算法來加密私密金鑰。{{site.data.keyword.cloudcerts_short}} 會儲存這個唯一加密金鑰，以與服務實例搭配使用。

## 身分及存取管理
{: #identity-access-management}

您可以保護 {{site.data.keyword.Bluemix_notm}} 內的服務，方法是只容許具有指定角色的使用者來完成特定動作。
{: shortdesc}

<table>
<caption> 表 1. 對映至使用者角色的動作</caption>
  <tr>
    <th> 動作</th>
    <th> 角色</th>
  </tr>
  <tr>
    <td>列出認證</td>
    <td> 管理者、操作員、編輯者、檢視者</td>
  </tr>
  <tr>
    <td>下載憑證及私密金鑰</td>
    <td> 管理者、操作員</td>
  </tr>
  <tr>
    <td>更新憑證資料</td>
    <td> 管理者、編輯者</td>
  </tr>
  <tr>
    <td>上傳憑證、私密金鑰及中繼憑證</td>
    <td> 管理者、編輯者</td>
  </tr>
  <tr>
    <td>刪除憑證及私密金鑰</td>
    <td> 管理者、編輯者</td>
  </tr>
</table>

如需使用者角色及許可權的相關資訊，請參閱[使用者角色](/docs/admin/patterns.html#userroles)。

### 指派使用者角色
{: #assigning-user-roles}

若要指派帳戶層次或資源群組層次的使用者角色，請完成下列步驟。
如果使用者不屬於您的組織，請從將邀請傳送至該使用者開始。

1. 移至**管理 > 帳戶 > 使用者**。
2. 從**動作**功能表中，選取**指派原則**。
3. 按一下**指派資源的存取權**或**指派資源群組內的存取權**。
4. 在**服務**下方，選取**憑證管理員**。
5. 選用項目：選取**地區**，或使用預設值：**所有地區**。
6. 選用項目：選取**服務實例**，或使用預設值：**所有實例**。
7. 在**選取角色 > 指派平台存取角色**下方，選取適當的存取層次。
