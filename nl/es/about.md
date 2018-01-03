---

copyright:
  years: 2017
lastupdated: "2017-12-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Acerca de 
{: #about-cloud-certs}

Más información sobre {{site.data.keyword.cloudcerts_full}}.

## ¿Qué es {{site.data.keyword.cloudcerts_short}}?
{: #what-is-cloud-certs}

{{site.data.keyword.cloudcerts_short}} le ayuda a gestionar los certificados SSL para las apps y los servicios basados en la nube de {{site.data.keyword.IBM_notm}}.
{: shortdesc}

Puede importar certificados SSL que obtenga para las apps y los servicios, almacenarlos de forma segura, y obtener una vista central de los certificados que está utilizando.

Puede gestionar los certificados de las formas siguientes:

* Supervisar las fechas de caducidad de los certificados para asegurarse de que los renueva a tiempo
* Ver los tipos de certificados en los despliegues y asegurarse de que cumplan las políticas de organización
* Buscar certificados que necesiten sustitución cuando se emitan nuevos requisitos de conformidad o de seguridad
* Establecer controles sobre quién puede acceder y gestionar sus certificados

## Disponibilidad
{: #availability}

{{site.data.keyword.cloudcerts_short}} solo está disponible en la región EE.UU. Sur.

## Seguridad de clave privada
{: #private-key-security}

Al importar un certificado y la correspondiente clave privada en {{site.data.keyword.cloudcerts_short}}, el servicio utilizará un algoritmo Advanced Encryption Standard (AES) 256 para cifrar la clave privada. {{site.data.keyword.cloudcerts_short}} guarda esta clave cifrada exclusiva para utilizarla con la instancia de servicio.

## Identity and Access Management
{: #identity-access-management}

Puede proteger los servicios dentro de {{site.data.keyword.Bluemix_notm}} permitiendo solo a los usuarios con roles específicos completar determinadas acciones.
{: shortdesc}

<table>
<caption> Tabla 1. Acciones que se correlacionan con roles de usuario</caption>
  <tr>
    <th> Acción </th>
    <th> Rol </th>
  </tr>
  <tr>
    <td>Listar certificados</td>
    <td> Administrador, Operador, Editor, Visor </td>
  </tr>
  <tr>
    <td>Descargar un certificado y clave privada </td>
    <td> Administrador, Operador </td>
  </tr>
  <tr>
    <td>Actualizar datos de certificado</td>
    <td> Administrador, Editor </td>
  </tr>
  <tr>
    <td>Cargar certificados, claves privadas y certificados intermedios </td>
    <td> Administrador, Editor  </td>
  </tr>
  <tr>
    <td>Suprimir un certificado y una clave privada </td>
    <td> Administrador, Editor </td>
  </tr>
</table>

Para obtener más información sobre los roles y los permisos de usuario, consulte [Roles de usuario](/docs/admin/patterns.html#userroles).

### Asignación de roles de usuario
{: #assigning-user-roles}

Para asignar un rol de usuario a nivel de cuenta o a nivel de grupo de recursos, siga estos pasos.
Si el usuario no forma parte de su organización, empiece enviando una invitación a dicho usuario.

1. Vaya a **Gestionar > Cuenta > Usuarios**.
2. En el menú **Acciones**, seleccione **Asignar política**.
3. Pulse **Asignar acceso a recursos** o **signar acceso dentro de un grupo de recursos**.
4. En **Servicios**, seleccione **Gestor de certificados**.
5. Opcional: Seleccione una **Región** o utilice el valor predeterminado, **Todas las regiones**.
6. Opcional: Seleccione una **Instancia de servicio** o utilice el valor predeterminado, **Todas las instancias**.
7. En **Seleccionar roles > Asignar roles de acceso a la plataforma**, seleccione el nivel de acceso apropiado.
