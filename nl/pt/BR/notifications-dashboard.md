---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Configurando Notificações para Expirar Certificados
{: #configuring-notifications-for-expiring-certificates}

Geralmente, os certificados são válidos apenas por um período de tempo configurado. Quando um certificado que você usa
expira, o seu aplicativo pode passar por um tempo de inatividade. Para evitar o tempo de inatividade, é possível configurar o {{site.data.keyword.cloudcerts_full}} para enviar notificações sobre os certificados que estão prestes a expirar para que seja possível renová-los a tempo.
{: shortdesc}

**Quando eu sou notificado?** </br>
Dependendo da data de expiração do certificado que você transferiu por upload para o {{site.data.keyword.cloudcerts_full}}, você será notificado 90, 60, 30, 10 e 1 dia antes da expiração. Além disso, você receberá notificações diárias sobre
certificados expirados a partir do primeiro dia após a expiração.

Deve-se renovar o seu certificado, fazer upload dele para o {{site.data.keyword.cloudcerts_full}} e excluir o certificado expirado para interromper o envio da notificação.

**Quais são as minhas opções para configurar as notificações?** </br>
É possível enviar notificações para o Slack usando um webhook do Slack ou usar qualquer URL de retorno de chamada que você desejar.

## Configurando um webhook do Slack
{: #setup-callback}

1. Inscreva-se no [Slack](https://slack.com/) e configure a sua área de trabalho.
2. Crie um canal Slack no qual deseja postar as suas notificações.
3. [Configure um webhook](https://api.slack.com/incoming-webhooks) para o canal Slack.

## Configurando uma URL de retorno de chamada
{: #callback}

Talvez você queria usar a URL de retorno de chamada para postar a notificação para as ferramentas usadas diariamente para acionar o processo de renovação para a sua equipe. Por exemplo, é possível enviar notificações para relatórios da tarefa de
pager, abrir automaticamente um problema no Github ou acionar scripts de renovação.  
{: shortdesc}

**Importante:** o terminal da sua URL de retorno de chamada deve atender aos seguintes requisitos para
ser usado com o {{site.data.keyword.cloudcerts_short}}:
* O terminal deve usar o protocolo HTTPS.
* O terminal não deve requerer cabeçalhos de HTTP. Este requisito inclui cabeçalhos de autorização.


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
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>
    "expiring_certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}


### Usando uma URL de retorno de chamada para abrir automaticamente um problema do GitHub
{: #sample}

O código de amostra a seguir mostra como é possível criar um problema GitHub para certificados em expiração quando uma notificação é enviada. É possível executar esse código no {{site.data.keyword.openwhisk}} ou usar o código em um ambiente diferente.   
{: shortdesc}

Para executar esse código no  {{site.data.keyword.openwhisk_short}}:

1. Crie uma ação no [Cloud Functions](/docs/openwhisk/index.html#index).
2. Use o código a seguir para criar automaticamente um problema GitHub:

```

    const {promisify} = require('bluebird');
    const request = promisify(require('request'));
    const jwtVerify = promisify(require('jsonwebtoken').verify);
    const jwtDecode = require('jsonwebtoken').decode;

    const personal_github_token = "< PERSONAL_GITHUB_TOKEN>";

    /**
     * Returns the expiration data as short date string
     * @param time
     * @returns {string}
    */
    function calcDays(time) {
        const date = new Date(time);
        return date.toDateString();
    }

    /**
     * Creates the issue body string
     * @param data
     * @returns {string}
     */
    function createBody(data) {
        return `The following certificates will expire at ${calcDays(data.expiry_date)}:
     ${data.expiring_certificates.reduce((accumulator, currentValue) => {
            return accumulator + `
    > Domain(s): ${currentValue.domains}
    CRN: ${currentValue.cert_crn}
    `;
        }, "")}`
    }

    /**
     * Gets the notification body and creates a Github issue
     * @param params
     * @returns {Promise}
     */
    async function githubIssueCreator(params) {
        // Decode message to get information
        const data = jwtDecode(params.data);
        try {
            // Create request options to get the public key for verification
            const keysOptions = {
                method: 'GET',
                url: `https://<CERTIFICATE_MANAGER_CLUSTER_BASE_URL>/api/v1/instances/${encodeURIComponent(data.instance_crn)}/notifications/publicKey`
            };

            // Send request to get the public key
            const keysResponse = await request(keysOptions);

            // Verify the data using the acquired public key
            await jwtVerify(params.data, JSON.parse(keysResponse.body).publicKey);

            // Create request options to send a new issue to Github
            // Based on Github API - https://developer.github.com/v3/issues/#create-an-issue
            const gitOptions = {
                method: 'POST',
                url: 'https://api.github.com/repos/<REPO_OWNER>/<REPO_NAME>/issues',
                headers:
                    {
                        'cache-control': 'no-cache',
                        'content-type': 'application/json',
                        authorization: 'Token 55fbe9a7e6776c9425a528783cc9755b5a0f2bb5'
                    },
                json:
                    {
                        title: "Certificates about to expire",
                        body: createBody(data),
                        labels: ['certificates']
                    }
            };
            // Send request to Github
            await request(gitOptions);
        } catch (err) {
            console.log(err);
            return Promise.reject({
                statusCode: 500,
                headers: {'Content-Type': 'application/json'},
                body: {message: 'Error processing your request'},
            });
        }

    }


    exports.main = githubIssueCreator;

```
{: codeblock}

Para outros comandos da API de REST, consulte a documentação da API do [](https://console.bluemix.net/apidocs/cloudcerts)
{: tip}


## Configurando um canal de notificação
{: #adding-channel}

Após criar um webhook do Slack ou uma URL de retorno de chamada, inclua no {{site.data.keyword.cloudcerts_short}} para começar a receber notificações sobre a expiração de certificados. O {{site.data.keyword.cloudcerts_short}} criptografa o
terminal e armazena-o com segurança.
{: shortdesc}

Para incluir um canal de notificação:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique em **Incluir canal de notificação**.
4. Escolha o tipo de canal de notificação que deseja usar.
5. Insira o webhook ou a URL de retorno de chamada para a qual você deseja enviar as notificações.
6. Clique em  ** Salvar **. Um resumo da sua configuração é exibido.

   Saída de exemplo:
   <table>
   <caption> Informações sobre o canal de notificação </caption>
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
7. Opcional: repita essas etapas para incluir mais canais de notificação.

## Testando um canal de notificação
{: #testing-channel}

É possível testar um canal de notificação para assegurar que o seu canal de notificação esteja configurado corretamente.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](#adding-channel).

Para testar um canal de notificação:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Localize o seu canal de notificação e clique em **Conexão de teste**.
3. Verifique se você recebeu uma notificação no canal configurado.


## Atualizando um canal de notificação
{: updating-channel}

É possível atualizar a configuração do seu canal de notificação, desativar ou ativar as notificações ou excluir os canais de
notificação do {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Antes de iniciar, [configure um canal de notificação](#adding-channel).

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Selecione a guia  ** Notificações ** .
3. Escolha entre as opções a seguir.
   - Para desativar ou ativar as notificações para um canal, configure o comutador para **Desativar**
ou **Ativar**.
   - Para atualizar as configurações de um canal, selecione **Editar** no menu Ações.
   - Para excluir um canal de notificação, selecione **Excluir** no menu Ações.


## Verificando a carga útil de HTTP para uma URL de retorno de chamada
{: #verify-callback}

Cada carga útil de HTTP enviada do {{site.data.keyword.cloudcerts_short}} para a sua URL de retorno de chamada é
assinada automaticamente de acordo com o padrão JWT usando um par de chaves assimétricas.  
{: shortdesc}

Para cada instância do {{site.data.keyword.cloudcerts_short}}, são geradas uma chave privada e uma pública que
não são compartilhadas entre as outras instâncias do {{site.data.keyword.cloudcerts_short}}. A chave privada é usada para
assinar a carga útil de HTTP, e é possível usar a chave pública para verificar se a carga útil é gerada pelo {{site.data.keyword.cloudcerts_short}} e não é alterada por um terceiro.

Para fazer download da chave pública:

1. Na navegação da página de detalhes do serviço, clique em **Configurações**.
2. Abra a guia  ** Notificações ** .
3. Clique no botão  ** Fazer download da chave ** . A chave é transferida por download como um arquivo PEM.
