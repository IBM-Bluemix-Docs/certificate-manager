---

copyright:
  years: 2018
lastupdated: "2018-06-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}} 事件  
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.cloudcerts_long}} 服务进行交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录更改 {{site.data.keyword.Bluemix_notm}} 中服务状态的由用户启动的活动。有关更多信息，请参阅 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。例如，导入证书时，会生成 {{site.data.keyword.cloudaccesstrailshort}} 事件。

下表列出在调用时会生成事件的 API 方法：

<table>
  <caption>生成事件的操作</caption>
  <tr>
    <th>操作 </th>
	  <th>描述</th>
  </tr>
  <tr>
    <td>cloudcerts.instance.create</td>
	  <td>供应 {{site.data.keyword.cloudcerts_short}} 实例。</td>
  </tr>
  <tr>
    <td>cloudcerts.instance.delete</td>
	  <td>删除 {{site.data.keyword.cloudcerts_short}} 实例。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>导入由第三方认证中心签发的证书。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>下载证书。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>列出证书。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>列出证书元数据。显示证书的详细信息。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>搜索证书。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>搜索证书元数据。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>删除证书。</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>更新证书，例如更改证书的描述。</td>
  </tr>
</table>


 	
 


## 在何处查找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件在生成这些事件的 {{site.data.keyword.Bluemix_notm}} 区域中可用的 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中提供。

{{site.data.keyword.cloudaccesstrailshort}} 事件会自动转发到供应 {{site.data.keyword.cloudcerts_short}} 服务的区域中的 {{site.data.keyword.cloudaccesstrailshort}} 服务。


## 其他信息
{: #info}

*requestData_str* 字段包含证书的可读名称。



