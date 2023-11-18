---
title: Administrar publicación
description: Publicar o cancelar la publicación de recursos en Experience Manager Assets, Dynamic Media y Brand Portal
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 6%

---

# Administrar publicación en Experience Manager Assets {#manage-publication-in-aem}

Como un [!DNL Adobe Experience Manager Assets] administrador, puede publicar recursos y carpetas que contengan recursos de su instancia de autor en [!DNL Experience Manager Assets], [!DNL Dynamic Media], y [!DNL Brand Portal]. Además, puede programar la publicación de un recurso o una carpeta en una fecha u hora posterior. Una vez publicados, los usuarios pueden acceder a los recursos y distribuirlos a otros usuarios. De forma predeterminada, puede publicar recursos y carpetas en [!DNL Experience Manager Assets]. Sin embargo, puede configurar lo siguiente [!DNL Experience Manager Assets] para habilitar la publicación en [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) y [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

Puede publicar recursos o cancelar la publicación de estos en el nivel de recurso o carpeta mediante **[!UICONTROL Publicación rápida]** o **[!UICONTROL Administrar publicación]** opción disponible en el [!DNL Experience Manager Assets] interfaz. Si realiza las modificaciones posteriores al recurso o la carpeta originales en [!DNL Experience Manager Assets]Sin embargo, los cambios no se reflejarán en la instancia de publicación hasta que vuelva a publicar desde [!DNL Experience Manager Assets]. Garantiza que los cambios en curso no estén disponibles en la instancia de publicación. Solo los cambios aprobados publicados por un administrador están disponibles en la instancia de publicación.

* [Publicación de recursos mediante Publicación rápida](#quick-publish)
* [Publicar recursos mediante Administrar publicación](#manage-publication)
* [Publicar recursos más tarde](#publish-assets-later)
* [Publicación de recursos en Dynamic Media](#publish-assets-to-dynamic-media)
* [Publicar recursos en Brand Portal](#publish-assets-to-brand-portal)
* [Solicitar publicación](#request-publication)
* [Limitaciones y sugerencias](#limitations-and-tips)

## Publicación de recursos mediante Publicación rápida {#quick-publish}

Publicación rápida permite publicar inmediatamente el contenido en el destino seleccionado. Desde el [!DNL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desee publicar. Clic **[!UICONTROL Publicación rápida]** en la barra de herramientas, seleccione un destino en la lista desplegable en el que desee publicar los recursos.

![Publicación rápida](assets/quick-publish-to-aem.png)

## Publicar recursos mediante Administrar publicación {#manage-publication}

Administrar publicación permite publicar o cancelar la publicación del contenido desde y hacia el destino seleccionado, [añadir contenido](#add-content) a la lista de publicaciones desde el repositorio de DAM, [incluir configuración de carpeta](#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, y [programar publicación](#publish-assets-later) hasta una fecha u hora posterior.

Desde el [!DNL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desee publicar. Clic **[!UICONTROL Administrar publicación]** de la barra de herramientas. Si no tiene [!DNL Dynamic Media] y [!DNL Brand Portal] configurado en su [!DNL Experience Manager Assets] Por ejemplo, solo puede publicar recursos y carpetas en [!DNL Experience Manager Assets].

![Administrar publicación](assets/manage-publication-aem.png)

Las siguientes opciones están disponibles en la [!UICONTROL Administrar publicación] interfaz:

* [!UICONTROL Acciones]
   * `Publish`: publique recursos y carpetas en el destino seleccionado
   * `Unpublish`: Cancele la publicación de recursos y carpetas desde el destino

* [!UICONTROL Destino]
   * `Publish`: Publicar recursos y carpetas en [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Publicar recursos en [!DNL Dynamic Media]
   * `Brand Portal`: Publicar recursos y carpetas en [!DNL Brand Portal]

* [!UICONTROL Programación]
   * `Now`: Publique los recursos inmediatamente
   * `Later`: publique recursos en función de `Activation` fecha u hora

Para continuar, haga clic en **[!UICONTROL Siguiente]**. En función de la selección, la variable **[!UICONTROL Ámbito]** refleja las distintas opciones. Las opciones para **[!UICONTROL Añadir contenido]** y **[!UICONTROL Incluir configuración de carpeta]** solo están disponibles para publicar los recursos y carpetas en [!DNL Experience Manager Assets] (`Destination: Publish`).

![Administrar ámbito de publicación](assets/manage-publication-aem-scope.png)

### Añadir contenido {#add-content}

Publicación en [!DNL Experience Manager Assets] permite añadir más contenido (recursos y carpetas) a la lista de publicación. Puede agregar más recursos o carpetas a la lista en los repositorios DAM. Clic **[!UICONTROL Añadir contenido]** para añadir más contenido.

Puede agregar varios recursos desde una carpeta o agregar varias carpetas a la vez. Pero no puede agregar recursos de varias carpetas a la vez.

![Añadir contenido](assets/manage-publication-add-content.png)

### Incluir configuración de carpeta {#include-folder-settings}

De forma predeterminada, publicar una carpeta en [!DNL Experience Manager Assets] publica todos los recursos, subcarpetas y sus referencias.

Para filtrar el contenido de la carpeta que desea publicar, haga clic en **[!UICONTROL Incluir configuración de carpeta]**:

* `Include folder contents`

   * Habilitado: se publican todos los recursos de la carpeta, las subcarpetas (incluidos todos los recursos de las subcarpetas) y las referencias seleccionadas.
   * Deshabilitado: solo se publican la carpeta seleccionada (vacía) y las referencias. Los recursos de la carpeta seleccionada no se publican.

* `Include folder contents` y `Include only immediate folder contents`

  Si se seleccionan ambas opciones, se publican todos los recursos de la carpeta, las subcarpetas (vacías) y las referencias seleccionadas. Los recursos de las subcarpetas no se publican.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Incluir configuración de carpeta](assets/manage-publication-include-folder-settings.png)

Después de aplicar los filtros, haga clic en **[!UICONTROL OK]** y haga clic en **[!UICONTROL Publish]**. Al hacer clic en el botón Publicar, aparece un mensaje de confirmación `Resource(s) have been scheduled for publication` aparece. Y los recursos y (o) carpetas seleccionados se publican en el destino definido en función del planificador (`Now` o `Later`). Inicie sesión en la instancia de publicación para comprobar que los recursos y las carpetas se han publicado correctamente.

![Publicar en AEM](assets/manage-publication-publish-aem.png)

En la ilustración anterior, puede ver diferentes valores para la variable **[!UICONTROL Destino de publicación]** atributo. Recordemos el hecho de que ha elegido publicar en [!DNL Experience Manager Assets] (`Destination: Publish`). A continuación, ¿por qué se muestra que solo se publican una carpeta y un recurso? `AEM`y los otros dos recursos se publican en ambos `AEM` y `Dynamic Media`?

En este caso, debe comprender la función de las propiedades de carpeta. Una carpeta de **[!UICONTROL Modo de publicación de Dynamic Media]** La propiedad desempeña un papel importante en la publicación. Para ver las propiedades de una carpeta, seleccione una carpeta y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. Para ver un recurso, consulte las propiedades de su carpeta principal.

En la tabla siguiente se explica cómo se produce la publicación en función del **[!UICONTROL Destino]** y **[!UICONTROL Modo de publicación de Dynamic Media]**:

| [!UICONTROL Destino] | [!UICONTROL Modo de publicación de Dynamic Media] | [!UICONTROL Destino de publicación] | Contenido permitido |
| --- | --- | --- | --- |
| Publicación | Publicación selectiva | `AEM` | Recursos y(o) carpetas |
| Publicación | Inmediato | `AEM` y `Dynamic Media` | Recursos y(o) carpetas |
| Publicación | Tras la activación | `AEM` y `Dynamic Media` | Recursos y(o) carpetas |
| Dynamic Media | Publicación selectiva | `Dynamic Media` | Assets |
| Dynamic Media | Inmediato | `None` | No se pueden publicar los recursos |
| Dynamic Media | Tras la activación | `None` | No se pueden publicar los recursos |

>[!NOTE]
>
>Solo se publican los recursos en [!DNL Dynamic Media].
>
>Publicación de una carpeta en [!DNL Dynamic Media] no es compatible.
>
>Si selecciona una carpeta (`Selective Publish`) y elija la [!DNL Dynamic Media] destino, el [!UICONTROL Destino de publicación] el atributo refleja `None`.


Ahora vamos a cambiar la **[!UICONTROL Destino]** en el caso de uso anterior para **[!UICONTROL Dynamic Media]** y compruebe los resultados. Al hacerlo, solo el activo de `Selective Publish` La carpeta se ha publicado en [!DNL Dynamic Media]. Los activos de `Immediate` y `Upon Activation` Las carpetas de no se publican y reflejan `None`.

![Publicar en Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>If [!DNL Dynamic Media] no está configurado en su [!DNL Experience Manager Assets] y la **[!UICONTROL Destino]** es **[!UICONTROL Publish]**, los recursos y carpetas siempre se publican en `AEM`.
>
>Publicación en [!DNL Brand Portal] es independiente de las propiedades de la carpeta. Todos los recursos, carpetas y colecciones se pueden publicar en Brand Portal. Consulte [publicación de recursos en Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Si ha personalizado la variable [!DNL Manage Publication] , la personalización seguirá funcionando con las funcionalidades existentes.
>
>Sin embargo, puede quitar la personalización existente para utilizar la nueva [!DNL Manager Publication] funciones.

## Publicar recursos más tarde {#publish-assets-later}

Para programar el flujo de trabajo de publicación de recursos para una fecha u hora posterior:

1. Desde el [!UICONTROL Experience Manager Assets] , vaya a la carpeta principal y seleccione todos los recursos o carpetas que desee programar para la publicación.
1. Clic **[!UICONTROL Administrar publicación]** de la barra de herramientas.
1. Clic **[!UICONTROL Publish]** de **[!UICONTROL Acción]** y, a continuación, seleccione **[!UICONTROL Destino]** donde desee publicar el contenido.
1. Seleccione **[!UICONTROL Más tarde]** en **[!UICONTROL Programación]**.
1. Seleccione un **[!UICONTROL Fecha de activación]** y especifique la fecha y la hora. Haga clic en **[!UICONTROL Siguiente]**.

   ![Administrar flujo de trabajo de publicación](assets/manage-publication-workflow.png)

1. En el **[!UICONTROL Ámbito]** pestaña, **[!UICONTROL Añadir contenido]** (si es necesario). Haga clic en **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Flujos de trabajo]** pestaña, especifique un título de flujo de trabajo. Haga clic en **[!UICONTROL Publicar más tarde]**.

   ![Título del flujo de trabajo](assets/manage-publication-workflow-title.png)

   Inicie sesión en la instancia de destino para verificar los recursos publicados (según la fecha u hora programadas).

## Publicación de recursos en Dynamic Media {#publish-assets-to-dynamic-media}

Solo se publican los recursos en [!DNL Dynamic Media]. Sin embargo, el comportamiento de publicación difiere según las propiedades de la carpeta. Una carpeta puede tener **[!UICONTROL Modo de publicación de Dynamic Media]** configurado para la publicación selectiva que puede ser cualquiera de las siguientes:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

El proceso de publicación para **[!UICONTROL Inmediato]** y **[!UICONTROL Tras la activación]** sin embargo, el modo es coherente para **[!UICONTROL Publicación selectiva]**. Consulte [configuración de la publicación selectiva en el nivel de carpeta en Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Cancelar la publicación selectiva de recursos desde Dynamic Media o Experience Manager mediante Administrar publicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Publicar o cancelar la publicación selectiva de recursos mediante resultados de búsqueda](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Publicar recursos en Brand Portal {#publish-assets-to-brand-portal}

Puede publicar recursos, carpetas y colecciones en [!DNL Experience Manager Assets Brand Portal] ejemplo.

* [Publicar recursos en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Publicar carpetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Publicar colecciones en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Solicitar publicación {#request-publication}

El `Request Publication` La opción ayuda a autenticar el flujo de trabajo de los recursos antes de publicarlos en [!DNL AEM] Entorno de recursos. [!DNL AEM] proporciona un nivel diferente de permisos a varios usuarios. Puede ser un *colaborador* que está cargando recursos, pero no puede publicarlos hasta que se verifiquen las cargas. Además, ser un *Administrador* puede administrar los flujos de trabajo de lectura y escritura de Assets.

La opción Solicitar publicación está disponible para los siguientes usuarios:

* **Colaborador:** Si es un usuario que puede contribuir a [!DNL AEM] Recursos, tendrá acceso limitado a la [!DNL AEM] Flujo de trabajo de recursos. `Manage publication` El botón está oculto para usted. Como colaborador, solo puede contribuir añadiendo recursos, pero no puede publicarlos ni tener acceso de lectura al flujo de trabajo.

* **Usuario de flujo de trabajo:** Este usuario no puede publicar recursos, pero tiene acceso de lectura al flujo de trabajo. Como usuario de flujo de trabajo, puede:
   * solicitar publicación
   * vista `Manage publication` botón
   * programe el flujo de trabajo y vea las opciones `schedule now` y `schedule later`

* **Administrador:** Como usuario del tipo administrador, puede administrar los pasos generales del flujo de trabajo para los recursos. `Manage publication` es visible para usted. Si el destino `publish` está seleccionado, puede programar un recurso más adelante para el paso del flujo de trabajo.

>[!NOTE]
>
>If [!DNL Dynamic Media] se selecciona como destino, el paso del flujo de trabajo se desactiva para **usuario de flujo de trabajo** y **administrador** usuarios.
>

## Limitaciones y sugerencias {#limitations-and-tips}

* `Manage publication` está disponible para los usuarios que tienen al menos permisos de lectura en el flujo de trabajo.
* Las carpetas vacías no se publican.
* Si publica un recurso que se está procesando, solo se publica el contenido original. Faltan las representaciones. Espere a que se complete el procesamiento y, a continuación, publique o vuelva a publicar el recurso una vez finalizado el procesamiento.
* Al cancelar la publicación de un recurso complejo, cancele la publicación solo del recurso. Evite cancelar la publicación de las referencias, ya que otras referencias pueden proceder de otros recursos publicados.
