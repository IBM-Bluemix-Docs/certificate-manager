---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre o Certificate Manager
{: #about-certificate-manager}

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

## Segurança de chave privada
{: #private-key-security}

Ao importar um certificado e a chave privada correspondente para {{site.data.keyword.cloudcerts_short}}, o
serviço usa um algoritmo Advanced Encryption Standard (AES) 256 para criptografar a chave privada. O {{site.data.keyword.cloudcerts_short}} salva essa chave criptografada exclusiva para usar com sua instância de serviço.

## Disponibilidade
{: #availability}

O {{site.data.keyword.cloudcerts_short}} está disponível na região sul dos EUA somente.

## Integrações
{: #integrations}
<table>
<caption> Tabela 1. Serviços IBM Cloud que usam o Certificate Manager</caption>
  <tr>
    <th> Service </th>
    <th> Descrição </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Armazene seus certificados de domínio customizado de cluster do Kubernetes no Certificate Manager e, então, implemente-os usando os [comandos de plug-in do Kubernetes Service](/docs/containers/cs_cli_reference.html) para a CLI do IBM Cloud. [Saiba mais sobre essa integração](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>IBM Cloud Security Advisor</td>
    <td>O Security Advisor centraliza os insights dos serviços IBM Cloud, incluindo a indicação de certificados expirados e prestes a expirar em instâncias do Certificate Manager em sua conta do IBM Cloud. [Saiba mais sobre o Security Advisor](/docs/services/security-advisor/index.html#index)</td>
  </tr>
</table>
