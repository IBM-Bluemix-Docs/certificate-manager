---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

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

# Gestión de roles de acceso al servicio
{: #managing-service-access-roles}

Puede proteger los servicios dentro de {{site.data.keyword.cloud_notm}} permitiendo solo a los usuarios con roles de acceso específicos completar determinadas acciones.
{: shortdesc}

## Roles de acceso a la plataforma
{: #platform-access-roles}

Puede utilizar roles de acceso a la plataforma para permitir a los usuarios realizar tareas en recursos de la plataforma, como crear o suprimir instancias en su cuenta de {{site.data.keyword.cloud_notm}}.

<table>
<caption> Tabla 1. Acciones que se correlacionan con roles de acceso a la plataforma</caption>
  <tr>
    <th> Acción </th>
    <th> Rol </th>
  </tr>
  <tr>
    <td>Ver instancias de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, Operador, Editor, Visor </td>
  </tr>
  <tr>
    <td>Crear una instancia de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Suprimir una instancia de {{site.data.keyword.cloudcerts_short}}</td>
    <td> Administrador, Editor </td>
  </tr>
</table>

## Roles de acceso al servicio
{: #service-access-roles}

Puede utilizar roles de acceso al servicio para permitir a los usuarios realizar tareas en instancias de {{site.data.keyword.cloudcerts_short}} como, por ejemplo, importar, descargar, editar o suprimir certificados.

<table>
<caption> Tabla 2. Acciones que se correlacionan con roles de acceso al servicio</caption>
  <tr>
    <th> Acción </th>
    <th> Rol </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Gestor, escritor, lector </td>
  </tr>
  <tr>
    <td>Descargar un certificado y clave privada </td>
    <td> Gestor, escritor </td>
  </tr>
  <tr>
     <td>Obtener metadatos del certificado </td>
     <td> Gestor, escritor, lector </td>
  </tr>      
  <tr>
    <td>Actualizar los metadatos de un certificado</td>
    <td> Gestor, escritor </td>
  </tr>
  <tr>
    <td>Importar o volver a importar certificados, claves privadas y certificados intermedios </td>
    <td> Gestor </td>
  </tr>
  <tr>
    <td>Solicitar un certificado </td>
    <td> Gestor </td>
  </tr>
  <tr>
    <td>Suprimir un certificado y una clave privada </td>
    <td> Gestor </td>
  </tr>
      <tr>
        <td>Listar todos los canales de notificación </td>
        <td> Gestor, escritor, lector </td>
      </tr>
   <tr>
     <td>Añadir, actualizar o suprimir un canal de notificación </td>
     <td> Gestor </td>
   </tr>
     <tr>
       <td>Probar un canal de notificación </td>
       <td> Gestor, escritor, lector </td>
     </tr>

</table>

Para obtener más información sobre los roles y los permisos de usuario, consulte [Roles de usuario](/docs/iam?topic=iam-userroles#userroles).

## Configuración de políticas de acceso para los usuarios
{: #configuring-access-policies}

Es posible configurar políticas de acceso para una instancia de {{site.data.keyword.cloudcerts_short}} (y por lo tanto de todos los certificados en dicha instancia), o establecer políticas para certificados individuales (recursos) dentro de una instancia.

**Ejemplos de asignación de roles**

* Asigne al menos un rol de Visor a cada usuario, de forma que cada usuario pueda ver instancias del servicio.
* Asigne el rol de Administrador o Editor a un usuario si desea que el usuario cree y suprima instancias.
* Asigne al menos el rol de Lector si desea que un usuario vea certificados dentro de una instancia.

{: shortdesc}

### Configuración de políticas de acceso
{: #configuring-access}

Para configurar políticas de acceso, siga los pasos siguientes:

1. Vaya a **Gestionar > Acceso (IAM) > Usuarios**. Se muestra una lista de usuarios con acceso a su cuenta de {{site.data.keyword.cloud_notm}}.
2. Pulse el nombre del usuario al que desea asignar una política de acceso. Si el usuario no aparece, pulse **Invitar a usuarios** para [añadir el usuario a su cuenta de {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-iamuserinv#iamuserinv).
3. Pulse **Políticas de acceso** y luego **Asignar acceso**.
4. Pulse **Asignar acceso a recursos**.
5. Desde el menú **Servicios**, seleccione **Certificate Manager**.
6. Desde el menú **Instancia de servicio**, seleccione una instancia de {{site.data.keyword.cloudcerts_short}}, o utilice el valor predeterminado de `Todas las instancias`.
7. Asigne un [rol de acceso a la plataforma](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#platform-access-roles) al usuario.
8. Asigne un [rol de acceso al servicio](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#service-access-roles) al usuario.
9. Pulse **Asignar** para asignar la política de acceso al usuario.

### Cómo permitir el acceso a un certificado específico
{: #allow-access-to-specific-certificate}

Para permitir el acceso a un certificado específico, siga los pasos siguientes:

1. [Recupere su ID de certificado](/docs/services/certificate-manager?topic=certificate-manager-managing-service-access-roles#get-certificate-id).
2. Cree dos políticas de acceso:
   - La primera política: asigne al menos el rol de acceso a la plataforma de **Visor** sobre la instancia de servicio
   - La segunda política: asigne al menos el rol de acceso al servicio de **Lector**
     - Especifique el `certificado` en el campo **Tipo de recurso**.
     - Especifique el ID de certificado en el campo **ID de recurso**.

### Recuperación del ID de un certificado
{: #get-certificate-id}

Para recuperar el ID de un certificado, siga los pasos siguientes:

1. Desde el panel de control de {{site.data.keyword.cloud_notm}}, seleccione su instancia de {{site.data.keyword.cloudcerts_short}}.
2. Desde la navegación en la página de detalles del servicio, seleccione **Gestionar**.
3. Seleccione un certificado.
4. En los detalles del certificado, encuentre el CRN del certificado.
5. Copie el ID del certificado. El CRN contiene varios valores separados por caracteres de dos puntos (`:`). El ID del certificado es el último valor en el CRN, por ejemplo: `e20cb664efcbfa2c2f57801230d246a6`
