---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

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

### Roles de acceso a la plataforma
{: #platform-access-roles}

Puede utilizar roles de acceso a la plataforma para permitir a los usuarios realizar tareas en recursos de la plataforma, como crear o suprimir instancias en su cuenta de IBM Cloud.

<table>
<caption> Tabla 1. Acciones que se correlacionan con roles de acceso a la plataforma</caption>
  <tr>
    <th> Acción </th>
    <th> Rol </th>
  </tr>
  <tr>
    <td>Ver instancias de Certificate Manager</td>
    <td> Administrador, Operador, Editor, Visor </td>
  </tr>
  <tr>
    <td>Crear una instancia de Certificate Manager</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Suprimir una instancia de Certificate Manager</td>
    <td> Administrador, Editor </td>
  </tr>
</table>

Históricamente, los roles de plataforma también proporcionan acceso a determinadas acciones sobre los certificados dentro de las instancias. Esta definición es obsoleta y se eliminará próximamente.

### Roles de acceso al servicio
{: #service-acceess-roles}

Puede utilizar roles de acceso al servicio para permitir a los usuarios realizar tareas en instancias de Certificate Manager, como importar, descargar, editar o suprimir certificados.

<table>
<caption> Tabla 2. Acciones que se correlacionan con roles de acceso al servicio</caption>
  <tr>
    <th> Acción </th>
    <th> Rol </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Gestor, escritor, lector</td>
  </tr>
  <tr>
    <td>Descargar un certificado y clave privada </td>
    <td> Gestor, escritor</td>
  </tr>
  <tr>
    <td>Actualizar datos de certificado</td>
    <td> Gestor, escritor</td>
  </tr>
  <tr>
    <td>Cargar certificados, claves privadas y certificados intermedios </td>
    <td> Gestor  </td>
  </tr>
  <tr>
    <td>Suprimir un certificado y una clave privada </td>
    <td> Gestor  </td>
  </tr>
</table>


Para obtener más información sobre los roles y los permisos de usuario, consulte [Roles de usuario](/docs/iam/users_roles.html#userroles).

### Asignación de roles de acceso de usuario
{: #assigning-user--access-roles}

Para asignar un rol de acceso a nivel de cuenta o a nivel de grupo de recursos, siga estos pasos.
Si el usuario no forma parte de su organización, empiece enviando una invitación a dicho usuario.

1. Vaya a **Gestionar > Cuenta > Usuarios**.
2. En el menú **Acciones**, seleccione **Asignar política**.
3. Pulse **Asignar acceso a recursos** o **signar acceso dentro de un grupo de recursos**.
4. En **Servicios**, seleccione **Gestor de certificados**.
5. Opcional: Seleccione una **Región** o utilice el valor predeterminado, **Todas las regiones**.
6. Opcional: Seleccione una **Instancia de servicio** o utilice el valor predeterminado, **Todas las instancias**.
7. En **Seleccionar roles > Asignar roles de acceso a la plataforma/al servicio**, seleccione el nivel de acceso apropiado.

**Ejemplos:**
* Asigne al menos un rol de Visor a cada usuario, de forma que cada usuario pueda ver instancias del servicio. 
* Asigne el rol de Administrador o Editor a un usuario si desea que el usuario cree instancias. 
* Asigne al menos el rol de Lector si desea que un usuario vea certificados dentro de una instancia.
