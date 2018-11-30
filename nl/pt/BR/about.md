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
# Sobre {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

O {{site.data.keyword.cloudcerts_long}} ajuda você a gerenciar os certificados SSL para seus aplicativos e serviços
{{site.data.keyword.IBM_notm}} baseados em nuvem.
{: shortdesc}

É possível importar certificados SSL que você obtém para seus aplicativos e serviços, armazená-los de forma segura e obter
uma visualização central dos certificados que você está usando.

É possível gerenciar seus certificados das maneiras a seguir:

* Receba uma notificação antes que seus certificados expirem para assegurar que você os renove a tempo
* Visualize os tipos de certificados em suas implementações e garanta que eles atendam às políticas da organização
* Localize certificados que precisam de substituição quando novos requisitos de conformidade ou segurança são emitidos
* Configure controles sobre quem pode acessar e gerenciar seus certificados

![Diagrama de arquitetura de serviço de alto nível](images/high-level-architecture.png)
<caption>Figura 1. Arquitetura de serviço de alto nível.</caption>

## Segurança de chave privada
{: #private-key-security}

Ao importar um certificado e a chave privada correspondente para {{site.data.keyword.cloudcerts_short}}, o
serviço usa um algoritmo Advanced Encryption Standard (AES) 256 para criptografar a chave privada. O {{site.data.keyword.cloudcerts_short}} salva essa chave criptografada exclusiva para usar com sua instância de serviço.

## Integrações
{: #integrations}

<table>
<caption>Tabela 1. Serviços do {{site.data.keyword.cloud_notm}} que usam o {{site.data.keyword.cloudcerts_short}}</caption>
  <tr>
    <th> Service </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Armazene os certificados de domínio customizado do cluster do Kubernetes em {{site.data.keyword.cloudcerts_short}} e, em seguida, implemente-os usando os [comandos de plug-in do serviço Kubernetes](/docs/containers/cs_cli_reference.html) para a CLI do {{site.data.keyword.cloud_notm}}. [Saiba mais sobre essa integração ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>O {{site.data.keyword.security-advisor_short}} centraliza as informações sobre os serviços do {{site.data.keyword.cloud_notm}}. As informações incluem a indicação de certificados expirados e certificados que estão prestes a expirar em instâncias do {{site.data.keyword.cloudcerts_short}} em sua conta do {{site.data.keyword.cloud_notm}}. [Saiba mais sobre o {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor/index.html#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Use o serviço {{site.data.keyword.cloudaccesstrailfull_notm}} para controlar como os usuários e os aplicativos interagem
com o serviço {{site.data.keyword.cloudcerts_long_notm}} no {{site.data.keyword.cloud_notm}}. [Saiba mais sobre o {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).
    <p>Para obter a lista de ações que geram um evento, consulte
Eventos do [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager/at_events.html#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Armazene os certificados de domínio customizado no serviço do {{site.data.keyword.cloudcerts_short}} e, em seguida, use os CRNs de certificado para ligar-se aos domínios customizados no {{site.data.keyword.apiconnect_short}}. [Saiba mais sobre o {{site.data.keyword.apiconnect_short}}](/docs/api-management/index.html#index).</p></td>
  </tr>
</table>

## Localidades
{: #availability}

O {{site.data.keyword.cloudcerts_short}} está disponível nas localizações de Dallas e de Londres.



## Limites
{: #limits}

É possível fazer upload de 1.000 certificados por instância, no máximo.
