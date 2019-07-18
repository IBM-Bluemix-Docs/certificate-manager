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

# Notas sobre a liberação
{: #release-notes}

Os recursos a seguir e as mudanças no serviço {{site.data.keyword.cloudcerts_long}} estão disponíveis.

## 8 de julho de 2019
{: 8July2019}

- **IBM Cloud Internet Services como um provedor DNS**  
  Agora, é possível usar o IBM Cloud Internet Services como um provedor DNS, simplificando a
experiência de pedidos de certificado. [Saiba mais sobre como pedir certificados](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 10 de junho de 2019
{: 10June2019}

- **Renovar certificados pedidos Let's Encrypt**  
  Agora é possível renovar os certificados Let's Encrypt que você pediu usando o {{site.data.keyword.cloudcerts_short}}. [Saiba mais sobre como pedir certificados](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 6 de maio de 2019
{: 6May2019}

- **Pedir certificados Let's Encrypt**  
  Agora é possível pedir os certificados Let's Encrypt. [Saiba mais sobre como pedir certificados](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 18 de fevereiro de 2019
{: 18February2019}

- **Ativo em Tóquio**  
  O {{site.data.keyword.cloudcerts_long_notm}} está disponível no local de Tóquio.

## 13 de janeiro de 2019
{: 13January2019}
- **Versão 3 da carga útil de retorno de chamada**  
  [Consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 6 de janeiro de 2019
{: 6January2019}
- **APIs descontinuadas**  
  As APIs **Listar certificados** e **Procurar repositório de certificados** da v2 foram descontinuadas e serão removidas futuramente. Deve-se fazer upgrade para as APIs v3. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 9 de dezembro de 2018
{: 9December2018}
- **Formatos adicionais de certificado**    
O {{site.data.keyword.cloudcerts_short}} suporta os seguintes formatos de certificado: RSA, DSA, ECDSA, ECDH.

## 5 de dezembro de 2018
{: 5December2018}
- **Reimportar Notificações**    
Ao reimportar um certificado renovado no lugar de um certificado expirado, é possível obter uma notificação de que o certificado foi reimportado. Isso lembrará você e sua equipe de implementar o certificado renovado em pontos de terminação SSL/TLS. Essa notificação está disponível somente para canais de notificação recém-criados.

- O **{{site.data.keyword.cloudcerts_short}} está disponível no local de Frankfurt.**     
O serviço está em conformidade com os requisitos da UE.

## 2 de dezembro de 2018
{: 2December2018}
- **Versão 2 da carga útil de retorno de chamada e do Slack**  
  [Consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 14 de novembro de 2018
{: 14November2018}

- **Reimportação**  
  É possível atualizar um certificado reimportando uma nova versão que tenha o mesmo domínio que o certificado existente, mas com uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup. Consulte [Reimportando um certificado](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

- **1.000 certificados por instância**  
  É possível importar até 1.000 certificados por instância.

## 28 de outubro de 2018
{: 28October2018}

- **Banner de comunicados**  
  Comunicados de serviço, como as descontinuações de API e outras notícias, são exibidos na guia **Gerenciar**.

## 12 de setembro de 2018
{: 12September2018}

- **O nome do certificado é obrigatório**  
  É obrigatório fornecer um valor para o nome do certificado ao importar um certificado.  

- **APIs descontinuadas**  
  As APIs v2 **Importar um certificado** e **Atualizar os metadados de um certificado** foram descontinuadas e serão removidas em 1º de dezembro de 2018. Deve-se fazer upgrade para as APIs v3. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/certificate-manager).

- **Notificações do Slack agrupadas**  
  As notificações no Slack são agrupadas pela data de expiração.

## 2 de setembro de 2018
{: 2September2018}

- O **{{site.data.keyword.cloudcerts_long_notm}} está disponível para uso geral**  
  O serviço {{site.data.keyword.cloudcerts_short}} está disponível para uso geral (GA) no {{site.data.keyword.cloud_notm}}.

## 22 de agosto de 2018
{: 22August2018}

- **Ativo em Londres**  
  O {{site.data.keyword.cloudcerts_long_notm}} Beta está disponível na localização de Londres.

## 15 de agosto de 2018
{: 15August2018}

- **Remover APIs v1 descontinuadas**  
  As APIs Versão 1 não estão mais disponíveis. Caso a API ainda não tenha sido atualizada, deve-se fazer isso o quanto antes. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/).

- **Funções da plataforma substituídas por funções de Serviço**  
  É possível controlar o acesso às instâncias do {{site.data.keyword.cloudcerts_short}} usando as funções de Serviço. [Saiba mais sobre o gerenciamento de acesso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12 de julho de 2018
{: 12July2018}

- **Notificações de retorno de chamada**  
  Suporte de retorno de chamada incluído para notificações. É possível escolher enviar notificações para
o Slack ou usar qualquer URL de retorno de chamada para postar notificações. Por exemplo, é possível
enviar notificações para o PagerDuty, abrir automaticamente um problema no GitHub ou acionar scripts
de renovação. [Saiba mais sobre notificações](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback).

## 12 de junho de 2018
{: 12June2018}

- **Notificações do Slack**  
  Notificações do Slack incluídas para que você nunca perca um certificado que está expirando. [Saiba mais sobre notificações](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8 de janeiro de 2018
{: 8January2018}

- **APIs descontinuadas**  
  As APIs da versão 1 foram descontinuadas e serão removidas em 8 de setembro de 2018. Deve-se fazer upgrade para as APIs v2. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 19 de dezembro de 2017
{: 19December2017}

- O **{{site.data.keyword.cloudcerts_long_notm}} está disponível como um serviço beta**  
  O serviço {{site.data.keyword.cloudcerts_short}} está disponível como um serviço beta no {{site.data.keyword.cloud_notm}}.
