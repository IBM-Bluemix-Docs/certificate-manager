---
copyright:
  years: 2017
lastupdated: "2017-12-14"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Gestión de certificados utilizando la API
{: #managing-certificates-api}

El servicio de {{site.data.keyword.cloudcerts_full}} proporciona puntos finales REST para importar, obtener y suprimir certificados. Con {{site.data.keyword.iamshort}}, también puede [asignar políticas para un certificado específico](#assigning-advanced-policies).
{: shortdesc}

## Prueba de API
{: #testing}

Puede probar puntos finales REST utilizando Swagger o ejecutando solicitudes cURL en la línea de mandatos.  
Swagger solo está disponible en la región EE.UU. Sur de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Requisitos previos
{: #prereq-api}

Debe completar las tareas siguientes para poder utilizar {{site.data.keyword.cloudcerts_full}}.
{: shortdesc}

* Instale la [CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/get_started.html#getting-started) para obtener los datos necesarios.

* Al trabajar con la API de {{site.data.keyword.cloudcerts_short}}, puede utilizar las siguientes variables en sus llamadas.


<table>
<caption> Tabla 1. Explicación de componentes de mandatos </caption>
  <tr>
    <th> Componente </th>
    <th> Explicación </th>
  </tr>
  <tr>
    <td> <code> IAM-token </code> </td>
    <td> Puede obtener la señal de acceso de {{site.data.keyword.iamshort}} (IAM) iniciando sesión en {{site.data.keyword.Bluemix_notm}} y ejecutando el mandato <code>bx iam oauth-tokens</code>. </td>
  </tr>
  <tr>
    <td> <code> certificateId </code> </td>
    <td> Puede encontrar el ID de certificado utilizando una de las siguientes opciones: <ul><li> Desde la GUI, seleccione el certificado desde la fila de la tabla Certificados. <li> Desde la API, [enumere los certificados disponibles](/docs/services/certificate-manager/rest-api.html#list-certificates).</ul> </td>
  </tr>
  <tr>
    <td> <code> instanceId </code> </td>
    <td> [ID de instancia basado en CRN (Cloud Resource Name)](/docs/overview/crn.html#format) que se asigna a la instancia de servicio una vez que se ha creado. Puede recuperar el ID de instancia de las formas siguientes:
    <ul>
      <li>En la página Gestionar del servicio.</li>
      <li>Ejecute el mandato <code>bx resource service-instance</code>, sustituyendo <i>&lt;Instance_Name&gt;</i> por el nombre de su instancia de servicio.
      <pre>bx resource service-instance &lt;Instance_Name&gt; --id</pre>
      </li>
      <li>Invoque el punto final REST de {{site.data.keyword.Bluemix_notm}} Resource Controller <code>[GET /resource_instances](https://console.bluemix.net/apidocs/700-resource-controller-api?&language=node#resource-instances-1)</code>, que requiere la cabecera <code>Authorization</code> con la señal IAM del administrador de la cuenta.</li>
    </ul>
  </td>
  </tr>
  <tr>
    <td>  <code> account-id </code> </td>
    <td> ID de cuenta del usuario que gestiona la cuenta de {{site.data.keyword.Bluemix_notm}}. Puede encontrar el ID de cuenta ejecutando el mandato <code>bx info</code>. </td>
  </tr>
  <tr>
    <td>  <code> cluster-url </code> </td>
    <td> URL del servicio de la región de {{site.data.keyword.Bluemix_notm}} en la que se ha creado. Puede encontrar el URL en la IU de Swagger. </td>
  </tr>
  <tr>
    <td>  <code> name (Opcional) </code> </td>
    <td> Nombre de visualización para el certificado importado. </td>
  </tr>
  <tr>
    <td> <code> description (Opcional) </code> </td>
    <td> Descripción para el certificado importado. </td>
  </tr>
  <tr>
    <td> <code> certificate </code> </td>
    <td> Datos de certificado, escapados. </td>
  </tr>
  <tr>
    <td> <code> privateKey </code> </td>
    <td> Datos de la clave privada, escapados. </td>
  </tr>
  <tr>
    <td> <code> intermediate (Opcional) </code> </td>
    <td> Datos de certificado intermedio, escapados. </td>
  </tr>
  <tr>
    <td> <code> user-id </code> </td>
    <td>ID del usuario al que desea asignar una política de acceso. Para buscar el ID de usuario, consulte [Recuperando el ID de usuario](#retrieve-user-id). </td>
  </tr>
</table>

## Importación de un certificado
{: #import-certificate}  

Importe un certificado en formato PEM (Privacy-enhanced Electronic Mail) con su clave privada. También puede importar un certificado intermedio.
{: shortdesc}


Ejecute el siguiente mandato `curl`:

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/import \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>",
	"data":{
		"content": "<certificate>",
		"priv_key": "<privateKey>",
		"intermediate": "<intermediate>"
	}
  }'
  ```
  {: pre}

Sustituya _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, _&lt;description&gt;_, _&lt;certificate&gt;_, _&lt;privateKey&gt;_, e _&lt;intermediate&gt;_ por los valores apropiados. Los valores _&lt;name&gt;_, _&lt;description&gt;_, e _&lt;intermediate&gt;_ son opcionales.

## Actualización de los metadatos de certificados
{: #update-certificate-metadata}  

Actualice la propiedad opcional del certificado `name`, `description`, o ambas.

**Nota**: Actualizar operaciones se limita a cinco acciones por minuto.  
{: shortdesc}


Ejecute el siguiente mandato `curl`:

  ```
  curl -X POST \
  https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId> \
  -H 'authorization: Bearer <IAM-token>' \
  -H 'content-type: application/json' \
  -d '{
	"name":"<name>",
	"description":"<description>"
  }'
  ```
  {: pre}

Sustituya _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, _&lt;certificateId&gt;_, _&lt;IAM-token&gt;_, _&lt;name&gt;_, y _&lt;description&gt;_ por los valores apropiados.

## Listado de todos los certificados
{: #list-certificates}  

Recupere una lista de todos los certificados disponibles.
{: shortdesc}

Ejecute el siguiente mandato `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/
  ```
  {: pre}

Sustituya _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, e _&lt;instanceId&gt;_ por los valores apropiados.

## Descarga de certificados
{: #get-certificate}  

Utilice un ID de certificado recuperado para descargar los datos de certificado.
{: shortdesc}

Ejecute el siguiente mandato `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

Sustituya _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, y _&lt;certificateId&gt;_ por los valores apropiados.

## Supresión de un certificado
{: #delete-certificate}  

Utilice un ID de certificado recuperado para suprimir el certificado y sus datos.
{: shortdesc}

Ejecute el siguiente mandato `curl`:

  ```
  curl -H "Authorization: Bearer <IAM-token>" -X DELETE https://<cluster-url>/api/v1/<instanceId>/certificates/<certificateId>
  ```
  {: pre}

Sustituya _&lt;IAM-token&gt;_, _&lt;cluster-url&gt;_, _&lt;instanceId&gt;_, y _&lt;certificateId&gt;_ por los valores apropiados.

## Asignación de políticas avanzadas
{: #assigning-advanced-policies}

Puede elegir permitir a determinados usuarios realizar ciertas acciones en certificados específicos. Puede que también desee permitir a los usuarios ver solo un subconjunto de los certificados de instancia de servicio disponibles.
{: shortdesc}

Para asignar la política, envíe una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato `curl` siguiente. Repita el mandato para cada certificado.

```
curl -X POST \
    https://iampap.<region>.bluemix.net/acms/v1/scopes/a%2<account-id>/users/<user-id>/policies \
    -H 'accept: application/json' \
    -H 'authorization: Bearer <Account-Admin-IAM-token>' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{
        "roles": [
        {
            "id": "crn:v1:bluemix:public:iam::::role:Viewer"
        }
    ],
  "resources": [
    {
            "serviceName”: "cloudcerts",
            "serviceInstance": "<instanceId>",
            "resourceType": "certificate",
            "resource": "<certificateId>"
        }
    ]
}'
```
{: pre}

Sustituya _&lt;account-id&gt;_, _&lt;user-id&gt;_, _&lt;instanceId&gt;_ y _&lt;certificateId&gt;_ por los valores apropiados.
Sustituya _&lt;Account-Admin-IAM-token&gt;_ por la señal IAM del administrador de la cuenta.
Sustituya _&lt;region&gt;_ por la región, por ejemplo, `ng` para EE.UU. Sur.

**Nota**: En la solicitud cURL anterior, <code>instanceId</code> no está basado en CRN, sino en GUID.  
Por ejemplo, en el CRN de <code>instanceId</code> siguiente, el valor de instancia es **58866f34-55ca-4477-8c32-fda435f01f97**.

```
crn:v1:staging:public:cloudcerts:us-south:a/d0c8a917589e40076a61e56b23056d16:58866f34-55ca-4477-8c32-fda435f01f97::
```

### Recuperando el ID de usuario
{: #retrieve-user-id}

Recupere el ID de usuario.
{: shortdesc}

Para recuperar el ID de usuario, siga estos pasos:

1. Solicite al usuario que [proporcione la señal IAM](/docs/services/certificate-manager/rest-api.html#prereq-api). La estructura de la señal IAM se encuentra en el formato siguiente: `<value_1>.<value_2>.<value_3>`
2. Copie el valor de _&lt;value_2&gt;_ y ejecute el mandato `echo` siguiente:

   ```
   echo -n "<value_2>" | base64 --decode
   ```
   {: pre}

   El resultado es un objeto JSON similar a la salida siguiente:

   ```
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

3. Copie el valor de la propiedad de `id`.
