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

# Gestión de certificados desde el panel de control
{: #managing-certificates-from-the-dashboard}

Puede utilizar el panel de control del servicio {{site.data.keyword.cloudcerts_full}} para gestionar certificados que obtenga de emisores externos para utilizarlos con las apps o servicios basados en la nube de {{site.data.keyword.IBM_notm}}. Después de importar los certificados y las claves, el servicio los cifrará y los almacenará.
{: shortdesc}

## Importación de un certificado
{: #importing-a-certificate}

Importe sus certificados para poderlos gestionar.
{: shortdesc}

**Antes de empezar**

* Cree un certificado válido no caducado con una clave privada coincidente.
* Convierta los archivos a formato PEM (Privacy-enhanced Electronic Mail).
* Mantenga la clave privada no cifrada para asegurarse de que se pueda importar.

Para importar un certificado, pulse **Importar certificado** y proporcione los detalles siguientes:

1. Especifique un nombre de visualización.
2. Para seleccionar el archivo de certificado en formato PEM, pulse **Examinar**.
3. Para seleccionar la clave privada del certificado en formato PEM, pulse **Examinar**.
4. Si es aplicable, proporcione el archivo de certificado intermedio en formato PEM.
5. (Opcional) Especifique una descripción.
6. Pulse **Importar**.

Tras importar un certificado, se mostrará la información siguiente en la tabla Certificados. Para ver más información sobre el certificado, puede ampliar la fila del certificado en la tabla Certificados.

<table>
<caption> Tabla 1. Información sobre el certificado importado </caption>
  <tr>
    <th> Componente </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td>Nombre</td>
    <td>Un nombre de visualización identificativo. La longitud máxima es 256 caracteres. </td>
  </tr>
  <tr>
    <td>Descripción</td>
    <td>(Opcional) Texto descriptivo para el certificado. La longitud máxima es 1024 caracteres.</td>
  </tr>
  <tr>
    <td>Dominio</td>
    <td>El dominio o dominios para los que el resultado es válido. </td>
  </tr>
  <tr>
    <td>Emisor</td>
    <td>La entidad emisora de certificados (CA) que ha emitido el certificado.</td>
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

## Reimportación de un certificado
{: #reimport-certificate}

Si el certificado está a punto de caducar, puede actualizar un certificado importando una nueva versión del certificado que tenga el mismo dominio que el certificado existente, pero una nueva fecha de caducidad. Cuando se vuelve a importar un certificado, la versión existente del certificado se conserva como copia de seguridad que se puede descargar si hace falta.
{: shortdesc}

### Reimportación de su certificado
{: #reimporting-certificate}

Para volver a importar un certificado, siga los pasos siguientes:

1. Expanda la fila correspondiente al certificado.
2. Pulse **Volver a importar certificado**.
3. Para seleccionar el nuevo archivo de certificado en formato PEM, pulse **Examinar**.
4. (Opcional) Para seleccionar la clave privada del nuevo certificado en formato PEM, pulse **Examinar**.
5. (Opcional) Para especificar un nuevo archivo de certificado intermedio en formato PEM, pulse **Examinar**.
6. Pulse **Volver a importar** y luego **Terminado**.

La reimportación de certificados está limitada a cinco acciones por minuto.
{: tip}

### Descarga de una versión anterior de un certificado
{: #downloading-certificate}

Para descargar la versión anterior de un certificado, siga los pasos siguientes:

1. Expanda la fila correspondiente al certificado.
2. Pulse el enlace **Versión anterior**.

## Búsqueda de certificados
{: #searching-certificates}

Si gestiona muchos certificados, puede utilizar la barra de búsqueda para ubicar el certificado necesario.
{: shortdesc}

* Para buscar el nombre, el dominio o el emisor del certificado, escriba el término de búsqueda en la barra de búsqueda y pulse Intro.
* Para ver todos los certificados, pulse el icono **X** en la barra de búsqueda.

## Descarga de certificados
{: #downloading-certificates}

Cuando esté listo para desplegar el certificado en la app o en el servicio, puede descargar el certificado y la clave privada asociada.
{: shortdesc}

Para descargar un certificado, siga los pasos siguientes:

1. Marque el recuadro de selección para el certificado que desea descargar.
2. Pulse **Descargar certificado**. En función de lo que haya importado en el servicio, recibirá un archivo comprimido que contiene archivos PEM para el certificado, una clave privada asociada, y un certificado intermedio asociado.

## Supresión de certificados
{: #deleting-certificates}

Si desea detener el seguimiento de un certificado, puede suprimirlo.
{: shortdesc}  

Para suprimir un certificado, siga los pasos siguientes:

1. Marque el recuadro de selección para el certificado que desee suprimir.
2. Pulse el icono **Papelera**.

## Actualización de metadatos de certificados
{: #updating-certificates-metadata}

También puede actualizar el nombre y la descripción de un certificado.
{: shortdesc}

Para actualizar un certificado, siga los pasos siguientes:

1. Seleccione una fila para abrir los detalles para dicho certificado.
2. Actualice el nombre o la descripción.
3. Guarde los cambios.

Puede realizar un máximo de cinco acciones de actualización por minuto.
{: tip}
