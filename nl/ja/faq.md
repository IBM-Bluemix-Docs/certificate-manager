---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-12"

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

# よくあるご質問 (FAQ)
{: #faq}

{{site.data.keyword.cloudcerts_long}} についてよくあるご質問。
{: shortdesc}

## 証明書はどの形式にする必要がありますか?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} は、PEM 形式の証明書のみをサポートします。

## どのタイプの公開鍵アルゴリズムがサポートされていますか?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} では、以下の公開鍵アルゴリズムを使用して生成された公開鍵を使用する証明書がサポートされています。

* Rivest-Shamir-Adleman (RSA)
* デジタル署名アルゴリズム (DSA)
* 楕円曲線デジタル署名アルゴリズム (ECDSA)
* 楕円曲線 Diffie-Hellman 鍵合意プロトコル (ECDH)


## パスワードで保護された秘密鍵をアップロードできますか?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} は、パスワードで保護された秘密鍵が付いた証明書のインポートはサポートしていません。

## 証明書と秘密鍵をアップロードしようとして、次のエラーが表示されます。`エラー: 秘密鍵がインポートしようとしている証明書と一致しません。 一致するようにして、やり直してください (Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.)。`
{: #import-cert-private-key}
{: faq}

秘密鍵が暗号化されているかどうかに応じて、次のいずれかのオプションを選択します。

* 秘密鍵が暗号化されています。 アップロードする前に、秘密鍵の暗号化を解除してください。

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* 秘密鍵は暗号化されていません。 次のコマンドの結果を比較して、証明書と秘密鍵が一致していることを確認します。ここで、`<certificate-file>` は証明書ファイルの名前で、`<key-file>` は秘密鍵ファイルの名前です。

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## 期限切れが近い証明書についての E メール通知を受け取ることはできますか?
{: #email-notifications}
{: faq}

コールバック通知と Slack 通知のみがサポートされています。

## 証明書をバージョン管理できますか?
{: #certificate-versioning}
{: faq}

証明書は、既存の証明書と同じドメインの、新たな有効期限日付を持つ新しいバージョンの証明書を再インポートすることで更新できます。 証明書が再インポートされると、証明書の既存のバージョンはバックアップとして保存されます。[証明書の再インポート](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate)を参照してください。

## 特定の証明書が特定のユーザーのみに表示されるようにすることはできますか?
{: #access-policies}
{: faq}

証明書は、IAM アクセス・ポリシーを使用してきめ細かいアクセス制御を実現することによって保護できます。[サービス・アクセス役割の管理](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles)を参照してください。
