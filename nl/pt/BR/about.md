---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

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

# Sobre {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

O {{site.data.keyword.cloudcerts_full}} o ajuda a obter, armazenar e gerenciar certificados SSL usados para implementações do {{site.data.keyword.cloud_notm}} ou outras implementações em nuvem e no local.
{: shortdesc}

É possível importar certificados SSL que você obtém para seus aplicativos e serviços, armazená-los de forma segura e obter
uma visualização central dos certificados que você está usando. Ou é possível pedir certificados públicos por meio do Certificate Manager das CAs suportadas.

É possível gerenciar seus certificados das maneiras a seguir:

* Receba uma notificação antes que seus certificados expirem para assegurar que você os renove a tempo  
* Use notificações para acionar a renovação automatizada de certificado  
* Visualize os tipos de certificados em suas implementações e garanta que eles atendam às políticas da organização  
* Localize certificados que precisam de substituição quando novos requisitos de conformidade ou segurança são emitidos  
* Configure controles sobre quem pode acessar e gerenciar seus certificados
* Peça novos certificados públicos


![Diagrama de arquitetura de serviço de alto nível](images/high-level-architecture.png)
<caption>Figura 1. Arquitetura de serviço de alto nível.</caption>


## Segurança de chave privada
{: #private-key-security}

Ao importar ou pedir um certificado para o {{site.data.keyword.cloudcerts_short}}, o serviço usa um algoritmo 256 do Padrão de Criptografia Avançado (AES) para criptografar a chave privada. O {{site.data.keyword.cloudcerts_short}} salva essa chave criptografada exclusiva para usar com sua instância de serviço.

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
    <td>É possível implementar certificados TLS de domínio customizado de maneira fácil e segura por meio do {{site.data.keyword.cloudcerts_short}} em seu cluster Kubernetes. Os administradores de cluster podem usar os [comandos de plug-in do Serviço Kubernetes](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) para atualizar certificados TLS como segredos do Kubernetes com um novo certificado, sem causar tempo de inatividade. Para começar, consulte as [Anotações de ingresso na documentação](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>O [{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) centraliza as informações sobre os serviços do {{site.data.keyword.cloud_notm}}. As informações incluem a indicação de certificados expirados e certificados que estão prestes a expirar em instâncias do {{site.data.keyword.cloudcerts_short}} em sua conta do {{site.data.keyword.cloud_notm}}. [Saiba mais sobre o {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>É possível usar o [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) para rastrear como os usuários e os aplicativos interagem com o serviço {{site.data.keyword.cloudcerts_long_notm}} no {{site.data.keyword.cloud_notm}}.
    <p>Para obter a lista de ações que geram um evento, veja [eventos do {{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Armazene os certificados de domínio customizado no serviço do {{site.data.keyword.cloudcerts_short}} e, em seguida, use os CRNs de certificado para ligar-se aos domínios customizados no {{site.data.keyword.apiconnect_short}}. [Saiba mais sobre o {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index).</p></td>
  </tr>
</table>

## Disponibilidade
{: #availability}

O {{site.data.keyword.cloudcerts_short}} está disponível nos locais Dallas, Londres, Frankfurt e Tóquio.



## Limites
{: #limits}

É possível fazer upload de 1.000 certificados por instância, no máximo.

## Conformidade e normas
{: #compliance-and-standards}

O {{site.data.keyword.cloudcerts_short}} concluiu com sucesso várias certificações e auditorias e atende a vários padrões importantes.

### HIPAA
{: #compliance-hippa}

O {{site.data.keyword.cloudcerts_short}} atende aos controles IBM necessários que são proporcionais aos requisitos de Segurança e Regra de privacidade do Health Insurance Portability and Accountability Act (HIPAA) de 1996.

### International Organization for Standardization (ISO)
{: #compliance-iso}

* Certificado de Serviços {{site.data.keyword.IBM_notm}} (PaaS e SaaS) - ISO 27001

### Regulamento Geral sobre a Proteção de Dados (GDPR)
{: #compliance-gdpr}

O GDPR procura criar uma estrutura de lei harmonizada de proteção de dados em toda a UE e pretende devolver aos cidadãos o controle de seus dados pessoais, ao mesmo tempo em que impõe regras rígidas àqueles que hospedam e 'processam' esses dados, em qualquer lugar do mundo. O Regulamento também introduz regras em relação à livre circulação de dados pessoais dentro e fora da UE. Para obter mais informações, consulte a [Declaração de privacidade da IBM](https://www.ibm.com/privacy/).
