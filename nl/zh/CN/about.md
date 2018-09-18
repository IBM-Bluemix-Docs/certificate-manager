---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 关于 Certificate Manager
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_short}} 可帮助您管理基于 {{site.data.keyword.IBM_notm}} 云的应用程序和服务的 SSL 证书。
{: shortdesc}

您可以导入为应用程序和服务获取的 SSL 证书，安全地存储它们并集中查看正在使用的证书。

您可以通过以下方式来管理您的证书：

* 在证书到期之前收到通知，以确保您可按时更新
* 跨部署查看证书的类型并确保它们满足组织策略
* 发出新合规性或安全性需求时，查找需要替换的证书
* 控制谁可以访问和管理证书

![高级服务体系结构图](images/high-level-architecture.png)
<caption>高级服务体系结构。</caption>

## 专用密钥安全性
{: #private-key-security}

当您将证书及相应专用密钥导入到 {{site.data.keyword.cloudcerts_short}} 时，该服务将使用高级加密标准 (AES) 256 算法来加密专用密钥。{{site.data.keyword.cloudcerts_short}} 会保存此唯一加密密钥以使用服务实例。

## 集成
{: #integrations}
<table>
<caption>使用 Certificate Manager 的 IBM Cloud 服务</caption>
  <tr>
    <th> 服务</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>在 Certificate Manager 中存储 Kubernetes 集群定制域证书，然后使用 IBM Cloud CLI 的 [Kubernetes 服务插件命令](/docs/containers/cs_cli_reference.html)进行部署。[了解有关此集成的更多信息](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/)。</td>
  </tr>
  <tr>
    <td>IBM Cloud 安全顾问程序</td>
    <td>安全顾问程序集中 IBM Cloud 服务的洞察，包括 IBM Cloud 帐户中 Certificate Manager 实例内已到期和即将到期的证书的指示。[了解有关安全顾问程序的更多信息](/docs/services/security-advisor/index.html#index)</td>
  </tr><tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.Bluemix}} 中的 {{site.data.keyword.cloudcerts_long}} 服务进行交互。[了解有关 {{site.data.keyword.cloudaccesstrailshort}} 的更多信息](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla)。
    <p>要获取用于生成事件的操作的列表，请参阅 [{{site.data.keyword.cloudaccesstrailshort}} 事件](/docs/services/certificate-manager/at_events.html#at_events)。</p></td>
  </tr>
</table>

## 区域
{: #availability}
{{site.data.keyword.cloudcerts_short}} 在美国南部区域和英国区域提供。

