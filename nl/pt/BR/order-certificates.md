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

# Pedindo certificados
{: #ordering-certificates}

É possível usar o {{site.data.keyword.cloudcerts_long}} para pedir certificados SSL/TLS públicos para os seus apps e serviços que são assinados por Autoridades de certificação externas suportadas. O {{site.data.keyword.cloudcerts_short}} facilita para você pedir certificados públicos, além da segurança extra para as suas chaves privadas do SSL/TLS. Após o seu certificado ser emitido, será possível implementá-lo em serviços integrados ou fazer download dele para usá-lo em outro lugar.  
{: shortdesc}

Quando você pedir um certificado, a sua chave privada para SSL/TLS será gerada diretamente no {{site.data.keyword.cloudcerts_short}} e armazenada com segurança. Todas as solicitações e o acesso aos certificados emitidos podem ser gerenciados por meio do [controle de acesso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles) e auditados automaticamente usando o [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events).  

O {{site.data.keyword.cloudcerts_short}} implementa o Protocolo v2 do Automatic Certificate Management Environment (ACME) como um cliente do ACME. O protocolo do ACME torna possível obter automaticamente certificados confiáveis do navegador sem intervenção humana.

## Características do certificado
{: #certificate-characteristics}

Ao pedir certificados por meio do {{site.data.keyword.cloudcerts_short}}:

- Eles são grátis
- São válidos por 90 dias
- Podem ser de domínio único, de vários domínios (SAN) ou um curinga
- São validados por domínio

A validação de domínio inclui a verificação de que você possui o domínio para o qual está
solicitando um certificado. Se você precisar de certificados de Validação estendida (EV) ou Validados pela organização (OV), será possível obtê-los em outro lugar e importá-los para o {{site.data.keyword.cloudcerts_short}} para gerenciar o seu ciclo de vida.


## Autoridades de certificação suportadas
{: #supported-certificate-authorities}

Uma Autoridade de certificação (CA) é uma entidade que emite certificados digitais. A CA age como um terceiro confiável para o solicitante do certificado e para o cliente que conta com o certificado.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) é uma CA baseada em ACME livre, automatizada, que fornece certificados validados por domínio válidos por 90 dias. É um serviço que é fornecido pelo
Internet Security Research Group (ISRG).

## Configurando o pedido de certificado
{: #setup}

Antes que um certificado possa ser emitido, o {{site.data.keyword.cloudcerts_short}} deve verificar se você controla todos os domínios que listou em sua solicitação. Para fazer isso,
o {{site.data.keyword.cloudcerts_short}} usa validação de DNS.
{: shortdesc}

O {{site.data.keyword.cloudcerts_short}} envia um desafio na forma de um registro de TXT do Sistema de Nomes de Domínio (DNS) para que você inclua em seu serviço do DNS. Para cada domínio que você solicitar em seu certificado, você obterá um registro de TXT do DNS separado. Depois de incluir o registro TXT do DNS, o {{site.data.keyword.cloudcerts_short}} e o Let’s Encrypt, verifique se ele está em
seu serviço DNS. Se você concluir com êxito o desafio, será emitido um certificado Let's Encrypt que estará disponível em sua instância do {{site.data.keyword.cloudcerts_short}}.

A forma como você verifica a propriedade do domínio depende de usar o {{site.data.keyword.cis_full_notm}} ou outro provedor DNS.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

Se você gerenciar seus domínios no {{site.data.keyword.cis_short}}, conclua as etapas
a seguir para verificar a propriedade:

1. Navegue até **{{site.data.keyword.cloud_notm}} > Gerenciar > Acesso (IAM) > Autorizações**.
2. Clique em **Criar** e designe um serviço de origem e de destino. O serviço
de origem tem acesso concedido ao serviço de destino com base nas funções que você configurar na próxima etapa.
  * Origem: {{site.data.keyword.cloudcerts_short}}
  * Destino: serviços da Internet
3. Especifique uma instância de serviço para a origem e o destino.
4. Designe a função de **Leitor** para permitir que o {{site.data.keyword.cloudcerts_short}} visualize a instância do {{site.data.keyword.cis_short_notm}} e seus domínios. Em seguida, clique em **Autorizar**.

  Para propósitos de teste, é possível designar a função de acesso ao serviço de **Gerenciador** por meio da IU para gerenciar todos os seus domínios. Se você
fizer isso, não será necessário concluir a etapa 5. Para ambientes de produção, é recomendável
designar a função de acesso ao serviço de **Leitor** e usar a API, conforme
mostrado na etapa 5 para controlar domínios específicos.
  {: note}
   
5. Para controlar domínios específicos, designe a função de **Gerenciador**
usando a API para que o {{site.data.keyword.cloudcerts_short}} possa gerenciar os registros
DNS para os domínios individuais que existem em sua instância do {{site.data.keyword.cis_short_notm}}. Você pode desejar copiar o comando para um arquivo de texto para tornar mais fácil editar os parâmetros necessários.
   
  

  
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
      <th>A</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>Um token do IAM válido. É possível localizar o valor usando a CLI
do {{site.data.keyword.cloud_notm}}: <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>O ID para a conta na qual existem as instâncias do {{site.data.keyword.cloudcerts_short}}
e {{site.data.keyword.cis_short_notm}}. É possível localizar o valor navegando para <b>{{site.data.keyword.cloud_notm}} > Gerenciar > Conta > Configurações da conta</b> ou
usando a CLI do {{site.data.keyword.cloud_notm}}: <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>O ID baseado em GUID para sua instância do {{site.data.keyword.cloudcerts_short}}. Para localizar o valor, use a CLI do {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>O ID baseado em GUID para sua instância do {{site.data.keyword.cis_short_notm}}. Para localizar o valor, use a CLI do {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>O ID do seu domínio conforme é localizado no {{site.data.keyword.cis_short_notm}}. Para localizar o valor, use a CLI do {{site.data.keyword.cloud_notm}} para executar
<code>ibmcloud cis domains</code>. Para gerenciar vários domínios, modifique a matriz <code>resources</code>.</td>
    </tr>
  </table>

Agora você está pronto para [pedir um certificado](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate)!


### Outro provedor DNS
{: #other_provider}

Para verificar seu controle sobre um domínio quando você está usando um provedor DNS de
terceiros, o {{site.data.keyword.cloudcerts_short}} envia o registro TXT para um canal
de notificações da URL de retorno de chamada que você fornece, o que permite automatizar o
processo de validação de domínio.

Primeiro, você implementa uma ação do IBM Cloud Function para validação de domínio e, em
seguida, fornece seu terminal para um canal de notificações da URL de retorno de chamada. Para
começar, veja [configurando um canal de notificações da URL de retorno de chamada](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

Para obter mais informações sobre como configurar a validação de domínio usando um canal de
notificação de URL de retorno de chamada, veja [esta postagem do blog](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}.
{: tip}


#### Respondendo ao desafio
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

Para ver as perguntas mais frequentes sobre o pedido de certificados, [revise
a página de Perguntas mais frequentes](/docs/services/certificate-manager?topic=certificate-manager-faq).
{: tip}

## Pedindo certificados
{: #ordering-certificate}

Para pedir um certificado, conclua as etapas a seguir:

1. Navegue para a guia Gerenciar do {{site.data.keyword.cloudcerts_short}}.
2. Clique em **Pedir certificado** 
3. Selecione o seu provedor DNS - o {{site.data.keyword.cis_full_notm}} ou outro Provedor DNS.
4. Se você selecionou **{{site.data.keyword.cis_full_notm}}**, forneça os detalhes a seguir:
   1. Conclua as instruções de configuração requeridas
   2. Forneça um nome de certificado e, opcionalmente, uma descrição
   3. Selecione uma autoridade de certificação
   4. Selecione a instância do {{site.data.keyword.cis_full_notm}} para a qual você
designou uma função de acesso ao serviço
   5. Selecione o tipo de certificado necessário
   6. Selecione o domínio
   7. Selecione o algoritmo apropriado e o algoritmo de chave
   8. Clique em **Pedir**
5. Se você selecionou **Outro Provedor DNS**, forneça os detalhes
a seguir:
   1. Conclua as instruções de configuração requeridas
   2. Forneça um nome de certificado e, opcionalmente, uma descrição
   3. Selecione uma Autoridade de certificação.
   4. Insira o domínio primário e quaisquer domínios alternativos
   5. Selecione o algoritmo apropriado e o algoritmo de chave
   6. Clique em **Pedir**

O seu pedido é colocado em um estado **Pendente**. Depois de responder ao
desafio de validação de domínio e de o {{site.data.keyword.cloudcerts_short}} verificar se
você possui o domínio solicitado, o certificado será emitido e seu estado mudará para **Válido**. Você será notificado quando seu certificado estiver pronto ou
se houver um problema em seu canal Slack e/ou de notificações da URL de retorno de chamada.

## Renovando certificados
{: #renew-certificate}

Se o seu certificado estiver prestes a expirar, será possível solicitar a renovação do seu certificado por meio do {{site.data.keyword.cloudcerts_short}}. Quando o seu certificado for renovado, a versão anterior do seu certificado será retida no caso de você precisar dela. 

Renovações funcionam de forma semelhante ao pedido de certificado. Quando você solicitar renovar um certificado, o {{site.data.keyword.cloudcerts_short}} enviará desafios de texto do DNS para a sua URL de retorno de chamada, de maneira que seja possível provar que você possui os domínios para os quais está renovando o certificado.

Para renovar um certificado, conclua as etapas a seguir:
  1. Clique no menu na linha de certificados que você deseja renovar.
  2. Clique em **Renovar certificado**.
  3. Opcional: é possível escolher rechavear o seu certificado verificando a caixa de seleção **Rechavear certificado**. Isso renova seu certificado com um novo par de chaves. Quando você rechavear um certificado, certifique-se de implementar os novos certificados e chaves em todos os lugares em que eles estiverem em uso.
  4. Clique em **Renovar**.


É possível renovar apenas os certificados que você pediu por meio do {{site.data.keyword.cloudcerts_short}}.
{: note}

Sua renovação será colocada em um estado **Renovação pendente**. Depois de
responder ao desafio de validação de domínio e de o {{site.data.keyword.cloudcerts_short}}
verificar se você possui o domínio solicitado, você obterá um certificado renovado e seu estado
mudará para **Válido**. Você será notificado quando seu certificado renovado
estiver pronto ou se houver um problema em seu canal Slack e/ou de notificações da URL de retorno
de chamada.
