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

# Configurar notificações
{: #configuring-notifications}

O {{site.data.keyword.cloudcerts_full}} pode enviar notificações a você sobre eventos de ciclo de vida do certificado. Elas incluem lembretes de renovação dos certificados antes que eles expirem e de implementação de certificados quando eles estiverem prontos. Para obter notificações do {{site.data.keyword.cloudcerts_short}}, é possível configurar um canal de notificação. É possível especificar um Webhook do Slack, uma URL de Retorno de chamada ou qualquer combinação dos dois.
{: shortdesc}

O recurso de notificações também é usado quando você [pede certificados](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates) por meio do {{site.data.keyword.cloudcerts_short}}. Para provar que você possui o domínio para o qual está solicitando um certificado, o {{site.data.keyword.cloudcerts_short}} envia um desafio como uma notificação para a sua URL de Retorno de chamada. O desafio é um registro de texto, que você coloca no Serviço do Sistema de Nomes de Domínio (DNS) no qual o seu domínio está registrado. Quando o registro de texto estiver em vigor, o desafio será considerado concluído. Como o desafio é enviado como uma notificação para sua URL de Retorno de chamada, você é capaz de automatizar o processo de validação de domínio executando o código em resposta ao evento de notificação.

## Notificações para monitorar a expiração do certificado
{: #notifications-monitoring-certificate-expiration}

Os certificados são geralmente válidos por uma quantia de tempo configurada. Quando um certificado que você usa
expira, o seu aplicativo pode passar por um tempo de inatividade. Para evitar o tempo de inatividade, é possível configurar o {{site.data.keyword.cloudcerts_short}} para enviar notificações a você sobre certificados que estão prestes a expirar, de modo que você seja lembrado de renová-los a tempo.

Você também será alertado quando uma versão renovada do seu certificado for reimportada para o {{site.data.keyword.cloudcerts_short}} no lugar da versão expirada. Isso é para lembrar você de implementá-lo em pontos de terminação de SSL/TLS. Essa notificação sobre certificados reimportados é enviada somente para canais da [versão 2 do canal](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


**Quando eu sou notificado?**  
Dependendo da data de expiração do certificado que você transferiu por upload para o {{site.data.keyword.cloudcerts_short}}, você será notificado 90, 60, 30, 10 e 1 dia antes da expiração. Além disso, você recebe notificações diárias sobre os certificados expirados. As notificações diárias se iniciam no primeiro dia após a expiração do certificado.

Deve-se renovar e reimportar esse certificado no lugar do anterior para que o {{site.data.keyword.cloudcerts_short}} pare de impedir que as notificações sejam enviadas. Ao reimportar o seu certificado, você receberá uma notificação de que o seu certificado foi reimportado para lembrar você de reimplementá-lo.

**Quais são as minhas opções para configurar as notificações?**  
É possível enviar notificações para o Slack usando um Webhook do Slack ou usar qualquer URL de Retorno de chamada que você desejar.

## Notificações relacionadas ao pedido de certificados
{: #notifications-ordering-certificates}

O {{site.data.keyword.cloudcerts_short}} notifica você quando um certificado que você pede do {{site.data.keyword.cloudcerts_short}} é emitido para você ou renovado com sucesso. Você também será notificado se o seu pedido falhar ou se uma renovação falhar.
{: shortdesc}

Configurar um canal de notificação de URL de Retorno de chamada e ter a capacidade de manipular eventos que estão relacionados à validação de domínio são pré-requisitos para pedir e renovar certificados. Quando você pedir um certificado, o {{site.data.keyword.cloudcerts_short}} enviará um registro de texto de desafio para a sua URL de Retorno de chamada que você usar para provar que você possui o domínio para o qual está solicitando o certificado. Um registro de texto de desafio também será enviado quando você solicitar a renovação de um certificado. 


## Configurando um Webhook do Slack
{: #setup-callback}

Para configurar um Webhook do Slack, conclua as etapas a seguir:

1. Inscreva-se no [Slack](https://slack.com/) e configure a sua área de trabalho.
2. Crie um canal Slack no qual deseja postar as suas notificações.
3. [Configure um webhook](https://api.slack.com/incoming-webhooks) para o canal do Slack.

## Configurando uma URL de Retorno de chamada
{: #callback}

Para acionar o processo de renovação para a sua equipe, será possível usar uma URL de Retorno de chamada para postar notificações para as ferramentas que você usar. Por exemplo, é possível enviar notificações para relatar ao PagerDuty, abrir automaticamente um problema no GitHub ou acionar scripts de renovação. Também será possível acionar automaticamente a implementação de certificados em resposta às notificações quando os certificados forem reimportados ou emitidos com sucesso.
{: shortdesc}

Uma URL de Retorno de chamada é um pré-requisito para pedir certificados.
{: note}

**Importante:** o seu terminal de URL de Retorno de chamada deve atender aos requisitos a seguir para serem usados com o {{site.data.keyword.cloudcerts_short}}:
* O terminal deve usar o protocolo HTTPS.
* O terminal não deve requerer cabeçalhos de HTTP. Este requisito inclui cabeçalhos de autorização.
* O terminal deve retornar um código de status `200 OK` para indicar uma entrega de notificação bem-sucedida.

### Formato da notificação
{: #notification_format}

A notificação que é enviada para a sua URL de Retorno de chamada é um documento JSON assinado com a sua chave assimétrica de instância no formato a seguir.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Após a decodificação e verificação da carga útil, o conteúdo será uma sequência JSON, [de acordo com a versão do canal](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configurando um canal de notificação
{: #adding-channel}

Após você criar um Webhook do Slack ou uma URL de Retorno de chamada, será possível incluí-lo no {{site.data.keyword.cloudcerts_short}} para começar a receber notificações sobre certificados expirados, certificados reimportados, certificados emitidos e desafios para validação de domínio.
{: shortdesc}

O {{site.data.keyword.cloudcerts_short}} criptografará os terminais que você configura para armazená-los com segurança.
{: important}

Para incluir um canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique em **Incluir canal de notificação**.
4. Escolha o tipo de canal de notificação que deseja usar.
5. Insira o Webhook ou a URL de Retorno de chamada no local para o qual você deseja enviar notificações.
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
    <td>O estado do canal de notificação. Se configurado como desativado, nenhuma notificação será enviada.</td>
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

    Quando você salvar um Webhook do Slack, o {{site.data.keyword.cloudcerts_short}} enviará automaticamente uma notificação de confirmação para o canal do Slack que você configurou. Consulte o seu canal Slack para verificar se você recebeu essa
notificação.
    {: tip}
7. (Opcional) Repita essas etapas para incluir mais canais de notificação.

## Testando um canal de notificação
{: #testing-channel}

É possível testar um canal de notificação para assegurar que o seu canal de notificação esteja configurado corretamente.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Para testar um canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Localize o seu canal de notificação e clique em **Conexão de teste**.
3. Verifique se você recebeu uma notificação no canal configurado.

## Atualizando um canal de notificação
{: #updating-channel}

É possível atualizar a configuração do seu canal de notificação, desativar ou ativar as notificações ou excluir os canais de
notificação do {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Para atualizar seu canal de notificação, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Selecione a guia  ** Notificações ** .
3. Escolha a partir das opções a seguir:
   * Para desativar ou ativar as notificações para um canal, configure o comutador para **Desativar**
ou **Ativar**.
   * Para atualizar as configurações de um canal, selecione **Editar** no menu Ações.
   * Para excluir um canal de notificação, selecione **Excluir** no menu Ações.

## Verificando a carga útil de HTTP para uma URL de Retorno de chamada
{: #verify-callback}

Cada carga útil de HTTP que é enviada do {{site.data.keyword.cloudcerts_short}} para a sua URL de Retorno de chamada é assinada automaticamente de acordo com o padrão do JWT usando um par de chaves assimétricas.  
{: shortdesc}

Para cada instância do {{site.data.keyword.cloudcerts_short}}, são geradas uma chave privada e uma pública que
não são compartilhadas entre as outras instâncias do {{site.data.keyword.cloudcerts_short}}. A chave privada é usada para
assinar a carga útil de HTTP, e é possível usar a chave pública para verificar se a carga útil é gerada pelo {{site.data.keyword.cloudcerts_short}} e não é alterada por um terceiro.

Para fazer download da chave pública, conclua as etapas a seguir:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique no botão  ** Fazer download da chave ** . A chave é transferida por download como um arquivo PEM.

## Versões de canal
{: #channel-versions}

Conforme o Certificate Manager evolui, podemos modificar o formato da estrutura de carga útil de notificações de tempos em tempos. Para assegurar a compatibilidade com versões anteriores, a carga útil que é enviada para os seus canais existentes não mudará.   

Se tiver canais de notificação existentes (Slack ou URL de Retorno de Chamada), para obter a nova versão da carga útil:

1. Para a URL de Retorno de Chamada, verifique se sua implementação pode aceitar a nova carga útil.
2. Crie um novo canal de notificação (novos canais são sempre criados com a versão mais recente do canal).
3. Teste se o novo canal funciona corretamente.
4. Exclua o canal antigo.

Para versões de canal, confira a [Documentação da API](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Exemplos
{: #examples}

* [Como usar o gerenciador de certificados para evitar interrupções usando as URLs de retorno de chamada - Parte 1 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Saiba como criar emissões do GitHub para notificações sobre um certificado que está expirando.
* [Como usar o gerenciador de certificados para evitar interrupções usando as URLs de retorno de chamada - Parte 2 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Saiba como criar incidentes do PagerDuty para notificações de certificado expiradas.
* [Como validar um domínio usando uma URL de retorno de chamada e uma ação do Cloud Function ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
