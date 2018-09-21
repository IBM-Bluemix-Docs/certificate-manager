
---
copyright:
  years: 2018
lastupdated: "2018-09-13"

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

## 12 de setembro de 2018
{: 12September2018}

- **O nome do certificado é obrigatório**  
  É obrigatório fornecer um valor para o nome do certificado ao importar um certificado.  
  Além disso, as APIs **Importar um certificado** e **Atualizar metadados do certificado** v2 estão descontinuadas e serão removidas em 1º de novembro de 2018. Deve-se fazer upgrade para as APIs v3. Para obter mais informações, consulte a [Documentação da API](https://console.bluemix.net/apidocs/certificate-manager).

- **Notificações do Slack agrupadas**  
  As notificações no Slack são agrupadas pela data de expiração.

## 2 de setembro de 2018
{: 2September2018}

- O **{{site.data.keyword.cloudcerts_long_notm}} está disponível para uso geral**  
  O serviço {{site.data.keyword.cloudcerts_short}} está disponível para uso geral (GA) no {{site.data.keyword.cloud_notm}}.

## 22 de agosto de 2018
{: 22August2018}

- **Ativo no Reino Unido**  
  O {{site.data.keyword.cloudcerts_long_notm}} Beta está disponível na região no Reino Unido
(Sul do Reino Unido).

## 15 de agosto de 2018
{: 15August2018}

- **Remover APIs v1 descontinuadas**  
  As APIs Versão 1 não estão mais disponíveis. Caso a API ainda não tenha sido atualizada, deve-se fazer isso o quanto antes. [Revise a documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/apidocs/).

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
  Foram incluídas notificações do Slack para que você nunca perca um certificado expirando. [Saiba mais sobre notificações](notifications-dashboard.html).

## 19 de dezembro de 2017
{: 19December2017}

- O **{{site.data.keyword.cloudcerts_long_notm}} está disponível como um serviço beta**  
  O serviço {{site.data.keyword.cloudcerts_short}} está disponível como um serviço beta no {{site.data.keyword.cloud_notm}}.
