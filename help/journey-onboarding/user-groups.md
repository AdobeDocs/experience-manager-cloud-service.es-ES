---
title: Grupos de usuarios para notificaciones
description: Obtenga información sobre cómo crear un grupo de usuarios en el Admin Console para administrar la recepción de notificaciones de correo electrónico importantes.
feature: Onboarding
role: Admin, User, Developer
source-git-commit: b56bb15f8330deefc11d19e784e36590ef674dd8
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 1%

---


# Grupos de usuarios para notificaciones {#user-groups}

Obtenga información sobre cómo crear un grupo de usuarios en el Admin Console para administrar la recepción de notificaciones de correo electrónico importantes.

## Información general {#overview}

De vez en cuando, el Adobe debe ponerse en contacto con los usuarios en relación con sus entornos as a Cloud Service AEM. Además de las notificaciones internas del producto, el Adobe también utiliza ocasionalmente el correo electrónico para las notificaciones. Existen dos tipos de notificación de correo electrónico:

* **Notificación de incidente** - Estas notificaciones se envían durante un incidente o cuando el Adobe ha identificado un posible problema de disponibilidad con su entorno as a Cloud Service AEM.
* **Notificación dinámica** : estas notificaciones se envían cuando un miembro del equipo de asistencia de Adobe desea proporcionar orientación sobre una posible optimización o recomendación que pueda beneficiar a su entorno as a Cloud Service AEM.

Para que los usuarios correctos reciban estas notificaciones, debe configurar y asignar grupos de usuarios y describirlos en este documento.

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

1. Verá la lista de todos los perfiles de producto de Cloud Manager configurados.

   ![Crear grupo de usuarios](assets/cloud_manager_profiles.png)

1. Haga clic en **Nuevo perfil** y proporcione los siguientes detalles:

   * **Nombre del perfil del producto**: `Incident Notification - Cloud Service`
   * **Nombre para mostrar**: `Incident Notification - Cloud Service`
   * **Descripción**: Perfil de Cloud Manager para los usuarios que recibirán notificaciones durante un incidente o cuando el Adobe haya identificado un posible problema de disponibilidad con su entorno as a Cloud Service AEM

1. Haga clic en **Guardar**.

1. Haga clic en **Nuevo perfil** una vez más y proporcione los siguientes detalles:

   * **Nombre del perfil del producto**: `Proactive Notification - Cloud Service`
   * **Nombre para mostrar**: `Proactive Notification - Cloud Service`
   * **Descripción**: Perfil de Cloud Manager para los usuarios que recibirán notificaciones cuando un miembro del equipo de asistencia de Adobe desee proporcionar orientación sobre una posible optimización o recomendación relacionada con la configuración AEM entorno as a Cloud Service

1. Haga clic en **Guardar**.

Se crean los dos nuevos grupos de notificación.

>[!NOTE]
>
>Es importante que Cloud Manager **nombre del perfil de producto** es exactamente igual que se proporciona. Copie y pegue el nombre de perfil de producto proporcionado para evitar errores. Cualquier desviación o error ocasionará que las notificaciones no se envíen como desee.
>
>En caso de error o si los perfiles no se han definido, el Adobe notificará de forma predeterminada a los usuarios existentes asignados al **Desarrollador de Cloud Manager** o **Administrador de implementación** perfiles.

## Asignar los usuarios a los nuevos perfiles de producto de notificación {#add-users}

Ahora que se han creado los grupos, debe asignar los usuarios adecuados. Puede hacerlo al crear usuarios nuevos o al actualizar los existentes.

### Agregar nuevos usuarios a grupos {#new-user}

Siga estos pasos para agregar usuarios para los que aún no se han configurado los Federated ID.

1. Identifique a los usuarios que deben recibir notificaciones de incidente o dinámicas.

1. Inicie sesión en el Admin Console en [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) si todavía no ha iniciado sesión.

1. En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Usuarios](assets/product_services.png)

1. Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione la opción **Usuarios** en la barra de navegación superior, seleccione **Agregar usuario**. De lo contrario, vaya a la sección [Agregar usuarios existentes a grupos.](#existing-users)

   ![Usuarios](assets/cloud_manager_add_user.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea añadir y seleccione `Adobe ID` para el **Tipo de ID**.

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos** para comenzar la selección del producto.

1. Select **Adobe Experience Manager as a Cloud Service** y asignar uno o ambos de los nuevos grupos al usuario.

   * **Notificación de incidentes: Cloud Service**
   * **Notificación dinámica: Cloud Service**

1. Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido.

El usuario invitado recibirá ahora las notificaciones. Repita estos pasos para los usuarios de su equipo que desee que reciban notificaciones.

### Agregar usuarios existentes a grupos {#existing-user}

Siga estos pasos para agregar usuarios para los que ya existen Federated ID.

1. Identifique a los usuarios que deben recibir notificaciones de incidente o dinámicas.

1. Inicie sesión en el Admin Console en [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) si todavía no ha iniciado sesión.

1. En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

1. Seleccione el **Usuarios** en la barra de navegación superior.

1. Si el ID federado ya existe para el miembro del equipo al que desea agregar un grupo de notificación, localice ese usuario en la lista y haga clic en él. De lo contrario, vaya a la sección [Agregar nuevos usuarios a grupos.](#add-user)

1. En el **Productos** de la ventana de detalles del usuario, haga clic en el botón elipsis y, a continuación, seleccione **Editar**.

1. En el **Editar productos** haga clic en el botón lápiz situado debajo de la ventana **Seleccionar productos** para comenzar la selección del producto.

1. Select **Adobe Experience Manager as a Cloud Service** y asignar uno o ambos de los nuevos grupos al usuario.

   * **Notificación de incidentes: Cloud Service**
   * **Notificación dinámica: Cloud Service**

1. Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido.

El usuario invitado recibirá ahora las notificaciones. Repita estos pasos para los usuarios de su equipo que desee que reciban notificaciones.
