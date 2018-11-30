---

copyright:
  years: 2017, 2018
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

# 配置证书到期通知
{: #configuring-notifications-for-expiring-certificates}

证书通常仅在设置的时间内有效。使用的证书到期时，可能会遇到应用程序停机时间。为了避免产生停机时间，可以配置 {{site.data.keyword.cloudcerts_full}} 以发送有关即将到期的证书的通知，以便您可以按时更新证书。
{: shortdesc}

**何时会收到通知？**   根据上传到 {{site.data.keyword.cloudcerts_full_notm}} 的证书的到期日期，您会在证书到期前 90 天、60 天、30 天、10 天、1 天收到通知。此外，从证书到期的第一天开始，您每天还会收到有关证书到期的通知。

您必须更新证书，将此证书上传到 {{site.data.keyword.cloudcerts_full_notm}}，并删除到期的证书后，才会停止继续发送通知。

**有哪些通知配置选项？**  您可以使用 Slack Webhook 或使用您喜欢的任何回调 URL 向 Slack 发送通知。

## 设置 Slack Webhook
{: #setup-callback}

要设置 Slack Webhook，请完成以下步骤：

1. 注册 [Slack](https://slack.com/) 并设置工作空间。
2. 创建要向其发布通知的 Slack 通道。
3. [设置 Webhook](https://api.slack.com/incoming-webhooks) 以用于 Slack 通道。

## 设置回调 URL
{: #callback}

您可能希望使用回调 URL 将通知发布到每天使用的工具，以触发团队的更新过程。例如，您可以发送通知向 PagerDuty 报告，在 GitHub 中自动创建问题，也可以触发更新脚本。  
{: shortdesc}

**重要信息：**回调 URL 端点必须满足以下需求才能用于 {{site.data.keyword.cloudcerts_short}}：

* 端点必须使用 HTTPS 协议。
* 端点不能需要 HTTP 头。此需求包括 Authorization 头。
* 端点必须返回 `200 OK` 状态码来指示已成功传递通知。

### 通知格式
{: #notification_format}

发送到回调 URL 的通知是以下格式的 JSON 文档：

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

在解码和验证有效内容后，内容为 JSON 字符串。

```
{
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
    "event_type": "<EVENT_TYPE>",
    "certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "name":"<CERTIFICATE_NAME>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}

## 配置通知通道
{: #adding-channel}

创建 Slack Webhook 或回调 URL 后，将其添加到 {{site.data.keyword.cloudcerts_short}} 以开始接收有关证书到期的通知。{{site.data.keyword.cloudcerts_short}} 会加密端点并对其进行安全存储。
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
    <td>通知通道状态。如果将其设置为禁用，那么不会发送任何通知。</td>
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

开始之前，请[配置通知通道](#adding-channel)。

要测试通知通道，请完成以下步骤：

1. 在“服务详细信息”页面上的导航中，单击**设置**。
2. 找到您的通知通道，然后单击**测试连接**。
3. 验证是否在已配置的通道中收到通知。

## 更新通知通道
{: updating-channel}

您可以更新通知通道配置，禁用或启用通知，或从 {{site.data.keyword.cloudcerts_short}} 中删除通知通道。
{: shortdesc}

开始之前，请[配置通知通道](#adding-channel)。

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

## 示例
{: #examples}

* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 1 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   了解如何创建 GitHub 问题以获取证书到期通知。
* [How to Use Certificate Manager to Avoid Outages Using Callback URLs - Part 2 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   了解如何创建 PagerDuty 事件问题以获取证书到期通知。
