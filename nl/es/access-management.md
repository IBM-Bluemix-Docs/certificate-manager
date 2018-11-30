---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de roles de acceso al servicio
{: #managing-service-access-roles}

Puede proteger los servicios dentro de {{site.data.keyword.Bluemix_notm}} permitiendo solo a los usuarios con roles de acceso específicos completar determinadas acciones.
{: shortdesc}

## Roles de acceso a la plataforma
{: #platform-access-roles}

Puede utilizar roles de acceso a la plataforma para permitir a los usuarios realizar tareas en recursos de la plataforma, como crear o suprimir instancias en su cuenta de {{site.data.keyword.Bluemix_notm}}.

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
    <td>Actualizar datos de certificado</td>
    <td> Gestor, escritor </td>
  </tr>
  <tr>
    <td>Importar o volver a importar certificados, claves privadas y certificados intermedios </td>
    <td> Gestor </td>
  </tr>
  <tr>
    <td>Suprimir un certificado y una clave privada </td>
    <td> Gestor </td>
  </tr>
      <tr>
        <td>Listar todos los canales de notificaciones </td>
        <td> Gestor, escritor, lector </td>
      </tr>
   <tr>
     <td>Añadir, actualizar o suprimir un canal de notificaciones </td>
     <td> Gestor </td>
   </tr>
     <tr>
       <td>Probar un canal de notificaciones </td>
       <td> Gestor, escritor, lector </td>
     </tr>
</table>

Para obtener más información sobre los roles y los permisos de usuario, consulte [Roles de usuario](/docs/iam/users_roles.html#userroles).

## Configuración de políticas de acceso para los usuarios
{: #configuring-access-policies}

Es posible configurar políticas de acceso para una instancia de {{site.data.keyword.cloudcerts_short}} (y por lo tanto de todos los certificados en dicha instancia), o establecer políticas para certificados individuales (recursos) dentro de una instancia.
{: shortdesc}

Para configurar políticas de acceso, siga los pasos siguientes:

1. Navegue a **Gestionar > Cuenta > Usuarios**. Se muestra una lista de usuarios con acceso a su cuenta de {{site.data.keyword.Bluemix_notm}}.
2. Pulse el nombre del usuario al que desea asignar una política de acceso. Si no se muestra el usuario, pulse **Invitar usuarios** para [añadir el usuario a su cuenta de {{site.data.keyword.Bluemix_notm}}](/docs/iam/iamuserinv.html#iamuserinv).
3. Pulse **Asignar acceso**.
4. Pulse **Asignar acceso a recursos**.
5. Desde el menú **Servicios**, seleccione **Certificate Manager**.
6. Desde el menú **Instancia de servicio**, seleccione una instancia de {{site.data.keyword.cloudcerts_short}}, o utilice el valor predeterminado de `Todas las instancias`.
7. (Opcional) Configure el acceso a un certificado específico:
    1. [Recupere su ID de certificado](#get-certificate-id).
    2. Especifique el `certificado` en el campo **Tipo de recurso**.
    3. Especifique el ID de certificado en el campo **ID de recurso**.
8. Asigne un [rol de acceso de plataforma](#platform-access-roles) al usuario.
9. Asigne un [rol de acceso de servicio](#service-access-roles) al usuario.
10. Pulse **Asignar** para asignar la política de acceso al usuario.

**Ejemplos de asignación de roles**

* Asigne al menos un rol de Visor a cada usuario, de forma que cada usuario pueda ver instancias del servicio.
* Asigne el rol de Administrador o Editor a un usuario si desea que el usuario cree y suprima instancias.
* Asigne al menos el rol de Lector si desea que un usuario vea certificados dentro de una instancia.

### Recuperación del ID de un certificado
{: #get-certificate-id}

Para recuperar el ID de un certificado, siga los pasos siguientes:

1. Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione su instancia de {{site.data.keyword.cloudcerts_short}}.
2. Desde la navegación en la página de detalles del servicio, seleccione **Gestionar**.
3. Seleccione un certificado.
4. En los detalles del certificado, encuentre el CRN del certificado.
5. Copie el ID del certificado. El CRN contiene varios valores separados por caracteres de dos puntos (`:`). El ID del certificado es el último valor en el CRN, por ejemplo: `e20cb664efcbfa2c2f57801230d246a6`
