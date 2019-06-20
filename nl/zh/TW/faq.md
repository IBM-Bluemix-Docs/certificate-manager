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
{:faq: data-hd-content-type='faq'}

# 常見問題 (FAQ)
{: #faq}

關於 {{site.data.keyword.cloudcerts_long}} 的常見問題。
{: shortdesc}

## 我的憑證需要使用何種格式？
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} 只支援 PEM 格式化憑證。

## 支援哪些類型的公開金鑰演算法？
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} 支援的憑證，公開金鑰需使用下列公開金鑰演算法產生：

* Rivest-Shamir-Adleman (RSA)
* 數位簽章演算法 (DSA)
* 橢圓曲線數位簽章演算法 (ECDSA)
* 橢圓曲線及 Diffie-Hellman 金鑰協定通訊協定 (ECDH)


## 可以上傳受密碼保護的私密金鑰嗎？
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} 不支援匯入具有密碼保護之私密金鑰的憑證。

## 我嘗試上傳憑證及私密金鑰，然後遇到此錯誤：`Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}
{: faq}

視您的私密金鑰是否加密而定，請選擇下列其中一個選項：

* 私密金鑰已加密。確保在上傳私密金鑰之前，對其進行解密。

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* 私密金鑰未加密。透過比較下列指令的結果，確保憑證和私密金鑰相符合，其中 `<certificate-file>` 是憑證檔的名稱，`<key-file>` 是私密金鑰檔的名稱：

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## 我可以收到將到期憑證的電子郵件通知嗎？
{: #email-notifications}
{: faq}

只支援回呼及 Slack 通知。


## 我可以進行憑證的版本控制嗎？
{: #certificate-versioning}
{: faq}

您可以藉由重新匯入新版憑證來更新憑證，此新版憑證具有與現有憑證相同的網域，但具有新的到期日。重新匯入憑證時，憑證的現有版本會保留作為備份，請參閱[重新匯入憑證](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)。



## 可以只讓特定使用者看到特定憑證嗎？
{: #access-policies}
{: faq}

可以使用 IAM 存取原則來保護憑證，以達到精細的存取控制。請參閱[管理服務存取角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)。



## 如何撤銷已發出的憑證？
{: #revoke-certificate}
{: faq}

目前，{{site.data.keyword.cloudcerts_short}} 沒有撤銷 API 可供您使用。但是，您可以使用 Let's Encrypt API，透過憑證私密金鑰來撤銷憑證。您可以在 [Let's Encrypt 文件](https://letsencrypt.org/docs/revoking/)中瞭解如何撤銷 Let's Encrypt 憑證。



## 憑證訂單狀態長時間處於擱置狀態
{: #certificate-order-status}
{: faq}

在緩慢的 DNS 網路上，訂單最長可能需要大約 20 分鐘才能順利完成。

## 服務會花費多長時間來嘗試驗證我是否擁有我在訂單中要求的網域？
{: #certificate-order-validation}
{: faq}

傳送網域驗證盤查後，{{site.data.keyword.cloudcerts_short}} 會嘗試驗證您是否擁有所要求的網域，驗證時間最長為 10 分鐘。如果 DNS 在 10 分鐘內未使用 TXT 記錄盤查進行更新，您的訂單將會失敗。

## 如何使用 {{site.data.keyword.cloudcerts_short}} 公用 API 來檢查憑證訂單的狀態？
{: #certificate-order-status-api}
{: faq}

使用`取得憑證 meta 資料` API 來輪詢憑證訂單狀態。

## 我的訂單完成後會通知我嗎？
{: #certificate-order-notification}
{: faq}

如果您配置了通知頻道，在發出憑證之後或訂單失敗時會通知您。請注意，通知頻道的版本應該為 V4 或更高版本。

## 我的訂單失敗了。為什麼？
{: #certificate-order-failure}
{: faq}

您可以在憑證 meta 資料、使用者介面以及訂單失敗時收到的通知中尋找錯誤碼和訊息。

## 為什麼在現有的 Slack 通知頻道中收不到憑證訂單事件？
{: #missing-notification-for-ordered-certificate}
{: faq}

在 Certificate Manager 的「設定」標籤中，將 Slack 通知頻道升級到最新版本。
