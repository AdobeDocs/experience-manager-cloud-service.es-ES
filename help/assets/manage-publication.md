---
title: Administrar publicación
description: Publicar o cancelar la publicación de recursos en Experience Manager Assets, Dynamic Media y Brand Portal
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 9%

---

# Administrar publicación en Experience Manager Assets {#manage-publication-in-aem}

Como [!DNL Adobe Experience Manager Assets] administrador, puede publicar recursos y carpetas que contengan recursos de la instancia de autor en [!DNL Experience Manager Assets], [!DNL Dynamic Media]y [!DNL Brand Portal]. Además, puede programar el flujo de trabajo de publicación de un recurso o carpeta para una fecha u hora posterior. Una vez publicados, los usuarios pueden acceder a los recursos y distribuirlos a otros usuarios. De forma predeterminada, puede publicar recursos y carpetas en [!DNL Experience Manager Assets]. Sin embargo, puede configurar [!DNL Experience Manager Assets] para habilitar la publicación en [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) y [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

Puede publicar o cancelar la publicación de recursos en el nivel de recurso o de carpeta mediante **[!UICONTROL Publicación rápida]** o **[!UICONTROL Administrar publicación]** en la [!DNL Experience Manager Assets] interfaz. Si realiza las modificaciones posteriores al recurso o la carpeta originales en [!DNL Experience Manager Assets], los cambios no se reflejarán en la instancia de publicación hasta que no vuelva a publicar desde [!DNL Experience Manager Assets]. Garantiza que los cambios en curso no estén disponibles en la instancia de publicación. En la instancia de publicación solo están disponibles los cambios aprobados publicados por un administrador.

* [Publicación de recursos mediante Publicación rápida](#quick-publish)
* [Publicar recursos mediante Administrar publicación](#manage-publication)
* [Publicar recursos más tarde](#publish-assets-later)
* [Publicar recursos en Dynamic Media](#publish-assets-to-dynamic-media)
* [Publicar recursos en Brand Portal](#publish-assets-to-brand-portal)
* [Limitaciones y sugerencias](#limitations-and-tips)

## Publicación de recursos mediante Publicación rápida {#quick-publish}

Publicación rápida permite publicar contenido inmediatamente en el destino seleccionado. En el [!DNL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desee publicar. Haga clic en **[!UICONTROL Publicación rápida]** en la barra de herramientas y seleccione destino en la lista desplegable donde desee publicar los recursos.

![Publicación rápida](assets/quick-publish-to-aem.png)

## Publicar recursos mediante Administrar publicación {#manage-publication}

Administrar publicación le permite publicar o cancelar la publicación del contenido desde y hacia el destino seleccionado, [añadir contenido](#add-content) a la lista de publicaciones desde el repositorio de DAM, [incluir configuración de carpeta](#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, y [programar publicación](#publish-assets-later) a una fecha u hora posterior.

En el [!DNL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desee publicar. Haga clic en **[!UICONTROL Administrar publicación]** en la barra de herramientas. Si no tiene [!DNL Dynamic Media] y [!DNL Brand Portal] configurado en su [!DNL Experience Manager Assets] Por ejemplo, solo puede publicar recursos y carpetas en [!DNL Experience Manager Assets].

![Administrar publicación](assets/manage-publication-aem.png)

Las siguientes opciones están disponibles en la [!UICONTROL Administrar publicación] interfaz:

* [!UICONTROL Acciones]
   * `Publish`: Publicar recursos y carpetas en el destino seleccionado
   * `Unpublish`: Cancelar la publicación de recursos y carpetas desde el destino

* [!UICONTROL Destino]
   * `Publish`: Publicar recursos y carpetas en [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Publicar recursos en [!DNL Dynamic Media]
   * `Brand Portal`: Publicar recursos y carpetas en [!DNL Brand Portal]

* [!UICONTROL Programación]
   * `Now`: Publicar recursos inmediatamente
   * `Later`: Publicar recursos en función de la variable `Activation` fecha y hora

Para continuar, haga clic en **[!UICONTROL Siguiente]**. Según la selección, la variable **[!UICONTROL Ámbito]** refleja diferentes opciones. Las opciones para **[!UICONTROL Añadir contenido]** y **[!UICONTROL Incluir configuración de carpeta]** solo están disponibles para la publicación de recursos y carpetas en [!DNL Experience Manager Assets] (`Destination: Publish`).

![Administrar ámbito de publicación](assets/manage-publication-aem-scope.png)

### Añadir contenido {#add-content}

Publicar en [!DNL Experience Manager Assets] le permite añadir más contenido (recursos y carpetas) a la lista de publicaciones. Puede agregar más activos o carpetas a la lista en los repositorios de dam. Haga clic en **[!UICONTROL Añadir contenido]** para añadir más contenido.

Puede agregar varios recursos desde una carpeta o agregar varias carpetas a la vez. Sin embargo, no se pueden agregar recursos de varias carpetas a la vez.

![Añadir contenido](assets/manage-publication-add-content.png)

### Incluir configuración de carpeta {#include-folder-settings}

De forma predeterminada, la publicación de una carpeta en [!DNL Experience Manager Assets] publica todos los recursos, subcarpetas y sus referencias.

Para filtrar el contenido de la carpeta que desea publicar, haga clic en **[!UICONTROL Incluir configuración de carpeta]**:

* `Include folder contents`

   * Habilitado: Se publican todos los recursos de la carpeta seleccionada, las subcarpetas (incluidos todos los recursos de las subcarpetas) y las referencias.
   * Deshabilitado: Solo se publican la carpeta seleccionada (vacía) y las referencias. Los recursos de la carpeta seleccionada no se publican.

* `Include folder contents` y `Include only immediate folder contents`

   Si se seleccionan ambas opciones, se publican todos los recursos de la carpeta seleccionada, las subcarpetas (vacías) y las referencias. Los recursos de las subcarpetas no se publican.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Incluir configuración de carpeta](assets/manage-publication-include-folder-settings.png)

Después de aplicar los filtros, haga clic en **[!UICONTROL OK]** y, a continuación, haga clic en **[!UICONTROL Publicación]**. Al hacer clic en el botón de publicación, aparece un mensaje de confirmación `Resource(s) have been scheduled for publication` aparece. Y los recursos y carpetas seleccionados (o) se publican en el destino definido en función del planificador (`Now` o `Later`). Inicie sesión en la instancia de publicación para comprobar que los recursos y las carpetas se han publicado correctamente.

![Publicar en AEM](assets/manage-publication-publish-aem.png)

En la ilustración anterior, puede ver diferentes valores para la variable **[!UICONTROL Publicar Target]** atributo. Recordemos el hecho de que ha elegido publicar para [!DNL Experience Manager Assets] (`Destination: Publish`). A continuación, ¿por qué muestra que solo se publican una carpeta y un recurso en `AEM`y los otros dos recursos se publican en ambas `AEM` y `Dynamic Media`?

Aquí, debe comprender la función de las propiedades de carpeta. Una carpeta **[!UICONTROL Modo de publicación de Dynamic Media]** tiene un papel importante en la publicación. Para ver las propiedades de una carpeta, seleccione una carpeta y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. Para un recurso, consulte las propiedades de su carpeta principal.

La tabla siguiente explica cómo se produce la publicación en función de los valores definidos **[!UICONTROL Destino]** y **[!UICONTROL Modo de publicación de Dynamic Media]**:

| [!UICONTROL Destino] | [!UICONTROL Modo de publicación de Dynamic Media] | [!UICONTROL Destino de publicación] | Contenido permitido |
| --- | --- | --- | --- |
| Publicación | Publicación selectiva | `AEM` | Recursos y/o carpetas |
| Publicación | Inmediato | `AEM` y `Dynamic Media` | Recursos y/o carpetas |
| Publicación | Tras la activación | `AEM` y `Dynamic Media` | Recursos y/o carpetas |
| Dynamic Media | Publicación selectiva | `Dynamic Media` | Assets |
| Dynamic Media | Inmediato | `None` | No se pueden publicar los recursos |
| Dynamic Media | Tras la activación | `None` | No se pueden publicar los recursos |

>[!NOTE]
>
>Solo los recursos se publican en [!DNL Dynamic Media].
>
>Publicación de una carpeta en [!DNL Dynamic Media] no es compatible.
>
>Si selecciona una carpeta (`Selective Publish`) y elija el [!DNL Dynamic Media] destino, la variable [!UICONTROL Publicar Target] reflejo de atributo `None`.


Cambiemos ahora el **[!UICONTROL Destino]** en el caso de uso anterior a **[!UICONTROL Dynamic Media]** y compruebe los resultados. Al hacerlo, solo el activo de `Selective Publish` se publica en [!DNL Dynamic Media]. Los activos de `Immediate` y `Upon Activation` las carpetas no se publican y reflejan `None`.

![Publicar en Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>If [!DNL Dynamic Media] no está configurado en el [!DNL Experience Manager Assets] y **[!UICONTROL Destino]** es **[!UICONTROL Publicación]**, los recursos y las carpetas siempre se publican en `AEM`.
>
>Publicar en [!DNL Brand Portal] es independiente de las propiedades de la carpeta. Todos los recursos, carpetas y colecciones se pueden publicar en Brand Portal. Consulte [publicar recursos en Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Si ha personalizado la variable [!DNL Manage Publication] , la personalización sigue funcionando con las funcionalidades existentes.
>
>Sin embargo, puede quitar la personalización existente para usar la nueva [!DNL Manager Publication] características.


## Publicar recursos más tarde {#publish-assets-later}

Para programar el flujo de trabajo de publicación de los recursos para una fecha u hora posterior:

1. En el [!UICONTROL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desea programar para la publicación.
1. Haga clic en **[!UICONTROL Administrar publicación]** en la barra de herramientas.
1. Haga clic en **[!UICONTROL Publicación]** from **[!UICONTROL Acción]** y, a continuación, seleccione **[!UICONTROL Destino]** donde desea publicar el contenido.
1. Seleccione **[!UICONTROL Más tarde]** en **[!UICONTROL Programación]**.
1. Seleccione un **[!UICONTROL Fecha de activación]** y especifique la fecha y la hora. Haga clic en **[!UICONTROL Siguiente]**.

   ![Flujo de trabajo Administrar publicación](assets/manage-publication-workflow.png)

1. En el **[!UICONTROL Ámbito]** , **[!UICONTROL Añadir contenido]** (si es necesario). Haga clic en **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Flujos de trabajo]** , especifique un título de flujo de trabajo. Haga clic en **[!UICONTROL Publicar más tarde]**.

   ![Título del flujo de trabajo](assets/manage-publication-workflow-title.png)

   Inicie sesión en la instancia de destino para verificar los recursos publicados (en función de la fecha u hora programadas).

## Publicar recursos en Dynamic Media {#publish-assets-to-dynamic-media}

Solo los recursos se publican en [!DNL Dynamic Media]. Sin embargo, el comportamiento de publicación difiere según las propiedades de la carpeta. Una carpeta puede tener **[!UICONTROL Modo de publicación de Dynamic Media]** configurado para publicación selectiva que puede ser cualquiera de las siguientes:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

El proceso de publicación de **[!UICONTROL Inmediato]** y **[!UICONTROL Tras la activación]** es coherente, sin embargo, diferente para **[!UICONTROL Publicación selectiva]**. Consulte [configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Cancelar la publicación de forma selectiva desde Dynamic Media o Experience Manager mediante Administrar publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Publicar recursos en Brand Portal {#publish-assets-to-brand-portal}

Puede publicar recursos, carpetas y colecciones en el [!DNL Experience Manager Assets Brand Portal] instancia.

* [Publicar recursos en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Publicar carpetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Publicar colecciones en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Limitaciones y sugerencias {#limitations-and-tips}

* La opción para [!UICONTROL Administrar publicación] solo está disponible para las cuentas de usuario que tienen permisos de replicación.
* Las carpetas vacías no se publican.
* Si publica un recurso que se está procesando, solo se publicará el contenido original. Faltan las representaciones. Espere a que se complete el procesamiento y, a continuación, publique o vuelva a publicar el recurso una vez finalizado el procesamiento.
* Al cancelar la publicación de un recurso complejo, cancele la publicación del recurso únicamente. Evite cancelar la publicación de las referencias, ya que otras fuentes publicadas pueden remitirlas.

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
