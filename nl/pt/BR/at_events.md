---

copyright:
  years: 2018
lastupdated: "2018-06-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# {{site.data.keyword.cloudaccesstrailshort}}  eventos  
{: #at_events}

Use o serviço {{site.data.keyword.cloudaccesstrailfull}} para controlar como os usuários e os aplicativos interagem com
o serviço {{site.data.keyword.cloudcerts_long}} no {{site.data.keyword.Bluemix}}.
{:shortdesc}

O serviço {{site.data.keyword.cloudaccesstrailfull_notm}} registra as atividades iniciadas pelo usuário que mudam
o estado de um serviço no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, consulte  [ {{site.data.keyword.cloudaccesstrailfull_notm}} ](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Por
exemplo, ao importar um certificado, um evento do {{site.data.keyword.cloudaccesstrailshort}} é gerado.

A tabela a seguir lista os métodos de API que geram um evento quando eles são chamados:

<table>
  <caption>Ações que geram eventos</caption>
  <tr>
    <th>Ações</th>
	  <th>Descrição</th>
  </tr>
  <tr>
    <td>cloudcerts.instance.create</td>
	  <td>Provisão de uma instância do  {{site.data.keyword.cloudcerts_short}} .</td>
  </tr>
  <tr>
    <td>cloudcerts.instance.delete</td>
	  <td>Exclua uma instância do  {{site.data.keyword.cloudcerts_short}} .</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>Importe um certificado que seja emitido por uma autoridade de certificado de empresa terceirizada.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>Faça download de um certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>Listar certificados.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>Listar metadados de certificados. Mostrar detalhes de um certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>Procurar os certificados.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>Metadados de certificados de procura.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>Excluir um certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>Atualizar um certificado, por exemplo, mudar a sua descrição.</td>
  </tr>
</table>


 	
 


## Onde procurar os eventos
{: #ui}

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} estão disponíveis no
{{site.data.keyword.cloudaccesstrailshort}} **domínio de contas** disponível na região do
{{site.data.keyword.Bluemix_notm}} na qual eles são gerados.

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} são encaminhados automaticamente para o serviço
{{site.data.keyword.cloudaccesstrailshort}} na mesma região em que o serviço {{site.data.keyword.cloudcerts_short}}
é fornecido.


## Informações Adicionais
{: #info}

O campo *requestData_str* inclui o nome legível do certificado.



