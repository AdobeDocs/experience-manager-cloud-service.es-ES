---
title: Carpetas privadas para compartir recursos
description: Obtenga información sobre cómo crear una carpeta privada en  [!DNL Adobe Experience Manager Assets] , compartirla con otros usuarios y asignarles varios privilegios.
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 10%

---

# Carpeta privada en [!DNL Adobe Experience Manager Assets] {#private-folder}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/private-folder.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Puede crear una carpeta privada en la interfaz de usuario de [!DNL Adobe Experience Manager Assets] que esté disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. En función del nivel de privilegio que asigne, los usuarios pueden realizar varias tareas en la carpeta, por ejemplo, ver los recursos de la carpeta o editarlos.

>[!NOTE]
>
>La carpeta privada tiene al menos un miembro con la función Propietario.
>
>Para crear una carpeta privada, necesita los permisos de `Read` y `Modify` en la carpeta principal en la que crea una carpeta privada. Si no es administrador, estos permisos no están habilitados de manera predeterminada en `/content/dam`. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas.

## Crear y compartir una carpeta privada  {#create-share-private-folder}

Para crear y compartir una carpeta privada:

1. En la consola [!DNL Assets], haga clic en el botón **[!UICONTROL Crear]** de la barra de herramientas y, a continuación, seleccione **[!UICONTROL Carpeta]** en el menú.

   ![Crear carpeta de recursos](assets/create-folder.png)

1. En el cuadro de diálogo **[!UICONTROL Crear carpeta]**, escriba un `Title` y `Name` (opcional) para la carpeta.

   Seleccione la casilla **[!UICONTROL Privado]** y haga clic en **[!UICONTROL Crear]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   Se crea una carpeta privada. Ahora puede [agregar recursos](add-assets.md#upload-assets) a la carpeta y compartirla con otros usuarios o grupos. La carpeta no será visible para ningún otro usuario hasta que la comparta y le asigne privilegios.

1. Para compartir la carpeta, selecciónela y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.

1. En la página **[!UICONTROL Propiedades de carpeta]**, seleccione un usuario o grupo de la lista **[!UICONTROL Agregar usuario]**, asigne un rol (`Viewer`, `Editor` o `Owner`) a su carpeta privada y haga clic en **[!UICONTROL Agregar]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   Puede asignar varios roles, como `Editor`, `Owner` o `Viewer` al usuario con el que comparte la carpeta. Si asigna un rol de `Owner` al usuario, este tiene privilegios de `Editor` en la carpeta. Además, el usuario puede compartir la carpeta con otros. Si asigna un rol `Editor`, el usuario puede editar los recursos de la carpeta privada. Si asigna una función de visualizador, el usuario solo puede ver los recursos de la carpeta privada.

   >[!NOTE]
   >
   >La carpeta privada tiene al menos un miembro con el rol `Owner`. Por lo tanto, el administrador no puede quitar todos los miembros propietarios de una carpeta privada. Sin embargo, para eliminar los propietarios existentes (y el propio administrador) de la carpeta privada, el administrador debe agregar otro usuario como propietario.

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Según la función que asigne, al usuario se le asignará un conjunto de privilegios en su carpeta privada cuando inicie sesión en [!DNL Assets].
1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido en su interfaz de usuario.

1. Haga clic en [!UICONTROL Notificaciones] para abrir una lista de notificaciones.

   ![notificación](assets/notification-icon.png)

1. Haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

## Eliminación de carpeta privada {#delete-private-folder}

Para eliminar una carpeta, selecciónela y seleccione la opción [!UICONTROL Eliminar] en el menú superior, o bien utilice la tecla Retroceso del teclado.

![eliminar opción en el menú superior](assets/delete-option.png)

>[!CAUTION]
>
>Si elimina una carpeta privada de CRXDE Lite, los grupos de usuarios redundantes quedan en el repositorio.

>[!NOTE]
>
>Si elimina una carpeta mediante el método anterior de la interfaz de usuario, también se eliminarán los grupos de usuarios asociados.
>
>Sin embargo, los grupos de usuarios redundantes, no utilizados y autogenerados se pueden eliminar del repositorio mediante el método `clean` en JMX en la instancia de autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

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
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
