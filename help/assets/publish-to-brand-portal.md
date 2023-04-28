---
title: Publicar recursos, carpetas y colecciones en Brand Portal
description: Publicar recursos, carpetas y colecciones en Brand Portal.
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution,Configuration
role: User
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 97%

---

# Publicar recursos en Brand Portal {#publish-assets-to-brand-portal}

Como administrador de recursos de Adobe Experience Manager (AEM), puede publicar recursos, carpetas y colecciones en la instancia Brand Portal de AEM Assets. Además, puede programar el flujo de trabajo de publicación de un recurso o carpeta para una fecha u hora posterior. Una vez publicados, los usuarios de Brand Portal pueden acceder a los recursos, carpetas y colecciones y distribuirlos a otros usuarios.

Sin embargo, primero debe configurar AEM Assets con Brand Portal. Para obtener más información, consulte [Configurar AEM Assets con Brand Portal](configure-aem-assets-with-brand-portal.md).

Si realiza las modificaciones posteriores al recurso, la carpeta o la colección originales en AEM Assets, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar desde AEM Assets. Esta función garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

* [Publicar recursos en Brand Portal](#publish-assets-to-bp)
* [Publicar carpetas en Brand Portal](#publish-folders-to-brand-portal)
* [Publicar colecciones en Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe recomienda la publicación escalonada, de preferencia durante las horas no pico, para que el autor de AEM no ocupe recursos excesivos.

## Publicar recursos en Brand Portal {#publish-assets-to-bp}

A continuación se indican los pasos para publicar recursos de AEM Assets en Brand Portal:

1. En la consola Assets, abra la carpeta principal, seleccione todos los recursos que desea publicar y haga clic en la opción **[!UICONTROL Publicación rápida]** en la barra de herramientas.

   ![publish2bp-2](assets/publish2bp.png)

1. A continuación se indican las dos formas de publicar recursos:
   * [Publicar ahora](#publish-to-bp-now) (Publica recursos inmediatamente)
   * [Publicar más tarde](#publish-to-bp-later) (Programa la publicación de recursos)

### Publicar recursos ahora {#publish-to-bp-now}

Para publicar los recursos seleccionados en Brand Portal, haga una de las acciones siguientes:

* En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Luego, en el menú, haga clic en **[!UICONTROL Publicar en Brand Portal]**.

* En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Publicar en Brand Portal]**.

      En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Ahora]**.

      Haga clic en **[!UICONTROL Siguiente]**. 

   2. Confirme su selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Publicar en Brand Portal]**.

Aparece un mensaje que indica que los recursos se han puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver los recursos publicados.

### Publicar recursos más tarde {#publish-to-bp-later}

Para programar la publicación de recursos en Brand Portal para una fecha u hora posterior:

1. Seleccione los recursos que desea programar para la publicación y haga clic en **[!UICONTROL Administrar publicación]** en la barra de herramientas de la parte superior.

1. En la página **[!UICONTROL Administrar publicación]** , seleccione **[!UICONTROL Publicar en Brand Portal]** desde **[!UICONTROL Acción]**.

   Seleccione **[!UICONTROL Más tarde]** en **[!UICONTROL Programación]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Seleccione una **[!UICONTROL Fecha de activación]** y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione una **Fecha de activación** y especifique la hora. Haga clic en **Siguiente**. 

1. Especifique un **[!UICONTROL título de flujo de trabajo]** en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Publicar más tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Inicie sesión en la interfaz de Brand Portal para ver los recursos publicados (según la fecha u hora programadas).

![bp_landingpage](assets/bp_landingpage.png)


## Publicar carpetas en Brand Portal {#publish-folders-to-brand-portal}

Puede publicar o cancelar la publicación de las carpetas de recursos inmediatamente o programarlas para una fecha u hora posterior.

### Publicar carpetas en Brand Portal {#publish-folders-to-bp}

1. En la consola Assets, seleccione las carpetas que desee publicar y haga clic en la opción **[!UICONTROL Publicación rápida]** en la barra de herramientas.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar carpetas ahora**

   Para publicar las carpetas seleccionadas en Brand Portal, haga una de las acciones siguientes:

   * En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

      En el menú, seleccione **[!UICONTROL Publicar en Brand Portal]**.

   * En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

      1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Publicar en Brand Portal]**.

         En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Ahora]**.

         Haga clic en **Siguiente.**

      1. Confirme su selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Publicar en Brand Portal]**.

   Aparece un mensaje que indica que la carpeta se ha puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver la carpeta publicada.

1. **Publicar carpetas más tarde**

   Para programar la publicación de las carpetas de recursos para una fecha u hora posterior:

   1. Seleccione las carpetas que desea programar para la publicación, seleccione **[!UICONTROL Administrar publicación]** en la barra de herramientas de la parte superior.
   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Publicar en Brand Portal]**.

      En **[!UICONTROL Programar]**, seleccione **[!UICONTROL Más tarde]**.

   1. Seleccione una **[!UICONTROL Fecha de activación]** y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Confirme la selección en **[!UICONTROL Ámbito]**. Haga clic en **[!UICONTROL Siguiente]**. 

   1. Especifique un título de flujo de trabajo en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Publicar más tarde]**.

      ![manageschedulepub](assets/manageschedulepub.png)

### Cancelar publicación desde Brand Portal {#unpublish-folders-from-brand-portal}

Puede eliminar cualquier carpeta de recursos publicada en Brand Portal cancelando la publicación de la instancia de AEM Assets. Después de cancelar la publicación de la carpeta original, su copia ya no estará disponible para los usuarios de Brand Portal.

Puede cancelar la publicación de las carpetas de recursos desde Brand Portal inmediatamente o programarlas para una fecha y hora posteriores.

Para cancelar la publicación de carpetas de recursos desde Brand Portal:

1. En la consola Assets, seleccione las carpetas de recursos que desea publicar y haga clic en la opción **[!UICONTROL Administrar publicación]** en la barra de herramientas.

   ![publish2bp-1](assets/publish2bp.png)

1. **Cancelar la publicación de carpetas de recursos**

   Para cancelar la publicación de la carpeta de recursos seleccionada de inmediato desde Brand Portal:

   1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Cancelar publicación en Brand Portal]**.

      En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Ahora]**.

      Haga clic en **[!UICONTROL Siguiente]**. 

   1. Confirme su selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Cancelar publicación desde Brand Portal]**.

      ![confirmar-cancelar publicación](assets/confirm-unpublish.png)

1. **Cancelar la publicación de carpetas de recursos más tarde**

   Para programar la cancelación de la publicación de una carpeta de recursos para una fecha y hora posteriores:

   1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Cancelar publicación en Brand Portal]**.

      En **[!UICONTROL Programar]**, seleccione **[!UICONTROL Más tarde]**.

   1. Seleccione una **[!UICONTROL Fecha de activación]** y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

   1. Confirme la selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Siguiente]**.

   1. Especifique un **[!UICONTROL título de flujo de trabajo]** en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Cancelar publicación más tarde]**.

      ![flujos de trabajo sin publicar](assets/unpublishworkflows.png)

## Publicar colecciones en Brand Portal {#publish-collections-to-brand-portal}

Puede publicar o cancelar la publicación de colecciones desde la instancia de nube de AEM Assets.

>[!NOTE]
>
>Los fragmentos de contenido no se pueden publicar en Brand Portal. Por lo tanto, si selecciona fragmentos de contenido en AEM Assets, la acción **[!UICONTROL Publicar en Brand Portal]** no estará disponible.
>
>Si las colecciones que contienen fragmentos de contenido se publican desde AEM Assets a Brand Portal, todo el contenido de la carpeta, excepto los fragmentos de contenido, se replicará en la interfaz de Brand Portal.

### Publicar colecciones {#publish-collections}

A continuación se indican los pasos para publicar colecciones de AEM Assets en Brand Portal:

1. En la interfaz de usuario de AEM Assets, haga clic en el logotipo de AEM.

1. En la página **Navegación**, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Colecciones]**.

1. En la consola **Colecciones**, seleccione las colecciones que desea publicar en Brand Portal.

   ![select_collection](assets/select_collection.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Publicar en Brand Portal]**.

1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Publicar]**.

1. Cierre el mensaje de confirmación.

   Inicie sesión en Brand Portal como administrador. La colección publicada está disponible en la consola Colecciones.

   ![colección publicada](assets/published_collection.png)

### Cancelar la publicación de colecciones {#unpublish-collections}

Puede eliminar cualquier colección publicada en Brand Portal cancelando la publicación de la instancia de AEM Assets. Después de cancelar la publicación de la colección original, la copia ya no estará disponible para los usuarios de Brand Portal.

A continuación se indican los pasos para cancelar la publicación de una colección:

1. En la consola **Colecciones** de su instancia de AEM Assets y seleccione la colección que desea cancelar la publicación.

   ![select_collection](assets/select_collection-1.png)

1. En la barra de herramientas, haga clic en el icono **[!UICONTROL Quitar de Brand Portal]** .
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Cancelar publicación]**.
1. Cierre el mensaje de confirmación. La colección se quita de la interfaz de Brand Portal.

Además de lo anterior, también puede publicar esquemas de metadatos, ajustes preestablecidos de imagen, facetas de búsqueda y etiquetas de AEM Assets en Brand Portal.

* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte la [documentación de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obtener más información.


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
