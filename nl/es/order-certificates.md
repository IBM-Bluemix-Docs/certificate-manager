---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-08"

keywords: certificates, SSL, dns,

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

# Solicitud de certificados
{: #ordering-certificates}

Puede utilizar {{site.data.keyword.cloudcerts_long}} para solicitar certificados SSL/TLS para sus apps y servicios firmados por entidades emisoras de certificados externas soportadas. {{site.data.keyword.cloudcerts_short}} facilita la solicitud de certificados públicos, además de ofrecer seguridad adicional para sus claves privadas SSL/TLS. Después de que se emita el certificado, puede desplegarlo en servicios integrados y lo puede descargar para utilizarlo donde desee.  
{: shortdesc}

Cuando solicita un certificado, la clave privada para SSL/TLS se genera directamente en {{site.data.keyword.cloudcerts_short}} y se almacena en un lugar seguro. Todas las solicitudes y el acceso a los certificados emitidos se pueden gestionar mediante el [control de acceso](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles) y se pueden auditar automáticamente mediante [{{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events).  

{{site.data.keyword.cloudcerts_short}} implementa el protocolo Automatic Certificate Management Environment (ACME) v2 como cliente ACME. El protocolo ACME permite obtener automáticamente certificados fiables para el navegador sin intervención humana.

## Características de los certificados
{: #certificate-characteristics}

Cuando solicita certificados mediante {{site.data.keyword.cloudcerts_short}}:

- Son gratuitos
- Son válidos durante 90 días
- Pueden ser de un solo dominio, de varios dominios (SAN) o un comodín
- Son de dominio validado

La validación de dominio incluye la verificación de que posee el dominio para el que solicita un certificado. Si necesita certificados de validación ampliada (EV) o validados por la organización (OV), los puede obtener en otro lugar e importarlos en {{site.data.keyword.cloudcerts_short}} para que gestione su ciclo de vida.


## Entidades emisoras de certificados soportadas
{: #supported-certificate-authorities}

Una entidad emisora de certificados (CA) es una entidad que emite certificados digitales. La CA actúa como un tercero fiable tanto para el solicitante del certificado como para el cliente que confía en el certificado.
{: shortdesc}

### Let's Encrypt
{: #lets-encrypt}
[Let’s Encrypt](https://letsencrypt.org) es una entidad de emisora basada en ACME, automatizada y gratuita que proporciona certificados validados por el dominio que son válidos durante 90 días. Es un servicio que proporciona el grupo Internet Security Research Group (ISRG).

## Configuración de la solicitud de un certificado
{: #setup}

Para que se le pueda emitir un certificado, {{site.data.keyword.cloudcerts_short}} debe verificar que controla todos los dominios que pone en la lista de su solicitud. Para ello, {{site.data.keyword.cloudcerts_short}} utiliza la validación de DNS.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} envía un desafío en forma de un registro TXT del sistema de nombres de dominio (DNS) para que lo añada en su servicio DNS. Para cada dominio que solicite en su certificado, recibirá un registro TXT de DNS separado. Después de añadir el registro TXT de DNS, {{site.data.keyword.cloudcerts_short}} y el servicio Let’s Encrypt comprueban si está en el servicio DNS. Si cumplimenta el desafío correctamente, se le emitirá un certificado Let’s Encrypt que estará disponible en su instancia de {{site.data.keyword.cloudcerts_short}}.

La forma en la que verifique la propiedad del dominio depende de si utiliza {{site.data.keyword.cis_full_notm}} u otro proveedor de DNS.


### {{site.data.keyword.cis_full_notm}}
{: #cis}

Si gestiona los dominios en {{site.data.keyword.cis_short}}, siga estos pasos para verificar la propiedad:

1. Navegue a **{{site.data.keyword.cloud_notm}} > Gestionar > Acceso (IAM) > Autorizaciones**.
2. Pulse **Crear** y asigne un servicio de origen y destino. Al servicio de origen se le otorga acceso al servicio de destino en función de los roles que se establecen en el paso siguiente.
  * Origen: {{site.data.keyword.cloudcerts_short}}
  * Destino: Internet Services
3. Especifique una instancia de servicio para el origen y el destino.
4. Asigne el rol **Lector** para permitir a {{site.data.keyword.cloudcerts_short}} ver la instancia de {{site.data.keyword.cis_short_notm}} y sus dominios. A continuación, pulse **Autorizar**.

  A efectos de prueba, puede asignar el rol de acceso al servicio **Gestor** en la interfaz de usuario para gestionar todos los dominios. En ese caso, no es necesario efectuar el paso 5. Para entornos de producción, se recomienda asignar el rol de acceso al servicio **Lector** y utilizar la API, tal como se muestra en el paso 5, para controlar dominios específicos.
  {: note}
   
5. Para controlar dominios específicos, asigne el rol **Gestor** mediante la API, de forma que {{site.data.keyword.cloudcerts_short}} pueda gestionar los registros de DNS para los dominios individuales que existan en la instancia de {{site.data.keyword.cis_short_notm}}. Quizá desee copiar el mandato a un archivo de texto para facilitar la edición de los parámetros necesarios.
   
  

  
  ```
  curl -X POST https://iam.cloud.ibm.com/acms/v1/policies \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <token>' \
  -d '{ "type": "authorization", "subjects": [ { "attributes": [ { "name": "serviceName", "value": "cloudcerts" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Certificate-Manager-GUID-based-instanceID>" } ] } ], "roles": [ { "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Manager" } ], "resources": [ { "attributes": [ { "name": "serviceName", "value": "internet-svcs" }, { "name": "accountId", "value": "<accountID>" }, { "name": "serviceInstance", "value": "<Cloud-Internet-Services-GUID-based-instanceID>" }, { "name": "domainId", "value": "<domainID>" }, { "name": "cfgType", "value": "reliability" }, { "name": "subScope", "value": "dnsRecord" } ] } ] }'
  ```
  {: codeblock} 
  

  <table>
    <tr>
      <th>Variable</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><code>token</code></td>
      <td>Una señal de IAM válida. Puede encontrar el valor mediante la CLI de {{site.data.keyword.cloud_notm}}: <code>ibmcloud iam oauth-tokens</code>.</td>
    </tr>
    <tr>
      <td><code>accountID</code></td>
      <td>El ID de la cuenta en la que existen las instancias de {{site.data.keyword.cloudcerts_short}} y {{site.data.keyword.cis_short_notm}}. Puede encontrar el valor navegando a <b>{{site.data.keyword.cloud_notm}} > Gestionar > Cuenta > Configuración de la cuenta</b> o utilizando la CLI de {{site.data.keyword.cloud_notm}}: <code>ibmcloud account show</code>.</td>
    </tr>
    <tr>
      <td><code>Certificate-Manager-GUID-based-instanceID</code></td>
      <td>El ID basado en GUID para la instancia de {{site.data.keyword.cloudcerts_short}}. Para encontrar el valor, utilice la CLI de {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>Cloud-Internet-Services-GUID-based-instanceID</code></td>
      <td>El ID basado en GUID para la instancia de {{site.data.keyword.cis_short_notm}}. Para encontrar el valor, utilice la CLI de {{site.data.keyword.cloud_notm}}: <code>ibmcloud resource service-instance "Instance name"</code>.</td>
    </tr>
    <tr>
      <td><code>domainID</code></td>
      <td>El ID del dominio tal como se encuentra en {{site.data.keyword.cis_short_notm}}. Para encontrar el valor, utilice la CLI de {{site.data.keyword.cloud_notm}} para ejecutar <code>ibmcloud cis domains</code>. Para gestionar varios dominios, modifique la matriz <code>resources</code>.</td>
    </tr>
  </table>

Ya está listo para [solicitar un certificado](/docs/services/certificate-manager?topic=certificate-manager-ordering-certificates#ordering-certificate).


### Otro proveedor de DNS
{: #other_provider}

Para verificar el control sobre un dominio cuando utiliza un proveedor de DNS, {{site.data.keyword.cloudcerts_short}} envía el registro TXT a un canal de notificaciones de URL de devolución de llamada que especifique, lo que le permite automatizar el proceso de validación del dominio.

Antes debe implementar una acción de IBM Cloud Function para la validación de dominio y, a continuación, proporcionar el punto final a un canal de notificaciones de URL de devolución de llamada. Para empezar, consulte [configuración de un canal de notificaciones de URL de devolución de llamada](/docs/services/certificate-manager?topic=certificate-manager-configuring-notifications#channel-versions).

Para obtener más información sobre la configuración de validación de dominio mediante un canal de notificaciones de URL de devolución de llamada, consulte [esta publicación de blog](https://www.ibm.com/cloud/blog/use-ibm-cloud-certificate-manager-to-obtain-lets-encrypt-tls-certificates-for-your-public-domains){: external}.
{: tip}


#### Cómo responder a un desafío
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

Para ver las preguntas más frecuentes sobre la solicitud de certificados, [revise la página de preguntas más frecuentes](/docs/services/certificate-manager?topic=certificate-manager-faq).
{: tip}

## Solicitud de certificados
{: #ordering-certificate}

Para solicitar un certificado, siga los pasos siguientes:

1. Vaya al separador Gestionar de {{site.data.keyword.cloudcerts_short}}.
2. Pulse **Solicitar certificado**. 
3. Seleccione el proveedor de DNS, {{site.data.keyword.cis_full_notm}} u otro proveedor de DNS.
4. Si ha seleccionado **{{site.data.keyword.cis_full_notm}}**, indique los detalles siguientes:
   1. Complete las instrucciones de configuración necesarias
   2. Especifique un nombre de certificado y, de forma opcional, una descripción
   3. Seleccione una entidad emisora de certificados
   4. Seleccione la instancia de {{site.data.keyword.cis_full_notm}} para la que ha asignado un rol de acceso al servicio
   5. Seleccione el tipo de certificado que necesite
   6. Seleccione el dominio
   7. Seleccione el algoritmo y el algoritmo de clave adecuados
   8. Pulse **Solicitar**
5. Si ha seleccionado **Otro proveedor de DNS**, indique los detalles siguientes:
   1. Complete las instrucciones de configuración necesarias
   2. Especifique un nombre de certificado y, de forma opcional, una descripción
   3. Seleccione una entidad emisora de certificados
   4. Especifique el dominio primario y los dominios alternativos
   5. Seleccione el algoritmo y el algoritmo de clave adecuados
   6. Pulse **Solicitar**

La solicitud se coloca en el estado **Pendiente**. Una vez que responda al desafío de validación del dominio y {{site.data.keyword.cloudcerts_short}} verifique que posee el dominio solicitado, se le emitirá un certificado y su estado parará a ser **Válido**. Se le notificará cuando el certificado esté listo o cuando se produzca un problema, en el canal Slack o en el canal de notificaciones de URL de devolución de llamada.

## Renovación de certificados
{: #renew-certificate}

Si su certificado está a punto de caducar, puede solicitar su renovación mediante {{site.data.keyword.cloudcerts_short}}. Si se renueva su certificado, la versión anterior se conserva por si lo necesita. 

Las renovaciones funcionan de forma similar a la solicitud de certificados. Cuando solicita la renovación de un certificado, {{site.data.keyword.cloudcerts_short}} envía desafíos TXT de DNS al URL de devolución de llamada para que pueda probar que posee los dominios cuyo certificado está renovando.

Para renovar un certificado, siga los pasos siguientes:
  1. Pulse el menú de la fila del certificado que desea renovar.
  2. Pulse **Renovar certificado**.
  3. Opcional: puede optar por volver a obtener una clave para el certificado marcando el recuadro de selección **Volver a obtener clave de certificado**. Esto renueva el certificado con un nuevo par de claves. Si solicita una nueva clave para un certificado, asegúrese de desplegar los nuevos certificados y claves en todo lugar en el que se utilicen.
  4. Pulse **Renovar**.


Solo puede renovar los certificados que haya solicitado mediante {{site.data.keyword.cloudcerts_short}}.
{: note}

La renovación se coloca en el estado **Renovación pendiente**. Cuando responde al desafío de validación del dominio y {{site.data.keyword.cloudcerts_short}} verifica que posee el dominio solicitado, obtiene un nuevo certificado y su estado pasa a ser **Válido**. Se le notificará cuando el certificado renovado esté listo o cuando se produzca un problema, en el canal Slack o en el canal de notificaciones de URL de devolución de llamada.
