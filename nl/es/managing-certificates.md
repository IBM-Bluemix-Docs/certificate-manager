---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de certificados desde el panel de control
{: #managing-certificates-from-the-dashboard}

Puede utilizar el panel de control del servicio {{site.data.keyword.cloudcerts_full}} para gestionar certificados que obtenga de emisores externos para utilizarlos con las apps o servicios basados en la nube de {{site.data.keyword.IBM_notm}}. Tras importar los certificados y las claves, el servicio los cifrará y los almacenará.
{: shortdesc}

## Importación de un certificado
{: #importing-a-certificate}

Para ayudarle a gestionar los certificados, puede cargarlos.
{: shortdesc}

Antes de empezar:

* Cree un certificado válido no caducado con una clave privada coincidente.
* Convierta los archivos a formato PEM (Privacy-enhanced Electronic Mail).
* Mantenga la clave privada no cifrada para asegurarse de que se pueda importar.

Para importar un certificado, pulse **Importar certificado** y proporcione los detalles siguientes:

1. Opcional: Especifique un nombre de visualización.
2. Pulse **Examinar**, seleccione el archivo de certificado en formato PEM.
3. Pulse **Examinar**, seleccione la clave privada del certificado en formato PEM.
4. Si es aplicable, proporcione el archivo de certificado intermedio en formato PEM.
5. Opcional: Escriba una descripción.
6. Pulse **Importar**.  

**Nota**: Para renovar un certificado importado, obtenga un certificado nuevo de la entidad emisora de certificados (CA) e importe el certificado nuevo en {{site.data.keyword.cloudcerts_short}}. Una vez desplegado el certificado nuevo, puede suprimir el antiguo.

Tras importar un certificado, se mostrará la información siguiente en la tabla Certificados. Para ver más información del certificado, puede seleccionar el certificado en la fila de tabla.

<table>
<caption> Tabla 1. Información sobre el certificado importado </caption>
  <tr>
    <th> Componente </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td>Nombre</td>
    <td>Opcional: Un nombre de visualización identificativo. Longitud máxima de 256 caracteres. </td>
  </tr>
  <tr>
    <td>Descripción</td>
    <td>Opcional: El texto descriptivo para el certificado. Longitud máxima de 1024 caracteres.</td>
  </tr>
  <tr>
    <td>Dominio</td>
    <td>El dominio o dominios para los que el resultado es válido. </td>
  </tr>
  <tr>
    <td>Emisor</td>
    <td>La entidad emisora de certificados que ha emitido el certificado.</td>
  </tr>
  <tr>
    <td>Algoritmo</td>
    <td>El tipo de cifrado por el que se ha creado el certificado. </td>
  </tr>
  <tr>
    <td>Algoritmo de clave</td>
    <td>El tipo y el tamaño de la clave que utiliza el algoritmo. </td>
  </tr>
  <tr>
    <td>Caduca en </td>
    <td>El número de días restantes antes de que el certificado no sea válido. </td>
  </tr>
  <tr>
    <td>Fecha de emisión</td>
    <td>La fecha en la que se ha emitido el certificado. </td>
  </tr>
  <tr>
    <td>Válido a partir de</td>
    <td>La fecha en la que el certificado pasará a ser válido. </td>
  </tr>
  <tr>
    <td>Caduca en</td>
    <td>La fecha en la que el certificado ya no será válido. </td>
  </tr>
  <tr>
    <td>ID de certificado</td>
    <td>El ID generado que se da al certificado al importar. </td>
  </tr>
</table>

## Búsqueda de certificados
{: #searching-certificates}
 
Si gestiona muchos certificados, puede utilizar la barra de búsqueda para ubicar el certificado necesario.
{: shortdesc}
 
-   Para buscar el nombre, el dominio o el emisor del certificado, escriba el término de búsqueda en la barra de búsqueda y pulse Intro.
-   Para ver todos los certificados, pulse el icono **X** en la barra de búsqueda.

## Descarga de certificados
{: #downloading-certificates}

Cuando esté listo para desplegar el certificado en la app o en el servicio, puede descargar el certificado y la clave privada asociada.
{: shortdesc}

Para descargar un certificado:

1. Marque el recuadro de selección para el certificado que desea descargar.
2. Pulse **Descargar certificado**. En función de lo que haya importado en el servicio, recibirá un archivo comprimido que contiene archivos PEM para el certificado, una clave privada asociada, y un certificado intermedio asociado.


## Supresión de certificados
{: #deleting-certificates}

Si desea detener el seguimiento de un certificado, puede suprimirlo.
{: shortdesc}  

Para suprimir un certificado:

1. Marque el recuadro de selección para el certificado que desee suprimir.
2. Pulse el icono **Papelera**.

## Actualización de metadatos de certificados
{: #updating-certificates-metadata}

También puede actualizar el nombre y la descripción de un certificado.
{: shortdesc}

Para actualizar un certificado:

1. Seleccione una fila para abrir los detalles para dicho certificado.
2. Actualice el nombre o la descripción.
3. Guarde los cambios.

**Nota**: Puede realizar un máximo de cinco acciones de actualización por minuto.
