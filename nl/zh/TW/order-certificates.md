---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# 訂購憑證
{: #ordering-certificates}

您可以使用 {{site.data.keyword.cloudcerts_long}} 為您的應用程式和服務訂購由支援的外部憑證管理中心簽署的公用 SSL/TLS 憑證。透過 {{site.data.keyword.cloudcerts_short}}，不僅可為 SSL/TLS 私密金鑰實現額外的安全，還能輕鬆訂購公用憑證。簽發您的憑證後，您可以將憑證部署到整合服務，也可以下載該憑證以在其他位置使用。  
{: shortdesc}

訂購憑證時，用於 SSL/TLS 的私密金鑰會直接在 {{site.data.keyword.cloudcerts_short}} 中產生並安全地儲存。對已簽發憑證的所有要求和存取權可以透過[存取控制](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)進行管理，並使用 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events) 自動進行審核。  

{{site.data.keyword.cloudcerts_short}} 將自動憑證管理環境 (ACME) V2 通訊協定實作為 ACME 用戶端。透過 ACME 通訊協定，可以在沒有人為介入的情況下自動取得瀏覽器授信憑證。

## 憑證性質
透過 {{site.data.keyword.cloudcerts_short}} 訂購的憑證具有下列性質：

- 免費
- 有效期 - 90 天
- 單網域憑證、多網域憑證 (SAN) 或萬用字元憑證
- 網域驗證 - 在簽發憑證之前，憑證管理中心會檢查您是否擁有要為其要求憑證的網域。

如果需要延伸驗證 (EV) 憑證或組織驗證 (OV) 的憑證，您可以在其他地方取得這些憑證，然後將其匯入到 {{site.data.keyword.cloudcerts_short}} 以管理其生命週期。

## 支援的憑證管理中心
{: #supported-certificate-authorities}

憑證管理中心 (CA) 是簽發數位憑證的實體。對於憑證要求者和依賴憑證的用戶端，CA 可充當可信的第三方。
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) 是一個以 ACME 為基礎的自動化免費 CA，提供有效期為 90 天、經網域驗證過的憑證。這是由 Internet Security Research Group (ISRG) 提供的服務。

## 設定憑證訂購
{: #setup}

在向您簽發憑證之前，{{site.data.keyword.cloudcerts_short}} 必須驗證您是否有權控制要求中列出的所有網域。{{site.data.keyword.cloudcerts_short}} 使用 DNS 驗證來驗證您的控制權。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} 以網域名稱系統 (DNS) TXT 記錄的形式傳送盤查，供您新增到 DNS 服務中。對於在憑證中要求的每個網域，您將獲得一個個別的 DNS TXT 記錄。新增 DNS TXT 記錄後，{{site.data.keyword.cloudcerts_short}} 和 Let’s Encrypt 會檢查此記錄是否已在 DNS 服務中。如果您順利完成了盤查，則會發出在 {{site.data.keyword.cloudcerts_short}} 實例中可用的 Let's Encrypt 憑證給您。

{{site.data.keyword.cloudcerts_short}} 將 TXT 記錄傳送到您在通知設定中提供的回呼 URL，這使您可以輕鬆地將網域驗證處理程序自動化。

若要開始訂購憑證，請在 {{site.data.keyword.cloudcerts_short}} 中將回呼 URL 登錄為通知頻道。然後，更新程式碼以處理包含 TXT 盤查的通知事件。[瞭解如何設定回呼 URL 通知頻道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)。

## 回應盤查
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

[檢閱常見問題頁面](/docs/services/certificate-manager?topic=certificate-manager-faq#faq)，以瞭解有關訂購憑證的常見問題。
{: tip}

## 訂購憑證
{: #ordering-certificate}

1. 導覽至 {{site.data.keyword.cloudcerts_short}} 的「管理」標籤。
2. 按一下**訂購憑證**，並提供下列詳細資料：

    1. 提供憑證名稱。
    2. 選取憑證管理中心。
    3. 輸入主要網域及任何替代網域。
    4. 選取適當的演算法及金鑰演算法。
    5. 按一下**訂購**。

您的訂購將處於**擱置**狀態。您回答了網域驗證盤查，並且 {{site.data.keyword.cloudcerts_short}} 驗證了您是否擁有所要求的網域後，將向您簽發憑證，其狀態將變更為**有效**。在憑證備妥或發生問題時，您會在 Slack 和/或回呼 URL 頻道中收到通知。

## 更新憑證
{: #renew-certificate}

如果憑證即將到期，您可以透過 {{site.data.keyword.cloudcerts_short}} 要求更新憑證。更新憑證後，先前版本的憑證會保留，以備不時之需。 

更新的運作方式類似於憑證訂購。要求更新憑證時，{{site.data.keyword.cloudcerts_short}} 會向回呼 URL 傳送 DNS TXT 盤查，以便您可以再次證明您擁有要更新其憑證的網域。

若要更新憑證，請完成下列步驟：
  1. 在您要更新的憑證列上按一下功能表。
  2. 按一下**更新憑證**。
  3. 選用項目：您可以選擇重設憑證的金鑰，方法是勾選**重設憑證金鑰**勾選框。這會以新的金鑰組更新您的憑證。
  
  當您重設憑證金鑰時，請務必在使用憑證和金鑰的任何位置部署新的憑證和金鑰。
  {: note}
    
  4. 按一下**更新**。
  
  您只能更新透過 {{site.data.keyword.cloudcerts_short}} 訂購的憑證。
  {: note}

您的更新將處於**更新擱置**狀態。在您回答網域驗證盤查，並且 {{site.data.keyword.cloudcerts_short}} 確認您擁有所要求的網域後，您將獲得更新的憑證，其狀態將變更為**有效**。在更新的憑證備妥或發生問題時，您會在 Slack 和/或回呼 URL 頻道中收到通知。
