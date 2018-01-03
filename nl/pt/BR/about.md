---

copyright:
  years: 2017
lastupdated: "2017-12-13"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Sobre
{: #about-cloud-certs}

Descubra {{site.data.keyword.cloudcerts_full}}.

## O que é {{site.data.keyword.cloudcerts_short}}
{: #what-is-cloud-certs}

O {{site.data.keyword.cloudcerts_short}} ajuda você a gerenciar os certificados SSL para seus aplicativos e serviços
{{site.data.keyword.IBM_notm}} baseados em nuvem.
{: shortdesc}

É possível importar certificados SSL que você obtém para seus aplicativos e serviços, armazená-los de forma segura e obter
uma visualização central dos certificados que você está usando.

É possível gerenciar seus certificados das maneiras a seguir:

* Monitore as datas de expiração dos seus certificados para garantir que você os renove a tempo
* Visualize os tipos de certificados em suas implementações e garanta que eles atendam às políticas da organização
* Localize certificados que precisam de substituição quando novos requisitos de conformidade ou segurança são emitidos
* Configure controles sobre quem pode acessar e gerenciar seus certificados

## Disponibilidade
{: #availability}

O {{site.data.keyword.cloudcerts_short}} está disponível na região sul dos EUA somente.

## Segurança de chave privada
{: #private-key-security}

Ao importar um certificado e a chave privada correspondente para {{site.data.keyword.cloudcerts_short}}, o
serviço usa um algoritmo Advanced Encryption Standard (AES) 256 para criptografar a chave privada. 
O {{site.data.keyword.cloudcerts_short}} salva essa chave criptografada exclusiva para usar com sua instância de serviço.

## Identidade e gerenciamento de acesso
{: #identity-access-management}

É possível proteger serviços no {{site.data.keyword.Bluemix_notm}} permitindo que apenas usuários com funções
especificadas concluam determinadas ações.
{: shortdesc}

<table>
<caption> Tabela 1. Ações que são mapeadas para funções de usuário</caption>
  <tr>
    <th> Ações </th>
    <th> Função </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Administrador, operador, editor, visualizador </td>
  </tr>
  <tr>
    <td>Fazer download de um certificado e chave privada </td>
    <td> Administrador, operador </td>
  </tr>
  <tr>
    <td>Atualizar dados do certificado</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Fazer upload dos certificados, chaves privadas e certificados intermediários </td>
    <td> Administrador, Editor  </td>
  </tr>
  <tr>
    <td>Excluir um certificado e chave privada </td>
    <td> Administrador, Editor </td>
  </tr>
</table>

Para obter mais informações sobre funções de usuário e permissões, consulte
[Funções do usuário](/docs/admin/patterns.html#userroles).

### Designando funções do usuário
{: #assigning-user-roles}

Para designar uma função de usuário no nível de conta ou de grupo de recursos, conclua as etapas a seguir.
Se o usuário não faz parte de sua organização, comece enviando um convite para esse usuário.

1. Acesse **Gerenciar > Conta > Usuários**.
2. No menu **Ações**, selecione **Designar política**.
3. Clique em **Designar acesso a recursos** ou **Designar acesso dentro de um grupo de recursos**.
4. Em **Serviços**, selecione **Certificate Manager**.
5. Opcional: selecione uma **Região** ou use o padrão, **Todas as regiões**.
6. Opcional: selecione uma **Instância de serviço** ou use o padrão, **Todas as instâncias**.
7. Em **Selecionar funções > Designar funções de acesso de plataforma**, selecione o nível de
acesso apropriado.
