---
title: Configuración del asistente de IA en Adobe Experience Manager
description: Obtenga información sobre cómo configurar el asistente de IA mediante Admin Console en Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: a7f3dc14-29f7-473a-9870-d52393e6fa6e
source-git-commit: e853e7b46c762ab724d5eecb344897a83e4fb724
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# Configuración del asistente de IA en Adobe Experience Manager {#aem-ai-asst-admin-setup}

Un administrador debe configurar el acceso, los permisos y la configuración para que los usuarios de su organización puedan utilizar las funciones del asistente de IA de AEM (Adobe Experience Manager).

El proceso de configuración del Asistente de IA de AEM consta de los siguientes pasos:

1. [Crear un nuevo perfil de producto en Adobe Admin Console](#create-profile).
1. [Habilite el permiso Conocimiento del producto del Asistente para IA](#enable-permission).
1. [Crear un nuevo grupo de usuarios (o usar uno existente)](#create-user-group).
1. [Agregar usuarios al grupo](#add-users).
1. [Asigne el perfil de producto al grupo de usuarios](#assign-product-profile).

**Requisitos previos**

Antes de empezar, asegúrese de cumplir los siguientes requisitos previos:

* Debe tener derechos de administrador de productos como mínimo en Adobe Admin Console.
* Tiene una comprensión de la estructura de administración de usuarios de su organización.

**Consideraciones de configuración**

* Tiempo de procesamiento: Los recursos creados en Cloud Manager pueden tardar hasta 2 minutos en mostrarse en Admin Console para la configuración de permisos.
* Múltiples perfiles: los usuarios pueden formar parte de varios perfiles y los permisos se combinan de todos los perfiles asignados.
* Ámbito de organización: algunos permisos pueden aplicarse en el nivel de organización en todos los programas.
* Perfiles predefinidos: no elimine perfiles de permiso predefinidos de Admin Console.


## 1 - Crear un nuevo perfil de producto en Adobe Admin Console{#create-profile}

1. Siga las instrucciones detalladas de [Crear un nuevo perfil de producto en Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) que se encuentra en la documentación de Experience Platform.

1. Al crear el nuevo perfil de producto, puede utilizar los siguientes valores sugeridos para el asistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nombre del perfil del producto | `AEM AI Assistant` (o su nombre descriptivo preferido) |
   | Nombre para mostrar (opcional) | `AI Assistant` |
   | Descripción (opcional) | `Product profile for managing AEM AI Assistant access` |
   | Notificación | Configure en función de las preferencias de su organización |


## 2 - Habilite el permiso Conocimiento del producto del asistente de IA{#enable-permission}

El proceso de asignación de permisos personalizados a perfiles de producto sigue el flujo de trabajo estándar de permisos personalizados de Adobe Cloud Manager.

Artículo de referencia: [Asignar permisos personalizados al nuevo perfil de producto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. En Admin Console, haga clic en el nombre del perfil de producto recién creado (`AEM AI Assistant`)

   ![Captura de pantalla](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. Para ver la lista de permisos editables, haga clic en la ficha **Permisos**.

1. En la lista de la tabla, busque el permiso `AI Assistant Product Knowledge`.

   ![Pestaña Permisos del asistente de IA en Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. A la derecha del nombre del permiso, haga clic en ![Icono de lápiz o Editar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. En la página **Editar permisos para el asistente de IA**, active la opción **Conocimiento del producto del asistente de IA**.

   ![Editar página de permisos para la opción de alternancia Conocimiento del producto del Asistente de IA](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.

   El perfil de producto ahora tiene habilitado el permiso Conocimiento del producto del asistente de IA.


## 3 - Crear un grupo de usuarios nuevo (o usar uno existente){#create-user-group}

1. Realice una de las siguientes acciones:

>[!BEGINTABS]

>[!TAB Crear un nuevo grupo de usuarios]

1. En Admin Console, haga clic en **Usuarios** > **Grupos de usuarios**.

   ![Grupos de usuarios](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. En la página **Grupos de usuarios**, haga clic en **Nuevo grupo de usuarios**.

   ![Botón Nuevo grupo de usuarios en la página Grupos de usuarios](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. En la página **Crear un nuevo grupo de usuarios**, proporcione la siguiente información:

   | Opción | Valor sugerido |
   | --- | --- |
   | Nombre del grupo de usuarios | `AEM AI Assistant` (o su nombre preferido) |
   | Descripción (opcional) | `User group for managing AEM AI Assistant access` |

   ![Crear una nueva página de grupo de usuarios](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.

>[!TAB Usar un grupo de usuarios existente]

Puede utilizar un grupo de usuarios de AEM existente si cumple los requisitos de acceso del Asistente de IA, en lugar de crear un nuevo grupo.

>[!ENDTABS]

## 4 - Añadir usuarios al grupo de usuarios{#add-users}

1. Realice una de las siguientes acciones:

>[!BEGINTABS]

>[!TAB Agregar usuarios individuales]

1. En la página **Grupos de usuarios**, en la tabla **Nombre de grupo**, haga clic en el nombre del grupo de usuarios que acaba de crear o en un nombre de grupo de usuarios existente.

   ![Página de grupos de usuarios que muestra el nombre del grupo de usuarios del Asistente de IA de AEM en la tabla](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. En la página **Grupos de usuarios** del **Asistente de IA de AEM**, haga clic en la ficha **Usuarios** y, a continuación, haga clic en **Agregar usuarios**.

   ![La página de grupos de usuarios del Asistente de IA de AEM, que muestra la pestaña Usuarios y la botón Agregar usuarios](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. En la página **`Add users to this user group`**, busque y seleccione usuarios que necesiten acceso al Asistente de IA de AEM.

   ![Agregar usuarios a esta página de grupo de usuarios](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.
1. Ahora, asigne el perfil de producto al grupo de usuarios [#assign-product-profile).

>[!TAB Agregar usuarios de forma masiva]

Puede utilizar la función de carga masiva en Admin Console.

1. Prepare un archivo CSV con información de usuario.
1. Utilice la opción **`Add users by CSV`** para una adición masiva eficiente.
1. Ahora, asigne el perfil de producto al grupo de usuarios [#assign-product-profile).

>[!ENDTABS]


## 5 - Asignar el perfil de producto al grupo de usuarios{#assign-product-profile}

Este paso sigue el flujo de trabajo estándar de Adobe Admin Console para asignar perfiles de producto a grupos de usuarios.

Artículo de referencia: [Administrar perfiles de producto para usuarios empresariales](https://helpx.adobe.com/es/enterprise/using/manage-product-profiles.html?lang=es)

1. Mientras sigue en el grupo de usuarios del Asistente de IA de AEM desde [4 - Agregar usuarios al grupo de usuarios](#add-users), haga clic en la ficha **Perfiles de producto asignados**.
1. Haga clic en **Asignar perfil**.

   ![Página del grupo de usuarios del Asistente de IA de AEM con la ficha Perfiles de producto asignados seleccionada](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. En la página **Asignar productos y perfiles**, en el cuadro de diálogo **Seleccionar perfiles de producto**, busque y seleccione su perfil de producto **Asistente de IA**.

   ![La página &quot;Asignar productos y perfiles&quot;, que muestra el cuadro de diálogo &quot;Seleccionar perfiles de producto&quot; y el perfil de producto &quot;Asistente de IA&quot; seleccionado](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. Cerca de la esquina inferior derecha del cuadro de diálogo, haga clic en **Aplicar**.
1. Cerca de la esquina inferior derecha de la página **Asignar productos y perfiles**, haga clic en **Guardar**.

   ![Se muestra el perfil de producto del Asistente de IA asignado al grupo de usuarios del Asistente de IA de AEM](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


## Compruebe la configuración

* Compruebe que el perfil de producto muestra el número correcto de grupos de usuarios asignados.
* Compruebe que el grupo de usuarios muestra el número correcto de usuarios.
* Confirme que el permiso Conocimiento del producto del asistente de IA está habilitado y configurado correctamente.


## Prueba de la configuración

Haga que un usuario del grupo asignado haga lo siguiente:

1. Inicie sesión en AEM.
2. Compruebe que las funciones del Asistente de IA son accesibles.
3. Pruebe la funcionalidad del asistente de IA para garantizar una activación adecuada.

## Véase también

* [Control de acceso de Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
* [Permisos personalizados de Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md)


