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

# Sucesos de Activity Tracker  
{: #at_events}

El servicio {{site.data.keyword.at_full}} permite rastrear la forma en la que usuarios y aplicaciones interactúan con el servicio {{site.data.keyword.cloudcerts_long}} en {{site.data.keyword.cloud_notm}}.
{:shortdesc}

El servicio {{site.data.keyword.at_short}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.cloud_notm}}. Por ejemplo, cuando se importa un certificado, se genera un suceso. Para obtener más información, consulte la [documentación de {{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

En la tabla siguiente se muestran los métodos de API que generan un suceso cuando se le llama.

<table>
  <caption>Tabla 1. Acciones que generan sucesos</caption>
  <tr>
    <th>Acción</th>
	  <th>Descripción</th>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.import`</td>
	  <td>Importar un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.order`</td>
	  <td>Solicitar un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.reimport`</td>
	  <td>Volver a importar un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.read`</td>
	  <td>Obtener los metadatos de un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.download`</td>
	  <td>Descargar un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.read`</td>
	  <td>Listar certificados.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.read`</td>
	  <td>Listar metadatos de certificados. Muestra los detalles de un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates.search`</td>
	  <td>Buscar certificados.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificates-metadata.search`</td>
	  <td>Buscar metadatos de certificados.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate.delete`</td>
	  <td>Suprimir un certificado.</td>
  </tr>
  <tr>
    <td>`cloudcerts.certificate-metadata.update`</td>
	  <td>Actualizar metadatos de un certificado, por ejemplo, cambiar su descripción.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels.list`</td>
	  <td>Listar canales de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.create`</td>
	  <td>Crear un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.state`</td>
	  <td>Habilitar o inhabilitar un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.update`</td>
	  <td>Actualizar el punto final de un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.delete`</td>
	  <td>Suprimir un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channel.test`</td>
	  <td>Comprobar un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification.sent`</td>
	  <td>Se ha enviado una notificación al punto final de un canal de notificaciones.</td>
  </tr>
  <tr>
    <td>`cloudcerts.notification-channels-publickey.read`</td>
	  <td>Se ha solicitado la clave pública.</td>
  </tr>
</table>

## Dónde buscar los sucesos
{: #at_ui}

Suministre una instancia de {{site.data.keyword.at_short}} en la misma ubicación que su instancia de {{site.data.keyword.cloudcerts_short}}.

Los sucesos se reenvían automáticamente a la instancia de servicio de {{site.data.keyword.at_short}} en la misma ubicación en la que se suministra el servicio {{site.data.keyword.cloudcerts_short}}.

## Información adicional
{: #info}

* El campo *requestData_str* incluye el nombre en lenguaje natural del certificado.

## Disponibilidad
{: #at-availability}

* El soporte de {{site.data.keyword.at_short}} está disponible actualmente en las ubicaciones **Dallas** y **Frankfurt**.
* Para las demás ubicaciones, se puede suministrar una instancia del servicio Activity Tracker en desuso hasta {{site.data.keyword.at_short}}.
