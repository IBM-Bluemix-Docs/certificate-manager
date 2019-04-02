---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-13"

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


# Acerca de {{site.data.keyword.cloudcerts_short}}
{: #about-certificate-manager}

{{site.data.keyword.cloudcerts_long}} le ayuda a gestionar los certificados SSL para las apps y los servicios basados en la nube de {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Puede importar certificados SSL que obtenga para las apps y los servicios, almacenarlos de forma segura, y obtener una vista central de los certificados que está utilizando.

Puede gestionar los certificados de las formas siguientes:

* Recibir notificaciones de caducidad de certificados para poder renovarlos a tiempo
* Ver los tipos de certificados en los despliegues y asegurarse de que cumplan las políticas de organización
* Buscar certificados que necesiten sustitución cuando se emitan nuevos requisitos de conformidad o de seguridad
* Establecer controles sobre quién puede acceder y gestionar sus certificados

![Diagrama de arquitectura de servicio de alto nivel](images/high-level-architecture.png)
<caption>Figura 1. Arquitectura de servicio de alto nivel.</caption>

## Seguridad de clave privada
{: #private-key-security}

Al importar un certificado y la correspondiente clave privada en {{site.data.keyword.cloudcerts_short}}, el servicio utilizará un algoritmo Advanced Encryption Standard (AES) 256 para cifrar la clave privada. {{site.data.keyword.cloudcerts_short}} guarda esta clave cifrada exclusiva para utilizarla con la instancia de servicio.

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
    <td>Puede desplegar de forma fácil y segura certificados TLS de dominio personalizado desde {{site.data.keyword.cloudcerts_short}} al clúster de Kubernetes. Los administradores del clúster pueden utilizar los [mandatos de plugin del servicio Kubernetes](/docs/containers?topic=containers-cs_cli_reference) para actualizar los certificados TLS como secretos de Kubernetes con un nuevo certificado sin causar tiempo de inactividad. Para empezar, consulte las [anotaciones de Ingress en la documentación](/docs/containers?topic=containers-ingress_annotation#https-auth).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>[{{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index) centraliza la información sobre los servicios de {{site.data.keyword.cloud_notm}}. La información incluye la indicación de certificados caducados y certificados que están a punto de caducar en instancias de {{site.data.keyword.cloudcerts_short}} de su cuenta de {{site.data.keyword.cloud_notm}}. [Más información sobre {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor?topic=security-advisor-index#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>Puede utilizar [el servicio {{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started) para rastrear la forma en la que usuarios y aplicaciones interactúan con el servicio {{site.data.keyword.cloudcerts_long_notm}} en {{site.data.keyword.cloud_notm}}. [Más información sobre {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started#getting-started).
    <p>Consulte [Sucesos de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager?topic=certificate-manager-at_events#at_events) para obtener una lista de las acciones que generan un suceso.</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Almacene sus certificados de dominio personalizado en el servicio {{site.data.keyword.cloudcerts_short}} y luego utilice los CRN de certificado para enlazar con dominios personalizados en {{site.data.keyword.apiconnect_short}}. [Más información sobre {{site.data.keyword.apiconnect_short}}](/docs/services/apiconnect?topic=apiconnect-index).</p></td>
  </tr>
</table>

## Ubicaciones
{: #availability}

{{site.data.keyword.cloudcerts_short}} está disponible en las ubicaciones de Dallas, Londres, Frankfurt y Tokio.



## Límites
{: #limits}

Puede cargar un máximo de 1000 certificados por instancia.
