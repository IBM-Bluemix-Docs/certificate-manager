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

# Gerenciando certificados no painel
{: #managing-certificates-from-the-dashboard}

É possível usar o painel de serviços do {{site.data.keyword.cloudcerts_full}} para gerenciar certificados que você obtém de emissores terceirizados para usar com os seus apps ou serviços baseados em nuvem do {{site.data.keyword.IBM_notm}}. Após a importação dos certificados e das chaves, eles são criptografados e armazenados pelo serviço.
{: shortdesc}

## Importando um certificado
{: #importing-a-certificate}

Importe os certificados para que seja possível gerenciá-los.
{: shortdesc}

**Antes de iniciar**

* Crie um certificado válido em vigor com uma chave privada correspondente.
* Converta os arquivos em formato Privacy-enhanced Electronic Mail (PEM).
* Mantenha a chave privada descriptografada para assegurar que ela possa ser importada.

Para importar um certificado, clique em **Importar certificado** e forneça os seguintes detalhes:

1. Insira um nome de exibição.
2. Selecione o arquivo de certificado no formato PEM clicando em **Procurar**.
3. Selecione a chave privada do certificado no formato PEM clicando em **Procurar**.
4. Se aplicável, forneça o arquivo de certificado intermediário no formato PEM.
5. (Opcional) Insira uma descrição. 
6. Clique em **Importar**.

Depois de importar um certificado, as seguintes informações serão exibidas na tabela de Certificados. Para visualizar mais informações sobre o certificado, é possível expandir a linha do certificado na tabela Certificados.

<table>
<caption> Tabela 1. Informações sobre o certificado importado </caption>
  <tr>
    <th> Componente </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td>Nome</td>
    <td>Um nome de exibição significativo. O comprimento máximo é de 256 caracteres. </td>
  </tr>
  <tr>
    <td>Descrição</td>
    <td>(Opcional) Texto descritivo para o certificado. O comprimento máximo é de 1.024 caracteres.</td>
  </tr>
  <tr>
    <td>Domínio</td>
    <td>O domínio ou domínios para os quais o certificado é válido. </td>
  </tr>
  <tr>
    <td>Emissor</td>
    <td>A autoridade de certificação (CA) que emitiu o certificado.</td>
  </tr>
  <tr>
    <td>Algoritmo</td>
    <td>O tipo de criptografia pelo qual o certificado é criado. </td>
  </tr>
  <tr>
    <td>Algoritmo de chave</td>
    <td>O tipo de chave e o tamanho que são usados pelo algoritmo. </td>
  </tr>
  <tr>
    <td>Expira em </td>
    <td>O número de dias restantes antes de o certificado não ser mais válido. </td>
  </tr>
  <tr>
    <td>Data de emissão</td>
    <td>A data na qual o certificado foi emitido. </td>
  </tr>
  <tr>
    <td>Válido de</td>
    <td>A data na qual o certificado tornou-se válido. </td>
  </tr>
  <tr>
    <td>Expira em</td>
    <td>A data em que o certificado não é mais válido. </td>
  </tr>
  <tr>
    <td>ID do certificado</td>
    <td>O ID gerado fornecido para o certificado na importação. </td>
  </tr>
</table>

## Reimportando um certificado
{: #reimport-certificate}

Se o seu certificado estiver prestes a expirar, será possível atualizá-lo importando uma nova versão do certificado que tenha o mesmo domínio que o certificado existente, mas com uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup que pode ser transferido por download, se necessário.
{: shortdesc}

### Reimportando o certificado
{: #reimporting-certificate}

Para reimportar um certificado, conclua as etapas a seguir:

1. Expanda a linha para o certificado.
2. Clique em **Reimportar certificado**.
3. Selecione o novo arquivo de certificado no formato PEM clicando em **Procurar**.
4. (Opcional) Selecione a chave privada do novo certificado no formato PEM clicando em **Procurar**.
5. (Opcional) Forneça um novo arquivo de certificado intermediário no formato PEM clicando em **Procurar**.
6. Clique em **Reimportar** e, em seguida, em **Pronto**.

A reimportação de certificados é limitada a cinco ações por minuto.
{: tip}

### Fazendo download de uma versão anterior do certificado
{: #downloading-certificate}

Para fazer download da versão anterior de um certificado, conclua as etapas a seguir:

1. Expanda a linha para o certificado.
2. Clique no link **Versão anterior**.

## Procurando certificados
{: #searching-certificates}

Se você gerencia muitos certificados, é possível usar a barra de procura para localizar o certificado necessário.
{: shortdesc}

* Para procurar por nome do certificado, domínio de certificado ou emissor do certificado, digite o termo de procura na
barra de procura e pressione Enter.
* Para visualizar todos os seus certificados, clique no ícone **X** na barra de procura.

## Fazendo download de certificados
{: #downloading-certificates}

Quando você estiver pronto para implementar seu certificado para seu aplicativo ou serviço, será possível fazer
download do certificado e da chave privada associada.
{: shortdesc}

Para fazer download de um certificado, conclua as etapas a seguir:

1. Selecione a caixa de seleção para o certificado que você deseja fazer download.
2. Clique em **Fazer o download do certificado**. Dependendo do que você importou para o serviço, você
receberá um arquivo compactado contendo arquivos PEM para o certificado, uma chave privada associada e um certificado
intermediário associado.

## Excluindo certificados
{: #deleting-certificates}

Se você deseja parar o rastreamento de um certificado, é possível excluí-lo.
{: shortdesc}  

Para excluir um certificado, conclua as etapas a seguir:

1. Selecione a caixa de seleção para o certificado que você deseja excluir.
2. Clique no ícone **Lixeira**.

## Atualizando metadados de certificados
{: #updating-certificates-metadata}

Também é possível atualizar o nome e a descrição de um certificado.
{: shortdesc}

Para atualizar um certificado, conclua as etapas a seguir:

1. Selecione uma linha para abrir os detalhes para esse certificado.
2. Atualize o nome ou a descrição.
3. Salve as suas mudanças.

É possível executar até cinco ações de atualização por minuto.
{: tip}
