---

copyright:
  years: 2017, 2018
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

# Configurando Notificações para Expirar Certificados
{: #configuring-notifications-for-expiring-certificates}

Geralmente, os certificados são válidos apenas por um período de tempo configurado. Quando um certificado que você usa
expira, o seu aplicativo pode passar por um tempo de inatividade. Para evitar o tempo de inatividade, é possível configurar o {{site.data.keyword.cloudcerts_full}} para enviar notificações sobre os certificados que estão prestes a expirar para que seja possível renová-los a tempo.
{: shortdesc}

**Quando eu sou notificado?**  
Dependendo da data de expiração do certificado que você transferiu por upload para o {{site.data.keyword.cloudcerts_full_notm}}, você será notificado 90, 60, 30, 10 e 1 dia antes da expiração. Além disso, você recebe notificações diárias sobre os certificados expirados. As notificações diárias se iniciam no primeiro dia após a expiração do certificado.

Deve-se renovar o seu certificado, fazer upload dele para o {{site.data.keyword.cloudcerts_full_notm}} e excluir o certificado expirado para interromper o envio da notificação.

**Quais são as minhas opções para configurar as notificações?**  
É possível enviar notificações para o Slack usando um webhook do Slack ou usar qualquer URL de retorno de chamada que você desejar.

## Configurando um webhook do Slack
{: #setup-callback}

Para configurar um webhook do Slack, conclua as etapas a seguir:

1. Inscreva-se no [Slack](https://slack.com/) e configure a sua área de trabalho.
2. Crie um canal Slack no qual deseja postar as suas notificações.
3. [Configure um webhook](https://api.slack.com/incoming-webhooks) para o canal Slack.

## Configurando uma URL de retorno de chamada
{: #callback}

Talvez você queria usar a URL de retorno de chamada para postar a notificação para as ferramentas usadas diariamente para acionar o processo de renovação para a sua equipe. Por exemplo, é possível enviar notificações para relatar ao PagerDuty, abrir automaticamente um problema no GitHub ou acionar scripts de renovação.  
{: shortdesc}

**Importante:** o terminal da sua URL de retorno de chamada deve atender aos seguintes requisitos para
ser usado com o {{site.data.keyword.cloudcerts_short}}:

* O terminal deve usar o protocolo HTTPS.
* O terminal não deve requerer cabeçalhos de HTTP. Este requisito inclui cabeçalhos de autorização.
* O terminal deve retornar um código de status `200 OK` para indicar uma entrega de notificação bem-sucedida.

### Formato da notificação
{: #notification_format}

A notificação que é enviada para a URL de retorno de chamada é um documento JSON que está no formato a seguir:

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Após decodificar e verificar a carga útil, o conteúdo será uma sequência JSON.

```
{
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
    "event_type": "<EVENT_TYPE>",
    "certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "name":"<CERTIFICATE_NAME>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}

## Configurando um canal de notificação
{: #adding-channel}

Após criar um webhook do Slack ou uma URL de retorno de chamada, inclua no {{site.data.keyword.cloudcerts_short}} para começar a receber notificações sobre a expiração de certificados. O {{site.data.keyword.cloudcerts_short}} criptografa o
terminal e armazena-o com segurança.
{: shortdesc}

Para incluir um canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique em **Incluir canal de notificação**.
4. Escolha o tipo de canal de notificação que deseja usar.
5. Insira o webhook ou a URL de retorno de chamada para a qual você deseja enviar as notificações.
6. Clique em  ** Salvar **. Um resumo da sua configuração é exibido.

   **Exemplo de saída**

   <table>
   <caption>Tabela 1. Informações sobre o canal de notificação </caption>
   <thead>
    <th> Componente </th>
    <th> Descrição </th>
   </thead>
   <tbody>
   <tr>
    <td>Tipo</td>
    <td>Tipo de canal de notificação: <i>Slack</i> ou <i>URL de retorno de chamada</i></td>
   </tr>
   <tr>
    <td>Nó de Extrem</td>
    <td>O terminal do canal de notificação para o qual as notificações são enviadas.</td>
   </tr>
   <tr>
    <td>Toggle de ativação</td>
    <td>O estado do canal de notificação. Se ele estiver configurado como desativado, nenhuma notificação será enviada.</td>
   </tr>
   <tr>
    <td>Botão Testar conexão</td>
    <td>Envia uma notificação de teste para o canal que você configurou. </td>
   </tr>
    <tr>
      <td>Menu Dots</td>
      <td>Ações disponíveis que podem ser executadas no canal: <i>editar</i> ou <i>excluir</i></td>
    </tr>
    </tbody>
    </table>

    Ao salvar um webhook do Slack, o {{site.data.keyword.cloudcerts_short}} envia automaticamente uma notificação
de confirmação para o canal Slack que você configurou. Consulte o seu canal Slack para verificar se você recebeu essa
notificação.
    {: tip}
7. (Opcional) Repita essas etapas para incluir mais canais de notificação.

## Testando um canal de notificação
{: #testing-channel}

É possível testar um canal de notificação para assegurar que o seu canal de notificação esteja configurado corretamente.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](#adding-channel).

Para testar um canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Localize o seu canal de notificação e clique em **Conexão de teste**.
3. Verifique se você recebeu uma notificação no canal configurado.

## Atualizando um canal de notificação
{: updating-channel}

É possível atualizar a configuração do seu canal de notificação, desativar ou ativar as notificações ou excluir os canais de
notificação do {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](#adding-channel).

Para atualizar seu canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Selecione a guia  ** Notificações ** .
3. Escolha a partir das opções a seguir:
   * Para desativar ou ativar as notificações para um canal, configure o comutador para **Desativar**
ou **Ativar**.
   * Para atualizar as configurações de um canal, selecione **Editar** no menu Ações.
   * Para excluir um canal de notificação, selecione **Excluir** no menu Ações.

## Verificando a carga útil de HTTP para uma URL de retorno de chamada
{: #verify-callback}

Cada carga útil de HTTP enviada do {{site.data.keyword.cloudcerts_short}} para a sua URL de retorno de chamada é
assinada automaticamente de acordo com o padrão JWT usando um par de chaves assimétricas.  
{: shortdesc}

Para cada instância do {{site.data.keyword.cloudcerts_short}}, são geradas uma chave privada e uma pública que
não são compartilhadas entre as outras instâncias do {{site.data.keyword.cloudcerts_short}}. A chave privada é usada para
assinar a carga útil de HTTP, e é possível usar a chave pública para verificar se a carga útil é gerada pelo {{site.data.keyword.cloudcerts_short}} e não é alterada por um terceiro.

Para fazer download da chave pública, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique no botão  ** Fazer download da chave ** . A chave é transferida por download como um arquivo PEM.

## Exemplos
{: #examples}

* [Como usar o gerenciador de certificados para evitar interrupções usando as URLs de retorno de chamada - Parte 1 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Saiba como criar emissões do GitHub para notificações sobre um certificado que está expirando.
* [Como usar o gerenciador de certificados para evitar interrupções usando as URLs de retorno de chamada - Parte 2 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Saiba como criar emissões de incidentes do PagerDuty para notificações sobre um certificado que está expirando.
