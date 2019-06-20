---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-06"

keywords: certificates, SSL, TLS, activity tracker,

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

# Eventos do Activity Tracker  
{: #at_events}

Use o serviço {{site.data.keyword.at_full}} para controlar como os usuários e os aplicativos interagem com
o serviço {{site.data.keyword.cloudcerts_long}} no {{site.data.keyword.cloud_notm}}.
{:shortdesc}

O serviço {{site.data.keyword.at_short}} registra as atividades iniciadas pelo usuário que mudam
o estado de um serviço no {{site.data.keyword.cloud_notm}}. Por exemplo, quando você importar um certificado, um evento será gerado. Para obter mais informações, consulte os [docs do {{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

A tabela a seguir lista os métodos de API que geram um evento quando eles são chamados.

<table>
  <caption>Tabela 1. Ações que geram eventos</caption>
  <tr>
    <th>Ações</th>
	  <th>Descrição</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Importe um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>Peça um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Reimporte um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>Obtenha os metadados de um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Faça download de um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>Listar certificados.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>Listar metadados de certificados. Mostrar detalhes de um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Procurar os certificados.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Metadados de certificados de procura.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Excluir um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Atualizar metadados de certificado, por exemplo, mudar a descrição de um certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>Listar canais de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Criar um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Desativar ou ativar um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Atualizar o terminal de um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Excluir um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Testar um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>Uma notificação foi enviada para o terminal de um canal de notificações.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>A chave pública foi solicitada.</td>
  </tr>
</table>

## Onde procurar os eventos
{: #at_ui}

Provisione uma instância do {{site.data.keyword.at_short}} no mesmo local que a sua instância do {{site.data.keyword.cloudcerts_short}}.

Os eventos são encaminhados automaticamente para a instância de serviço do {{site.data.keyword.at_short}} no mesmo local em que o serviço do {{site.data.keyword.cloudcerts_short}} é provisionado.

## Informações Adicionais
{: #info}

* O campo *requestData_str* inclui o nome legível do certificado.

## Disponibilidade
{: #at-availability}

* O suporte do {{site.data.keyword.at_short}} está atualmente disponível para os locais **Dallas** e **Frankfurt**.
* Para outros locais, provisione uma instância do serviço Activity Tracker descontinuado até que o {{site.data.keyword.at_short}} esteja disponível.
