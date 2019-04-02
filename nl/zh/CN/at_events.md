---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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

# {{site.data.keyword.cloudaccesstrailshort}} 事件  
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.cloudcerts_long_notm}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录更改 {{site.data.keyword.Bluemix_notm}} 中服务状态的由用户启动的活动。有关更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)。例如，导入证书时，会生成 {{site.data.keyword.cloudaccesstrailshort}} 事件。

下表列出了在调用时会生成事件的 API 方法。

<table>
  <caption>表 1. 生成事件的操作</caption>
  <tr>
    <th>操作 </th>
	  <th>描述</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>导入证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>重新导入证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>下载证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>列出证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>列出证书元数据。显示证书的详细信息。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>搜索证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>搜索证书元数据。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>删除证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>更新证书元数据，例如更改证书的描述。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>列出通知通道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>创建通知通道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>禁用或启用通知通道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>更新通知通道的端点。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>删除通知通道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>测试通知通道。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>已将通知发送到通知通道端点。</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>已请求公用密钥。</td>
  </tr>
</table>

## 在何处查找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件位于 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中，而该帐户域位于这些事件生成所在的 {{site.data.keyword.Bluemix_notm}} 位置中。

系统会自动将 {{site.data.keyword.cloudaccesstrailshort}} 事件转发给 {{site.data.keyword.cloudaccesstrailshort}} 服务，而且位置与供应 {{site.data.keyword.cloudcerts_short}} 服务所在的位置相同。

## 其他信息
{: #info}

*requestData_str* 字段包含证书的可读名称。
