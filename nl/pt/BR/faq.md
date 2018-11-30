---

copyright:
  years: 2018,
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
{:faq: data-hd-content-type='faq'}

# Perguntas mais frequentes (FAQs)
{: #faq}

Perguntas mais frequentes sobre o {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Que tipo de certificados posso armazenar no {{site.data.keyword.cloudcerts_short}}?
{: #supported-certificate-types}
{: faq}

O {{site.data.keyword.cloudcerts_short}} suporta somente certificados formatados em PEM.

## Posso transferir por upload as chaves privadas protegidas por senha?
{: #password-protected-private-keys}
{: faq}

O {{site.data.keyword.cloudcerts_short}} não suporta a importação de certificados com chaves privadas protegidas por senha.

## Estou tentando fazer upload de um certificado e de uma chave privada e aparece este erro: `Error: The private key doesn't match the certificate that you're trying to import. Ensure that they match and try again.`
{: #import-cert-private-key}
{: faq}

Dependendo do fato de a sua chave privada estar criptografada, escolha uma das opções a seguir:

* A chave privada está criptografada. Certifique-se de decriptografar a chave privada antes de fazer upload dela.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* A chave privada não está criptografada. Certifique-se da correspondência do certificado e da chave privada comparando os resultados do comando a seguir, em que `<certificate-file>` é o nome do arquivo de certificado e `<key-file>` é o nome do arquivo de chave privada:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## Posso receber notificações por e-mail para os certificados que estão expirando?
{: #email-notifications}
{: faq}

Apenas as notificações de retorno de chamada e do Slack são suportadas.

## Posso controlar a versão dos certificados?
{: #certificate-versioning}
{: faq}

É possível atualizar um certificado reimportando uma nova versão dele que tenha o mesmo domínio que o certificado existente, mas com uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup. Consulte [Reimportando um certificado](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

## Posso fazer com que certificados específicos fiquem visíveis apenas para usuários específicos?
{: #access-policies}
{: faq}

Os certificados podem ser protegidos usando as políticas de acesso do IAM para obter o controle de acesso granular. Consulte [Gerenciando as funções de acesso de serviço](access-management.html).
