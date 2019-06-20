---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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
{:faq: data-hd-content-type='faq'}

# 常见问题 (FAQ)
{: #faq}

有关 {{site.data.keyword.cloudcerts_long}} 的常见问题。
{: shortdesc}

## 我的证书需要采用什么格式？
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} 仅支持 PEM 格式的证书。

## 支持何种类型的公用密钥算法？
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} 支持包含使用以下公用密钥算法生成的公用密钥的证书：

* Rivest-Shamir-Adleman (RSA)
* 数字签名算法 (DSA)
* 椭圆曲线数字签名算法 (ECDSA)
* 使用 Diffie-Hellman 的椭圆曲线密钥协商协议 (ECDH)


## 我可以上传受密码保护的专用密钥吗？
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} 不支持导入证书和受密码保护的专用密钥。

## 我在尝试上传证书和专用密钥时遇到以下错误：`错误：专用密钥与您尝试导入的证书不匹配。请确保它们匹配，然后重试。`
{: #import-cert-private-key}
{: faq}

您可以选择以下某个选项，具体取决于您的专用密钥是否已加密：

* 专用密钥已加密。确保在上传专用密钥之前，对其进行解密。

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* 专用密钥未加密。通过比较以下命令的结果，确保证书和专用密钥相匹配，其中 `<certificate-file>` 是证书文件的名称，`<key-file>` 是专用密钥文件的名称：

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## 我可以接收证书到期的电子邮件通知吗？
{: #email-notifications}
{: faq}

仅支持回调和 Slack 通知。


## 我可以控制我的证书版本吗？
{: #certificate-versioning}
{: faq}

您可以重新导入与现有证书具有相同域但到期日期为新日期的新证书版本来更新证书。重新导入证书时，会保留现有版本的证书作为备份，请参阅[重新导入证书](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)。



## 我是否可以将特定证书设置为仅对特定用户可见？
{: #access-policies}
{: faq}

您可以使用 IAM 访问策略来保护证书，从而实现精细访问控制，请参阅[管理服务访问角色](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)。



## 如何撤销签发的证书？
{: #revoke-certificate}
{: faq}

目前，{{site.data.keyword.cloudcerts_short}} 没有撤销 API 可以使用。但是，可以使用 Let's Encrypt API 通过证书专用密钥来撤销证书。您可以在 [Let's Encrypt 文档](https://letsencrypt.org/docs/revoking/)中了解如何撤销 Let's Encrypt 证书。



## 证书订购状态长时间处于暂挂状态
{: #certificate-order-status}
{: faq}

在慢速 DNS 网络上，订购最长可能需要大约 20 分钟才能成功完成。

## 服务会花费多长时间来尝试验证我是否拥有在订购中请求的域？
{: #certificate-order-validation}
{: faq}

发送域验证质询后，{{site.data.keyword.cloudcerts_short}} 会尝试验证您是否拥有所请求的域，验证时间最长为 10 分钟。如果 DNS 在 10 分钟内未使用 TXT 记录质询进行更新，订购将失败。

## 如何使用 {{site.data.keyword.cloudcerts_short}} 公共 API 来检查证书订购的状态？
{: #certificate-order-status-api}
{: faq}

使用`获取证书元数据` API 来轮询证书订购状态。

## 订购完成后会通知我吗？
{: #certificate-order-notification}
{: faq}

如果您配置了通知通道，那么在签发了证书之后或订购失败时会通知您。请注意，通知通道的版本应该为 V4 或更高版本。

## 我的订购失败了。为什么？
{: #certificate-order-failure}
{: faq}

您可以在证书元数据、UI 以及订购失败时收到的通知中查找错误代码和消息。

## 为什么在现有的 Slack 通知通道中收不到证书订购事件？
{: #missing-notification-for-ordered-certificate}
{: faq}

在 Certificate Manager 的“设置”选项卡中，将 Slack 通知通道升级到最新版本。
