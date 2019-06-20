---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-04"

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

# Solicitud de certificados
{: #ordering-certificates}

Puede utilizar {{site.data.keyword.cloudcerts_long}} para solicitar certificados SSL/TLS para sus apps y servicios firmados por entidades emisoras de certificados externas soportadas. {{site.data.keyword.cloudcerts_short}} facilita la solicitud de certificados públicos, además de ofrecer seguridad adicional para sus claves privadas SSL/TLS. Después de que se emita el certificado, puede desplegarlo en servicios integrados y lo puede descargar para utilizarlo donde desee.  
{: shortdesc}

Cuando solicita un certificado, la clave privada para SSL/TLS se genera directamente en {{site.data.keyword.cloudcerts_short}} y se almacena en un lugar seguro. Todas las solicitudes y el acceso a los certificados emitidos se pueden gestionar mediante el [control de acceso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles) y se pueden auditar automáticamente mediante [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).  

{{site.data.keyword.cloudcerts_short}} implementa el protocolo Automatic Certificate Management Environment (ACME) v2 como cliente ACME. El protocolo ACME permite obtener automáticamente certificados fiables para el navegador sin intervención humana.

## Características de los certificados
Los certificados que se solicitan mediante {{site.data.keyword.cloudcerts_short}} tienen las siguientes características:

- Gratuito
- Periodo de validez: 90 días
- Certificado de un solo dominio, de varios dominios (SAN) o comodín
- Dominio validado: antes de que se le emita un certificado, la entidad emisora de certificados comprueba que posee el dominio para el que solicita un certificado.

Si necesita certificados de validación ampliada (EV) o validados por la organización (OV), los puede obtener en otro lugar e importarlos en {{site.data.keyword.cloudcerts_short}} para que gestione su ciclo de vida.

## Entidades emisoras de certificados soportadas
{: #supported-certificate-authorities}

Una entidad emisora de certificados (CA) es una entidad que emite certificados digitales. La CA actúa como un tercero fiable tanto para el solicitante del certificado como para el cliente que confía en el certificado.
{: shortdesc}

### Let's Encrypt
[Let’s Encrypt](https://letsencrypt.org) es una entidad de emisora basada en ACME, automatizada y gratuita que proporciona certificados validados por el dominio que son válidos durante 90 días. Es un servicio que proporciona el grupo Internet Security Research Group (ISRG).

## Configuración de la solicitud de un certificado
{: #setup}

Para que se le pueda emitir un certificado, {{site.data.keyword.cloudcerts_short}} debe verificar que controla todos los dominios que ha puesto en la lista de su solicitud. {{site.data.keyword.cloudcerts_short}} utiliza la validación DNS para verificar este control.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} envía un desafío en forma de un registro TXT del sistema de nombres de dominio (DNS) para que lo añada en su servicio DNS. Para cada dominio que solicite en su certificado, recibirá un registro TXT de DNS separado. Después de añadir el registro TXT de DNS, {{site.data.keyword.cloudcerts_short}} y el servicio Let’s Encrypt comprueban si está en el servicio DNS. Si cumplimenta el desafío correctamente, se le emitirá un certificado Let’s Encrypt que estará disponible en su instancia de {{site.data.keyword.cloudcerts_short}}.

{{site.data.keyword.cloudcerts_short}} envía un registro TXT a un URL de devolución de llamada que especifique en los valores de Notificaciones, lo que le permite automatizar fácilmente el proceso de validación del dominio.

Para empezar a solicitar certificados, registre su URL de devolución de llamada como un canal de notificación en {{site.data.keyword.cloudcerts_short}}. Luego, actualice el código para que gestione los sucesos de notificación que incluyan el desafío de TXT. [Más información sobre cómo configurar un canal de notificación de URL de devolución de llamada](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

## Cómo responder a un desafío
{: #responding-to-challenge}

El canal de notificación recibe una notificación con la siguiente estructura:

```javascript
{
"instance_crn: '"<INSTANCE_CRN>"
"certificate_manager_url": "certificate_manager_url",
    "event_type": "cert_domain_validation_required" | "cert_domain_validation_completed", // El primer suceso es para añadir el registro TXT de desafío necesario y el segundo es para borrar el mismo registro TXT una vez finalizado el desafío.
    "certificateCRN": "<CERTIFICATE_CRN>", // El CRN del certificado solicitado
    "userToken": "<USER_TOKEN>", /// La señal de IAM que contiene la identidad del usuario que ha solicitado el certificado
    "domain_validation_method": "dns-01", // Especifica el método de validación del dominio; actualmente solo está disponible DNS.
    "domain": "<ORDERED_DOMAIN>", // El dominio solicitado; se envía un desafío diferente por cada dominio del pedido (el primario y cada uno de los dominios alternativos).
    "challenge": {
        "txt_record_name": "<TXT_REC_NAME>", // El nombre del registro TXT; se suele utilizar junto con el dominio.
        "txt_record_val": "<TXT_REC_VALUE>" // El valor del registro TXT
    },
    "version": "<CHANNEL_VERSION>" // Versión del canal de notificación que da soporte a las  notificaciones relacionadas con el pedido. 4 y por encima
}
```
{: screen}

Una vez se envía el desafío TXT de DNS al URL de devolución de llamada, recibirá la respuesta al desafío en 10 minutos. {{site.data.keyword.cloudcerts_short}} comprueba si el desafío se ha completado. Cuando {{site.data.keyword.cloudcerts_short}} verifica que ha respondido al desafío, se le envía una segunda notificación para informarle de que puede eliminar el registro TXT.

[Revise la página de preguntas frecuentes](/docs/services/certificate-manager?topic=certificate-manager-faq#faq) para ver las preguntas que se suelen plantear sobre la solicitud de certificados.
{: tip}

## Solicitud de certificados
{: #ordering-certificate}

1. Vaya al separador Gestionar de {{site.data.keyword.cloudcerts_short}}.
2. Pulse **Solicitar certificado** y especifique los siguientes detalles:

    1. Especifique un nombre de certificado.
    2. Seleccione una entidad emisora de certificados.
    3. Especifique el dominio primario y los dominios alternativos.
    4. Seleccione el algoritmo y el algoritmo de clave adecuados.
    5. Pulse **Solicitar**.

La solicitud se coloca en el estado **Pendiente**. Cuando responda al desafío de validación del dominio y {{site.data.keyword.cloudcerts_short}} verifique que posee los dominios solicitados, se le emitirá un certificado y su estado parará a ser **Válido**. Se le notificará cuando el certificado esté listo o cuando se produzca un problema, en el canal Slack o en el URL de devolución de llamada.

## Renovación de certificados
{: #renew-certificate}

Si su certificado está a punto de caducar, puede solicitar su renovación mediante {{site.data.keyword.cloudcerts_short}}. Si se renueva su certificado, la versión anterior se conserva por si lo necesita. 

Las renovaciones funcionan de forma similar a la solicitud de certificados. Cuando solicita la renovación de un certificado, {{site.data.keyword.cloudcerts_short}} envía desafíos TXT de DNS al URL de devolución de llamada para que pueda probar que posee los dominios cuyo certificado está renovando.

Para renovar un certificado, siga los pasos siguientes:
  1. Pulse el menú de la fila del certificado que desea renovar.
  2. Pulse **Renovar certificado**.
  3. Opcional: puede optar por volver a obtener una clave para el certificado marcando el recuadro de selección **Volver a obtener clave de certificado**. Esto renovará el certificado con un nuevo par de claves.
  
  Si solicita una nueva clave para un certificado, asegúrese de desplegar los nuevos certificados y claves en todo lugar en el que se utilicen.
  {: note}
    
  4. Pulse **Renovar**
  
  Solo puede renovar los certificados que haya solicitado mediante {{site.data.keyword.cloudcerts_short}}.
  {: note}

La renovación se coloca en el estado **Renovación pendiente**. Cuando responda al desafío de validación del dominio y {{site.data.keyword.cloudcerts_short}} verifique que posee los dominios solicitados, obtendrá un nuevo certificado y su estado parará a ser **Válido**. Se le notificará cuando el certificado renovado esté listo o cuando se produzca un problema, en el canal Slack o en el URL de devolución de llamada.
