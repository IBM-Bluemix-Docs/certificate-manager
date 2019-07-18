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

# Gerenciando certificados no painel
{: #managing-certificates-from-the-dashboard}

É possível usar o painel de serviços do {{site.data.keyword.cloudcerts_full}} para gerenciar certificados que você obtém de emissores terceirizados para usar com os seus apps ou serviços baseados em nuvem do {{site.data.keyword.IBM_notm}}.
{: shortdesc}

## Algoritmos de chave pública e formatos de certificado suportados
{: supported-formats-and-algorithms}

### Formatos de certificado
* PEM

### Algoritmos de chave pública
* Rivest-Shamir-Adleman (RSA)
* Algoritmo de Assinatura Digital (DSA)
* Algoritmo de Assinatura Digital de Curva Elíptica (ECDSA)
* Protocolo de acordo de chave de Curva Elíptica com Diffie-Hellman (ECDH)

## Importando um certificado
{: #importing-a-certificate}

Importe os certificados para que seja possível gerenciá-los.
{: shortdesc}

**Antes de iniciar**

* Crie um certificado válido e não expirado com uma chave privada correspondente (a chave é opcional).
* Converta os arquivos em formato Privacy-enhanced Electronic Mail (PEM).
* Mantenha a chave privada descriptografada para assegurar que ela possa ser importada.

Para importar um certificado, clique em **Importar certificado** e forneça os seguintes detalhes:

1. Forneça um nome do certificado.
2. Selecione o arquivo de certificado no formato PEM clicando em **Procurar**.
3. Opcional: selecione a chave privada do certificado em formato PEM clicando em **Procurar**.
4. Se aplicável, forneça o arquivo de certificado intermediário no formato PEM.
5. Opcional: insira uma descrição.
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
    <td>O algoritmo de assinatura do certificado.</td>
  </tr>
  <tr>
    <td>Algoritmo de chave</td>
    <td>O algoritmo de chave pública</td>
  </tr>
  <tr>
    <td>Expira em</td>
    <td>O número de dias restantes antes de o certificado não ser mais válido. </td>
  </tr>
  <tr>
    <td>Válido de</td>
    <td>A data na qual o certificado se tornou válido (no fuso horário de Hora Universal Coordenada). </td>
  </tr>
  <tr>
    <td>Expira em</td>
    <td>A data na qual o certificado não é mais válido (no fuso horário de Hora Universal Coordenada). </td>
  </tr>
  <tr>
    <td>Status</td>
    <td>O status de seu certificado. </td>
  </tr>
  <tr>
    <td>ID do certificado</td>
    <td>O ID gerado fornecido para o certificado na importação.</td>
  </tr>
</table>

</br>

## Reimportando um certificado
{: #reimport-certificate}

Se o seu certificado estiver prestes a expirar, será possível atualizá-lo importando uma nova
versão que tenha o mesmo domínio que o do certificado existente, mas que tenha uma nova data de validade. Quando um certificado é reimportado, a versão existente dele é retida como um backup que pode ser transferido por download, se necessário.
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
{: note}

### Fazendo download de uma versão anterior do certificado
{: #downloading-certificate}

Para fazer download da versão anterior de um certificado, conclua as etapas a seguir:

1. Expanda a linha para o certificado.
2. Clique no link **Versão anterior**.

## Pedindo certificados
{: #order-certificates}

Antes de pedir um certificado, [primeiro, conclua a configuração requerida](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates).  
Para pedir um certificado, clique em **Pedir certificado**, selecione **{{site.data.keyword.cis_full_notm}}** ou **Outro Provedor DNS** e forneça os detalhes a seguir:

1. Nome do certificado.
2. Autoridade de certificação.
3. Domínios requeridos.
4. Algoritmo apropriado e algoritmo de chave.
5. Clique em **Pedir**.

Os pedidos de certificados estão limitados a cinco pedidos/minuto por instância do {{site.data.keyword.cloudcerts_short}}, 100 pedidos por hora por conta do
usuário IBM e cinco certificados para os mesmos domínios por semana.
{: note}

## Renovando certificados
{: #renew-certificates}

Para renovar um certificado, conclua as etapas a seguir:
  1. Clique no menu na linha de certificados que você deseja renovar.
  2. Clique em **Renovar certificado**.
  3. Opcional: é possível escolher rechavear o seu certificado verificando a caixa de seleção **Rechavear certificado**. Isso renova seu certificado com um novo par de chaves.
  
    Quando você rechavear um certificado, certifique-se de implementar os novos certificados e chaves em todos os lugares em que eles estiverem em uso.
    {: note}
    
  4. Clique em **Renovar**.
  
  É possível renovar apenas os certificados que você pediu por meio do {{site.data.keyword.cloudcerts_short}}.
  {: note}

A renovação de um certificado está limitada a cinco solicitações de renovação por certificado por minuto, 100 renovações por hora por conta do usuário IBM.
{: note}


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

Não é possível fazer download de certificados expirados.
{: note}

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
{: note}
