---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

keywords: certificates, SSL, TLS, activity tracker,

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

# Activity Tracker 事件  
{: #at_events}

使用 {{site.data.keyword.at_full}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.cloudcerts_long}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.at_short}} 服务记录由用户启动的会更改 {{site.data.keyword.cloud_notm}} 中服务状态的活动。例如，导入证书时，会生成事件。有关更多信息，请参阅 [{{site.data.keyword.at_short}} 文档](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)。

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
    <td>`cloudcerts.certificate.order`</td>
	  <td>订购证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.renew`</td>
	  <td>更新签发的证书。</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>获取证书元数据。</td>
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
{: #at_ui}

在 {{site.data.keyword.cloudcerts_short}} 实例所在位置供应 {{site.data.keyword.at_short}} 实例。

完成以下步骤：

1. 转至 [{{site.data.keyword.cloud_notm}} 可观察性](https://cloud.ibm.com/observe/){: external}。
2. 在 {{site.data.keyword.cloudcerts_short}} 实例所在位置供应 {{site.data.keyword.at_short}} 实例。

系统会自动将事件转发给供应 {{site.data.keyword.cloudcerts_short}} 服务的相同位置中的 {{site.data.keyword.at_short}} 服务实例。

## 其他信息
{: #info}

* *requestData_str* 字段包含证书的可读名称。

## 可用性
{: #at-availability}

{{site.data.keyword.at_short}} 支持可用于**达拉斯**、**法兰克福**、**东京**和**伦敦**位置。
