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

# 配置通知
{: #configuring-notifications}

{{site.data.keyword.cloudcerts_full}} 可以向您发送有关证书生命周期事件的通知。这包括在证书到期之前更新证书的提醒，以及在证书准备就绪时部署证书的提醒。要获取 {{site.data.keyword.cloudcerts_short}} 发送的通知，可以设置通知通道。可以指定 Slack Webhook、回调 URL 或这两者的任意组合。
{: shortdesc}

向 {{site.data.keyword.cloudcerts_short}} [订购证书](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates)时，也会使用通知功能。要证明您拥有要为其请求证书的域，{{site.data.keyword.cloudcerts_short}} 会将质询作为通知发送到回调 URL。质询是一种文本记录，应将其放入在其中注册域的域名系统 (DNS) 服务中。文本记录准备妥当后，质询被视为是完整的。由于质询是作为通知发送到回调 URL 的，因此您能够通过运行代码来自动执行域验证过程，以响应通知事件。

## 用于监视证书到期的通知
{: #notifications-monitoring-certificate-expiration}

证书通常在设置的时间内有效。使用的证书到期时，可能会遇到应用程序停机时间。为避免产生停机时间，您可以配置 {{site.data.keyword.cloudcerts_short}} 以发送有关证书即将到期的通知，以便提醒您按时更新证书。

在将更新版本的证书重新导入到 {{site.data.keyword.cloudcerts_short}} 以代替即将到期的证书时，您也将收到警报。这是为了提醒您将其部署到 SSL/TLS 终止点。有关重新导入证书的此通知仅发送到[通道 V2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) 中的通道。


**何时会收到通知？**   
根据上传到 {{site.data.keyword.cloudcerts_short}} 的证书的到期日期，您会在证书到期前 90 天、60 天、30 天、10 天、1 天收到通知。此外，从证书到期的第一天开始，您每天还会收到有关证书到期的通知。

您必须更新证书并将用于替换旧证书的此证书重新导入到 {{site.data.keyword.cloudcerts_short}}，以停止发送通知。在重新导入证书时，您将收到重新导入证书的通知以提醒您重新部署证书。

**有哪些通知配置选项？**  您可以使用 Slack Webhook 或使用您喜欢的任何回调 URL 向 Slack 发送通知。

## 与订购证书相关的通知
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} 会在您向 {{site.data.keyword.cloudcerts_short}} 订购的证书签发时或成功更新时通知您。如果订购失败或更新失败，也会通知您。
{: shortdesc}

设置回调 URL 通知通道，并能够处理与域验证相关的事件是订购和更新证书的先决条件。订购证书时，{{site.data.keyword.cloudcerts_short}} 会向回调 URL 发送质询 TXT 记录，用于证明您拥有要为其请求证书的域。请求更新证书时，也会发送质询 TXT 记录。 


## 设置 Slack Webhook
{: #setup-callback}

要设置 Slack Webhook，请完成以下步骤：

1. 注册 [Slack](https://slack.com/) 并设置工作空间。
2. 创建要向其发布通知的 Slack 通道。
3. [设置 Webhook](https://api.slack.com/incoming-webhooks) 以用于 Slack 通道。

## 设置回调 URL
{: #callback}

要触发团队的更新过程，您可以使用回调 URL 以将通知发布到使用的工具。例如，您可以发送通知向 PagerDuty 报告，在 GitHub 中自动创建问题，也可以触发更新脚本。您还可以自动触发证书部署，以响应在成功重新导入或签发证书时发送的通知。
{: shortdesc}

回调 URL 是订购证书的先决条件。
{: note}

**重要信息：**回调 URL 端点必须满足以下需求才能用于 {{site.data.keyword.cloudcerts_short}}：
* 端点必须使用 HTTPS 协议。
* 端点不能需要 HTTP 头。此需求包括 Authorization 头。
* 端点必须返回 `200 OK` 状态码来指示已成功传递通知。

### 通知格式
{: #notification_format}

发送到回调 URL 的通知是使用以下格式的实例非对称密钥签名的 JSON 文档。

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

在解码和验证有效内容后，内容为[根据通道版本的](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions) JSON 字符串。


## 配置通知通道
{: #adding-channel}

创建 Slack Webhook 或回调 URL 后，可以将其添加到 {{site.data.keyword.cloudcerts_short}} 以开始接收有关证书到期、已重新导入证书、已签发证书以及域验证质询的通知。{{site.data.keyword.cloudcerts_short}} 会加密端点并对其进行安全存储。
{: shortdesc}

要添加通知通道，请完成以下步骤：

1. 在“服务详细信息”页面上的导航中，单击**设置**。
2. 打开**通知**选项卡。
3. 单击**添加通知通道**。
4. 选择要使用的通知通道类型。
5. 输入要向其发送通知的 Webhook 或回调 URL。
6. 单击**保存**。 这将显示配置摘要。

   **输出示例**

   <table>
   <caption>表 1. 有关通知通道的信息</caption>
   <thead>
    <th> 组件</th>
    <th> 描述</th>
   </thead>
   <tbody>
   <tr>
    <td>类型</td>
    <td>通知通道类型：<i>Slack</i> 或<i>回调 URL</i></td>
   </tr>
   <tr>
    <td>端点</td>
    <td>向其发送通知的通知通道端点。</td>
   </tr>
   <tr>
    <td>启用切换开关</td>
    <td>通知通道状态。如果设置为禁用，那么不会发送任何通知。</td>
   </tr>
   <tr>
    <td>“测试连接”按钮</td>
    <td>将测试通知发送到已配置的通道。</td>
   </tr>
    <tr>
      <td>点菜单</td>
      <td>可以在通道上执行的可用操作：<i>编辑</i>或<i>删除</i></td>
    </tr>
    </tbody>
    </table>

    保存 Slack Webhook 时，{{site.data.keyword.cloudcerts_short}} 会自动向已配置的 Slack 通道发送确认通知。请检查 Slack 通道以验证是否收到此通知。
    {: tip}
7. （可选）重复这些步骤以添加更多通知通道。

## 测试通知通道
{: #testing-channel}

您可以测试通知通道，以确保正确配置通知通道。
{: shortdesc}

开始之前，请[配置通知通道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

要测试通知通道，请完成以下步骤：

1. 在“服务详细信息”页面上的导航中，单击**设置**。
2. 找到您的通知通道，然后单击**测试连接**。
3. 验证是否在已配置的通道中收到通知。

## 更新通知通道
{: #updating-channel}

您可以更新通知通道配置，禁用或启用通知，或从 {{site.data.keyword.cloudcerts_short}} 中删除通知通道。
{: shortdesc}

开始之前，请[配置通知通道](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel)。

要更新通知通道，请完成以下步骤：

1. 在“服务详细信息”页面上的导航中，单击**设置**。
2. 选择**通知**选项卡。
3. 从以下选项中进行选择：
   * 要禁用或启用通道通知，请将相应开关设置为**禁用**或**启用**。
   * 要更新通道的设置，请从操作菜单中选择**编辑**。
   * 要删除通知通道，请从操作菜单中选择**删除**。

## 验证回调 URL 的 HTTP 有效内容
{: #verify-callback}

从 {{site.data.keyword.cloudcerts_short}} 发送到回调 URL 的每个 HTTP 有效内容都会根据 JWT 标准使用非对称密钥对自动签名。  
{: shortdesc}

对于每个 {{site.data.keyword.cloudcerts_short}} 实例，生成的专用密钥和公用密钥不会在其他 {{site.data.keyword.cloudcerts_short}} 实例之间共享。专用密钥用于对 HTTP 有效内容签名，然后可以使用公用密钥来验证该有效内容是否由 {{site.data.keyword.cloudcerts_short}} 生成，并且未被第三方更改。

要下载公用密钥，请完成以下步骤：

1. 在“服务详细信息”页面上的导航中，单击**设置**。
2. 打开**通知**选项卡。
3. 单击**下载密钥**按钮。密钥将下载为 PEM 文件。

## 通道版本
{: #channel-versions}

随着 Certificate Manager 的发展，我们可能会不时修改通知有效内容结构的格式。为确保与更早版本的兼容性，发送到现有通道的有效内容不会进行更改。   

如果已有现有通知通道（Slack 或回调 URL），那么要开始获取新版本的有效内容：

1. 对于回调 URL，确保实施可接受新的有效内容。
2. 创建新通知通道（新通道始终使用最新通道版本进行创建）。
3. 测试新通道是否正常运行。
4. 删除旧通道。

有关通道版本的信息，请查看 [API 文档](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions)。

## 示例
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   了解如何创建 GitHub 问题以获取证书到期通知。
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   了解如何创建 PagerDuty 事件以获取证书到期通知。
* [如何使用回调 URL 和 Cloud Functions 操作验证域 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
