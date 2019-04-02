---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-12"

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

{{site.data.keyword.cloudcerts_short}} da soporte a certificados con claves públicas generadas utilizando los siguientes algoritmos de claves públicas:

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

* La clave privada no está cifrada. Asegúrese de que el certificado y la clave privada coincidan comparando los resultados del siguiente mandato, donde `<certificate-file>` es el nombre del archivo de certificado y `<key-file>` es el nombre del archivo de clave privada:

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
