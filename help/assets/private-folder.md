---
title: Carpetas privadas para compartir recursos
description: Obtenga información sobre cómo crear una carpeta privada en [!DNL Adobe Experience Manager Assets] y compartirlo con otros usuarios y asignarles varios privilegios.
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 7%

---

# Carpeta privada en [!DNL Adobe Experience Manager Assets] {#private-folder}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/private-folder.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Puede crear una carpeta privada en el [!DNL Adobe Experience Manager Assets] interfaz de usuario de disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. En función del nivel de privilegio que asigne, los usuarios pueden realizar varias tareas en la carpeta, por ejemplo, ver los recursos de la carpeta o editarlos.

>[!NOTE]
>
>La carpeta privada tiene al menos un miembro con la función Propietario.
>
>Para crear una carpeta privada, necesita lo siguiente `Read` y `Modify` permisos en la carpeta principal en la que se crea una carpeta privada. Si no es administrador, estos permisos no están habilitados de forma predeterminada en `/content/dam`. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas.

## Crear y compartir una carpeta privada  {#create-share-private-folder}

Para crear y compartir una carpeta privada:

1. En el [!DNL Assets] consola, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, seleccione **[!UICONTROL Carpeta]** en el menú.

   ![Crear carpeta de recursos](assets/create-folder.png)

1. En el **[!UICONTROL Crear carpeta]** diálogo, introduzca un `Title` y `Name` (opcional) para la carpeta.

   Seleccione el **[!UICONTROL Privado]** y haga clic en **[!UICONTROL Crear]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   Se crea una carpeta privada. Ahora puede [añadir recursos](add-assets.md#upload-assets) Vaya a la carpeta y comparta la carpeta con otros usuarios o grupos. La carpeta no será visible para ningún otro usuario hasta que la comparta y le asigne privilegios.

1. Para compartir la carpeta, seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.

1. En el **[!UICONTROL Propiedades de carpeta]** , seleccione un usuario o grupo de la página **[!UICONTROL Añadir usuario]** , asigne una función (`Viewer`, `Editor`, o `Owner`) en la carpeta privada y haga clic en **[!UICONTROL Añadir]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   Puede asignar varias funciones, como `Editor`, `Owner`, o `Viewer` al usuario con el que comparte la carpeta. Si asigna un `Owner` función para el usuario, el usuario tiene `Editor` privilegios en la carpeta. Además, el usuario puede compartir la carpeta con otros. Si asigna un `Editor` El usuario puede editar los recursos de su carpeta privada. Si asigna una función de visualizador, el usuario solo puede ver los recursos de la carpeta privada.

   >[!NOTE]
   >
   >La carpeta privada tiene al menos un miembro con `Owner` función. Por lo tanto, el administrador no puede quitar todos los miembros propietarios de una carpeta privada. Sin embargo, para eliminar los propietarios existentes (y el propio administrador) de la carpeta privada, el administrador debe agregar otro usuario como propietario.

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Según la función que asigne, al usuario se le asigna un conjunto de privilegios en la carpeta privada cuando inicia sesión en [!DNL Assets].
1. Clic **[!UICONTROL Ok]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido en su interfaz de usuario.

1. Clic [!UICONTROL Notificaciones] para abrir una lista de notificaciones.

   ![notificación](assets/notification-icon.png)

1. Haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

## Eliminación de carpeta privada {#delete-private-folder}

Puede eliminar una carpeta seleccionando la carpeta y [!UICONTROL Eliminar] en el menú superior o utilizando la tecla Retroceso en el teclado.

![eliminar opción en el menú superior](assets/delete-option.png)

>[!CAUTION]
>
>Si elimina una carpeta privada de CRXDE Lite, los grupos de usuarios redundantes quedan en el repositorio.

>[!NOTE]
>
>Si elimina una carpeta mediante el método anterior de la interfaz de usuario, también se eliminarán los grupos de usuarios asociados.
>
>Sin embargo, los grupos de usuarios redundantes, no utilizados y autogenerados se pueden eliminar del repositorio mediante `clean` en JMX en la instancia de autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
