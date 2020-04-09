---
title: Publicación de recursos, carpetas y colecciones en Brand Portal
description: Publique recursos, carpetas y colecciones en Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 4677a8771c5891b8c9846e0adb58025304a71bdd

---


# Publish assets to Brand Portal {#publish-assets-to-brand-portal}

Como administrador de Recursos Adobe Experience Manager (AEM), puede publicar recursos, carpetas y colecciones en la instancia de AEM Assets Brand Portal. Asimismo, puede programar el flujo de trabajo de publicación de un recurso o carpeta para una fecha u hora posterior. Una vez publicados, los usuarios de Brand Portal pueden acceder a los recursos, carpetas y colecciones y distribuirlos aún más a otros usuarios.

Sin embargo, primero debe configurar Recursos AEM con Brand Portal. Para obtener más información, consulte [Configuración de AEM Assets con Brand Portal](configure-aem-assets-with-brand-portal.md).

Si realiza las modificaciones posteriores en el recurso, la carpeta o la colección originales en Recursos AEM, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar desde Recursos AEM. Esta función garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

* [Publicación de recursos en Brand Portal](#publish-assets-to-bp)
* [Publicar carpetas en Brand Portal](#publish-folders-to-brand-portal)
* [Publicar colecciones en Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe recomienda la publicación escalonada, preferiblemente durante las horas no pico, para que el autor de AEM no ocupe recursos excesivos.


## Publish assets to Brand Portal {#publish-assets-to-bp}

A continuación se indican los pasos para publicar recursos de Recursos AEM en Brand Portal:

1. En la consola Recursos, abra la carpeta principal, seleccione todos los recursos que desee publicar y haga clic en la opción Publicación **** rápida de la barra de herramientas.

   ![publish2bp-2](assets/publish2bp.png)

1. A continuación se indican las dos formas de publicar recursos:
   * [Publicar ahora](#publish-to-bp-now) (Publicar recursos inmediatamente)
   * [Publicar más tarde](#publish-to-bp-later) (Programar la publicación de recursos)

### Publicar recursos ahora {#publish-to-bp-now}

Para publicar los recursos seleccionados en Brand Portal, realice una de las acciones siguientes:

* En la barra de herramientas, seleccione **[!UICONTROL Publicación]** rápida. A continuación, en el menú, haga clic en **[!UICONTROL Publicar en Brand Portal]**.

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

   Seleccione **[!UICONTROL Más adelante]** en **[!UICONTROL Programación]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Seleccione una fecha **[!UICONTROL de]** Activación y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

1. Seleccione una fecha **de** Activación y especifique la hora. Haga clic en **Siguiente**. 

1. Especifique un título **[!UICONTROL de]** flujo de trabajo en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Publicar posteriormente]**.

   ![publishworkflow](assets/publishworkflow.png)

Inicie sesión en la interfaz de Brand Portal para ver los recursos publicados (según la fecha u hora programadas).

![bp_landing_page](assets/bp_landing_page.png)


## Publish folders to Brand Portal {#publish-folders-to-brand-portal}

Puede publicar o cancelar la publicación de las carpetas de recursos inmediatamente o programarlas para una fecha u hora posterior.

### Publish folders to Brand Portal {#publish-folders-to-bp}

1. En la consola Recursos, seleccione las carpetas que desee publicar y haga clic en la opción Publicación **** rápida de la barra de herramientas.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar carpetas ahora**

   Para publicar las carpetas seleccionadas en Brand Portal, realice una de las acciones siguientes:

   * En la barra de herramientas, seleccione **[!UICONTROL Publicación]** rápida.

      En el menú, seleccione **[!UICONTROL Publicar en Brand Portal]**.

   * En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

      1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Publicar en Brand Portal]**.

         En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Ahora]**.

         Haga clic en **Siguiente.**

      1. Confirme su selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Publicar en Brand Portal]**.
   Aparece un mensaje que indica que la carpeta se ha puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver la carpeta publicada.

1. **Publicar carpetas más tarde**

   Para programar la publicación de las carpetas de recursos para una fecha u hora posterior:

   1. Seleccione las carpetas que desee programar para la publicación, seleccione **[!UICONTROL Administrar publicación]** en la barra de herramientas de la parte superior.
   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Publicar en Brand Portal]**.

      En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Más adelante]**.

   1. Seleccione una fecha **[!UICONTROL de]** Activación y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Confirme la selección en **[!UICONTROL Ámbito]**. Haga clic en **[!UICONTROL Siguiente]**. 

   1. Especifique un título de flujo de trabajo en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Publicar posteriormente]**.

      ![management eschedulepub](assets/manageschedulepub.png)

### Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

Puede eliminar cualquier carpeta de recursos publicada en Brand Portal cancelándola de la instancia de Recursos AEM. Después de cancelar la publicación de la carpeta original, su copia ya no estará disponible para los usuarios de Brand Portal.

Puede cancelar la publicación de las carpetas de recursos desde Brand Portal inmediatamente o programarlas para una fecha y hora posteriores.

Para cancelar la publicación de carpetas de recursos desde Brand Portal:

1. En la consola Recursos, seleccione las carpetas de recursos que desee publicar y haga clic en la opción **[!UICONTROL Administrar publicación]** de la barra de herramientas.

   ![publish2bp-1](assets/publish2bp.png)

1. **Cancelar la publicación de carpetas de recursos**

   Para cancelar inmediatamente la publicación de la carpeta de recursos seleccionada desde Brand Portal:

   1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. En **[!UICONTROL Acción]** , seleccione **[!UICONTROL Cancelar publicación en Brand Portal]**.

      En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Ahora]**.

      Haga clic en **[!UICONTROL Siguiente]**. 

   1. Confirme su selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Cancelar publicación desde Brand Portal]**.

      ![confirmar-cancelar publicación](assets/confirm-unpublish.png)

1. **Cancelar la publicación de carpetas de recursos más tarde**

   Para programar la cancelación de la publicación de una carpeta de recursos para una fecha y hora posteriores:

   1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**.

   1. En **[!UICONTROL Acción]**, seleccione **[!UICONTROL Cancelar publicación en Brand Portal]**.

      En **[!UICONTROL Programación]**, seleccione **[!UICONTROL Más adelante]**.

   1. Seleccione una fecha **[!UICONTROL de]** Activación y especifique la hora. Haga clic en **[!UICONTROL Siguiente]**. 

   1. Confirme la selección en **[!UICONTROL Ámbito]** y haga clic en **[!UICONTROL Siguiente]**.

   1. Especifique un título **[!UICONTROL de]** flujo de trabajo en **[!UICONTROL Flujos de trabajo]**. Haga clic en **[!UICONTROL Cancelar publicación posteriormente]**.

      ![flujos de trabajo sin publicar](assets/unpublishworkflows.png)

## Publish collections to Brand Portal {#publish-collections-to-brand-portal}

Puede publicar o cancelar la publicación de colecciones desde la instancia de nube de AEM Assets.

>[!NOTE]
>
>Los fragmentos de contenido no se pueden publicar en Brand Portal. Por lo tanto, si selecciona fragmentos de contenido en Recursos AEM, la acción **[!UICONTROL Publicar en Brand Portal]** no estará disponible.
>
>Si las colecciones que contienen fragmentos de contenido se publican desde Recursos AEM a Brand Portal, todo el contenido de la carpeta, excepto los fragmentos de contenido, se replicará en la interfaz de Brand Portal.


### Publicación de colecciones {#publish-collections}

A continuación se indican los pasos para publicar colecciones de Recursos AEM en Brand Portal:

1. En la interfaz de usuario de AEM Assets, haga clic en el logotipo de AEM.

1. From **Navigation** page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

1. En la consola **Colecciones** , seleccione las colecciones que desee publicar en Brand Portal.

   ![select_collection](assets/select_collection.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Publicar en Brand Portal]**.

1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Publicar]**.

1. Cierre el mensaje de confirmación.

   Inicie sesión en Brand Portal como administrador. La colección publicada está disponible en la consola Colecciones.

   ![colección publicada](assets/published_collection.png)

### Cancelar la publicación de colecciones {#unpublish-collections}

Puede eliminar cualquier colección publicada en Brand Portal cancelándola de su instancia de Recursos AEM. Después de cancelar la publicación de la colección original, los usuarios de Brand Portal ya no podrán acceder a su copia.

A continuación se indican los pasos para cancelar la publicación de una colección:

1. En la consola **Colecciones** de su instancia de Recursos AEM y seleccione la colección que desee cancelar la publicación.

   ![select_collection](assets/select_collection-1.png)

1. En la barra de herramientas, haga clic en el icono **[!UICONTROL Eliminar de Brand Portal]** .
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Cancelar publicación]**.
1. Cierre el mensaje de confirmación. La colección se elimina de la interfaz de Brand Portal.

Además de lo anterior, también puede publicar esquemas de metadatos, ajustes preestablecidos de imagen, facetas de búsqueda y etiquetas de Recursos AEM en Brand Portal.

* [Publicación de ajustes preestablecidos, esquemas y facetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte la documentación [de](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) Brand Portal para obtener más información.


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
