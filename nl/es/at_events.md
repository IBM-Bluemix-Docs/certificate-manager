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


# Sucesos de {{site.data.keyword.cloudaccesstrailshort}}  
{: #at_events}

El servicio {{site.data.keyword.cloudaccesstrailfull}} permite rastrear la forma en la que usuarios y aplicaciones interactúan con el servicio {{site.data.keyword.cloudcerts_long}} en {{site.data.keyword.Bluemix}}. 
{:shortdesc}

El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} graba las actividades iniciadas por los usuarios que cambian el estado de un servicio en {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla). Por ejemplo, cuando se importa un certificado, se genera un suceso de {{site.data.keyword.cloudaccesstrailshort}}.

En la tabla siguiente se muestran los métodos de API que generan un suceso cuando se le llama:

<table>
  <caption>Acciones que generan sucesos</caption>
  <tr>
    <th>Acción</th>
	  <th>Descripción</th>
  </tr>
  <tr>
    <td>cloudcerts.instance.create</td>
	  <td>Aprovisionar a una instancia de {{site.data.keyword.cloudcerts_short}}.</td>
  </tr>
  <tr>
    <td>cloudcerts.instance.delete</td>
	  <td>Suprimir una instancia de {{site.data.keyword.cloudcerts_short}}.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.import</td>
	  <td>Importar un certificado que ha emitido una tercera autoridad de certificación.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.read</td>
	  <td>Descargar un certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.list</td>
	  <td>Listar certificados.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.list</td>
	  <td>Listar metadatos de certificados. Muestra los detalles de un certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates.search</td>
	  <td>Buscar certificados.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificates-metadata.search</td>
	  <td>Buscar metadatos de certificados.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.delete</td>
	  <td>Suprimir un certificado.</td>
  </tr>
  <tr>
    <td>cloudcerts.certificate.update</td>
	  <td>Actualizar un certificado, por ejemplo, al cambiar su descripción.</td>
  </tr>
</table>


 	
 


## Dónde buscar los sucesos
{: #ui}

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} están disponibles en el **dominio de cuenta** de {{site.data.keyword.cloudaccesstrailshort}} que está disponible en la región de {{site.data.keyword.Bluemix_notm}} en la que se generan los sucesos.

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} se reenvían de forma automática al servicio {{site.data.keyword.cloudaccesstrailshort}} en la misma región que la utilizada para aprovisionar el servicio {{site.data.keyword.cloudcerts_short}}.


## Información adicional
{: #info}

El campo *requestData_str* incluye el nombre en lenguaje natural del certificado.



