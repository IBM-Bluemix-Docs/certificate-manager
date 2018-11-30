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

# Configuración de notificaciones para la caducidad de certificados
{: #configuring-notifications-for-expiring-certificates}

Habitualmente los certificados únicamente son válidos durante un intervalo de tiempo. Cuando un certificado que se utiliza caduca, podría significar un tiempo de inactividad para su app. Para evitar esta inactividad, puede configurar {{site.data.keyword.cloudcerts_full}} para que envíe notificaciones con relación a certificados que están a punto de caducar de forma que los pueda renovar a tiempo.
{: shortdesc}

**¿Cuándo se me avisa?**  
Dependiendo de la fecha de caducidad del certificado que descargó en {{site.data.keyword.cloudcerts_full_notm}}, es notificado 90, 60, 30, 10 y 1 días antes de que caduque el certificado. Además, recibirá notificaciones diarias sobre los certificados caducados. Las notificaciones diarias comienzan el primer días después de que caduque el certificado.

Debe renovar el certificado, subirlo a {{site.data.keyword.cloudcerts_full_notm}} y suprimir el certificado caducado para evitar que se le continúen enviando las notificaciones.

**¿Cuáles son las opciones de configuración de las notificaciones?**  
Se pueden enviar notificaciones a Slack utilizando un webhook de Slack o utilizando cualquier URL de devolución de llamada que desee.

## Configuración de un webhook de Slack
{: #setup-callback}

Para configurar un webhook Slack, siga los pasos siguientes:

1. Regístrese en [Slack](https://slack.com/) y configure su espacio de trabajo.
2. Cree un canal de Slack en el que publicar sus notificaciones.
3. [Configure un webhook](https://api.slack.com/incoming-webhooks) para el canal de Slack.

## Configuración de un URL de devolución de llamada
{: #callback}

Es posible que desee utilizar un URL de devolución de llamada para publicar notificaciones en las herramientas que utiliza diariamente para desencadenar el proceso de renovación para su equipo. Por ejemplo, puede enviar notificaciones para informar a PagerDuty, abrir de forma automática un problema en GitHub o para desencadenar scripts de renovación.  
{: shortdesc}

**Importante:** Su punto final del URL de devolución de llamada debe satisfacer los siguientes requisitos para poder utilizarlo con {{site.data.keyword.cloudcerts_short}}:

* El punto final debe utilizar el protocolo HTTPS.
* El punto no debe requerir cabeceras HTTP. Este requisito incluye cabeceras de automatización.
* El punto final debe devolver un código de estado `200 OK`, lo que indica que la notificación se ha entrado correctamente.

### Formato de notificación
{: #notification_format}

La notificación que se envía al URL de devolución de llamada es un documento JSON que tiene el siguiente formato:

```
{ "data":"<JWT FORMAT STRING>" }
```
{: screen}

Tras descodificar y verificar la carga útil, el contenido es una serie JSON.

```
{
    "instance_crn": "<INSTANCE_CRN>",
    "certificate_manager_url":"<INSTANCE_DASHBOARD_URL>",
    "expiry_date": <EXPIRY_DAY_TIMESTAMP>,
    "event_type": "<EVENT_TYPE>",
    "certificates":[
          {
             "cert_crn":"<CERTIFICATE_CRN>",
             "name":"<CERTIFICATE_NAME>",
             "domains":"<CERTIFICATE_DOMAIN>"
          },
          ...
}
```
{: screen}

## Configuración de un canal de notificaciones
{: #adding-channel}

Después de crear un webhook de Slack o un URL de devolución de llamada, debe añadirlo a {{site.data.keyword.cloudcerts_short}} para empezar a recibir notificaciones sobre la caducidad de los certificados. {{site.data.keyword.cloudcerts_short}} cifra el punto final y lo almacena de forma segura.
{: shortdesc}

Para añadir un canal de notificaciones, siga los pasos siguientes:

1. En la navegación en la página de detalles del servicio, pulse **Valores**.
2. Abra el separador **Notificaciones**.
3. Pulse **Añadir canal de notificaciones**.
4. Elija el tipo de canal de notificaciones que desee utilizar.
5. Especifique el webhook o URL de devolución de llamada al que enviar las notificaciones.
6. Pulse **Guardar**. Se visualizará un resumen de su configuración.

   **Salida de ejemplo**

   <table>
   <caption>Tabla 1. Información sobre el canal de notificaciones </caption>
   <thead>
    <th> Componente </th>
    <th> Descripción </th>
   </thead>
   <tbody>
   <tr>
    <td>Tipo</td>
    <td>Tipo de canal de notificaciones: <i>Slack</i> o <i>URL de devolución de llamada</i></td>
   </tr>
   <tr>
    <td>Punto final</td>
    <td>Punto final del canal al que se enviarán las notificaciones.</td>
   </tr>
   <tr>
    <td>Conmutador de habilitación</td>
    <td>Estado del canal de notificaciones. Si se establece en inhabilitado, no se envían notificaciones.</td>
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
7. (Opcional) Repita estos pasos para añadir más canales de notificaciones.

## Cómo probar un canal de notificaciones
{: #testing-channel}

Pruebe un canal de notificaciones para asegurarse de que el canal de notificaciones está correctamente configurado.
{: shortdesc}

Antes de empezar, [configure un canal de notificaciones](#adding-channel).

Para probar un canal de notificaciones, siga los pasos siguientes:

1. En la navegación en la página de detalles del servicio, pulse **Valores**.
2. Encuentre su canal de notificaciones y pulse **Probar conexión**.
3. Asegúrese de que ha recibido una notificación en el canal que ha configurado.

## Actualización de un canal de notificaciones
{: updating-channel}

Puede actualizar su configuración del canal de notificaciones, inhabilitar o habilitar notificaciones o suprimir canales de notificaciones desde {{site.data.keyword.cloudcerts_short}}.
{: shortdesc}

Antes de empezar, [configure un canal de notificaciones](#adding-channel).

Para actualizar su canal de notificaciones, siga los pasos siguientes:

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

## Ejemplos
{: #examples}

* [Cómo utilizar el gestor de certificados para evitar interrupciones utilizando URL de devolución de llamada - Parte 1 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/08/use-certificate-manager-avoid-outages-using-callback-urls/)  
   Información sobre cómo crear problemas de GitHub para notificaciones de caducidad de certificados.
* [Cómo utilizar el gestor de certificados para evitar interrupciones utilizando URL de devolución de llamada - Parte 2 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/10/how-to-use-certificate-manager-to-avoid-outages-using-callback-urls-part-2/)  
   Información sobre cómo crear problemas de incidencias de PagerDuty para notificaciones de caducidad de certificados.
