---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# 訂購憑證
{: #ordering-certificates}

您可以使用 {{site.data.keyword.cloudcerts_long}} 為您的應用程式和服務訂購由支援的外部憑證管理中心簽署的公用 SSL/TLS 憑證。透過 {{site.data.keyword.cloudcerts_short}}，不僅可為 SSL/TLS 私密金鑰實現額外的安全，還能輕鬆訂購公用憑證。簽發您的憑證後，您可以將憑證部署到整合服務，也可以下載該憑證以在其他位置使用。  
{: shortdesc}

訂購憑證時，用於 SSL/TLS 的私密金鑰會直接在 {{site.data.keyword.cloudcerts_short}} 中產生並安全地儲存。對已簽發憑證的所有要求和存取權可以透過[存取控制](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles)進行管理，並使用 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events) 自動進行審核。  

{{site.data.keyword.cloudcerts_short}} 將自動憑證管理環境 (ACME) V2 通訊協定實作為 ACME 用戶端。透過 ACME 通訊協定，可以在沒有人為介入的情況下自動取得瀏覽器授信憑證。

## 憑證性質
{: #certificate-characteristics}

當您透過 {{site.data.keyword.cloudcerts_short}} 訂購憑證時：

- 它們是免費的
- 它們有效期間為 90 天
- 他們可以是單網域憑證、多網域憑證 (SAN) 或萬用字元憑證
- 它們經過網域驗證

網域驗證包含驗證您擁有要為其要求憑證的網域。如果需要延伸驗證 (EV) 憑證或組織驗證 (OV) 的憑證，您可以在其他地方取得這些憑證，然後將其匯入到 {{site.data.keyword.cloudcerts_short}} 以管理其生命週期。


## 支援的憑證管理中心
{: #supported-certificate-authorities}

憑證管理中心 (CA) 是簽發數位憑證的實體。對於憑證要求者和依賴憑證的用戶端，CA 可充當可信的第三方。
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) 是一個以 ACME 為基礎的自動化免費 CA，提供有效期為 90 天、經網域驗證過的憑證。這是由 Internet Security Research Group (ISRG) 提供的服務。

## 設定憑證訂購
{: #setup}

在向您簽發憑證之前，{{site.data.keyword.cloudcerts_short}} 必須驗證您是否有權控制要求中列出的所有網域。為了這麼做，{{site.data.keyword.cloudcerts_short}} 會使用 DNS 驗證。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} 以網域名稱系統 (DNS) TXT 記錄的形式傳送盤查，供您新增到 DNS 服務中。對於在憑證中要求的每個網域，您將獲得一個個別的 DNS TXT 記錄。新增 DNS TXT 記錄後，{{site.data.keyword.cloudcerts_short}} 和 Let’s Encrypt 會檢查此記錄是否已在 DNS 服務中。如果您順利完成了盤查，則會發出在 {{site.data.keyword.cloudcerts_short}} 實例中可用的 Let's Encrypt 憑證給您。

您驗證網域所有權的方式取決於您使用 {{site.data.keyword.cis_full_notm}} 還是另一個 DNS 提供者。


### {{site.data.keyword.cis_full_notm}}
{: #cis}

如果您在 {{site.data.keyword.cis_short}} 中管理網域，請完成下列步驟來驗證所有權：

1. 導覽至**{{site.data.keyword.cloud_notm}} >管理 > 存取權 (IAM) > 授權**。
2. 按一下**建立**，然後指派來源及目標服務。來源服務會根據您在下個步驟中設定的角色，而被授與對目標服務的存取權。
  * 來源：{{site.data.keyword.cloudcerts_short}}
  * 目標：Internet Services
3. 指定來源及目標的服務實例。
4. 指派**讀者**角色，以容許 {{site.data.keyword.cloudcerts_short}} 檢視 {{site.data.keyword.cis_short_notm}} 實例及其網域。然後，請按一下**授權**。

  針對測試目的，您可以透過使用者介面指派**管理員**服務存取角色，來管理所有網域。如果您這麼做，則不需要完成步驟 5。對於正式作業環境，建議您指派**讀者**服務存取角色，並如步驟 5 所示使用 API 來控制特定網域。
  {: note}
   
5. 若要控制特定網域，請使用 API 指派**管理員**角色，讓 {{site.data.keyword.cloudcerts_short}} 能管理 {{site.data.keyword.cis_short_notm}} 實例中存在之個別網域的 DNS 記錄。建議您將指令複製到文字檔，以便能輕鬆編輯必要的參數。
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>變數</th>
      <th>說明</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>有效的 IAM 記號。您可以使用 {{site.data.keyword.cloud_notm}} CLI <code>ibmcloud iam oauth-tokens</code> 來尋找值。</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} 及 {{site.data.keyword.cis_short_notm}} 實例所在帳戶的 ID。您可以導覽至 <b>{{site.data.keyword.cloud_notm}} > 管理 > 帳戶 > 帳戶設定</b>，或使用 {{site.data.keyword.cloud_notm}} CLI <code>ibmcloud account show</code> 來尋找值。</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} 實例的 GUID 型 ID。若要尋找值，請使用 {{site.data.keyword.cloud_notm}} CLI <code>ibmcloud resource service-instance "Instance name"</code>。</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} 實例的 GUID 型 ID。若要尋找值，請使用 {{site.data.keyword.cloud_notm}} CLI <code>ibmcloud resource service-instance "Instance name"</code>。</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} 中找到的網域 ID。若要尋找值，請使用 {{site.data.keyword.cloud_notm}} CLI 執行 <code>ibmcloud cis domains</code>。若要管理多個網域，請修改 <code>resources</code> 陣列。</td>
    </tr>
  </table>

現在，您可以[訂購憑證](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)！


### 另一個 DNS 提供者
{: #other_provider}

使用第三方 DNS 提供者時，為了驗證您對網域的控制，{{site.data.keyword.cloudcerts_short}} 會將 TXT 記錄傳送到您提供的回呼 URL 通知頻道，這使您可以將網域驗證處理程序自動化。

首先，請實作 IBM Cloud Function 動作以進行網域驗證，然後提供其端點給回呼 URL 通知頻道。若要開始使用，請參閱[設定回呼 URL 通知頻道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)。

如需使用回呼 URL 通知頻道設定網域驗證的相關資訊，請參閱[這篇部落格文章](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}。
{: tip}


#### 回應盤查
{: #responding-to-challenge}

通知頻道接收的通知具有下列結構：

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

DNS TXT 盤查傳送到回呼 URL 後，您必須在 10 分鐘內回答盤查。{{site.data.keyword.cloudcerts_short}} 會檢查以確認盤查是否完成。{{site.data.keyword.cloudcerts_short}} 驗證您是否回答了盤查後，會向您傳送第二個通知，指示您可以移除該 TXT 記錄。

若要查看訂購憑證的常見問題，[請檢閱常見問題頁面](/docs/services/certificate-manager?topic=certificate-manager-faq)。
{: tip}

## 訂購憑證
{: #ordering-certificate}

若要訂購憑證，請完成下列步驟：

1. 導覽至 {{site.data.keyword.cloudcerts_short}} 的「管理」標籤。
2. 按一下**訂購憑證**。 
3. 選取您的 DNS 提供者 - {{site.data.keyword.cis_full_notm}} 或另一個 DNS 提供者。
4. 如果您選取了 **{{site.data.keyword.cis_full_notm}}**，請提供下列詳細資料：
   1. 完成必要的設定指示
   2. 提供憑證名稱，並選擇性地提供說明
   3. 選取憑證管理中心
   4. 選取您已為其指派服務存取角色的 {{site.data.keyword.cis_full_notm}} 實例
   5. 選取您需要的憑證類型
   6. 選取網域
   7. 選取適當的演算法及金鑰演算法
   8. 按一下**訂購**
5. 如果您選取了**另一個 DNS 提供者**，請提供下列詳細資料：
   1. 完成必要的設定指示
   2. 提供憑證名稱，並選擇性地提供說明
   3. 選取憑證管理中心
   4. 輸入主要網域及任何替代網域
   5. 選取適當的演算法及金鑰演算法
   6. 按一下**訂購**

您的訂購將處於**擱置**狀態。您回答了網域驗證盤查，並且 {{site.data.keyword.cloudcerts_short}} 驗證了您是否擁有所要求的網域後，將向您簽發憑證，其狀態將變更為**有效**。在憑證備妥或發生問題時，您會在 Slack 和/或回呼 URL 通知頻道中收到通知。

## 更新憑證
{: #renew-certificate}

如果憑證即將到期，您可以透過 {{site.data.keyword.cloudcerts_short}} 要求更新憑證。更新憑證後，先前版本的憑證會保留，以備不時之需。 

更新的運作方式類似於憑證訂購。要求更新憑證時，{{site.data.keyword.cloudcerts_short}} 會向回呼 URL 傳送 DNS TXT 盤查，以便您可以再次證明您擁有要更新其憑證的網域。

若要更新憑證，請完成下列步驟：
  1. 在您要更新的憑證列上按一下功能表。
  2. 按一下**更新憑證**。
  3. 選用項目：您可以選擇重設憑證的金鑰，方法是勾選**重設憑證金鑰**勾選框。這會以新的金鑰組更新您的憑證。當您重設憑證金鑰時，請務必在使用憑證和金鑰的任何位置部署新的憑證和金鑰。
  
  4. 按一下**更新**。


您只能更新透過 {{site.data.keyword.cloudcerts_short}} 訂購的憑證。
{: note}

您的更新將處於**更新擱置**狀態。在您回答網域驗證盤查，並且 {{site.data.keyword.cloudcerts_short}} 確認您擁有所要求的網域後，您將獲得更新的憑證，其狀態將變更為**有效**。在更新的憑證備妥或發生問題時，您會在 Slack 和/或回呼 URL 通知頻道中收到通知。
