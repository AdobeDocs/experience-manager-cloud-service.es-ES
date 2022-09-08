---
title: Grupos de usuarios para notificaciones
description: Obtenga información sobre cómo crear un grupo de usuarios en el Admin Console para administrar la recepción de notificaciones de correo electrónico importantes.
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 93a5e1b8851353f368a01ea6b50265ec3f2de836
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# Grupos de usuarios para notificaciones {#user-groups}

Obtenga información sobre cómo crear un grupo de usuarios en el Admin Console para administrar la recepción de notificaciones de correo electrónico importantes.

## Información general {#overview}

De vez en cuando, el Adobe debe ponerse en contacto con respecto a sus entornos as a Cloud Service AEM. Además de la notificación interna del producto, el Adobe también utiliza ocasionalmente el correo electrónico para estas notificaciones. Existen dos tipos de notificación:

* **Notificación de incidentes: Cloud Service** - Estas notificaciones se envían durante un incidente o cuando el Adobe ha identificado un posible problema de disponibilidad con su entorno as a Cloud Service AEM.
* **Cloud Service de notificaciones dinámicas** : estas notificaciones se envían cuando un miembro del equipo de asistencia de Adobe desea proporcionar orientación sobre una posible optimización o recomendación que pueda beneficiar a su entorno as a Cloud Service AEM.

Para que los usuarios correctos reciban estas notificaciones, debe configurar los grupos de usuarios.

## Requisitos previos {#prerequisites}

Debido a que los grupos de usuarios se crean y mantienen en el Admin Console, antes de crear grupos de usuarios para las notificaciones, debe:

* Tiene permisos para agregar y editar miembros de grupos.
* Tener un perfil de Adobe Admin Console válido.

## Crear nuevos perfiles de producto de Cloud Manager {#create-groups}

Para configurar correctamente la recepción de notificaciones, deberá crear dos grupos de usuarios. Estos pasos deben realizarse una sola vez.

1. Inicie sesión en el Admin Console en [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Grupos de usuarios](assets/products_services.png)

1. Vaya a la **Cloud Manager** de la lista de todas las instancias.

   ![Crear grupo de usuarios](assets/cloud_manager_instance.png)

1. Verá la lista de todos los perfiles de producto de Cloud Manager configurados. Por ejemplo:

   ![Crear grupo de usuarios](assets/cloud_manager_profiles.png)

1. Haga clic en **Nuevo perfil** e introduzca los siguientes detalles:

   * Nombre del perfil de producto: Notificación de incidentes: Cloud Service
   * Nombre para mostrar: Notificación de incidentes: Cloud Service
   * Descripción: Perfil de Cloud Manager para los usuarios que recibirán notificaciones durante un incidente o cuando el Adobe haya identificado un posible problema de disponibilidad con su entorno as a Cloud Service AEM.

1. Haga clic en **Guardar** y repita el paso 5 con los siguientes detalles:

   * Nombre del perfil de producto: Notificación dinámica: Cloud Service
   * Nombre para mostrar: Notificación dinámica: Cloud Service
   * Descripción: Perfil de Cloud Manager para los usuarios que recibirán notificaciones cuando un miembro del equipo de asistencia de Adobe desee proporcionar orientación sobre una posible optimización o recomendación relacionada con la configuración de entorno as a Cloud Service de su AEM.

>[!NOTE]
>
>Es importante que el nombre del perfil de Cloud Manager sea exactamente el mismo que el anterior. Copie y pegue el nombre del perfil del producto de la descripción proporcionada. Cualquier desviación o error ocasionará que las notificaciones no se envíen como desee. En caso de error o si no se han definido perfiles, el Adobe notificará de forma predeterminada a los usuarios existentes asignados a los perfiles de Cloud Manager Developer (ya sea o , o , y) Deployment Manager.

## Asignar los usuarios a los nuevos perfiles de producto de notificación {#add-users}

Ahora que se han creado los grupos, debe asignar los usuarios adecuados. Puede hacerlo al crear usuarios nuevos o al actualizar los existentes.

### Agregar nuevos usuarios a grupos {#new-user}

1. Identifique a los usuarios que deben recibir notificaciones de incidentes o proactivas.

1. Inicie sesión en el Admin Console en [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) si todavía no ha iniciado sesión.

1. En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Usuarios](assets/product_services.png)

1. Seleccione el **Usuarios** en la barra de navegación superior, seleccione **Agregar usuario**.

![Usuarios](assets/cloud_manager_add_user.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione Adobe ID para el tipo de ID.
   * Si el usuario ya existe, consulte el paso 9.

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Notificación de incidentes: Cloud Service** o **Notificación dinámica: Cloud Service**, o ambas al usuario.

1. Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado recibirá ahora las notificaciones.

1. Repita estos pasos para los usuarios de su equipo que desee que reciban las notificaciones.

1. En caso de que el usuario ya exista, busque el nombre del usuario y:

   * Haga clic en el nombre del usuario.
   * En el **Productos** , haga clic en **Editar**.
   * Haga clic en el botón Lápiz en el botón **Seleccionar productos** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Notificación de incidentes: Cloud Service** o **Notificación dinámica: Cloud Service**, o ambas al usuario.
   * Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado recibirá ahora las notificaciones.
