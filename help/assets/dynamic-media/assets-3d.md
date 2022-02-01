---
title: Trabajar con recursos 3D en Dynamic Media
description: Aprenda a trabajar con recursos 3D en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 446edfd83affb062585dca81052575b73c2e796f
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 5%

---

# Trabajar con recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media permite cargar, administrar, ver y entregar recursos 3D como experiencias envolventes.

* Publicación con un solo clic (con **[!UICONTROL Publicación rápida]** en la barra de herramientas) de recursos 3D para generar una URL.
* Se ha optimizado la compatibilidad con la visualización de recursos 3D con el ajuste preestablecido interactivo de visualizador de dimensiones de alta calidad con tecnología de Adobe Dimension.
* El componente WCM de medios 3D le permite añadir fácilmente recursos 3D a sus [!DNL Adobe Experience Manager Sites] páginas.

No se requiere ninguna instalación adicional para utilizar recursos 3D en Dynamic Media.

![Zapato en 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatibles con Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos de archivo 3D.

Consulte también [Formatos 3D compatibles con Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary | Incluye los materiales y texturas como un único recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | *Compatibilidad únicamente con la ingesta; no hay visualización ni interacción disponibles.* USDZ es un formato 3D propietario que Safari o iOS pueden ver de forma nativa. |

<!-- >[!NOTE]
>
>The 3D Media WCM component and 3D preview on an asset's Details page is not compatible with the latest version of Chrome (97.x). Instead, to work with 3D assets, use Firefox or Safari, or use an earlier version of Chrome (96.x). UNHIDE 2/3/22 CQDOC-18921-->

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo está diseñada para ayudarle a poner en marcha rápidamente los recursos 3D en Dynamic Media.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que su [!DNL Experience Manager] el administrador ya ha habilitado y configurado los Cloud Services de Dynamic Media.

Consulte [Configuración de Cloud Services de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Cargar recursos 3D**

   * [Cargar los recursos 3D para utilizarlos en Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de archivo 3D compatibles con la carga en Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Administrar recursos 3D**

   * Organizar y buscar recursos 3D

      * [Organización de recursos digitales](/help/assets/organize-assets.md)
      * [Buscar recursos 3D](/help/assets/search-assets.md)
   * Ver recursos 3D

      * [Ver e interactuar con recursos 3D](#viewing-three-d-assets)
      * [Administrar el ajuste preestablecido de visualizador de dimensiones](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabajar con metadatos de recursos 3D

      * [Administrar metadatos de recursos digitales](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md)



1. **Publicar recursos 3D**

   * [Publicar recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visor Dimensional](#alternate-publish-methods)

## Acerca de la visualización y la interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo ver e interactuar con recursos 3D de dos formas diferentes: desde la página de detalles del recurso y desde el componente de medios 3D en Sitios.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, ampliar o reducir y recorrer el recurso 3D.

El tiempo que se tarda en abrir un recurso 3D en la vista de página Detalles del recurso depende de varios factores. Estos factores incluyen elementos como los siguientes:

* Ancho de banda del servidor.
* Latencias al servidor
* Complejidad de la imagen.

Además, las capacidades del equipo cliente (como una estación de trabajo, un portátil o un dispositivo táctil móvil) también son importantes de tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visualizador de dimensiones en el Editor de ajustes preestablecidos de visualizador para practicar la navegación por un recurso 3D sin necesidad de cargar primero cualquier archivo 3D. El ajuste preestablecido de visualizador de dimensiones tiene un recurso 3D integrado con el que puede interactuar.
>
>Consulte [Administrar ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

## Ver e interactuar con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D desde la página de detalles del recurso:**

1. Asegúrese de que ha cargado los recursos 3D en [!DNL Experience Manager].

   Consulte [Cargar los recursos 3D para utilizarlos en Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. De [!DNL Experience Manager], en el **[!UICONTROL Navegación]** página, seleccione **[!UICONTROL Assets > Archivos]**.
1. Cerca de la esquina superior derecha de la página, desde la **[!UICONTROL Ver]** lista desplegable, seleccione **[!UICONTROL Vista de tarjeta]**.
1. Vaya a un recurso 3D que desee ver.
1. Para abrir el recurso en la página Detalles, seleccione la tarjeta del recurso 3D.
1. En la página Detalles del recurso 3D, realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic y arrastre con el botón izquierdo. | Presione con un solo dedo y arrastre. |
   | **Panorámica de la cámara** | Desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos y arrastre. |
   | **Ampliar la cámara** | Entrada y salida de áreas en la escena 3D. | Rueda de desplazamiento. | Pellizque con dos dedos. |
   | **Vuelva a introducir la cámara** | Vuelva a introducir la cámara en un punto de un objeto de la escena 3D. | Hacer doble clic. | Toque dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable. |  |  |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa . |  |  |

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]** para volver a la página Recursos.

## Ver e interactuar con un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en **[!UICONTROL Editar]** no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede usar la variable **[!UICONTROL Vista previa]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Solo puede realizar esta tarea después de añadir un componente de medios 3D a una página web y asignar un recurso 3D al componente. Consulte [Añadir el componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page) y [Asignar un recurso 3D a un componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D dentro de un componente de medios 3D:**

1. Mientras una página web se encuentra en **[!UICONTROL Editar]** realice una de las siguientes acciones:

   * Cerca de la parte superior derecha de la página, haga clic en **[!UICONTROL Vista previa]** para especificar **[!UICONTROL Vista previa]** en el menú contextual.
   * Eliminar `/editor.html` desde la dirección URL de la página en el explorador.

Un recurso 3D totalmente interactivo, tal como se muestra en    ![Se muestra un recurso 3D dentro del componente de medios 3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Un recurso 3D totalmente interactivo, tal como se muestra en **[!UICONTROL Vista previa]** en el menú contextual.

1. Mientras **[!UICONTROL Vista previa]** realice una de las acciones siguientes:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic y arrastre con el botón izquierdo. | Presione con un solo dedo y arrastre. |
   | **Panorámica de la cámara** | Desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos y arrastre. |
   | **Ampliar la cámara** | Entrada y salida de áreas en la escena 3D. | Rueda de desplazamiento. | Pellizque con dos dedos. |
   | **Vuelva a introducir la cámara** | Vuelva a introducir la cámara en un punto de un objeto de la escena 3D. | Hacer doble clic. | Toque dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable. |  |  |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa . |  |  |

## Acerca del trabajo con el componente de medios 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente de medios 3D de Dynamic Media que puede usar en [!DNL Experience Manager Sites] para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Añadir el componente de medios 3D a la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Añadir el componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: Configuración del componente de medios 3D](#configuring-the-three-d-component)
* [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

## Añadir el componente de medios 3D a la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]**.
1. Vaya a la plantilla de página en la que desea habilitar el componente 3D y seleccione la plantilla.
1. Para abrir la plantilla, seleccione **[!UICONTROL Editar]**.
1. Cerca de la parte superior derecha de la página, en el menú desplegable, seleccione **[!UICONTROL Estructura]** , si no está activo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Para seleccionar un área vacía y abrir su barra de herramientas asociada, seleccione el área vacía en la **[!UICONTROL Contenedor de diseño]** región.
1. En la barra de herramientas, seleccione la opción **[!UICONTROL Política]** para abrir **[!UICONTROL Editor de directivas]**.
1. En el **[!UICONTROL Propiedades]** en la sección **[!UICONTROL Componentes permitidos]** , desplácese hasta **[!UICONTROL Dynamic Media]**, luego expanda la lista y marque **[!UICONTROL Medios 3D]**.
1. Toque **[!UICONTROL Listo]** para guardar los cambios y cerrar el **[!UICONTROL Editor de directivas]**.

   Ahora puede colocar el componente de medios 3D de Dynamic Media en todas las páginas que utilicen esta plantilla.

## Añadir el componente de medios 3D a una página web {#adding-the-three-d-media-component-to-a-web-page}

Si está utilizando [!DNL Experience Manager] como sistema de administración de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

Consulte también [Agregar recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Apertura [!DNL Experience Manager Sites] y seleccione la página web a la que desea añadir el componente de medios 3D de Dynamic Media.
1. Para abrir la página en el editor de páginas, seleccione la opción **[!UICONTROL Editar]** (lápiz). Asegúrese de que **[!UICONTROL Editar]** está seleccionado cerca de la parte superior derecha de la página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. En la barra de herramientas, seleccione el icono Panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, seleccione el icono de signo más para abrir el **[!UICONTROL Componentes]** lista.

   ![3d-media-component-arrastrar-soltar](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arrastre el **[!UICONTROL Medios 3D]** del **[!UICONTROL Componentes]** a la ubicación en la página donde desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

### Opcional: Configuración del componente de medios 3D {#configuring-the-three-d-component}

1. En el [!DNL Experience Manager Sites] editor de páginas, seleccione **[!UICONTROL Visor de medios 3D]** que agregó anteriormente a la página.
1. Para abrir el cuadro de diálogo de configuración de componentes, seleccione la opción **[!UICONTROL Configuración]** (llave inglesa).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visor , seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visualizador de dimensiones al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. En la esquina superior derecha, seleccione la marca de verificación para guardar los cambios.

## Asignar un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de añadir un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Añadir el componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page).

1. En el [!DNL Experience Manager Sites] editor de páginas, haga clic en el botón **[!UICONTROL Recursos]** icono para abrir **[!UICONTROL Recursos]** en el panel lateral.
1. En la lista desplegable , seleccione **[!UICONTROL 3D]** para mostrar solo los tipos de archivo de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D que desea ver en la página que se está editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el **[!UICONTROL Medios 3D]** que agregó anteriormente a la página.

   ![Asignar un recurso 3d al componente de medios 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Mientras que una página web está en la [!DNL Experience Manager Sites] **[!UICONTROL Editar]** , el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con el recurso. Para que el recurso sea interactivo, puede usar la variable **[!UICONTROL Vista previa]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publicar recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta varios formatos de archivo 3D compatibles con *contenido estático* en Dynamic Media. El contenido estático significa que puede cargar y publicar recursos 3D, pero no hay compatibilidad con *dinámico* rehacer imágenes o imágenes asociadas al recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La dirección URL del recurso 3D sigue la estructura URL habitual de Dynamic Media. Sin embargo, no puede editar ningún parámetro en la URL del recurso, a diferencia de los recursos de imagen tradicionales en Dynamic Media.

Consulte también [Obtener una URL para un recurso estático](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de su fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si está utilizando [!DNL Experience Manager] como WCM, utilice este método de publicación para añadir los recursos 3D de Dynamic Media directamente en la página web.

Consulte también [Publicar recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Consulte también [Publicar páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**Para publicar recursos estáticos de Dynamic Media 3D:**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL).
1. En la página Detalles, en la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Toque **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre del archivo del recurso 3D, seleccione **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Toque **[!UICONTROL original]**. Cuando se publica (o &quot;activa&quot;) un recurso 3D, la variable **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las siguientes condiciones de recursos 3D:
   * El recurso 3D es un formato compatible (GLB, OBJ, STL y USDZ).
   * El recurso 3D se incorporó al sistema de producción de imágenes (IPS) de Dynamic Media.
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Para mostrar la URL de producción directa del recurso 3D, que puede copiar y utilizar en páginas web, seleccione **[!UICONTROL URL]**.

### Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visor Dimensional {#alternate-publish-methods}

Utilice los dos métodos siguientes para publicar recursos de Dynamic Media 3D si *not* using [!DNL Experience Manager] como WCM.

* **[!UICONTROL URL]** - Uso **[!UICONTROL URL]** si utiliza un sistema de administración de contenido web de terceros y desea vincular recursos 3D de Dynamic Media a sus páginas web mediante el visor dimensional.

   Consulte [Vincular URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incrustar]** - Uso **[!UICONTROL Incrustar]** cuando desee ver un recurso 3D de Dynamic Media incrustado en una página web mediante el visor dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. La edición del código no está permitida en la variable **[!UICONTROL Incrustar]** para abrir el Navegador.

   Consulte [Incrustar el vídeo de Dynamic Media, el visor de imágenes o el visor dimensional en una página web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
