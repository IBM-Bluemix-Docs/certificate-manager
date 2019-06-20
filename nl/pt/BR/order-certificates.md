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

# Pedindo certificados
{: #ordering-certificates}

É possível usar o {{site.data.keyword.cloudcerts_long}} para pedir certificados SSL/TLS públicos para os seus apps e serviços que são assinados por Autoridades de certificação externas suportadas. O {{site.data.keyword.cloudcerts_short}} facilita para você pedir certificados públicos, além da segurança extra para as suas chaves privadas do SSL/TLS. Após o seu certificado ser emitido, será possível implementá-lo em serviços integrados ou fazer download dele para usá-lo em outro lugar.  
{: shortdesc}

Quando você pedir um certificado, a sua chave privada para SSL/TLS será gerada diretamente no {{site.data.keyword.cloudcerts_short}} e armazenada com segurança. Todas as solicitações e o acesso aos certificados emitidos podem ser gerenciados por meio do [controle de acesso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) e auditados automaticamente usando o [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).  

O {{site.data.keyword.cloudcerts_short}} implementa o Protocolo v2 do Automatic Certificate Management Environment (ACME) como um cliente do ACME. O protocolo do ACME torna possível obter automaticamente certificados confiáveis do navegador sem intervenção humana.

## Características do certificado
Os certificados que são pedidos por meio do {{site.data.keyword.cloudcerts_short}} têm as características a seguir:

- Free
- Período de validade - 90 dias
- Certificado curinga, de domínio único ou de domínio múltiplo (SAN)
- Validado pelo domínio - antes de emitir um certificado para você, a Autoridade de certificação verifica se você possui o domínio para o qual está solicitando um certificado.

Se você precisar de certificados de Validação estendida (EV) ou Validados pela organização (OV), será possível obtê-los em outro lugar e importá-los para o {{site.data.keyword.cloudcerts_short}} para gerenciar o seu ciclo de vida.

## Autoridades de certificação suportadas
{: #supported-certificate-authorities}

Uma Autoridade de certificação (CA) é uma entidade que emite certificados digitais. A CA age como uma 3ª parte confiável para o solicitante do certificado e para o cliente que depende do certificado.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) é uma CA baseada em ACME livre, automatizada, que fornece certificados validados por domínio válidos por 90 dias. É um serviço fornecido pelo Internet Security Research Group (ISRG).

## Configurando o pedido de certificado
{: #setup}

Antes que um certificado possa ser emitido para você, o {{site.data.keyword.cloudcerts_short}} deve verificar se você controla todos os domínios que você listou em sua solicitação. O {{site.data.keyword.cloudcerts_short}} usa a validação de DNS para verificar o seu controle.
{: shortdesc}

O {{site.data.keyword.cloudcerts_short}} envia um desafio na forma de um registro de TXT do Sistema de Nomes de Domínio (DNS) para que você inclua em seu serviço do DNS. Para cada domínio que você solicitar em seu certificado, você obterá um registro de TXT do DNS separado. Após você incluir o registro de TXT do DNS, o {{site.data.keyword.cloudcerts_short}} e Let’s Encrypt verificam se ele está em seu serviço do DNS. Se você concluir com êxito o desafio, será emitido um certificado Let's Encrypt que estará disponível em sua instância do {{site.data.keyword.cloudcerts_short}}.

O {{site.data.keyword.cloudcerts_short}} envia o registro de TXT para uma URL de Retorno de chamada que você fornece nas configurações de Notificações, que permite a você automatizar facilmente o processo de validação de domínio.

Para iniciar o pedido de certificados, registre a sua URL de Retorno de chamada como um canal de Notificação no {{site.data.keyword.cloudcerts_short}}. Em seguida, atualize o seu código para manipular os eventos de notificação que incluem o desafio de TXT. [Saiba como configurar um canal de notificação de URL de Retorno de chamada](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Respondendo ao desafio
{: #responding-to-challenge}

O canal de notificação recebe uma notificação com a estrutura a seguir:

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

Assim que o desafio de TXT do DNS for enviado para a sua URL de retorno de chamada, você terá que responder ao desafio dentro de 10 minutos. O {{site.data.keyword.cloudcerts_short}} verifica se o desafio está completo. Assim que o {{site.data.keyword.cloudcerts_short}} verificar se você respondeu ao desafio, será enviada a você uma segunda notificação para permitir que saiba que é possível remover o registro de TXT.

[Revise a página Perguntas mais frequentes](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) para ver as perguntas mais frequentes sobre como pedir certificados.
{: tip}

## Pedindo certificados
{: #ordering-certificate}

1. Navegue para a guia Gerenciar do {{site.data.keyword.cloudcerts_short}}.
2. Clique em **Pedir certificado** e forneça os detalhes a seguir:

    1. Forneça um nome do certificado.
    2. Selecione uma Autoridade de certificação.
    3. Insira o domínio primário e quaisquer domínios alternativos.
    4. Selecione o algoritmo apropriado e o algoritmo de chave.
    5. Clique em **Pedir**.

O seu pedido é colocado em um estado **Pendente**. Assim que você responder ao desafio de validação de domínio e o {{site.data.keyword.cloudcerts_short}} verificar se você possui os domínios solicitados, será emitido o certificado e o seu estado mudará para **Válido**. Quando o seu certificado estiver pronto ou se tiver ocorrido um problema, você será notificado em seu canal do Slack e/ou de URL de Retorno de chamada.

## Renovando certificados
{: #renew-certificate}

Se o seu certificado estiver prestes a expirar, será possível solicitar a renovação do seu certificado por meio do {{site.data.keyword.cloudcerts_short}}. Quando o seu certificado for renovado, a versão anterior do seu certificado será retida no caso de você precisar dela. 

Renovações funcionam de forma semelhante ao pedido de certificado. Quando você solicitar renovar um certificado, o {{site.data.keyword.cloudcerts_short}} enviará desafios de texto do DNS para a sua URL de retorno de chamada, de maneira que seja possível provar que você possui os domínios para os quais está renovando o certificado.

Para renovar um certificado, conclua as etapas a seguir:
  1. Clique no menu na linha do certificado que você deseja renovar.
  2. Clique em **Renovar certificado**.
  3. Opcional: é possível escolher rechavear o seu certificado verificando a caixa de seleção **Rechavear certificado**. Isso renovará o seu certificado com um novo par de chaves.
  
  Quando você rechavear um certificado, certifique-se de implementar os novos certificados e chaves em todos os lugares em que eles estiverem em uso.
  {: note}
    
  4. Clique em **Renovar**
  
  É possível renovar apenas os certificados que você pediu por meio do {{site.data.keyword.cloudcerts_short}}.
  {: note}

A sua renovação é colocada em um estado **Renovar pendente**. Assim que você responder ao desafio de validação de domínio e o {{site.data.keyword.cloudcerts_short}} verificar se você possui os domínios solicitados, você obterá um certificado renovado e o seu estado mudará para **Válido**. Quando o seu certificado renovado estiver pronto ou se tiver ocorrido um problema, você será notificado em seu canal do Slack e/ou de URL de Retorno de chamada.
