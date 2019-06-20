---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-10"

keywords: certificates, SSL,

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

# Notas del release
{: #release-notes}

Están disponibles las siguientes características y cambios del servicio {{site.data.keyword.cloudcerts_long}}.


## 10 de junio de 2019
{: 10June2019}

- **Renovar certificados de Let's Encrypt solicitados**  
  Ahora puede renovar certificados de Let's Encrypt que ha solicitado mediante {{site.data.keyword.cloudcerts_short}}. [Más información sobre la solicitud de certificados](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).


## 6 de mayo de 2019
{: 6May2019}

- **Solicitar certificados de Let's Encrypt**  
  Ahora puede solicitar certificados de Let's Encrypt. [Más información sobre la solicitud de certificados](/docs/services/certificate-manager?topic=certificate-manager-order-certificates).

## 18 de febrero de 2019
{: 18February2019}

- **Entrada en funcionamiento en Tokio**  
  {{site.data.keyword.cloudcerts_long_notm}} está disponible en la ubicación Tokio.

## 13 de enero de 2019
{: 13January2019}
- **Carga útil de devolución de llamada versión 3**  
  [Consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 6 de enero de 2019
{: 6January2019}
- **API en desuso**  
  Las API **Listar certificados** y **Buscar repositorio de certificados** v2 han quedado en desuso y se eliminarán en una fecha futura. Debe actualizar a la v3 de las API. Para obtener más información, [consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 9 de diciembre de 2018
{: 9December2018}
- **Formatos de certificado adicionales**    
{{site.data.keyword.cloudcerts_short}} da soporte a los siguientes formatos de certificado: RSA, DSA, ECDSA, ECDH.

## 5 de diciembre de 2018
{: 5December2018}
- **Notificación de reimportación**    
Al reimportar un certificado renovado en lugar de uno que caduca, puede recibir una notificación de que se ha reimportado el certificado. Esto le recordará, y también al equipo, que despliegue el certificado renovado en los puntos de terminación SSL/TLS. Esta notificación solo está disponible para los nuevos canales de notificación que se creen.

- **{{site.data.keyword.cloudcerts_short}} está disponible en la ubicación Frankfurt.**     
El servicio cumple con los requisitos de la UE.

## 2 de diciembre de 2018
{: 2December2018}
- **Carga útil de devolución de llamada y Slack versión 2**  
  [Consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 14 de noviembre de 2018
{: 14November2018}

- **Reimportar**  
  Puede actualizar un certificado volviendo a importar una nueva versión que tenga el mismo dominio que el certificado existente, pero una nueva fecha de caducidad. Cuando se vuelve a importar un certificado, la versión existente del certificado se conserva como copia de seguridad; consulte el apartado sobre [Reimportación de un certificado](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).

- **1000 certificados por instancia**  
  Puede importar un máximo de 1000 certificados por instancia.

## 28 de octubre de 2018
{: 28October2018}

- **Cabecera de anuncios**  
  Los anuncios de servicios, como API que han quedado en desuso y otras noticias, se muestran en el separador **Gestionar**.

## 12 de septiembre de 2018
{: 12September2018}

- **El nombre de certificado es obligatorio**  
  Al importar un certificado, es obligatorio proporcionar un valor para el nombre del certificado.  

- **API en desuso**  
  Las API de la v2 **Importar un certificado** y **Actualizar los metadatos de un certificado** han quedado en desuso y se eliminarán el 1 de diciembre de 2018. Debe actualizar a la v3 de las API. Para obtener más información, [consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/certificate-manager).

- **Notificaciones de Slack agrupadas**  
  Las notificaciones en Slack están agrupadas por fecha de caducidad.

## 2 de septiembre de 2018
{: 2September2018}

- **Disponibilidad general de {{site.data.keyword.cloudcerts_long_notm}}**  
  El servicio {{site.data.keyword.cloudcerts_short}} está disponible a nivel general (GA) en {{site.data.keyword.cloud_notm}}.

## 22 de agosto de 2018
{: 22August2018}

- **Entrada en funcionamiento en Londres**  
  {{site.data.keyword.cloudcerts_long_notm}} Beta está disponible en la ubicación Londres.

## 15 de agosto de 2018
{: 15August2018}

- **Eliminación de API v1 obsoletas**  
  Las API de la versión 1 ya no están disponibles. Si todavía no ha actualizado su API, debe hacerlo lo antes posible. Para obtener más información, [consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/).

- **Los roles de plataforma se sustituyen por los roles de servicio**  
  Puede controlar el acceso a las instancias de {{site.data.keyword.cloudcerts_short}} utilizando roles de servicio. [Más información sobre la gestión de accesos](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).

## 12 de julio de 2018
{: 12July2018}

- **Notificaciones de devolución de llamada**  
  Se ha añadido soporte a la devolución de llamada para las notificaciones. Puede elegir enviar las notificaciones a Slack o utilizar cualquier URL de devolución de llamada para enviar notificaciones. Por ejemplo, puede enviar notificaciones a PagerDuty, abrir de forma automática un problema en GitHub o para desencadenar scripts de renovación. [Más información sobre las notificaciones](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#callback).

## 12 de junio de 2018
{: 12June2018}

- **Notificaciones de Slack**  
  Se han añadido notificaciones de Slack para que nunca se pierda ningún certificado a punto de caducar. [Más información sobre las notificaciones](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#setup-callback).

## 8 de enero de 2018
{: 8January2018}

- **API en desuso**  
  Las API de la versión 1 han quedado en desuso y se eliminarán el 8 de septiembre de 2018. Debe actualizar a la v2 de las API. Para obtener más información, [consulte la documentación de las API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/certificate-manager).

## 19 de diciembre de 2017
{: 19December2017}

- **{{site.data.keyword.cloudcerts_long_notm}} está disponible como servicio beta**  
  El servicio {{site.data.keyword.cloudcerts_short}} está disponible somo servicio beta en {{site.data.keyword.cloud_notm}}.
