---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-12"

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

# 版本注意事項
{: #release-notes}

{{site.data.keyword.cloudcerts_long}} 服務的下列特性及變更已可使用。

## 2019 年 2 月 18 日
{: 18February2018}

- **在東京推出**  
  {{site.data.keyword.cloudcerts_long_notm}} 提供於東京位置。

## 2019 年 1 月 13 日
{: 13January2019}
- **Callback payload 第 3 版**  
  [請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/certificate-manager)。

## 2019 年 1 月 6 日
{: 6January2019}
- **已淘汰的 API**  
**列出憑證**及**搜尋憑證儲存庫** v2 API 已淘汰，並且將在未來某日移除。您必須升級至 v3 API。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/certificate-manager)。

## 2018 年 12 月 9 日
{: 9December2018}
- **其他憑證格式**    
{{site.data.keyword.cloudcerts_short}} 支援下列憑證格式：RSA、DSA、ECDSA、ECDH。

## 2018 年 12 月 5 日
{: 5December2018}
- **重新匯入通知**    
當您重新匯入更新的憑證以取代到期的憑證時，會收到已重新匯入憑證的通知。這將提醒您及您的團隊將已更新的憑證部署到 SSL/TLS 終止點。此通知僅適用於新建立的通知頻道。

- **{{site.data.keyword.cloudcerts_short}} 提供於法蘭克福位置。**     
此服務符合 EU 需求。

## 2018 年 12 月 2 日
{: 2December2018}
- **回呼及 Slack 有效負載第 2 版**  
  [請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/certificate-manager)。

## 2018 年 11 月 14 日
{: 14November2018}

- **重新匯入**  
  您可以藉由重新匯入新版本來更新憑證，此新版本具有與現有憑證相同的網域，但具有新的到期日。重新匯入憑證時，憑證的現有版本會保留作為備份，請參閱[重新匯入憑證](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)。

- **每個實例 1000 個憑證**  
  每個實例可以匯入最多 1000 個憑證。

## 2018 年 10 月 28 日
{: 28October2018}

- **公告橫幅**  
  服務公告，例如 API 淘汰及其他新聞，會顯示在**管理**標籤。

## 2018 年 9 月 12 日
{: 12September2018}

- **憑證名稱是必要的**  
  在您匯入憑證時，必須提供值給憑證名稱。  

- **已淘汰的 API**  
  **Import a certificate** 和 **Update a certificate's metadata** v2 API 已淘汰，將在 2018 年 12 月 1 日移除。您必須升級至 v3 API。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/certificate-manager)。

- **分組的 Slack 通知**  
  Slack 中的通知會依到期日分組。

## 2018 年 9 月 2 日
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} 已正式提供**  
  {{site.data.keyword.cloudcerts_short}} 服務已在 {{site.data.keyword.cloud_notm}} 正式提供。

## 2018 年 8 月 22 日
{: 22August2018}

- **在倫敦推出**  
  {{site.data.keyword.cloudcerts_long_notm}} 測試版在倫敦位置提供。

## 2018 年 8 月 15 日
{: 15August2018}

- **移除已淘汰的 v1 API**  
  第 1 版的 API 已不再可用。如果您尚未更新 API，必須儘快完成。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/)。

- **平台角色取代為服務角色**  
  您可以使用服務角色控制對 {{site.data.keyword.cloudcerts_short}} 實例的存取。[進一步瞭解存取管理](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)。

## 2018 年 7 月 12 日
{: 12July2018}

- **回呼通知**  
  已新增通知的回呼支援。您可以選擇傳送通知到 Slack，或使用任何回呼 URL 來張貼通知。例如，您可以傳送通知至 PagerDuty、自動在 GitHub 開啟問題，或是觸發更新 Script。[進一步瞭解通知](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback)。

## 2018 年 6 月 12 日
{: 12June2018}

- **Slack 通知**  
  已新增 Slack 通知，讓您不錯過任何一個到期的憑證。[進一步瞭解通知](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback)。

## 2018 年 1 月 8 日
{: 8January2018}

- **已淘汰的 API**  
  第 1 版 API 已淘汰，將在 2018 年 9 月 8 日移除。您必須升級至 v2 API。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/certificate-manager)。

## 2017 年 12 月 19 日
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} 已提供為測試版服務**  
  {{site.data.keyword.cloudcerts_short}} 服務已在 {{site.data.keyword.cloud_notm}} 中提供為測試版服務。
