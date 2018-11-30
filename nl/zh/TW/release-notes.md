---

copyright:
  years: 2018
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

# 版本注意事項
{: #release-notes}

{{site.data.keyword.cloudcerts_long}} 服務的下列特性及變更已可使用。

## 2018 年 11 月 14 日
{: 14November2018}

- **重新匯入**  
  您可以藉由重新匯入新版本來更新憑證，此新版本具有與現有憑證相同的網域，但具有新的到期日。重新匯入憑證時，憑證的現有版本會保留作為備份，請參閱[重新匯入憑證](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate)。

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
  **Import a certificate** 和 **Update a certificate's metadata** v2 API 已淘汰，將在 2018 年 12 月 1 日移除。您必須升級至 v3 API。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/apidocs/certificate-manager)。

- **分組的 Slack 通知**  
  Slack 中的通知會依到期日分組。

## 2018 年 9 月 2 日
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} 已正式提供**  
  {{site.data.keyword.cloudcerts_short}} 服務已在 {{site.data.keyword.cloud_notm}} 正式提供。

## 2018 年 8 月 22 日
{: 22August2018}

- **在倫敦推出**  
  {{site.data.keyword.cloudcerts_long_notm}} 測試版提供於倫敦位置。

## 2018 年 8 月 15 日
{: 15August2018}

- **移除已淘汰的 v1 API**  
  第 1 版的 API 已不再可用。如果您尚未更新 API，必須儘快完成。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/apidocs/)。

- **平台角色取代為服務角色**  
  您可以使用服務角色控制對 {{site.data.keyword.cloudcerts_short}} 實例的存取。[進一步瞭解存取管理](access-management.html)。

## 2018 年 7 月 12 日
{: 12July2018}

- **回呼通知**  
  已新增通知的回呼支援。您可以選擇傳送通知到 Slack，或使用任何回呼 URL 來張貼通知。例如，您可以傳送通知至 PagerDuty、自動在 GitHub 開啟問題，或是觸發更新 Script。[進一步瞭解通知](notifications-dashboard.html)。

## 2018 年 6 月 12 日
{: 12June2018}

- **Slack 通知**  
  已新增 Slack 通知，讓您不錯過任何一個到期的憑證。[進一步瞭解通知](notifications-dashboard.html)。

## 2018 年 1 月 8 日
{: 8January2018}

- **已淘汰的 API**  
  第 1 版 API 已淘汰，將在 2018 年 9 月 8 日移除。您必須升級至 v2 API。如需相關資訊，[請參閱 API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/apidocs/certificate-manager)。

## 2017 年 12 月 19 日
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} 已提供為測試版服務**  
  {{site.data.keyword.cloudcerts_short}} 服務已在 {{site.data.keyword.cloud_notm}} 中提供為測試版服務。
