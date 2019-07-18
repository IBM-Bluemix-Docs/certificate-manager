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
{:faq: data-hd-content-type='faq'}

# Preguntas frecuentes (FAQ)
{: #faq}

Preguntas frecuentes sobre {{site.data.keyword.cloudcerts_long}}.
{: shortdesc}

## ¿En qué formato deben estar los certificados?
{: #supported-certificate-types}
{: faq}

{{site.data.keyword.cloudcerts_short}} solo admite certificados en formato PEM.

## ¿A qué tipo de algoritmos de claves públicas se da soporte?
{: #supported-pk-algorithms}
{: faq}

{{site.data.keyword.cloudcerts_short}} da soporte a certificados con claves públicas que se generan utilizando los siguientes algoritmos de claves públicas:

* Rivest-Shamir-Adleman (RSA)
* Digital Signature Algorithm (DSA)
* Elliptic Curve Digital Signature Algorithm (ECDSA)
* Protocolo de establecimiento de claves Elliptic Curve Diffie-Hellman (ECDH)


## ¿Puedo cargar claves privadas protegidas por contraseña?
{: #password-protected-private-keys}
{: faq}

{{site.data.keyword.cloudcerts_short}} no admite la importación de certificados con claves privadas protegidas por contraseña.

## Estoy intentando cargar un certificado y una clave privada y recibo este error `Error: La clave privada no coincide con el certificado que está intentando importar. Asegúrese de que coincidan e inténtelo de nuevo.`
{: #import-cert-private-key}
{: faq}

En función de si la clave privada está o no cifrada, elija una de estas opciones:

* La clave privada está cifrada. Asegúrese de descifrar la clave antes de cargarla.

   ```
   openssl rsa -in [file1.key] -out [file2.key]
   ```
   {: pre}

* La clave privada no está cifrada. Asegúrese de que el certificado y la clave privada coincidan comparando los resultados del siguiente mandato, donde `<certificate-file>` es el nombre del archivo del certificado y `<key-file>` es el nombre del archivo de clave privada:

   ```
   openssl x509 -modulus -noout -in <certificate-file>.pem | openssl md5; openssl rsa -modulus -noout -in <key-file>.key | openssl md5
   ```
   {: pre}

## ¿Puedo recibir notificaciones por correo electrónico sobre la caducidad de los certificados?
{: #email-notifications}
{: faq}

Solo se admiten notificaciones de tipo Callback y Slack.


## ¿Puedo controlar la versión de mis certificados?
{: #certificate-versioning}
{: faq}

Puede actualizar un certificado volviendo a importar una nueva versión del certificado que tenga el mismo dominio que el certificado existente, pero una nueva fecha de caducidad. Cuando se vuelve a importar un certificado, la versión existente del certificado se conserva como copia de seguridad; consulte el apartado sobre [Reimportación de un certificado](/docs/services/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#reimport-certificate).



## ¿Puedo hacer que determinados certificados solo estén visibles para usuarios específicos?
{: #access-policies}
{: faq}

Los certificados se pueden proteger mediante políticas de acceso de IAM para conseguir un control de acceso granular; consulte [Gestión de roles de acceso al servicio](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#managing-service-access-roles).



## ¿Cómo se revoca un certificado emitido?
{: #revoke-certificate}
{: faq}

Actualmente {{site.data.keyword.cloudcerts_short}} no dispone de ninguna API de renovación que pueda utilizar. Sin embargo, puede utilizar la API de Let's Encrypt para revocar certificados utilizando la clave privada del certificado. Encontrará información sobre cómo revocar certificados de Let's Encrypt en la [documentación de Let's Encrypt](https://letsencrypt.org/docs/revoking/).



## Mi solicitud de certificado lleva mucho tiempo en estado pendiente
{: #certificate-order-status}
{: faq}

En redes DNS lentas, una solicitud puede tardar hasta 20 minutos en completarse correctamente.

## ¿Durante cuánto tiempo intenta el servicio validar que poseo los dominios que solicito en mi pedido?
{: #certificate-order-validation}
{: faq}

Una vez que el servicio envía el desafío de validación de dominio, {{site.data.keyword.cloudcerts_short}} intenta validar que posee los dominios que ha solicitado durante un máximo de 10 minutos. Si el DNS no se actualiza con el desafío del registro TXT en un plazo de 10 minutos, la solicitud falla.

## ¿Cómo puedo comprobar el estado de mi solicitud de certificado mediante la API pública de {{site.data.keyword.cloudcerts_short}}?
{: #certificate-order-status-api}
{: faq}

Utilice la API `Obtener metadatos de certificado` para sondear el estado de la solicitud de certificado.

## ¿Puedo recibir una notificación cuando se complete mi solicitud?
{: #certificate-order-notification}
{: faq}

Si ha configurado un canal de notificación, se le notificará cuando se emita el certificado o bien cuando la solicitud falle. Tenga en cuenta que la versión del canal de notificación debe ser la v4 o posterior.

## Mi solicitud ha fallado. ¿Por qué?
{: #certificate-order-failure}
{: faq}

Encontrará un código de error y un mensaje en los metadatos del certificado, en la IU y en la notificación que ha recibido cuando ha fallado la solicitud.

## ¿Por qué no recibo sucesos de solicitud de certificado en mi canal de notificación Slack existente?
{: #missing-notification-for-ordered-certificate}
{: faq}

Actualice el canal de notificación Slack a la versión más reciente en el separador Valores del gestor de certificados.
