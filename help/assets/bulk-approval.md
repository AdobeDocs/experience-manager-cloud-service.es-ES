---
title: Revisión de recursos en carpetas y colecciones
description: Configure flujos de trabajo de revisión para los recursos de una carpeta o una colección y compártala con revisores o socios creativos para buscar comentarios.
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 11%

---

# Revisión de recursos en carpetas y colecciones {#review-folder-assets-and-collections}

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
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Con Adobe Experience Manager Assets, puede establecer flujos de trabajo de revisión específicos para los recursos que se encuentran en una carpeta o en una colección. Puede compartirlo con revisores o socios creativos para que busquen sus comentarios. Puede asociar un flujo de trabajo de revisión a un proyecto o crear una tarea de revisión independiente.

Una vez compartidos los recursos, los revisores pueden aprobarlos o rechazarlos. Las notificaciones se envían en varias fases del flujo de trabajo para notificar a los destinatarios objetivo la finalización de diversas tareas. Por ejemplo, cuando comparte una carpeta o colección, el revisor recibe una notificación que le informa de que una carpeta o colección se ha compartido para su revisión.

Una vez que el revisor haya completado la revisión (aprueba o rechaza los recursos), recibirá una notificación de finalización de la revisión.

## Creación de una tarea de revisión para carpetas {#creating-a-review-task-for-folders}

1. En la interfaz de usuario de Assets, seleccione la carpeta para la que desea crear una tarea de revisión.
1. En la barra de herramientas, seleccione el icono **[!UICONTROL Crear tarea de revisión]** para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver el icono en la barra de herramientas, seleccione **[!UICONTROL Más]** y, a continuación, seleccione el icono.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]**, seleccione el proyecto al que desea asociar la tarea de revisión. De manera predeterminada, la opción **[!UICONTROL None]** está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la lista **[!UICONTROL Proyectos]**.

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]**.

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]**.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details](assets/task_details.png)

1. En la pestaña Advanced, introduzca una etiqueta para utilizar para crear el URI.

   ![nombre_revisión](assets/review_name.png)

1. Seleccione **[!UICONTROL Enviar]** y, a continuación, seleccione **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en [!DNL Experience Manager Assets] como aprobador y vaya a la interfaz de usuario de Assets. Para aprobar los recursos, seleccione el icono **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.

   ![notificación](assets/notification.png)

1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, seleccione **[!UICONTROL Revisar]**.
1. En la página **[!UICONTROL Revisar tarea]**, seleccione los recursos y el icono **[!UICONTROL Aprobar o rechazar]** que desee aprobar o rechazar, según corresponda.

   ![tarea_de_revisión](assets/review_task.png)

1. Seleccione el icono **[!UICONTROL Completar]** en la barra de herramientas. En el cuadro de diálogo, escriba un comentario y seleccione **[!UICONTROL Completar]** para confirmar.
1. Vaya a la interfaz de usuario de Assets y abra la carpeta. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   **Vista de tarjeta**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Vista de lista**

   ![review_status_listview](assets/review_status_listview.png)

## Creación de una tarea de revisión para colecciones {#creating-a-review-task-for-collections}

1. En la página Colecciones, seleccione la colección para la que desea crear una tarea de revisión.
1. En la barra de herramientas, seleccione el icono **[!UICONTROL Crear tarea de revisión]** para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver el icono en la barra de herramientas, seleccione **[!UICONTROL Más]** y, a continuación, seleccione el icono.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) En la lista **[!UICONTROL Proyecto]**, seleccione el proyecto al que desea asociar la tarea de revisión. De manera predeterminada, la opción **[!UICONTROL None]** está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la lista **[!UICONTROL Proyectos]**.

1. Escriba un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]**.

   >[!NOTE]
   >
   >Los miembros o grupos del proyecto seleccionado están disponibles como aprobadores en la lista **[!UICONTROL Asignar a]**.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details-collection](assets/task_details-collection.png)

1. Seleccione **[!UICONTROL Enviar]** y, a continuación, seleccione **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Inicie sesión en [!DNL Experience Manager Assets] como aprobador y vaya a la consola de Assets. Para aprobar los recursos, seleccione el icono **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.
1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, seleccione **[!UICONTROL Revisar]**.
1. Todos los recursos de la colección están visibles en la página de revisión. Seleccione los recursos y seleccione el icono **[!UICONTROL Aprobar/Rechazar]** para aprobar o rechazar recursos, según corresponda.

   ![review_task_collection](assets/review_task_collection.png)

1. Seleccione el icono **[!UICONTROL Completar]** en la barra de herramientas. En el cuadro de diálogo, escriba un comentario y seleccione **[!UICONTROL Completar]** para confirmar.
1. Vaya a la consola Colecciones y abra la colección. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   **Vista de tarjeta**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Vista de lista**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

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
