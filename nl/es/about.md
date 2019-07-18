---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-09"

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

# Acerca de {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_full}} le ayuda a obtener, almacenar y gestionar certificados SSL que utiliza para despliegues de {{site.data.keyword.cloud_notm}} u otros despliegues locales o en la nube.
{: shortdesc}

Puede importar certificados SSL que obtenga para las apps y los servicios, almacenarlos de forma segura, y obtener una vista central de los certificados que está utilizando. O bien puede solicitar certificados públicos de entidades emisoras de certificados mediante el gestor de certificados.

Puede gestionar los certificados de las formas siguientes:

* Recibir notificaciones de caducidad de certificados para poder renovarlos a tiempo  
* Utilizar notificaciones para activar la renovación automática de certificados  
* Ver los tipos de certificados en los despliegues y asegurarse de que cumplan las políticas de organización  
* Buscar certificados que necesiten sustitución cuando se emitan nuevos requisitos de conformidad o de seguridad  
* Establecer controles sobre quién puede acceder y gestionar sus certificados
* Solicitar nuevos certificados públicos


![Diagrama de arquitectura de servicio de alto nivel](images/high-level-architecture.png)
<caption>Figura 1. Arquitectura de servicio de alto nivel.</caption>


## Seguridad de clave privada
{: #private-key-security}

Cuando importe o solicite un certificado en {{site.data.keyword.cloudcerts_short}}, el servicio utilizará un algoritmo Advanced Encryption Standard (AES) 256 para cifrar la clave privada. {{site.data.keyword.cloudcerts_short}} guarda esta clave cifrada exclusiva para utilizarla con la instancia de servicio.

## Integraciones
{: #integrations}

<table>
<caption>Tabla 1. Servicios de {{site.data.keyword.cloud_notm}} que utilizan {{site.data.keyword.cloudcerts_short}}</caption>
  <tr>
    <th> Servicio </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td>{{site.data.keyword.containerlong_notm}}</td>
    <td>Puede desplegar de forma fácil y segura certificados TLS de dominio personalizado desde {{site.data.keyword.cloudcerts_short}} al clúster de Kubernetes. Los administradores del clúster pueden utilizar los [mandatos de plugin del servicio Kubernetes](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) para actualizar los certificados TLS como secretos de Kubernetes con un nuevo certificado sin causar tiempo de inactividad. Para empezar, consulte las [anotaciones de Ingress en la documentación](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started) centraliza la información sobre los servicios de {{site.data.keyword.cloud_notm}}. La información incluye la indicación de certificados caducados y certificados que están a punto de caducar en instancias de {{site.data.keyword.cloudcerts_short}} de su cuenta de {{site.data.keyword.cloud_notm}}. [Más información sobre {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-getting-started#getting-started).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.at_short}}</td>
    <td>Puede utilizar [{{site.data.keyword.at_short}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started) para realizar un seguimiento de la forma en que los usuarios y las aplicaciones interactúan con el servicio {{site.data.keyword.cloudcerts_long_notm}} en {{site.data.keyword.cloud_notm}}.
    <p>Para obtener una lista de las acciones que generan un suceso, consulte [Sucesos de {{site.data.keyword.at_short}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events).</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Almacene sus certificados de dominio personalizado en el servicio {{site.data.keyword.cloudcerts_short}} y luego utilice los CRN de certificado para enlazar con dominios personalizados en {{site.data.keyword.apiconnect_short}}. [Más información sobre {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index#index).</p></td>
  </tr>
</table>

## Disponibilidad
{: #availability}

{{site.data.keyword.cloudcerts_short}} está disponible en las ubicaciones de Dallas, Londres, Frankfurt y Tokio.



## Límites
{: #limits}

Puede cargar un máximo de 1000 certificados por instancia.

## Conformidad y estándares
{: #compliance-and-standards}

{{site.data.keyword.cloudcerts_short}} ha completado correctamente diversas certificaciones y auditorías y cumple con diversos estándares de primer orden.

### HIPAA
{: #compliance-hippa}

{{site.data.keyword.cloudcerts_short}} cumple con los controles de IBM necesarios, en consonancia con los requisitos de seguridad y de reglas de privacidad del acta de la Ley de Transferencia y Responsabilidad de Seguro Médico (HIPAA) de 1996.

### International Organization for Standardization (ISO)
{: #compliance-iso}

* Certificado de servicios de {{site.data.keyword.IBM_notm}} (PaaS y SaaS) - ISO 27001

### Reglamento General de Protección de Datos (GDPR)
{: #compliance-gdpr}

El GDPR busca crear un marco de ley de protección de datos unificado en la Unión Europea y trata de devolver a los ciudadanos el control de sus datos personales mientras impone reglas estrictas a quienes alojan y 'procesan' los datos, en cualquier parte del mundo. El reglamento también presenta reglas referentes a la libre circulación de datos personales dentro y fuera de la Unión Europea. Para obtener más información, consulte la [Declaración de privacidad de IBM](https://www.ibm.com/privacy/).
