---
title: Configuración del asistente de IA en Adobe Experience Manager
description: Obtenga información sobre cómo configurar el asistente de IA mediante Admin Console en Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---

# Configuración del asistente de IA de AEM: configuración del administrador {#aem-ai-asst-admin-setup}

Un administrador debe configurar el acceso, los permisos y la configuración para que los usuarios de su organización puedan utilizar las funciones del Ayudante de IA de AEM. Este artículo describe cómo habilitar el Asistente de IA para su organización, configurar las credenciales necesarias y guardar los cambios de configuración.

**Información general sobre el proceso de configuración del Asistente de IA de AEM**

El proceso de configuración consta de los siguientes pasos:

1. Cree un nuevo perfil de producto en Adobe Admin Console.
1. Habilite el permiso &quot;Conocimiento del producto del asistente de IA&quot;.
1. Cree o utilice un grupo de usuarios existente.
1. Agregar usuarios al grupo de usuarios.
1. Asigne el perfil de producto al grupo de usuarios.

**Requisitos previos**

Antes de empezar, asegúrese de cumplir los siguientes requisitos previos:

* Debe tener derechos de administrador de productos como mínimo en Adobe Admin Console.
* Tiene una comprensión de la estructura de administración de usuarios de su organización.

## 1 - Crear un nuevo perfil de producto en Adobe Admin Console{#create-profile}

1. Siga las instrucciones detalladas de [Crear un nuevo perfil de producto en Adobe Admin Console](https://experienceleague.adobe.com/es/docs/experience-platform/access-control/ui/create-profile) encontró la documentación de Experience Platform.

1. Al crear el nuevo perfil de producto, utilice los siguientes ejemplos de los valores que puede utilizar para el asistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nombre del perfil del producto | `AEM AI Assistant` (o su nombre descriptivo preferido) |
   | Nombre para mostrar (opcional) | `AI Assistant` |
   | Descripción (opcional) | `Product profile for managing AEM AI Assistant access` |
   | Notificación | Configure en función de las preferencias de su organización |




## 2 - Habilitar el permiso &quot;Conocimiento del producto del asistente de IA&quot;{#enable-permission}

El proceso de asignación de permisos personalizados a perfiles de producto sigue el flujo de trabajo estándar de permisos personalizados de Adobe Cloud Manager.

Artículo de referencia: [Asignar permisos personalizados al nuevo perfil de producto](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

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


## 3 - Crear un grupo de usuarios (o usar un grupo de usuarios existente){#create-user-group}

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

1. En la página **Agregar usuarios a este grupo de usuarios**, busque y seleccione usuarios que necesiten acceso al Asistente de IA de AEM.

   ![Agregar usuarios a esta página de grupo de usuarios](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. En la esquina inferior derecha de la página, haga clic en **Guardar**.

>[!TAB Agregar usuarios de forma masiva]

Puede utilizar la función de carga masiva en Admin Console.

1. Prepare un archivo CSV con información de usuario.

1. Utilice la opción **Agregar usuarios mediante CSV** para realizar una adición masiva de forma eficaz.

>[!ENDTABS]




## 5 - Asignar el perfil de producto al grupo de usuarios{#assign-product-profile}




