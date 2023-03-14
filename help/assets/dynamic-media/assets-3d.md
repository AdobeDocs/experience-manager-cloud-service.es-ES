---
title: Uso de recursos 3D en Dynamic Media
description: Aprenda a trabajar con recursos 3D en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: 347da5edf4c8ad2ae72284f4e1a4003493596194
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 5%

---

# Uso de recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media le permite cargar, gestionar, ver y distribuir recursos 3D como experiencias envolventes.

* Publicación con un clic (con **[!UICONTROL Publicación rápida]** en la barra de herramientas) de recursos 3D para generar una URL.
* Compatibilidad optimizada para ver recursos 3D con el ajuste preestablecido de visualizador dimensional interactivo de alta calidad con tecnología Adobe Dimension.
* El componente WCM de medios en 3D le permite agregar fácilmente recursos 3D al [!DNL Adobe Experience Manager Sites] páginas.

No se requiere ninguna instalación adicional para utilizar recursos 3D en Dynamic Media.

![Zapato en 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D admitidos en Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos de archivo 3D.

Consulte también [Formatos 3D admitidos en Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| Extensión de archivo 3D | Formato de archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | Incluye los materiales y las texturas como un solo recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | *Compatibilidad únicamente con la ingesta; no hay visualización ni interacción disponibles.* USDZ es un formato 3D propiedad que Safari o iOS pueden ver de forma nativa. |

El componente WCM de medios en 3D y la vista previa 3D de la página de detalles de un recurso no son compatibles con la última versión de Chrome (97.x). En su lugar, para trabajar con recursos 3D, utilice Firefox o Safari, o bien utilice una versión anterior de Chrome (96.x).

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle a ponerse en marcha rápidamente con los recursos 3D en Dynamic Media.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que [!DNL Experience Manager] ya ha habilitado y configurado los Cloud Services de Dynamic Media.

Consulte [Configuración de Cloud Services de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Carga de recursos 3D**

   * [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de archivo 3D compatibles para la carga en Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Administración de recursos 3D**

   * Organización y búsqueda de recursos 3D

      * [Organización de recursos digitales](/help/assets/organize-assets.md)
      * [Búsqueda de recursos 3D](/help/assets/search-assets.md)
   * Ver recursos 3D

      * [Visualización e interacción con recursos 3D](#viewing-three-d-assets)
      * [Administrar el ajuste preestablecido de visualizador dimensional](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabajo con metadatos de recursos 3D

      * [Administración de metadatos para recursos digitales](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md)



1. **Publicación de recursos 3D**

   * [Publicación de recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional](#alternate-publish-methods)

## Visualización e interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo ver recursos 3D e interactuar con ellos de dos formas diferentes: desde la página de detalles de recursos y desde el componente Medios 3D en Sites.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y recorrer el recurso 3D.

El tiempo que se tarda en abrir un recurso 3D en la vista de página Detalles del recurso depende de varios factores. Estos factores incluyen elementos como los siguientes:

* Ancho de banda al servidor.
* Latencias al servidor
* Complejidad de la imagen.

Además, las capacidades del equipo cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes a la hora de manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visualizador dimensional en el Editor de ajustes preestablecidos de visualizador para practicar la navegación por un recurso 3D sin necesidad de cargar primero ningún archivo 3D. El ajuste preestablecido de visualizador dimensional tiene un recurso 3D integrado con el que puede interactuar.
>
>Consulte [Administrar ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

## Ver e interactuar con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D desde la página de detalles de recursos:**

1. Asegúrese de que ha cargado los recursos 3D en [!DNL Experience Manager].

   Consulte [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. Desde [!DNL Experience Manager], en el **[!UICONTROL Navegación]** página, seleccione **[!UICONTROL Recursos > Archivos]**.
1. Cerca de la esquina superior derecha de la página, desde el **[!UICONTROL Ver]** , seleccione la opción **[!UICONTROL Vista de tarjeta]**.
1. Vaya a un recurso 3D que desee ver.
1. Para abrir el recurso en la página Detalles, seleccione la tarjeta del recurso 3D.
1. En la página Detalles del recurso 3D, realice una de las siguientes acciones:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica de la cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho + arrastre. | Presione con dos dedos + arrastre. |
   | **Zoom de la cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Hacer doble clic. | Pulse dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |  |  |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |  |  |

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]** para volver a la página Assets.

## Ver e interactuar con un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en **[!UICONTROL Editar]** modo, no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede utilizar el **[!UICONTROL Previsualizar]** función para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Solo podrá realizar esta tarea una vez que haya añadido un componente de medios 3D a una página web y le haya asignado un recurso 3D. Consulte [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page) y [Asignar un recurso 3D a un componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D dentro de un componente de medios 3D:**

1. Mientras una página web se encuentra en **[!UICONTROL Editar]** modo, realice una de las siguientes acciones:

   * Cerca de la parte superior derecha de la página, haga clic en **[!UICONTROL Previsualizar]** para entrar **[!UICONTROL Previsualizar]** modo.
   * Eliminar `/editor.html` desde la dirección URL de la página en el explorador.

Un recurso 3D completamente interactivo, como se muestra en    ![Recurso 3D que se muestra dentro del componente de medios 3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Un recurso 3D completamente interactivo, como se muestra en **[!UICONTROL Previsualizar]** modo.

1. Mientras está en **[!UICONTROL Previsualizar]** modo, realice una de las siguientes acciones:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gire la cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica de la cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho + arrastre. | Presione con dos dedos + arrastre. |
   | **Zoom de la cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Hacer doble clic. | Pulse dos veces. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |  |  |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |  |  |

## Acerca del trabajo con el componente de medios en 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente multimedia en 3D de Dynamic Media que puede usar en [!DNL Experience Manager Sites] para habilitar la visualización interactiva de modelos 3D en las páginas web.

* [Añadir el componente Medios 3D a la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: Configuración del componente de medios 3D](#configuring-the-three-d-component)
* [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

## Añadir el componente Medios 3D a la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]**.
1. Desplácese hasta la plantilla de página en la que desea activar el componente 3D y seleccione la plantilla.
1. Para abrir la plantilla, seleccione **[!UICONTROL Editar]**.
1. Cerca de la parte superior derecha de la página, en el menú desplegable, seleccione **[!UICONTROL Estructura]** modo, si aún no está activo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Para seleccionar un área vacía y abrir su barra de herramientas asociada, seleccione el área vacía en la **[!UICONTROL Contenedor de diseño]** región.
1. En la barra de herramientas, seleccione **[!UICONTROL Política]** para abrir el **[!UICONTROL Editor de directivas]**.
1. En el **[!UICONTROL Propiedades]** , en la sección **[!UICONTROL Componentes permitidos]** pestaña, desplácese hasta **[!UICONTROL Dynamic Media]**, luego expanda la lista y marque **[!UICONTROL Medios en 3D]**.
1. Tocar **[!UICONTROL Listo]** para guardar los cambios y cerrar el **[!UICONTROL Editor de directivas]**.

   Ahora puede colocar el componente Dynamic Media 3D Media en todas las páginas que utilicen esta plantilla.

## Adición del componente Medios 3D a una página web {#adding-the-three-d-media-component-to-a-web-page}

Si está utilizando [!DNL Experience Manager] como sistema de gestión de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

Consulte también [Añadir recursos de Dynamic Media a las páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Abrir [!DNL Experience Manager Sites] y seleccione la página web a la que desea añadir el componente Dynamic Media 3D Media.
1. Para abrir la página en el editor de páginas, seleccione **[!UICONTROL Editar]** Icono (lápiz). Asegúrese de que **[!UICONTROL Editar]** El modo está seleccionado cerca de la parte superior derecha de la página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. En la barra de herramientas, seleccione el icono Panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, seleccione el icono del signo más para abrir **[!UICONTROL Componentes]** lista.

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arrastre el **[!UICONTROL Medios en 3D]** del componente de **[!UICONTROL Componentes]** a la ubicación de la página donde desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignar un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

### Opcional: Configuración del componente de medios 3D {#configuring-the-three-d-component}

1. En el [!DNL Experience Manager Sites] editor de páginas, seleccione **[!UICONTROL Visor de medios en 3D]** componente que agregó anteriormente a la página.
1. Para abrir el cuadro de diálogo de configuración del componente, seleccione la **[!UICONTROL Configuración]** icono (llave inglesa).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visualizador, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visualizador dimensional al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. En la esquina superior derecha, seleccione la marca de verificación para guardar los cambios.

## Asignar un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de agregar un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Adición del componente Medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page).

1. En el [!DNL Experience Manager Sites] editor de página, haga clic en **[!UICONTROL Assets]** icono para abrir **[!UICONTROL Assets]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo tipos de archivos de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D que desee ver en la página que está editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el **[!UICONTROL Medios en 3D]** componente que agregó anteriormente a la página.

   ![Asignar un recurso 3d a un componente de medios 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Mientras una página web se encuentra en [!DNL Experience Manager Sites] **[!UICONTROL Editar]** modo, el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con él. Para que el recurso sea interactivo, puede utilizar el **[!UICONTROL Previsualizar]** función para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publicación de recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta varios formatos de archivo 3D compatibles con *contenido estático* en Dynamic Media. El contenido estático significa que puede cargar y publicar recursos 3D, pero no es compatible con *dinámico* imagen o ajuste de imagen asociado al recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La dirección URL del recurso 3D sigue la estructura URL habitual de Dynamic Media. Sin embargo, no se puede editar ningún parámetro en la dirección URL del recurso, a diferencia de los recursos de imagen tradicionales de Dynamic Media.

Consulte también [Obtener una URL para un recurso estático](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de su fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si está utilizando [!DNL Experience Manager] como WCM, utilice este método de publicación para añadir los recursos de Dynamic Media 3D directamente en la página web.

Consulte también [Publicar recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Consulte también [Publicar páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**Para publicar recursos estáticos de Dynamic Media 3D:**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL).
1. En la página Detalles, en la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Tocar **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre de fichero del recurso 3D, seleccione **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Tocar **[!UICONTROL original]**. Cuando se publica un recurso 3D (o &quot;activado&quot;), la variable **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones de recurso 3D siguientes:
   * El recurso 3D es un formato compatible (GLB, OBJ, STL y USDZ).
   * El recurso 3D se ha introducido en Dynamic Media Image Production System (IPS).
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Para mostrar la URL de producción directa del recurso 3D que puede copiar y utilizar en páginas web, seleccione **[!UICONTROL URL]**.

### Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visualizador dimensional {#alternate-publish-methods}

Utilice los dos métodos siguientes para publicar recursos de Dynamic Media 3D si *no* usando [!DNL Experience Manager] como WCM.

* **[!UICONTROL URL]** - Uso **[!UICONTROL URL]** si utiliza un sistema de administración de contenido web de terceros y desea vincular recursos de Dynamic Media 3D a sus páginas web mediante el visualizador dimensional.

   Consulte [Vinculación de URL en la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incrustar]** - Uso **[!UICONTROL Incrustar]** si desea ver un recurso de Dynamic Media 3D incrustado en una página web mediante el visualizador dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en **[!UICONTROL Incrustar]** Cuadro de diálogo.

   Consulte [Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
