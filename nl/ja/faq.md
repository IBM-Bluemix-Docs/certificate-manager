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



## 発行された証明書をどうすれば失効させることができますか?
{: #revoke-certificate}
{: faq}

{{site.data.keyword.cloudcerts_short}} には現在、使用可能な失効 API がありません。ただし、Let's Encrypt API を使用して、証明書の秘密鍵を使用することにより、証明書を失効させることができます。Let's Encrypt 証明書を失効させる方法は、[Let's Encrypt の資料](https://letsencrypt.org/docs/revoking/)で確認できます。



## 注文した証明書の状況が長時間保留状態になっています
{: #certificate-order-status}
{: faq}

DNS ネットワークが低速の場合、注文が正常に完了するまでに最大 20 分かかることがあります。

## 注文で要求したドメインが自分の所有になっていることをサービスで確認できるまでにどのくらいの時間がかかりますか?
{: #certificate-order-validation}
{: faq}

ドメイン検証チャレンジが送信された後、{{site.data.keyword.cloudcerts_short}} は、要求されたドメインがユーザーの所有になっていることの検証を最大 10 分間試行します。10 分以内に DNS が TXT レコード・チャレンジで更新されない場合、注文は失敗します。

## {{site.data.keyword.cloudcerts_short}} パブリック API を使用して証明書の注文状況を確認するにはどうすればよいですか?
{: #certificate-order-status-api}
{: faq}

`Get certificate metadata` API を使用して、証明書の注文状況をポーリングします。

## 注文完了時に通知を受けることはできますか?
{: #certificate-order-notification}
{: faq}

通知チャネルを構成した場合は、証明書が発行されたとき、または注文に失敗したときに通知されます。通知チャネルのバージョンは v4 以上でなければなりません。

## 注文に失敗しました。なぜでしょうか?
{: #certificate-order-failure}
{: faq}

エラー・コードとメッセージは、証明書のメタデータ、UI、および注文が失敗したときに受け取った通知で確認することができます。

## 既存の Slack 通知チャネルで証明書注文イベントが受信できないのはなぜですか?
{: #missing-notification-for-ordered-certificate}
{: faq}

証明書マネージャーの「設定」タブで、Slack 通知チャネルを最新バージョンにアップグレードしてください。
