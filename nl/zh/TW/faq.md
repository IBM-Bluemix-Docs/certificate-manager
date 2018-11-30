---

copyright:
  years: 2018,
lastupdated: "2018-11-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:faq: data-hd-content-type='faq'}

# 常見問題 (FAQ)
{: #faq}

關於 {{site.data.keyword.cloudcerts_long}} 的常見問題。
{: shortdesc}

## 我可以在 {{site.data.keyword.cloudcerts_short}} 中儲存什麼類型的憑證？
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} 只支援 PEM 格式化憑證。

## 可以上傳受密碼保護的私密金鑰嗎？
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} 不支援匯入具有密碼保護之私密金鑰的憑證。

## 我嘗試上傳憑證及私密金鑰，然後遇到此錯誤：`Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}
{: faq}

視您的私密金鑰是否加密而定，請選擇下列其中一個選項：

* 私密金鑰已加密。請確定您先將私密金鑰解密，再上傳它。

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* 私密金鑰未加密。請確定憑證及私密金鑰相符，方法是比較下列指令的結果，其中 `<certificate-file>` 是您的憑證檔名稱，而 `<key-file>` 是您的私密金鑰檔名稱：

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

您可以藉由重新匯入新版憑證來更新憑證，此新版憑證具有與現有憑證相同的網域，但具有新的到期日。重新匯入憑證時，憑證的現有版本會保留作為備份，請參閱[重新匯入憑證](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate)。

## 可以只讓特定使用者看到特定憑證嗎？
{: #access-policies}
{: faq}

可以使用 IAM 存取原則來保護憑證，以達到精細的存取控制。請參閱[管理服務存取角色](access-management.html)。
