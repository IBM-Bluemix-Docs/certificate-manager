---
copyright:
  years: 2017, 2018
lastupdated: "2018-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Gerenciando certificados usando a API
{: #managing-certificates-by-using-api}

O serviço {{site.data.keyword.cloudcerts_full}} fornece terminais REST para importar, obter e excluir certificados. Usando
o {{site.data.keyword.iamshort}}, também é possível [atribuir políticas para um certificado específico](#assigning-advanced-policies).
{: shortdesc}

## Testando as APIs
{: #testing}

É possível testar terminais REST usando Swagger ou executando solicitações de cURL na linha de comandos.  
Swagger está disponível na região Sul dos EUA somente. {{site.data.keyword.Bluemix_notm}}
{: shortdesc}

## Pré-requisito
{: #prereq-api}

Deve-se concluir as seguintes tarefas antes de poder usar {{site.data.keyword.cloudcerts_full}}.
{: shortdesc}

* Instale a [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/bluemix_cli/get_started.html#getting-started)
para obter os dados necessários.

* Ao trabalhar com a API do {{site.data.keyword.cloudcerts_short}}, é possível usar as seguintes variáveis em suas chamadas.


<table>
<caption> Tabela 1. Componentes de comando explicados </caption>
  <tr>
    <th> Componente </th>
    <th> Explicação </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> É possível obter o token de acesso {{site.data.keyword.iamshort}} (IAM) efetuando login no
{{site.data.keyword.Bluemix_notm}} e executando o comando <code>bx iam oauth-tokens</code>. </td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> O [ID de certificado baseado em Cloud Resource Name (CRN)](/docs/overview/crn.html#format) que é designado ao seu certificado após ele ser importado. É possível localizar o ID do certificado usando uma das seguintes opções: <ul><li> Na guia Gerenciar do serviço, visualize as informações do certificado selecionando-o na tabela Certificados. <li> Por API: [liste seus certificados disponíveis](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> O [ID da instância baseado em Cloud Resource Name (CRN)](/docs/overview/crn.html#format)
que é designado à sua instância de serviço após ter sido criada. É possível recuperar o ID da instância das maneiras a seguir:
    <ul>
      <li>Na página Gerenciar do serviço.</li>
      <li>Execute o comando <code>bx resource service-instance</code>, substituindo <i>&lt;Instance_Name&gt;</i> pelo nome da
sua instância de serviço.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Chame o terminal REST {{site.data.keyword.Bluemix_notm}} Resource Controller
<code>[GET
/resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code>, que requer o cabeçalho de <code>Autorização</code> com o token IAM do administrador da sua conta.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> O ID da conta do usuário que gerencia a conta do {{site.data.keyword.Bluemix_notm}}. É possível localizar seu ID da
conta executando o comando <code>bx info</code>. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> A URL do serviço na região do {{site.data.keyword.Bluemix_notm}} na qual ele foi criado. É possível localizar a URL
na UI do Swagger. </td>
  </tr>
  <tr>
    <td>  <code> name (Opcional) </code> </td>
    <td> O nome de exibição para o certificado importado. </td>
  </tr>
  <tr>
    <td> <code> description (Opcional) </code> </td>
    <td> A descrição para o certificado importado. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> Os dados do certificado, escapados. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> Os dados da chave privada, escapados. </td>
  </tr>
  <tr>
    <td> <code> intermediate (Opcional) </code> </td>
    <td> Os dados do certificado intermediário, escapados. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>O ID do usuário ao qual deseja designar uma política de acesso. Para localizar o ID do usuário, consulte [Recuperando o ID do usuário](#retrieve-user-id). </td>
  </tr>
</table>

## Importando um certificado
{: #import-certificate}  

Importe um certificado no formato Privacy-enhanced Electronic Mail (PEM) com sua chave privada. Também é possível importar
um certificado intermediário.
{: shortdesc}


Execute o seguinte comando `curl`:

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
    {: pre}

Substitua _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_,
_&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_,
_&lt;privateKey&gt;_ e _&lt;intermediate&gt;_ pelos valores apropriados. Os valores _&lt;name&gt;_,
_&lt;description&gt;_ e _&lt;intermediate&gt;_ são opcionais.

## Atualizando metadados do certificado
{: #update-certificate-metadata}  

Atualize as propriedades opcionais `name`, `description` ou ambas de um certificado.

**Nota**: operações de atualização são limitadas a cinco ações por minuto.  
{: shortdesc}

Execute o seguinte comando `curl`:

  ```
  curl -X POST \
  https://<cluster-url>/api/v2/certificate/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```

{: pre}

Substitua _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_,
_&lt;IAM-token&gt;_, _&lt;name&gt;_ e _&lt;description&gt;_ pelos valores apropriados.

## Listando todos os certificados
{: #list-certificates}  

Recupere uma lista de todos os certificados disponíveis.
{: shortdesc}

Execute o seguinte comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/<instanceId>/certificates/
  ```

  {: pre}

Substitua _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_ e _&lt;instanceId&gt;_ pelos
valores apropriados.

## Fazendo download de um certificado
{: #get-certificate}  

Use um ID do certificado recuperado para fazer download dos dados do certificado.
{: shortdesc}

Execute o seguinte comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

{: pre}

Substitua _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ e _&lt;certificateId&gt;_ pelos valores apropriados.

## Excluindo um certificado
{: #delete-certificate}  

Use um ID do certificado recuperado para excluir o certificado e seus dados.
{: shortdesc}

Execute o seguinte comando `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v2/certificate/<certificateId>
  ```

  {: pre}

Substitua _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_ e _&lt;certificateId&gt;_ pelos valores apropriados.

## Designando políticas avançadas
{: #assigning-advanced-policies}

É possível optar por permitir que determinados usuários executem determinadas ações em certificados específicos. Você pode
querer permitir que os usuários visualizem apenas um subconjunto dos certificados de instância de serviço disponíveis.
{: shortdesc}

Para designar a política, envie uma solicitação para {{site.data.keyword.iamshort}} executando o seguinte comando `curl`. Repita o comando para cada certificado.

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<account-id>/users/<user-id>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <Account-Admin-IAM-token>' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{
        "roles": [ {
            "id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }
    ],
    "resources": [
        {
            "serviceName”: "cloudcerts",
            "serviceInstance": "<instanceId>",
            "resourceType": "certificate",
            "resource": "<certificateId>"
        }
    ]
}'
```
{: pre}

Substitua _&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ e _&lt;certificateId&gt;_ pelos valores apropriados.
Substitua _&lt;Account-Admin-IAM-token&gt;_ pelo token IAM do administrador de conta.
Substitua _&lt;region&gt;_ por sua região, por exemplo, `ng` para o sul dos EUA.

**Observação**: na solicitação cURL precedente, <code>instanceId</code> e <code>certificateId</code> não são baseadas em CRN, são baseadas em GUID.  
Por exemplo, no CRN <code>certificateId</code> a seguir, o valor de instanceId é **58866f34-55ca-4477-8c32-fda435f01f97** e o valor de certificateId é **e20cb664efcbfa2c2f57801230d246a6**.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97:certificate:e20cb664efcbfa2c2f57801230d246a6
```

### Recuperando o ID do usuário
{: #retrieve-user-id}

Recupere o ID do usuário.
{: shortdesc}

Para recuperar o ID do usuário, conclua as etapas a seguir:

1. Peça ao usuário para [fornecer o token IAM](/docs/services/certificate-manager/rest-api.html#prereq-api). A estrutura do token IAM está no formato a seguir: `<value_1>.<value_2>.<value_3>`
2. Copie o valor de _&lt;value_2&gt;_ e execute o seguinte comando `echo`:

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   O resultado é um objeto JSON similar à seguinte saída:

   ```
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

3. Copie o valor da propriedade `id`.
