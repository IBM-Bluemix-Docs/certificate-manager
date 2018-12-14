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

# 发行说明
{: #release-notes}

提供 {{site.data.keyword.cloudcerts_long}} 服务的下列功能和更改。

## 2018 年 11 月 14 日
{: 14November2018}

- **重新导入**  
  您可以重新导入与现有证书具有相同域但到期日期为新日期的新版本来更新证书。重新导入证书时，会保留现有版本的证书作为备份，请参阅[重新导入证书](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate)。

- **每个实例 1000 个证书**  
  每个实例最多可导入 1000 个证书。

## 2018 年 10 月 28 日
{: 28October2018}

- **公告条幅**  
  服务公告（例如不推荐的 API 和其他新闻）会显示在**管理**选项卡上。

## 2018 年 9 月 12 日
{: 12September2018}

- **证书名称是必需的**  
  导入证书时，必须提供证书的名称值。  

- **不推荐的 API**  
  不推荐使用**导入证书**和**更新证书元数据** V2 API，将于 2018 年 12 月 1 日将它们移除。必须升级到 V3 API。有关更多信息，请参阅 [API 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/apidocs/certificate-manager)。

- **分组 Slack 通知**  
 Slack 中的通知按到期日期分组。

## 2018 年 9 月 2 日
{: 2September2018}

- **{{site.data.keyword.cloudcerts_long_notm}} 已正式发布**  
  The {{site.data.keyword.cloudcerts_short}} 服务已在 {{site.data.keyword.cloud_notm}} 中正式发布 (GA)。

## 2018 年 8 月 22 日
{: 22August2018}

- **位于伦敦**  
  将在位置“伦敦”提供 {{site.data.keyword.cloudcerts_long_notm}} Beta。

## 2018 年 8 月 15 日
{: 15August2018}

- **除去不推荐的 V1 API**  
  V1 API 不再可用。如果您尚未更新 API，那么必须尽快更新。有关更多信息，请参阅 [API 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/apidocs/)。

- **平台角色替换为服务角色**  
  您可以使用服务角色来控制对 {{site.data.keyword.cloudcerts_short}} 实例的访问。[了解有关访问管理的更多信息](access-management.html)。

## 2018 年 7 月 12 日
{: 12July2018}

- **回调通知**  
  已添加通知的回调支持。您既可以选择将通知发送到 Slack，也可以使用任意回调 URL 来发布通知。例如，您可以向 PagerDuty 发送通知，在 GitHub 中自动创建问题，也可以触发更新脚本。[了解有关通知的更多信息](notifications-dashboard.html)。

## 2018 年 6 月 12 日
{: 12June2018}

- **Slack 通知**  
  已添加 Slack 通知，这样您就不会错过证书到期通知了。[了解有关通知的更多信息](notifications-dashboard.html)。

## 2018 年 1 月 8 日
{: 8January2018}

- **不推荐的 API**  
  不推荐使用 V1 API，将于 2018 年 9 月 8 日将它们移除。必须升级到 V2 API。有关更多信息，请参阅 [API 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/apidocs/certificate-manager)。

## 2017 年 12 月 19 日
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} 以 beta 服务形式提供**  
  {{site.data.keyword.cloudcerts_short}} 服务在 {{site.data.keyword.cloud_notm}} 中以 beta 服务形式提供。