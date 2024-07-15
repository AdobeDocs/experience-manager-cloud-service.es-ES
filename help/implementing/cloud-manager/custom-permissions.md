---
title: Permisos personalizados
description: Descubra cómo puede utilizar permisos personalizados para crear perfiles de permisos personalizados con permisos configurables para restringir el acceso a programas, canalizaciones y entornos para usuarios de Cloud Manager.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
solution: Experience Manager
feature: Security, Developing
role: Admin, Architect, Developer
source-git-commit: bc92ed7acefbbd906b0986ea0b6b96fa6d8422de
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 41%

---


# Permisos personalizados {#custom-permissions}

Descubra cómo puede utilizar permisos personalizados para crear perfiles de permisos personalizados con permisos configurables para restringir el acceso a programas, canalizaciones y entornos para usuarios de Cloud Manager.

## Introducción {#introduction}

Cloud Manager tiene un conjunto de funciones predefinidas que regulan el acceso a las diversas funciones de Cloud Manager:

* Propietario del negocio
* Administrador de programa
* Administrador de implementación
* Desarrollador

Los permisos personalizados permiten a los usuarios crear perfiles de permisos personalizados con permisos configurables para restringir el acceso de los usuarios de Cloud Manager a programas, canalizaciones y entornos.

>[!TIP]
>
>Para obtener más información sobre las funciones predefinidas, consulte [Perfiles de equipo y producto de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md).

## Cómo utilizar los permisos personalizados {#using}

Para crear y utilizar sus propios permisos personalizados, se requieren tres pasos:

1. [Cree un perfil de producto.](#create)
1. [Asigne permisos personalizados al perfil del producto.](#assign-permissions)
1. [Asigne usuarios al perfil de producto.](#assign-users)

Esta sección detalla estos pasos. Puede que le resulte útil ver las secciones [Términos](#terms) y [Permisos configurables](#configurable-permissions) a medida que crea sus propios permisos personalizados.

>[!NOTE]
>
>Debe tener derechos de administrador de productos en Admin Console para Adobe Experience Manager as a Cloud Service para crear perfiles y administrar permisos para Cloud Manager.

### Crear un nuevo perfil de producto {#create}

Cree primero un perfil de producto antes del cual pueda asignar permisos personalizados.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. En la página de aterrizaje de Cloud Manager, selecciona el botón **Administrar acceso**.

![Botón Administrar acceso](assets/manage-access.png)

1. Se le redirigirá a la pestaña **Productos** de Admin Console, donde puede administrar usuarios y permisos para Cloud Manager. En el Admin Console, seleccione el botón **Nuevo perfil**.

![Botón Nuevo perfil](assets/admin-console-new-profile.png)

1. Proporcione los detalles generales sobre el perfil.

   * **Nombre del perfil del producto**: un nombre descriptivo para el perfil
   * **Nombre para mostrar** - Un nombre abreviado que se muestra en la interfaz de usuario (opciones)
   * **Descripción**: una descripción informativa del perfil en la que se explique su finalidad (opcional)
   * **Notificar a los usuarios por correo electrónico**: cuando se selecciona, se notifica a los usuarios por correo electrónico cuando se agregan o se eliminan de este perfil.

1. Seleccione **Guardar** cuando haya terminado.

El nuevo perfil de producto se guarda y es visible en la lista de perfiles de producto de Admin Console.

### Asignar permisos personalizados al perfil {#assign-permissions}

Ahora que tiene un nuevo perfil de producto, puede asignarle permisos personalizados.

1. En el Admin Console, seleccione el nombre del [nuevo perfil de producto que creó](#create).

1. En la ventana que se abre, seleccione la pestaña **Permisos** para ver una lista de permisos editables.

   ![Permisos editables](assets/permissions-tab.png)

1. Seleccione el vínculo **Editar** de un permiso para poder editarlo.

1. Se abre la ventana **Editar permiso**.
   * El permiso seleccionado en el paso anterior se selecciona en la columna izquierda.
   * Los elementos de permiso disponibles para la asignación del permiso se encuentran en la columna central denominada Elementos de **permisos disponibles**.
   * Los elementos de permisos asignados se encuentran en la columna derecha con la etiqueta **Elementos de permisos incluidos**.

   ![Editar elementos de permiso](assets/edit-permission-items.png)

1. Seleccione el icono de signo más (`+`) junto al elemento de permiso para poder agregarlo a la columna **Elementos de permisos incluidos**.

   * Seleccione el icono `i` que se encuentra junto a un elemento de permiso si desea obtener más información al respecto.

1. Seleccione el botón **Agregar todos** en la parte superior de la columna **Permisos disponibles** para que pueda agregar todos los permisos.

1. Seleccione **Guardar** cuando termine de definir los elementos de permiso para el nuevo perfil de producto.

El nuevo perfil de producto se guarda ahora con sus permisos personalizados.

### Asignar usuarios a los permisos personalizados {#assign-users}

Ahora puede asignar usuarios al nuevo perfil de producto que ha creado con permisos personalizados.

1. En el Admin Console, seleccione el nombre del [nuevo perfil de producto al que asignó permisos personalizados.](#assign-permissions)

1. En la ventana que se abre, seleccione la pestaña **Usuarios**.

1. Seleccione el botón **Agregar usuarios** y asigne usuarios a su nuevo perfil de productos con permisos personalizados.

Consulte la sección **Agregar usuarios y grupos de usuarios a un perfil de producto** del documento [Administrar perfiles de producto para usuarios empresariales](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html?lang=es) para obtener más información sobre cómo usar el Admin Console.

## Permisos configurables {#configurable-permissions}

Los siguientes permisos están disponibles para crear perfiles personalizados.

| Permiso | Descripción |
|---|---|
| Creación de programa | Permitir que los usuarios creen un programa |
| Acceso al programa | Permitir que los usuarios tengan acceso a los programas |
| Edición del programa | Permitir que los usuarios editen programas |
| Crear entorno | Permitir que los usuarios creen un entorno |
| Edición de entorno | Permitir que los usuarios actualicen y editen entornos |
| Registros de entorno leídos | Permitir que los usuarios lean los registros del entorno |
| Administrar variables de entorno | Permitir que los usuarios creen, editen o eliminen configuraciones de entorno |
| Entorno Restaurar crear | Permitir que los usuarios creen una restauración del entorno |
| Restablecimiento rápido del entorno de desarrollo | Permitir a los usuarios restablecer el entorno de desarrollo rápido |
| Administración de copia de contenido | Permitir que los usuarios administren las operaciones de copia de contenido |
| Creación de canalización | Permitir que los usuarios creen canalizaciones |
| Eliminación de canalización | Permitir que los usuarios eliminen canalizaciones |
| Edición de canalizaciones | Permitir que los usuarios editen canalizaciones |
| Aprobar/Rechazar implementaciones de producción | Permitir que los usuarios aprueben o rechacen un paso de implementación de producción |
| Cancelar ejecuciones de canalización | Permitir a los usuarios cancelar las ejecuciones de canalización |
| Iniciar ejecuciones de canalizaciones | Permitir que los usuarios inicien una nueva ejecución de canalización |
| Anular/Rechazar errores de métricas importantes | Permitir que los usuarios anulen o rechacen errores importantes de métricas |
| Programar implementaciones de producción | Permitir a los usuarios programar un paso de implementación de producción |
| Acceso a información de repositorios | Permitir a los usuarios acceder a la información del repositorio y generar una contraseña de acceso |
| Creación de repositorios | Permitir que los usuarios creen repositorios de Git |
| Eliminación de repositorios | Permitir que los usuarios eliminen repositorios de Git |
| Edición de repositorios | Permitir que los usuarios editen repositorios de Git |
| Generación de código de repositorios | Permitir que los usuarios generen proyectos a partir de arquetipos |
| Administrador de nombres de dominio | Permitir que los usuarios creen, editen o eliminen nombres de dominio |
| Administrar Lista de permitidos IP | Permitir a los usuarios crear, editar o eliminar enlaces de lista de permitidos y lista de permitidos IP |
| Administrador de infraestructura de red | Permitir a los usuarios crear, editar o eliminar la infraestructura de red |
| Administrador de certificados SSL | Permitir a los usuarios crear, editar o eliminar certificados SSL |
| Administrador de usuarios de subcuenta de New Relic | Permitir a los usuarios leer o editar usuarios de subcuentas de New Relic |

### Permisos de nivel de organización {#organization-level}

Los permisos de nivel de organización hacen referencia a permisos que siempre se conceden a todos los programas de una organización.

Los siguientes permisos son permisos de nivel de organización:

* **Creación de programa**: este permiso permite a los usuarios crear un programa en la organización.
* **Acceso a información de repositorio** Este permiso de nivel de inquilino/organización permite a los usuarios generar un nombre de usuario, una contraseña y una URL de repositorio para acceder y contribuir en un proyecto de cliente.
   * El nombre de usuario y la contraseña para acceder al repositorio son comunes en todos los repositorios de la organización, pero la URL del repositorio es única para cada programa.
   * Consulte [Acceder a repositorios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) para obtener más información.

## Términos {#terms}

Los siguientes términos se utilizan para crear y administrar permisos personalizados y funciones predefinidas.

| Término | Descripción |
|---|---|
| Permisos predefinidos | Funciones predefinidas como **Propietario empresarial** y **Administrador de implementación** para regular varias funciones de Cloud Manager. Para obtener más información sobre las funciones predefinidas, consulte [Perfiles de equipo y producto de AEM as a Cloud Service.](/help/onboarding/aem-cs-team-product-profiles.md) |
| Permisos personalizados | Las funciones de Cloud Manager permiten a los usuarios crear perfiles de permisos para definir funciones que rigen las funciones compatibles con Cloud Manager |
| Perfil del producto | Se crea en el Admin Console para administrar los permisos configurables que se aplican a los usuarios que forman parte del perfil de permisos |
| Permiso configurable | Permisos de Cloud Manager que se pueden configurar en el perfil de permisos |
| Elemento de permiso | Un programa, entorno o recurso de canalización en el que se puede aplicar un permiso |

Los elementos de permisos hacen referencia al ámbito donde se aplica el permiso. Normalmente, es una de las siguientes:

| Tipo de elemento de permiso | Ejemplos | Descripción |
|---|---|---|
| Organización | organization:companyA | Todos los recursos aplicables de una organización. Un recurso puede ser un programa, un entorno o una canalización. Si el usuario agrega una organización para cualquier permiso, todos los recursos nuevos de esa organización también tendrán ese permiso. |
| Programa | Programa A | Todos los recursos aplicables de un programa |
| Entorno | Programa A: entorno | Aplicable en un entorno específico |
| Canalización | Programa A: canalización | Aplicable en una canalización específica |

## Restricciones {#limitations}

Tenga en cuenta las siguientes limitaciones al utilizar permisos personalizados.

* El perfil de permisos personalizados también enumera los programas, entornos y canalizaciones de AMS al configurar los permisos.
* Los recursos como programa, entorno y canalización creados en Cloud Manager pueden tardar dos minutos en mostrarse en Admin Console para la configuración de permisos.
* En casos excepcionales en los que el servicio de permisos personalizados no responde, los perfiles predefinidos siguen estando disponibles y teniendo el acceso adecuado.

## Preguntas frecuentes {#faq}

### ¿Qué perfiles de permisos son los predefinidos?

* Propietario del negocio
* Administrador de programa
* Administrador de implementación
* Desarrollador

Para obtener más información sobre las funciones predefinidas, consulte [Perfiles de equipo y producto de AEM as a Cloud Service.](/help/onboarding/aem-cs-team-product-profiles.md)

### ¿Qué les sucede a los perfiles de permiso predefinidos con introducción a los perfiles personalizados?

Los perfiles de producto predeterminados y las funciones de Cloud Manager siguen funcionando igual que antes.

### ¿Puedo editar perfiles de permisos predefinidos?

No, los perfiles predeterminados no se pueden editar. No puede añadir ni quitar permisos al perfil de permisos predeterminado. Solo puede añadir o quitar usuarios de perfiles predefinidos.

### ¿Debería eliminar los perfiles de permiso predefinidos, ya que los perfiles personalizados ya están disponibles?

No elimine perfiles de permiso predefinidos del Admin Console.

### ¿Puedo añadir usuarios a varios perfiles de permisos?

Sí, un usuario puede formar parte de varios perfiles, incluidos perfiles de permisos predefinidos y personalizados. Cuando se asigna a un usuario a varios perfiles, los permisos combinados de todos los perfiles de permiso asignados están disponibles para ese usuario.

### ¿Qué sucede si un usuario tiene permiso para editar un entorno o canalización, pero no tiene acceso a un programa que contenga el entorno o canalización?

En este caso, el usuario no puede acceder al entorno o la canalización si no tiene los permisos de **Acceso al programa** que contienen el entorno o la canalización.
