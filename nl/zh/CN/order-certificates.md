---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# 订购证书
{: #ordering-certificates}

您可以使用 {{site.data.keyword.cloudcerts_long}} 为应用程序和服务订购由支持的外部认证中心签名的公用 SSL/TLS 证书。通过 {{site.data.keyword.cloudcerts_short}}，不仅可为 SSL/TLS 专用密钥实现额外的安全性，还能轻松订购公用证书。签发您的证书后，您可以将证书部署到集成服务，也可以下载该证书以在其他位置使用。  
{: shortdesc}

订购证书时，用于 SSL/TLS 的专用密钥会直接在 {{site.data.keyword.cloudcerts_short}} 中生成并安全地存储。对已签发证书的所有请求和访问权可以通过[访问控制](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles)进行管理，并使用 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events) 自动进行审计。  

{{site.data.keyword.cloudcerts_short}} 将自动证书管理环境 (ACME) V2 协议实现为 ACME 客户机。通过 ACME 协议，可以在没有人为干预的情况下自动获取浏览器可信证书。

## 证书特征
{: #certificate-characteristics}

通过 {{site.data.keyword.cloudcerts_short}} 订购证书时：

- 证书是免费的
- 证书有效期为 90 天
- 证书可以为单域证书、多域 (SAN) 证书或通配符证书
- 证书会进行域验证

域验证包括验证您拥有要为其请求证书的域。如果需要扩展验证 (EV) 证书或组织验证 (OV) 的证书，您可以在其他地方获取这些证书，然后将其导入到 {{site.data.keyword.cloudcerts_short}} 以管理其生命周期。


## 支持的认证中心
{: #supported-certificate-authorities}

认证中心 (CA) 是签发数字证书的实体。对于证书请求者和依赖证书的客户机，CA 可充当可信的第三方。
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) 一个基于 ACME 的自动化免费 CA，提供有效期为 90 天的通过域验证的证书。这是由 Internet Security Research Group (ISRG) 提供的服务。

## 设置证书订购
{: #setup}

在向您签发证书之前，{{site.data.keyword.cloudcerts_short}} 必须验证您是否有权控制请求中列出的所有域。为此，{{site.data.keyword.cloudcerts_short}} 将使用 DNS 验证。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} 以域名系统 (DNS) TXT 记录的形式发送质询，供您添加到 DNS 服务中。对于在证书中请求的每个域，您将获得一个单独的 DNS TXT 记录。添加 DNS TXT 记录后，{{site.data.keyword.cloudcerts_short}} 和 Let’s Encrypt 会检查此记录是否已在 DNS 服务中。如果您成功完成了质询，那么将向您签发在 {{site.data.keyword.cloudcerts_short}} 实例中可用的 Let's Encrypt 证书。

如何验证域所有权取决于您是使用 {{site.data.keyword.cis_full_notm}} 还是其他 DNS 提供者。


### {{site.data.keyword.cis_full_notm}}
{: #cis}

如果在 {{site.data.keyword.cis_short}} 中管理域，请完成以下步骤以验证所有权：

1. 导航至 **{{site.data.keyword.cloud_notm}} > 管理 > 访问权 (IAM) > 用户**。
2. 单击**创建**并分配源和目标服务。将基于您在下一步中设置的角色为源服务授予对目标服务的访问权。
  * 源：{{site.data.keyword.cloudcerts_short}}
  * 目标：Internet Services
3. 为源和目标指定服务实例。
4. 分配**读取者**角色以允许 {{site.data.keyword.cloudcerts_short}} 查看 {{site.data.keyword.cis_short_notm}} 实例及其域。然后，单击**授权**。

  对于测试目的，您可以通过 UI 分配**管理者**服务访问角色以管理所有域。如果这样做，那么无需完成步骤 5。对于生产环境，建议分配**读取者**服务访问角色，并使用步骤 5 中所示的 API 来控制特定域。
  {: note}
   
5. 要控制特定域，请使用 API 分配**管理者**角色，以便 {{site.data.keyword.cloudcerts_short}} 可以管理 {{site.data.keyword.cis_short_notm}} 实例中存在的各个域的 DNS 记录。您可能希望将该命令复制到文本文件，以方便编辑必需参数。
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>变量</th>
      <th>描述</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>有效的 IAM 令牌。可以使用以下 {{site.data.keyword.cloud_notm}} CLI 来查找该值：<code>ibmcloud iam oauth-tokens</code>。</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} 和 {{site.data.keyword.cis_short_notm}} 实例所在帐户的标识。可以通过导航至 <b>{{site.data.keyword.cloud_notm}} > 管理 > 帐户 > 帐户设置</b>或通过使用以下 {{site.data.keyword.cloud_notm}} CLI 来查找该值：<code>ibmcloud account show</code>。</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cloudcerts_short}} 实例的基于 GUID 的标识。要查找该值，请使用以下 {{site.data.keyword.cloud_notm}} CLI：<code>ibmcloud resource service-instance "Instance name"</code>。</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} 实例的基于 GUID 的标识。要查找该值，请使用以下 {{site.data.keyword.cloud_notm}} CLI：<code>ibmcloud resource service-instance "Instance name"</code>。</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>{{site.data.keyword.cis_short_notm}} 中您的域的标识。要查找该值，请使用 {{site.data.keyword.cloud_notm}} CLI 运行 <code>ibmcloud cis domains</code>。要管理多个域，请修改 <code>resources</code> 数组。</td>
    </tr>
  </table>

现在，您可以随时[订购证书](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)！


### 其他 DNS 提供者
{: #other_provider}

为了在使用第三方 DNS 提供者时验证您对域的控制权，{{site.data.keyword.cloudcerts_short}} 会将 TXT 记录发送到您提供的回调 URL 通知通道，这使您可以自动执行域验证过程。

首先，实现用于域验证的 IBM Cloud Function 操作，然后提供其对回调 URL 通知通道的端点。要开始使用，请参阅[设置回调 URL 通知通道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)。

有关使用回调 URL 通知通道来设置域验证的更多信息，请参阅[此博客帖子](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}。
{: tip}


#### 响应质询
{: #responding-to-challenge}

通知通道接收的通知具有以下结构：

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // The first event is for adding the required challenge TXT record and the second is for clearing that same TXT record once the challenge has finished.
    "certificateCRN": "<CERTIFICATE_CRN>", // The ordered certificate CRN
    "userToken": "<USER_TOKEN>", /// The IAM token holding the identity of user who ordered the certificate
    "domain_validation_method": "dns-01", // Specifies the domain validation method, currently only DNS validation is available.
    "domain": "<ORDERED_DOMAIN>", // The requested domain, a different challenge is sent for each domain in the order (primary and each of the alternative domains).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // TXT record name - usually used with conjunction with the domain.
        "txt_record_val": "<TXT_REC_VALUE>" // TXT record value
    },
    "version": "<CHANNEL_VERSION>" // notification channel version that supports order related notifications - 4 and above
}
```
{: screen}

DNS TXT 质询发送到回调 URL 后，您必须在 10 分钟内应答质询。{{site.data.keyword.cloudcerts_short}} 会检查以确认质询是否完成。{{site.data.keyword.cloudcerts_short}} 验证您是否应答了质询后，会向您发送第二个通知，指示您可以除去该 TXT 记录。

要查看有关订购证书的常见问题，请[查看常见问题页面](/docs/services/certificate-manager?topic=certificate-manager-faq)。
{: tip}

## 订购证书
{: #ordering-certificate}

要订购证书，请完成以下步骤：

1. 导航至 {{site.data.keyword.cloudcerts_short}} 的“管理”选项卡。
2. 单击**订购证书**。 
3. 选择 DNS 提供者，可以是 {{site.data.keyword.cis_full_notm}} 或其他 DNS 提供者。
4. 如果选择了 **{{site.data.keyword.cis_full_notm}}**，请提供以下详细信息：
   1. 完成必需的设置指示信息
   2. 提供证书名称和（可选）描述
   3. 选择认证中心
   4. 选择已为其分配服务访问角色的 {{site.data.keyword.cis_full_notm}} 实例
   5. 选择所需的证书类型
   6. 选择域
   7. 选择适当的算法和密钥算法
   8. 单击**订购**
5. 如果选择了**其他 DNS 提供者**，请提供以下详细信息：
   1. 完成必需的设置指示信息
   2. 提供证书名称和（可选）描述
   3. 选择认证中心。
   4. 输入主域和任何备用域
   5. 选择适当的算法和密钥算法
   6. 单击**订购**

您的订购将处于**暂挂**状态。在您应答域验证质询，并且 {{site.data.keyword.cloudcerts_short}} 确认您拥有所请求的域后，将向您签发证书，其状态将更改为**有效**。在证书准备就绪或发生问题时，您会在 Slack 和/或回调 URL 通知通道中收到通知。

## 更新证书
{: #renew-certificate}

如果证书即将到期，您可以通过 {{site.data.keyword.cloudcerts_short}} 请求更新证书。更新证书后，先前版本的证书会保留，以备不时之需。 

更新的工作方式类似于证书订购。请求更新证书时，{{site.data.keyword.cloudcerts_short}} 会向回调 URL 发送 DNS TXT 质询，以便您可以再次证明您拥有要更新其证书的域。

要更新证书，请完成以下步骤：
  1. 单击要更新的证书所在行中的菜单。
  2. 单击**更新证书**。
  3. 可选：可以通过选中**再加密证书**复选框来选择对证书再加密。这将使用新密钥对来更新证书。对证书再加密后，请确保将新的证书和密钥部署到使用它们的所有位置。
  4. 单击**更新**。


只能更新通过 {{site.data.keyword.cloudcerts_short}} 订购的证书。
{: note}

您的更新将处于**更新暂挂**状态。在您应答域验证质询，并且 {{site.data.keyword.cloudcerts_short}} 确认您拥有所请求的域后，将向您签发证书，其状态将更改为**有效**。在更新的证书准备就绪或发生问题时，您会在 Slack 和/或回调 URL 通知通道中收到通知。
