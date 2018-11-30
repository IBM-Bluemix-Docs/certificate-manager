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
    <td>Almacene sus certificados de dominio personalizado de clúster de Kubernetes en {{site.data.keyword.cloudcerts_short}} y luego despliéguelos mediante [mandatos de plugin del servicio Kubernetes](/docs/containers/cs_cli_reference.html) para la CLI de {{site.data.keyword.cloud_notm}}. [Obtenga más información sobre esta integración ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2018/01/use-ibm-cloud-certificate-manager-ibm-cloud-container-service-deploy-custom-domain-tls-certificates/).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.security-advisor_full_notm}}</td>
    <td>{{site.data.keyword.security-advisor_short}} centraliza la información sobre los servicios de {{site.data.keyword.cloud_notm}}. La información incluye la indicación de certificados caducados y certificados que están a punto de caducar en instancias de {{site.data.keyword.cloudcerts_short}} de su cuenta de {{site.data.keyword.cloud_notm}}. [Aprenda más sobre {{site.data.keyword.security-advisor_short}}](/docs/services/security-advisor/index.html#index).</td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloudaccesstrailfull_notm}}</td>
    <td>El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} permite rastrear la forma en la que usuarios y aplicaciones interactúan con el servicio {{site.data.keyword.cloudcerts_long_notm}} en {{site.data.keyword.cloud_notm}}. [Aprenda más sobre {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).
    <p>Consulte [Sucesos de {{site.data.keyword.cloudaccesstrailshort}}](/docs/services/certificate-manager/at_events.html#at_events) para obtener una lista de las acciones que generan un suceso.</p></td>
  </tr>
  <tr>
    <td>{{site.data.keyword.cloud_notm}} {{site.data.keyword.apiconnect_short}}</td>
    <td>Almacene sus certificados de dominio personalizado en el servicio {{site.data.keyword.cloudcerts_short}} y luego utilice los CRN de certificado para enlazar con dominios personalizados en {{site.data.keyword.apiconnect_short}}. [Aprenda más sobre {{site.data.keyword.apiconnect_short}}](/docs/api-management/index.html#index).</p></td>
  </tr>
</table>

## Ubicaciones
{: #availability}

{{site.data.keyword.cloudcerts_short}} está disponible en las ubicaciones Dallas y Londres.



## Límites
{: #limits}

Puede cargar un máximo de 1000 certificados por instancia.
