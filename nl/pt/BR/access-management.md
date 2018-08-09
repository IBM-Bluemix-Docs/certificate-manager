---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-20"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando funções de acesso de serviço
{: #managing-service-access-roles}

É possível proteger os serviços dentro do {{site.data.keyword.Bluemix_notm}} permitindo que somente usuários com funções de acesso especificadas concluam determinadas ações.
{: shortdesc}


## Funções de acesso de plataforma
{: #platform-access-roles}

É possível usar as funções de acesso de plataforma para permitir que os usuários concluam as tarefas nos recursos da plataforma,
como a criação ou a exclusão de instâncias em sua conta do {{site.data.keyword.Bluemix_notm}}.

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

As funções de plataforma também fornecem acesso a determinadas ações nos certificados dentro das instâncias. Essas ações foram descontinuadas.


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
    <td>Atualizar dados do certificado</td>
    <td> Gerenciador, gravador </td>
  </tr>
  <tr>
    <td>Fazer upload dos certificados, chaves privadas e certificados intermediários </td>
    <td> Gerenciador  </td>
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
[Funções do usuário](/docs/iam/users_roles.html#userroles).


## Configurando políticas de acesso para usuários
{: #configuring-access-policies}

É possível configurar as políticas de acesso para uma instância do {{site.data.keyword.cloudcerts_short}} (e, portanto,
para todos os certificados nessa instância) ou configurar políticas para certificados individuais (recursos) dentro de uma
instância.
{: shortdesc}

1.  Navegue para  ** Gerenciar > Conta > Usuários **. Uma lista dos usuários com acesso à sua conta do {{site.data.keyword.Bluemix_notm}} é mostrada.
2.  Clique no nome do usuário ao qual você deseja designar uma política de acesso. Se o usuário não for mostrado, clique em **Convidar usuários** para [incluir o usuário em sua conta do {{site.data.keyword.Bluemix_notm}}](/docs/iam/iamuserinv.html#iamuserinv).
3.  Clique em  ** Designar acesso **.
4.  Clique em  ** Designar acesso a recursos **.
5.  No menu suspenso **Serviços**, selecione **Gerenciador de certificados**.
6.  No menu **Instância de serviço**, selecione uma instância do {{site.data.keyword.cloudcerts_short}} ou use o valor padrão `Todas as instâncias`.
7.  Opcional: configure o acesso a um certificado específico.
    1. [ Recupere seu ID do certificado ](#get-certificate-id).
    2. Insira `certificado` no campo **Tipo de recurso**.
    3. Insira o ID do certificado no campo **ID do recurso**.
8.  Designe uma [função de acesso de plataforma](#platform-access-roles) para o usuário.
9.  Designe uma [função de acesso de serviço](#service-access-roles) para o usuário.
10. Clique em **Designar** para designar a política de acesso para o usuário.

** Exemplos de alocação de função: **
* Designe pelo menos a função de Visualizador a todos os usuários, para que cada um deles possa ver as instâncias de serviço.
* Designe a função de administrador ou de editor a um usuário se desejar que esse usuário crie/exclua instâncias.
* Designe pelo menos a função de Leitor se desejar que um usuário visualize os certificados dentro de uma instância.

### Recuperando o ID de um certificado
{: #get-certificate-id}

1. No painel do  {{site.data.keyword.Bluemix_notm}} , selecione sua instância do  {{site.data.keyword.cloudcerts_short}} .
2. Na navegação na página de detalhes do serviço, selecione **Gerenciar**.
3. Selecione um certificado.
4. Nos detalhes do certificado, localize o CRN do certificado.
5. Copie o ID do certificado. O CRN contém valores diferentes que são todos separados por dois-pontos
(`:`). O ID do certificado é o último valor em seu CRN; por exemplo: `e20cb664efcbfa2c2f57801230d246a6)`
