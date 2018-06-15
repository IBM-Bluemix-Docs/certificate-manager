---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

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

### Funções de acesso de plataforma
{: #platform-access-roles}

É possível usar as funções de acesso de plataforma para permitir que os usuários concluam tarefas nos recursos da plataforma, tais como criar ou excluir instâncias em sua conta do IBM Cloud.

<table>
<caption> Tabela 1. Ações que são mapeadas para as funções de acesso de plataforma</caption>
  <tr>
    <th> Ações </th>
    <th> Função </th>
  </tr>
  <tr>
    <td>Visualizar instâncias do Certificate Manager</td>
    <td> Administrador, operador, editor, visualizador </td>
  </tr>
  <tr>
    <td>Criar uma instância do Certificate Manager</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Excluir uma instância do Certificate Manager</td>
    <td> Administrador, Editor </td>
  </tr>
</table>

Historicamente, as funções de plataforma também dão acesso a determinadas ações nos certificados dentro de instâncias. Essa definição está obsoleta e será removida no futuro próximo.

### Funções de acesso de serviço
{: #service-acceess-roles}

É possível usar funções de acesso para permitir que os usuários concluam tarefas nas instâncias do Certificate Manager, tais como importar, fazer download, editar ou excluir certificados.

<table>
<caption> Tabela 2. Ações que são mapeadas para as funções de acesso do serviço</caption>
  <tr>
    <th> Ações </th>
    <th> Função </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Gerenciador, gravador, leitor</td>
  </tr>
  <tr>
    <td>Fazer download de um certificado e chave privada </td>
    <td> Gerenciador, gravador</td>
  </tr>
  <tr>
    <td>Atualizar dados do certificado</td>
    <td> Gerenciador, gravador</td>
  </tr>
  <tr>
    <td>Fazer upload dos certificados, chaves privadas e certificados intermediários </td>
    <td> Gerenciador  </td>
  </tr>
  <tr>
    <td>Excluir um certificado e chave privada </td>
    <td> Gerente </td>
  </tr>
</table>


Para obter mais informações sobre funções de usuário e permissões, consulte
[Funções do usuário](/docs/iam/users_roles.html#userroles).

### Designando funções de acesso do usuário
{: #assigning-user--access-roles}

Para designar uma função de acesso no nível de conta ou no nível de grupo de recursos, conclua as etapas a seguir.
Se o usuário não faz parte de sua organização, comece enviando um convite para esse usuário.

1. Acesse **Gerenciar > Conta > Usuários**.
2. No menu **Ações**, selecione **Designar política**.
3. Clique em **Designar acesso a recursos** ou **Designar acesso dentro de um grupo de recursos**.
4. Em **Serviços**, selecione **Certificate Manager**.
5. Opcional: selecione uma **Região** ou use o padrão, **Todas as regiões**.
6. Opcional: selecione uma **Instância de serviço** ou use o padrão, **Todas as instâncias**.
7. Em **Selecionar funções > Designar funções de acesso de plataforma/serviço**, selecione o nível de acesso apropriado.

**Exemplos:**
* Designe pelo menos a função de Visualizador a todos os usuários, para que cada um deles possa ver as instâncias de serviço. 
* Designe a função de Administrador ou de Editor a um usuário se desejar que esse usuário crie instâncias. 
* Designe pelo menos a função de Leitor se desejar que um usuário visualize os certificados dentro de uma instância.
