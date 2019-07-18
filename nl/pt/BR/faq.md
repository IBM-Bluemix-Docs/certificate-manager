---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL,

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
{:faq: data-hd-content-type='faq'}

# Perguntas mais frequentes (FAQs)
{: #faq}

Perguntas mais frequentes sobre o {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## Meus certificados devem estar em qual formato?
{: #supported-certificate-types}
{: faq}

O {{site.data.keyword.cloudcerts_short}} suporta somente certificados formatados em PEM.

## Quais tipos de algoritmos de chave pública são suportados?
{: #supported-pk-algorithms}
{: faq}

O {{site.data.keyword.cloudcerts_short}} suporta certificados com chaves públicas que são geradas usando os algoritmos de chave pública a seguir:

* Rivest-Shamir-Adleman (RSA)
* Algoritmo de Assinatura Digital (DSA)
* Algoritmo de Assinatura Digital de Curva Elíptica (ECDSA)
* Protocolo de acordo de chave de Curva Elíptica com Diffie-Hellman (ECDH)


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

* A chave privada não está criptografada. Certifique-se da correspondência do certificado e da chave privada comparando os resultados do comando a seguir, em que `<certificate-file>` é o nome de seu arquivo de certificado e `<key-file>` é o nome de seu arquivo de chave privado:

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

É possível atualizar um certificado reimportando uma nova versão dele que tenha o mesmo domínio que o certificado existente, mas com uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup. Consulte [Reimportando um certificado](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).



## Posso fazer com que certificados específicos fiquem visíveis apenas para usuários específicos?
{: #access-policies}
{: faq}

Os certificados podem ser protegidos usando as políticas de acesso do IAM para obter o controle de acesso granular. Consulte [Gerenciando as funções de acesso de serviço](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).



## Como eu revogo um certificado emitido?
{: #revoke-certificate}
{: faq}

Atualmente, o {{site.data.keyword.cloudcerts_short}} não tem nenhuma API de revogação que você possa usar. No entanto, é possível usar a API Let's Encrypt para revogar os certificados usando a chave privada do certificado. É possível aprender como revogar os certificados Let's Encrypt na [documentação do Let's Encrypt](https://letsencrypt.org/docs/revoking/).



## O status do pedido do meu certificado está no estado pendente por um longo tempo
{: #certificate-order-status}
{: faq}

Em redes de DNS lentas, um pedido pode levar até cerca de 20 minutos para ser concluído com sucesso.

## Por quanto tempo o serviço tenta validar que você possui os domínios que eu solicito em meu pedido?
{: #certificate-order-validation}
{: faq}

Depois que o serviço envia o desafio de validação de domínio, o {{site.data.keyword.cloudcerts_short}} tenta validar que você possui os domínios que solicitou por até 10 minutos. Se o seu DNS não for atualizado com o desafio do registro do TXT dentro de 10 minutos, o seu pedido falhará.

## Como eu verifico o status do meu pedido de certificado usando a API pública do
{{site.data.keyword.cloudcerts_short}}?
{: #certificate-order-status-api}
{: faq}

Use a API `Get certificate metadata` para pesquisar o status do pedido do certificado.

## Posso ser notificado quando o meu pedido estiver concluído?
{: #certificate-order-notification}
{: faq}

Se você configurou um canal de notificação, será notificado quando o seu certificado for emitido ou se o seu pedido tiver falhado. Observe que a versão do seu canal de notificação deve ser v4 ou superior.

## Meu pedido falhou. Por que?
{: #certificate-order-failure}
{: faq}

É possível localizar um código de erro e uma mensagem nos metadados do certificado, na IU e na notificação recebida quando o seu pedido falhou.

## Por que não estou recebendo eventos de pedido de certificado em meu canal de notificação do Slack existente?
{: #missing-notification-for-ordered-certificate}
{: faq}

Atualize o seu canal de notificação do Slack para a versão mais recente na guia Configurações do Certificate Manager.
