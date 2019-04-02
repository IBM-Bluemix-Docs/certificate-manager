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


# 关于 {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_long}} 可帮助您管理基于 {{site.data.keyword.IBM_notm}} 云的应用程序和服务的 SSL 证书。
{: shortdesc}

您可以导入为应用程序和服务获取的 SSL 证书，安全地存储它们并集中查看正在使用的证书。

您可以通过以下方式来管理您的证书：

* 在证书到期之前收到通知，以确保您可按时更新
* 跨部署查看证书的类型并确保它们满足组织策略
* 发出新合规性或安全性需求时，查找需要替换的证书
* 控制谁可以访问和管理证书

![高级服务体系结构图](images/high-level-architecture.png)
<caption>图 1. 高级服务体系结构。</caption>

## 专用密钥安全性
{: #private-key-security}

当您将证书及相应专用密钥导入到 {{site.data.keyword.cloudcerts_short}} 时，该服务将使用高级加密标准 (AES) 256 算法来加密专用密钥。{{site.data.keyword.cloudcerts_short}} 会保存此唯一加密密钥以使用服务实例。

## 集成
{: #integrations}

<table>
<caption>表 1. 使用 {{site.data.keyword.cloudcerts_short}} 的 {{site.data.keyword.cloud_notm}} 服务</caption>
  <tr>
    <th> 服务</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>您可以轻松且安全地将定制域证书 TLS 证书从 {{site.data.keyword.cloudcerts_short}} 部署到 Kubernetes 集群。集群管理员可使用 [Kubernetes Service 插件命令](/docs/containers?topic=containers-cs_cli_reference)以用新证书将 TLS 证书更新为 Kubernetes 密钥，而不会导致停机时间。要开始，请查看[文档中的 Ingress 注释](/docs/containers?topic=containers-ingress_annotation#https-auth)。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index) 会集中管理有关 {{site.data.keyword.cloud_notm}} 服务的信息。这些信息包括到期证书以及您 {{site.data.keyword.cloud_notm}} 帐户下 {{site.data.keyword.cloudcerts_short}} 实例中即将到期证书的相关指示信息。[了解有关 {{site.data.keyword.security-advisor_short}} 的更多信息](/docs/services/security-advisor?topic=security-advisor-index#index)。</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>您可以使用 [{{site.data.keyword.cloudaccesstrailfull_notm}} 服务](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started)来跟踪用户和应用程序如何与 {{site.data.keyword.cloud_notm}} 中的 {{site.data.keyword.cloudcerts_long_notm}} 服务进行交互。[了解有关 {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started) 的更多信息。<p>要获取用于生成事件的操作的列表，请参阅 [{{site.data.keyword.cloudaccesstrailshort}} 事件](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events)。</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>将您的定制域证书存储在 {{site.data.keyword.cloudcerts_short}} 服务中，然后使用服务 CRN 与 {{site.data.keyword.apiconnect_short}} 中的定制域进行绑定。[了解有关 {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index) 的更多信息。</p></td>
  </tr>
</table>

## 位置
{: #availability}

{{site.data.keyword.cloudcerts_short}} 在达拉斯、伦敦、法兰克福和东京位置中可用。



## 限制
{: #limits}

每个实例最多可上传 1000 个证书。
