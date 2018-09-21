
---
copyright:
  years: 2018
lastupdated: "2018-09-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}

# Notas del release
{: #release-notes}

Están disponibles las siguientes características y cambios del servicio {{site.data.keyword.cloudcerts_long}}.

## 12 de septiembre de 2018
{: 12September2018}

- **El nombre de certificado es obligatorio**  
  Al importar un certificado, es obligatorio proporcionar un valor para el nombre del vertificado.  
  Además, las API v2 **Importar un certificado** y **Actualizar los metadatos de un certificado** han quedado en desuso y se eliminarán el 1 de noviembre de 2018. Debe actualizar a la v3 de las API. Para obtener más información, consulte [Documentación de la API](https://console.bluemix.net/apidocs/certificate-manager).

- **Notificaciones de Slack agrupadas**  
  Las notificaciones en Slack están agrupadas por fecha de caducidad.

## 2 de septiembre de 2018
{: 2September2018}

- **Disponibilidad general de {{site.data.keyword.cloudcerts_long_notm}}**  
  El servicio {{site.data.keyword.cloudcerts_short}} está disponible a nivel general (GA) en {{site.data.keyword.cloud_notm}}.

## 22 de agosto de 2018
{: 22August2018}

- **Entra en funcionamiento en el Reino Unido**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta está disponible en la región de Reino Unido (RU sur).

## 15 de agosto de 2018
{: 15August2018}

- **Eliminación de API v1 obsoletas**  
  Las API de la versión 1 ya no están disponibles. Si todavía no ha actualizado su API, debe hacerlo lo antes posible. [Consulte la documentación de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/apidocs/).

- **Los roles de plataforma se sustituyen por los roles de servicio**  
  Puede controlar el acceso a las instancias de {{site.data.keyword.cloudcerts_short}} utilizando roles de servicio. [Más información sobre la gestión de accesos](access-management.html).

## 12 de julio de 2018
{: 12July2018}

- **Notificaciones de devolución de llamada**  
  Se ha añadido soporte a la devolución de llamada para las notificaciones. Puede elegir enviar las notificaciones a Slack o utilizar cualquier URL de devolución de llamada para enviar notificaciones. Por ejemplo, puede enviar notificaciones a PagerDuty, abrir de forma automática un problema en GitHub o para desencadenar scripts de renovación. [Más información sobre las notificaciones](notifications-dashboard.html).

## 12 de junio de 2018
{: 12June2018}

- **Notificaciones de Slack**  
  Se han añadido notificaciones de Slack para que nunca se pierda ningún certificado a punto de caducar. [Más información sobre las notificaciones](notifications-dashboard.html).

## 19 de diciembre de 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} está disponible como servicio beta**  
  El servicio {{site.data.keyword.cloudcerts_short}} está disponible somo servicio beta en {{site.data.keyword.cloud_notm}}.
