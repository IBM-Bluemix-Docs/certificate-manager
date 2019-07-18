---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

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

# Configuración de notificaciones
{: #configuring-notifications}

{{site.data.keyword.cloudcerts_full}} le puede enviar notificaciones sobre sucesos relacionados con el ciclo de vida de los certificados. Esto incluye recordatorios para renovar certificados antes de que caduquen y para desplegar certificados cuando estén listos. Para obtener notificaciones de {{site.data.keyword.cloudcerts_short}}, puede configurar un canal de notificación. Puede especificar un webhook de Slack, un URL de devolución de llamada o cualquier combinación de los dos.
{: shortdesc}

La característica de notificaciones también se utiliza cuando [solicita certificados](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificates) de {{site.data.keyword.cloudcerts_short}}. Para probar que posee el dominio para el que está solicitando un certificado, {{site.data.keyword.cloudcerts_short}} envía un desafío como notificación a su URL de devolución de llamada. El desafío es un registro de texto, que debe colocar en el servicio del sistema de nombres de dominio (DNS) en el que está registrado el dominio. Cuando el registro de texto está en vigor, se considera que se ha cumplido el desafío. Puesto que el desafío se envía como una notificación al URL de devolución de llamada, puede automatizar el proceso de validación del dominio ejecutando código como respuesta al suceso de notificación.

## Notificaciones para supervisar la caducidad de los certificados
{: #notifications-monitoring-certificate-expiration}

Normalmente los certificados son válidos durante un intervalo de tiempo. Cuando un certificado que se utiliza caduca, podría significar un tiempo de inactividad para su app. Para evitar esta inactividad, puede configurar {{site.data.keyword.cloudcerts_short}} para que le envíe notificaciones sobre los certificados que están a punto de caducar, de forma que recibirá un recordatorio para renovarlos a tiempo.

También recibirá una alerta cuando se vuelva a importar una versión renovada del certificado en {{site.data.keyword.cloudcerts_short}} en lugar del que va a caducar. Esto sirve para recordarle que lo despliegue en los puntos de terminación de SSL/TLS. Esta notificación sobre los certificados reimportados se envía solo a los [canales de la versión 2](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


**¿Cuándo se me avisa?**  
Dependiendo de la fecha de caducidad del certificado que descargó en {{site.data.keyword.cloudcerts_short}}, es notificado 90, 60, 30, 10 y 1 días antes de que caduque el certificado. Además, recibirá notificaciones diarias sobre los certificados caducados. Las notificaciones diarias comienzan el primer días después de que caduque el certificado.

Debe renovar el certificado y reimportarlo en lugar del antiguo para que {{site.data.keyword.cloudcerts_short}} pare de enviar notificaciones. Al reimportar el certificado, recibe una notificación de que se ha reimportado el certificado, para recordarle que lo vuelva a desplegar.

**¿Cuáles son las opciones de configuración de las notificaciones?**  
Se pueden enviar notificaciones a Slack utilizando un Webhook de Slack o utilizando el URL de devolución de llamada que desee.

## Notificaciones relacionadas con la solicitud de certificados
{: #notifications-ordering-certificates}

{{site.data.keyword.cloudcerts_short}} le notifica cuando se le emite un certificado que ha solicitado de {{site.data.keyword.cloudcerts_short}} o cuando se renueva correctamente. También se le notifica si la solicitud o la renovación fallan.
{: shortdesc}

La configuración de un canal de notificación de URL de devolución de llamada y la capacidad para gestionar los sucesos relacionados con la validación del dominio son requisitos previos para poder solicitar y renovar certificados. Cuando solicita un certificado, {{site.data.keyword.cloudcerts_short}} envía un registro txt de desafío al URL de devolución de llamada que utiliza para probar que posee el dominio para el que solicita el certificado. También se envía un registro txt de desafío cuando solicita la renovación de un certificado. 


## Configuración de un webhook de Slack
{: #setup-callback}

Para configurar un webhook de Slack, siga los pasos siguientes:

1. Regístrese en [Slack](https://slack.com/) y configure su espacio de trabajo.
2. Cree un canal de Slack en el que publicar sus notificaciones.
3. [Configure un Webhook](https://api.slack.com/incoming-webhooks) para el canal de Slack.

## Configuración de un URL de devolución de llamada
{: #callback}

Para desencadenar el proceso de renovación para su equipo, puede utilizar un URL de devolución de llamada para publicar notificaciones en las herramientas que utilice. Por ejemplo, puede enviar notificaciones para informar a PagerDuty, abrir de forma automática un problema en GitHub o para desencadenar scripts de renovación. También puede activar automáticamente el despliegue de certificados como respuesta a notificaciones cuando se vuelven a importar o se emiten correctamente certificados.
{: shortdesc}

Un URL de devolución de llamada es un requisito previo para solicitar certificados.
{: note}

**Importante:** su punto final del URL de devolución de llamada debe satisfacer los siguientes requisitos para poder utilizarlo con {{site.data.keyword.cloudcerts_short}}:
* El punto final debe utilizar el protocolo HTTPS.
* El punto no debe requerir cabeceras HTTP. Este requisito incluye cabeceras de automatización.
* El punto final debe devolver un código de estado `200 OK`, lo que indica que la notificación se ha entrado correctamente.

### Formato de notificación
{: #notification_format}

La notificación que se envía al URL de devolución de llamada es un documento JSON firmado con su clave asimétrica de instancia en el siguiente formato.

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Tras descodificar y verificar la carga útil, el contenido es una serie JSON [según la versión del canal](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).


## Configuración de un canal de notificación
{: #adding-channel}

Después de crear un webhook de Slack o un URL de devolución de llamada, debe añadirlo a {{site.data.keyword.cloudcerts_short}} para empezar a recibir notificaciones sobre la caducidad de certificados, certificados reimportados, certificados emitidos y desafíos para la validación del dominio.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} cifrará los puntos finales que configure para almacenarlos de forma segura.
{: important}

Para añadir un canal de notificación, siga los pasos siguientes:

1. En la navegación en la página de detalles del servicio, pulse **Valores**.
2. Abra el separador **Notificaciones**.
3. Pulse **Añadir canal de notificación**.
4. Elija el tipo de canal de notificación que desee utilizar.
5. Especifique el webhook o el URL de devolución de llamada al que enviar las notificaciones.
6. Pulse **Guardar**. Se visualizará un resumen de su configuración.

   **Salida de ejemplo**

   <table>
   <caption>Tabla 1. Información sobre el canal de notificación </caption>
   <thead>
    <th> Componente </th>
    <th> Descripción </th>
   </thead>
   <tbody>
   <tr>
    <td>Tipo</td>
    <td>Tipo de canal de notificación: <i>Slack</i> o <i>URL de devolución de llamada</i></td>
   </tr>
   <tr>
    <td>Punto final</td>
    <td>Punto final del canal de notificación al que se enviarán las notificaciones.</td>
   </tr>
   <tr>
    <td>Conmutador de habilitación</td>
    <td>Estado del canal de notificación. Si se establece en inhabilitado, no se envían notificaciones.</td>
   </tr>
   <tr>
    <td>Botón Probar conexión</td>
    <td>Envía una notificación de prueba al canal que ha configurado. </td>
   </tr>
    <tr>
      <td>Menú de puntos</td>
      <td>Acciones disponibles que puede realizar en el canal: <i>editar</i> o <i>suprimir</i></td>
    </tr>
    </tbody>
    </table>

    Cuando guarda un webhook de Slack, {{site.data.keyword.cloudcerts_short}} envía de forma automática una notificación de confirmación al canal de Slack que haya configurado. Verifique que ha recibido esta notificación en su canal de Slack.
    {: tip}
7. (Opcional) Repita estos pasos para añadir más canales de notificación.

## Cómo probar un canal de notificación
{: #testing-channel}

Pruebe un canal de notificación para asegurarse de que el canal de notificación está correctamente configurado.
{: shortdesc}

Antes de empezar, [configure un canal de notificación](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Para probar un canal de notificación, siga los pasos siguientes:

1. En la navegación en la página de detalles del servicio, pulse **Valores**.
2. Encuentre su canal de notificación y pulse **Probar conexión**.
3. Asegúrese de que ha recibido una notificación en el canal que ha configurado.

## Actualización de un canal de notificación
{: #updating-channel}

Puede actualizar su configuración del canal de notificación, inhabilitar o habilitar notificaciones o suprimir canales de notificación desde {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Antes de empezar, [configure un canal de notificación](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#adding-channel).

Para actualizar su canal de notificación, siga los pasos siguientes:

1. En la navegación en la página de detalles del servicio, pulse **Valores**.
2. Seleccione el separador **Notificaciones**.
3. Elija entre las siguientes opciones:
   * Para habilitar o inhabilitar las notificaciones para un canal, establezca el conmutador en **Inhabilitar** o **Habilitar**.
   * Para actualizar los valores para un canal, seleccione **Editar** desde el menú de acciones.
   * Para suprimir un canal de notificación, seleccione **Suprimir** en el menú de acciones.

## Verificación de la carga útil HTTP para un URL de devolución de llamada
{: #verify-callback}

Cada carga útil HTTP que se envía desde {{site.data.keyword.cloudcerts_short}} al URL de devolución de llamada se firma de forma automática de acuerdo al estándar JWT utilizando un par de claves asimétricas.  
{: shortdesc}

Para cada instancia de {{site.data.keyword.cloudcerts_short}}, se genera una clave pública y privada que no se comparten con otras instancias de {{site.data.keyword.cloudcerts_short}}. La clave privada se utiliza para firmar la carga útil HTTP. La clave pública sirve para verificar que la carga útil la ha generado {{site.data.keyword.cloudcerts_short}} y que no ha sido modificada por parte de un tercero.

Para descargar la clave pública, lleve a cabo los pasos siguientes:

1. Desde la navegación en la página de detalles del servicio, pulse **Valores**.
2. Abra el separador **Notificaciones**.
3. Pulse el botón **Descargar clave**. La clave se descarga como un archivo PEM.

## Versiones de canal
{: #channel-versions}

A medida que Certificate Manager evoluciona, es posible que se modifique el formato de la estructura de carga útil de las notificaciones de vez en cuando. Para garantizar la compatibilidad con versiones anteriores, no se modificará la carga útil que se envía a los canales existentes.   

Si tiene canales de notificación existentes (Slack o URL de devolución de llamada), para empezar a recibir la nueva versión de la carga útil:

1. Para el URL de devolución de llamada, asegúrese de que su implementación pueda aceptar la nueva carga útil.
2. Cree un nuevo canal de notificación (los canales nuevos siempre se crean con la última versión de canal).
3. Compruebe que el nuevo canal funciona correctamente.
4. Suprima el canal antiguo.

Para ver las versiones de canales, consulte la [documentación de la API](https://cloud.ibm.com/apidocs/certificate-manager#notification-channel-versions).

## Ejemplos
{: #examples}

* [Cómo utilizar el gestor de certificados para evitar interrupciones utilizando URL de devolución de llamada - Parte 1 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/use-certificate-manager-avoid-outages-using-callback-urls)  
   Información sobre cómo crear problemas de GitHub para notificaciones de caducidad de certificados.
* [Cómo utilizar el gestor de certificados para evitar interrupciones utilizando URL de devolución de llamada - Parte 2 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2)  
   Información sobre cómo crear incidencias de PagerDuty para notificaciones de caducidad de certificados.
* [Cómo validar un dominio mediante un URL de devolución de llamada y una acción de Cloud Function ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains)
