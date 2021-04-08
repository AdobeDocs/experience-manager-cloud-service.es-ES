---
title: Uso de recursos 3D en Dynamic Media
description: Aprenda a trabajar con recursos 3D en Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: Recursos 3D
topic: Profesional empresarial
role: Business Practitioner
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '2271'
ht-degree: 4%

---

# Uso de recursos 3D en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media permite cargar, administrar, ver y entregar recursos 3D como experiencias envolventes.

* Publicación con un solo clic (con **[!UICONTROL Publicación rápida]** en la barra de herramientas) de recursos 3D para generar una URL.
* Se ha optimizado la compatibilidad con la visualización de recursos 3D con el ajuste preestablecido interactivo de visualizador de dimensiones de alta calidad con tecnología de Adobe Dimension.
* El componente WCM de medios 3D permite añadir fácilmente recursos 3D a las páginas de Adobe Experience Manager Sites.

No se requiere ninguna instalación adicional para utilizar recursos 3D en Dynamic Media.

![Zapato en 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatibles con Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos de archivo 3D.

Consulte también [Formatos 3D admitidos](/help/assets/file-format-support.md#support-3d-formats)

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary | Incluye los materiales y texturas como un único recurso. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | *Compatibilidad únicamente con la ingesta; no hay visualización ni interacción disponibles.* USDZ es un formato 3D propietario que Safari o iOS pueden ver de forma nativa. |

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo está diseñada para ayudarle a poner en marcha rápidamente los recursos 3D en Dynamic Media.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que el administrador del Experience Manager ya haya habilitado y configurado los Cloud Services de Dynamic Media.

Consulte [Configuración de Cloud Services de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Cargar recursos 3D**

   * [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de archivo 3D compatibles con la carga en Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Administrar recursos 3D**

   * Organizar y buscar recursos 3D

      * [Organización de recursos digitales](/help/assets/organize-assets.md)
      * [Búsqueda de recursos 3D](/help/assets/search-assets.md)
   * Ver recursos 3D

      * [Visualización e interacción con recursos 3D](#viewing-three-d-assets)
      * [Administración del ajuste preestablecido de visualizador de dimensiones](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabajar con metadatos de recursos 3D

      * [Administración de metadatos de recursos digitales](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md)



1. **Publicar recursos 3D**

   * [Publicación de recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visor Dimensional](#alternate-publish-methods)

## Acerca de la visualización y la interacción con activos 3D {#viewing-three-d-assets}

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
>Consulte [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

## Visualización e interacción con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D desde la página de detalles del recurso**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.

   Consulte [Carga de los recursos 3D para su uso en Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. En el Experience Manager, en la página **[!UICONTROL Navegación]**, pulse **[!UICONTROL Assets > Archivos]**.
1. Cerca de la esquina superior derecha de la página, en la lista desplegable **[!UICONTROL Ver]**, pulse **[!UICONTROL Vista de tarjeta]**.
1. Vaya a un recurso 3D que desee ver.
1. Para abrir el recurso en la página Detalles , pulse la tarjeta del recurso 3D.
1. En la página Detalles del recurso 3D, realice una de las acciones siguientes:

   * **Girar la cámara** : Girar la vista alrededor de la escena 3D y los objetos.
      * _Mouse_: Haga clic y arrastre con el botón izquierdo.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Panorre la cámara** : desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Mouse_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione con dos dedos y arrastre.
   * **Zoom de la cámara** : Aumente el zoom de la cámara para moverse dentro y fuera de las áreas de la escena 3D.
      * _Mouse_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Vuelva a introducir la cámara** : vuelva a introducirla en un punto de un objeto de la escena 3D.
      * _Mouse_: Haga doble clic en .
      * _Pantalla_ táctil: Toque dos veces.
   * **Restablecer** : cerca de la esquina inferior derecha de la página, pulse el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo de pantalla completa** : para entrar al modo de pantalla completa, en la esquina inferior derecha de la página, pulse el icono de pantalla completa.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Cerrar]** para volver a la página Recursos.

## Visualización e interacción con un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en modo **[!UICONTROL Editar]**, no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede utilizar la función **[!UICONTROL Preview]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Solo puede realizar esta tarea después de añadir un componente de medios 3D a una página web y asignar un recurso 3D al componente. Consulte [Adición del componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page) y [Asignación de un recurso 3D a un componente de medios 3D](#assigning-a-three-d-asset-to-the-component).

Consulte también [Vista previa de recursos mediante la interfaz de software](/help/assets/dynamic-media/previewing-assets.md).

**Para ver e interactuar con un recurso 3D dentro de un componente de medios 3D**

1. Mientras una página web está en modo **[!UICONTROL Edit]** , realice una de las siguientes acciones:

   * Cerca de la parte superior derecha de la página, haga clic en **[!UICONTROL Vista previa]** para entrar al modo **[!UICONTROL Vista previa]**.
   * Elimine `/editor.html` de la dirección URL de la página en el explorador.

Un recurso 3D totalmente interactivo, tal como se muestra en    ![Recurso 3D que se muestra dentro del ](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
componente de medios 3D Un recurso 3D totalmente interactivo tal y como se muestra en  **** modo de vista previa.

1. Cuando esté en modo **[!UICONTROL Preview]**, realice una de las siguientes acciones:

   * **Girar la cámara** : Girar la vista alrededor de la escena 3D y los objetos.
      * _Mouse_: Haga clic y arrastre con el botón izquierdo.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Panorre la cámara** : desplace la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Mouse_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione con dos dedos y arrastre.
   * **Zoom de la cámara** : Aumente el zoom de la cámara para moverse dentro y fuera de las áreas de la escena 3D.
      * _Mouse_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Vuelva a introducir la cámara** : vuelva a introducirla en un punto de un objeto de la escena 3D.
      * _Mouse_: Haga doble clic en .
      * _Pantalla_ táctil: Toque dos veces.
   * **Restablecer** : cerca de la esquina inferior derecha de la página, pulse el icono Restablecer para restaurar el punto de destino de la vista al centro del recurso 3D. Restablecer también mueve la cámara más cerca o más lejos para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo de pantalla completa** : para entrar al modo de pantalla completa, en la esquina inferior derecha de la página, pulse el icono de pantalla completa.

## Acerca del trabajo con el componente multimedia 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente de medios 3D de Dynamic Media que puede utilizar en sitios de Experience Manager para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Adición del componente de medios 3D a la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Adición del componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: Configuración del componente de medios 3D](#configuring-the-three-d-component)
* [Asignación de un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)


## Adición del componente de medios 3D a la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas > General > Plantillas]**.
1. Vaya a la plantilla de página en la que desea habilitar el componente 3D y seleccione la plantilla.
1. Para abrir la plantilla, pulse **[!UICONTROL Editar]**.
1. Cerca de la parte superior derecha de la página, en el menú desplegable, seleccione el modo **[!UICONTROL Estructura]** si no está activo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Para seleccionar un área vacía y abrir su barra de herramientas asociada, pulse el área vacía de la región **[!UICONTROL Contenedor de diseño]**.
1. En la barra de herramientas, pulse el icono **[!UICONTROL Policy]** para abrir el **[!UICONTROL Editor de directivas]**.
1. En la sección **[!UICONTROL Properties]**, en la pestaña **[!UICONTROL Allowed Components]**, desplácese hasta **[!UICONTROL Dynamic Media]**, expanda la lista y marque **[!UICONTROL 3D Media]**.
1. Pulse **[!UICONTROL Listo]** para guardar los cambios y cerrar el **[!UICONTROL Editor de directivas]**.

   Ahora puede colocar el componente de medios 3D de Dynamic Media en todas las páginas que utilicen esta plantilla.

## Adición del componente de medios 3D a una página web {#adding-the-three-d-media-component-to-a-web-page}

Si utiliza Experience Manager como sistema de administración de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

Consulte también [Adición de recursos de Dynamic Media a las páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Abra Sitios Experience Manager y seleccione la página web a la que desea agregar el componente de medios 3D de Dynamic Media.
1. Para abrir la página en el editor de páginas, pulse el icono **[!UICONTROL Editar]** (lápiz). Asegúrese de que el modo **[!UICONTROL Edit]** está seleccionado cerca de la parte superior derecha de la página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. En la barra de herramientas, pulse el icono del panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, pulse el icono de signo más para abrir la lista **[!UICONTROL Componentes]**.

   ![3d-media-component-arrastrar-soltar](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arrastre el componente **[!UICONTROL 3D Media]** de la lista **[!UICONTROL Componentes]** a la ubicación de la página en la que desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignación de un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)

### Opcional: Configuración del componente multimedia 3D {#configuring-the-three-d-component}

1. En el editor de páginas Sitios del Experience Manager, seleccione el componente **[!UICONTROL Visor de medios 3D]** que agregó anteriormente a la página.
1. Para abrir el cuadro de diálogo de configuración de componentes, pulse el icono **[!UICONTROL Configuration]** (llave inglesa).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visualizador, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visualizador dimensional al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. En la esquina superior derecha, pulse la marca de verificación para guardar los cambios.

## Asignación de un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de añadir un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Adición del componente de medios 3D a una página web](#adding-the-three-d-media-component-to-a-web-page).

1. En el editor de páginas Sitios del Experience Manager, haga clic en el icono **[!UICONTROL Recursos]** para abrir **[!UICONTROL Recursos]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo los tipos de archivo de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D que desea ver en la página que se está editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el componente **[!UICONTROL 3D Media]** que agregó anteriormente a la página.

   ![Asignar un recurso 3d al componente de medios 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Mientras una página web está en modo de Experience Manager Sites **[!UICONTROL Edit]** , el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con el recurso. Para que el recurso sea interactivo, puede utilizar la función **[!UICONTROL Preview]** para ver la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publicación de recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta varios formatos de archivo 3D compatibles con *contenido estático* en Dynamic Media. El contenido estático significa que puede cargar y publicar recursos 3D, pero no hay compatibilidad con imágenes *dinámicas* ni con redistribuciones de imágenes asociadas al recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La dirección URL del recurso 3D sigue la estructura URL habitual de Dynamic Media. Sin embargo, no puede editar ningún parámetro en la URL del recurso, a diferencia de los recursos de imagen tradicionales en Dynamic Media.

Consulte también [Obtención de una URL para un recurso estático](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

En la **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de su fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si utiliza Experience Manager como WCM, utilice este método de publicación para añadir los recursos 3D de Dynamic Media directamente en la página web.

Consulte también [Publicación de recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Consulte también [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**Para publicar recursos estáticos de Dynamic Media 3D**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL) para verlo en la página Detalles .
1. En la barra de herramientas, pulse **[!UICONTROL Publicación rápida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Pulse **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre del archivo del recurso 3D, pulse **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Toque **[!UICONTROL original]**. Cuando se publica un recurso 3D (o &quot;activado&quot;), el botón **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones de recursos 3D siguientes:
   * El recurso 3D es un formato compatible (GLB, OBJ, STL y USDZ).
   * El recurso 3D se incorporó al sistema de producción de imágenes (IPS) de Dynamic Media.
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Para mostrar la URL de producción directa del recurso 3D que puede copiar y usar en páginas web, pulse **[!UICONTROL URL]**.

### Métodos alternativos para publicar recursos de Dynamic Media 3D mediante el visor de dimensiones {#alternate-publish-methods}

Utilice los dos métodos siguientes para publicar recursos de Dynamic Media 3D si utiliza *no* como Experience Manager de WCM.

* **[!UICONTROL URL]** : utilice la  **** URL si utiliza un sistema de administración de contenido web de terceros y desea vincular recursos 3D de Dynamic Media a sus páginas web mediante el visor dimensional.

   Consulte [Vinculación de URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incrustar]** : utilice  **** Incrustar cuando desee ver un recurso 3D de Dynamic Media incrustado en una página web mediante el visor Dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Incrustar]**.

   Consulte [Incrustación del vídeo de Dynamic Media, el visor de imágenes o el visor dimensional en una página web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
