---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# 订购证书
{: #ordering-certificates}

您可以使用 {{site.data.keyword.cloudcerts_long}} 为应用程序和服务订购由支持的外部认证中心签名的公用 SSL/TLS 证书。通过 {{site.data.keyword.cloudcerts_short}}，不仅可为 SSL/TLS 专用密钥实现额外的安全性，还能轻松订购公用证书。签发您的证书后，您可以将证书部署到集成服务，也可以下载该证书以在其他位置使用。  
{: shortdesc}

订购证书时，用于 SSL/TLS 的专用密钥会直接在 {{site.data.keyword.cloudcerts_short}} 中生成并安全地存储。对已签发证书的所有请求和访问权可以通过[访问控制](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)进行管理，并使用 [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events) 自动进行审计。  

{{site.data.keyword.cloudcerts_short}} 将自动证书管理环境 (ACME) V2 协议实现为 ACME 客户机。通过 ACME 协议，可以在没有人为干预的情况下自动获取浏览器可信证书。

## 证书特征
通过 {{site.data.keyword.cloudcerts_short}} 订购的证书具有以下特征：

- 免费
- 有效期 - 90 天
- 单域证书、多域证书 (SAN) 或通配符证书
- 域验证 - 在签发证书之前，认证中心会检查您是否拥有要为其请求证书的域。

如果需要扩展验证 (EV) 证书或组织验证 (OV) 的证书，您可以在其他地方获取这些证书，然后将其导入到 {{site.data.keyword.cloudcerts_short}} 以管理其生命周期。

## 支持的认证中心
{: #supported-certificate-authorities}

认证中心 (CA) 是签发数字证书的实体。对于证书请求者和依赖证书的客户机，CA 可充当可信的第三方。
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) 一个基于 ACME 的自动化免费 CA，提供有效期为 90 天的通过域验证的证书。这是由 Internet Security Research Group (ISRG) 提供的服务。

## 设置证书订购
{: #setup}

在向您签发证书之前，{{site.data.keyword.cloudcerts_short}} 必须验证您是否有权控制请求中列出的所有域。{{site.data.keyword.cloudcerts_short}} 使用 DNS 验证来验证您的控制权。
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} 以域名系统 (DNS) TXT 记录的形式发送质询，供您添加到 DNS 服务中。对于在证书中请求的每个域，您将获得一个单独的 DNS TXT 记录。添加 DNS TXT 记录后，{{site.data.keyword.cloudcerts_short}} 和 Let’s Encrypt 会检查此记录是否已在 DNS 服务中。如果您成功完成了质询，那么将向您签发在 {{site.data.keyword.cloudcerts_short}} 实例中可用的 Let's Encrypt 证书。

{{site.data.keyword.cloudcerts_short}} 将 TXT 记录发送到您在通知设置中提供的回调 URL，这使您可以轻松地自动执行域验证过程。

要开始订购证书，请在 {{site.data.keyword.cloudcerts_short}} 中将回调 URL 注册为通知通道。然后，更新代码以处理包含 TXT 质询的通知事件。[了解如何设置回调 URL 通知通道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions)。

## 响应质询
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

[查看常见问题页面](/docs/services/certificate-manager?topic=certificate-manager-faq#faq)，以了解有关订购证书的常见问题。
{: tip}

## 订购证书
{: #ordering-certificate}

1. 导航至 {{site.data.keyword.cloudcerts_short}} 的“管理”选项卡。
2. 单击**订购证书**，并提供以下详细信息：

    1. 提供证书名称。
    2. 选择认证中心。
    3. 输入主域和任何备用域。
    4. 选择适当的算法和密钥算法。
    5. 单击**订购**。

您的订购将处于**暂挂**状态。您应答了域验证质询，并且 {{site.data.keyword.cloudcerts_short}} 验证了您是否拥有所请求的域后，将向您签发证书，其状态将更改为**有效**。在证书准备就绪或发生问题时，您会在 Slack 和/或回调 URL 通道中收到通知。

## 更新证书
{: #renew-certificate}

如果证书即将到期，您可以通过 {{site.data.keyword.cloudcerts_short}} 请求更新证书。更新证书后，先前版本的证书会保留，以备不时之需。 

更新的工作方式类似于证书订购。请求更新证书时，{{site.data.keyword.cloudcerts_short}} 会向回调 URL 发送 DNS TXT 质询，以便您可以再次证明您拥有要更新其证书的域。

要更新证书，请完成以下步骤：
  1. 单击要更新的证书所在行中的菜单。
  2. 单击**更新证书**。
  3. 可选：可以通过选中**再加密证书**复选框来选择对证书再加密。这将使用新密钥对来更新证书。
  
  对证书再加密后，请确保将新的证书和密钥部署到使用它们的所有位置。
  {: note}
    
  4. 单击**更新**。
  
  只能更新通过 {{site.data.keyword.cloudcerts_short}} 订购的证书。
  {: note}

您的更新将处于**更新暂挂**状态。在您应答域验证质询，并且 {{site.data.keyword.cloudcerts_short}} 确认您拥有所请求的域后，您将获得更新的证书，其状态将更改为**有效**。在更新的证书准备就绪或发生问题时，您会在 Slack 和/或回调 URL 通道中收到通知。
