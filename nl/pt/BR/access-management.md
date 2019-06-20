---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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

# Gerenciando funções de acesso de serviço
{: #managing-service-access-roles}

É possível proteger os serviços dentro do {{site.data.keyword.cloud_notm}} permitindo que somente usuários com funções de acesso especificadas concluam determinadas ações.
{: shortdesc}

## Funções de acesso de plataforma
{: #platform-access-roles}

É possível usar as funções de acesso de plataforma para permitir que os usuários concluam as tarefas nos recursos da plataforma,
como a criação ou a exclusão de instâncias em sua conta do {{site.data.keyword.cloud_notm}}.

<table>
<caption> Tabela 1. Ações que são mapeadas para as funções de acesso de plataforma</caption>
  <tr>
    <th> Ações </th>
    <th> Função </th>
  </tr>
  <tr>
    <td>Visualizar instâncias do  {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, operador, editor, visualizador </td>
  </tr>
  <tr>
    <td>Criar uma instância do  {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Excluir uma instância do  {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, Editor </td>
  </tr>
</table>

## Funções de acesso de serviço
{: #service-access-roles}

É possível usar as funções de acesso de serviço para permitir que os usuários concluam as tarefas nas instâncias do
{{site.data.keyword.cloudcerts_short}}, como importar, fazer download, editar ou excluir certificados.

<table>
<caption> Tabela 2. Ações que são mapeadas para as funções de acesso do serviço</caption>
  <tr>
    <th> Ações </th>
    <th> Função </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Gerenciador, gravador, leitor </td>
  </tr>
  <tr>
    <td>Fazer download de um certificado e chave privada </td>
    <td> Gerenciador, gravador </td>
  </tr>
  <tr>
     <td>Obter metadados do certificado </td>
     <td> Gerenciador, gravador, leitor </td>
  </tr>      
  <tr>
    <td>Atualizar os metadados do certificado</td>
    <td> Gerenciador, gravador </td>
  </tr>
  <tr>
    <td>Importar ou reimportar os certificados, as chaves privadas e os certificados intermediários </td>
    <td> Gerenciador </td>
  </tr>
  <tr>
    <td>Pedir um certificado </td>
    <td> Gerenciador </td>
  </tr>
  <tr>
    <td>Excluir um certificado e chave privada </td>
    <td> Gerenciador </td>
  </tr>
      <tr>
        <td>Listar todos os canais de notificação </td>
        <td> Gerenciador, gravador, leitor </td>
      </tr>
   <tr>
     <td>Incluir, atualizar ou excluir um canal de notificação </td>
     <td> Gerenciador </td>
   </tr>
     <tr>
       <td>Testar um canal de notificação </td>
       <td> Gerenciador, gravador, leitor </td>
     </tr>

</table>

Para obter mais informações sobre funções de usuário e permissões, consulte
[Funções do usuário](/docs/iam?topic=iam-userroles#userroles).

## Configurando políticas de acesso para usuários
{: #configuring-access-policies}

É possível configurar as políticas de acesso para uma instância do {{site.data.keyword.cloudcerts_short}} (e, portanto,
para todos os certificados nessa instância) ou configurar políticas para certificados individuais (recursos) dentro de uma
instância.

**Exemplos de alocação de função**

* Designe pelo menos a função de Visualizador a todos os usuários, para que cada um deles possa ver as instâncias de serviço.
* Designe a função de Administrador ou de Editor a um usuário se desejar que esse usuário crie e exclua instâncias.
* Designe pelo menos a função de Leitor se desejar que um usuário visualize os certificados dentro de uma instância.

{: shortdesc}

### Configurando políticas de acesso
{: #configuring-access}

Para configurar as políticas de acesso, conclua as etapas a seguir:

1. Navegue para **Gerenciar > Acesso (IAM) > Usuários**. Uma lista dos usuários com acesso à sua conta do {{site.data.keyword.cloud_notm}} é mostrada.
2. Clique no nome do usuário ao qual você deseja designar uma política de acesso. Se o usuário não for mostrado, clique em **Convidar usuários** para [incluir o usuário em sua conta do {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Clique em **Políticas de acesso** e, em seguida, em **Designar acesso**.
4. Clique em  ** Designar acesso a recursos **.
5. No menu **Serviços**, selecione **Gerenciador de certificados**.
6. No menu **Instância de serviço**, selecione uma instância do {{site.data.keyword.cloudcerts_short}} ou use o valor padrão `Todas as instâncias`.
7. Designe uma [função de acesso de plataforma](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) para o usuário.
8. Designe uma [função de acesso de serviço](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) para o usuário.
9. Clique em **Designar** para designar a política de acesso para o usuário.

### Permitindo o acesso a um certificado específico
{: #allow-access-to-specific-certificate}

Para permitir o acesso a um certificado específico, conclua as etapas a seguir:

1. [ Recupere seu ID do certificado ](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Crie duas políticas de acesso:
   - A primeira política: designar pelo menos a função de acesso à plataforma **Visualizador** para a instância de serviço
   - A segunda política: designar pelo menos a função de acesso ao serviço **Leitor**
     - Insira `certificado` no campo **Tipo de recurso**.
     - Insira o ID do certificado no campo **ID do recurso**.

### Recuperando o ID de um certificado
{: #get-certificate-id}

Para recuperar o ID de um certificado, conclua as etapas a seguir:

1. No painel do  {{site.data.keyword.cloud_notm}} , selecione sua instância do  {{site.data.keyword.cloudcerts_short}} .
2. Na navegação na página de detalhes do serviço, selecione **Gerenciar**.
3. Selecione um certificado.
4. Nos detalhes do certificado, localize o CRN do certificado.
5. Copie o ID do certificado. O CRN contém valores diferentes que são todos separados por dois-pontos
(`:`). O ID do certificado é o último valor no CRN. Por exemplo: `e20cb664efcbfa2c2f57801230d246a6`
