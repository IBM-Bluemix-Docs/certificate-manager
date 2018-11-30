---

copyright:
  years: 2018
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

# Notas sobre a liberação
{: #release-notes}

Os recursos a seguir e as mudanças no serviço {{site.data.keyword.cloudcerts_long}} estão disponíveis.

## 14 de novembro de 2018
{: 14November2018}

- **Reimportação**  
  É possível atualizar um certificado reimportando uma nova versão que tenha o mesmo domínio que o certificado existente, mas com uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup. Consulte [Reimportando um certificado](/docs/services/certificate-manager/managing-certificates.html#reimport-certificate).

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
  As APIs v2 **Importar um certificado** e **Atualizar os metadados de um certificado** foram descontinuadas e serão removidas em 1º de dezembro de 2018. Deve-se fazer upgrade para as APIs v3. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/apidocs/certificate-manager).

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
  As APIs Versão 1 não estão mais disponíveis. Caso a API ainda não tenha sido atualizada, deve-se fazer isso o quanto antes. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/apidocs/).

- **Funções da plataforma substituídas por funções de Serviço**  
  É possível controlar o acesso às instâncias do {{site.data.keyword.cloudcerts_short}} usando as funções de Serviço. [Saiba mais sobre o gerenciamento de acesso](access-management.html).

## 12 de julho de 2018
{: 12July2018}

- **Notificações de retorno de chamada**  
  Suporte de retorno de chamada incluído para notificações. É possível escolher enviar notificações para
o Slack ou usar qualquer URL de retorno de chamada para postar notificações. Por exemplo, é possível
enviar notificações para o PagerDuty, abrir automaticamente um problema no GitHub ou acionar scripts
de renovação. [Saiba mais sobre notificações](notifications-dashboard.html).

## 12 de junho de 2018
{: 12June2018}

- **Notificações do Slack**  
  Notificações do Slack incluídas para que você nunca perca um certificado que está expirando. [Saiba mais sobre notificações](notifications-dashboard.html).

## 8 de janeiro de 2018
{: 8January2018}

- **APIs descontinuadas**  
  As APIs da versão 1 foram descontinuadas e serão removidas em 8 de setembro de 2018. Deve-se fazer upgrade para as APIs v2. Para obter mais informações, [consulte a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/apidocs/certificate-manager).

## 19 de dezembro de 2017
{: 19December2017}

- O **{{site.data.keyword.cloudcerts_long_notm}} está disponível como um serviço beta**  
  O serviço {{site.data.keyword.cloudcerts_short}} está disponível como um serviço beta no {{site.data.keyword.cloud_notm}}.
