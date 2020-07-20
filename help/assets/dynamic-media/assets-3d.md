---
title: Uso de recursos 3D en Dynamic Media
seo-title: Uso de recursos 3D en Dynamic Media
description: Aprenda a trabajar con recursos 3D en Dynamic Media
seo-description: Aprenda a trabajar con recursos 3D en Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: b44e6a522b6f2363daa40c6c6f9640ba2fadd35e
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 5%

---


# Working with 3D assets in Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media permite cargar, gestionar, vista y distribuir recursos 3D como experiencias envolventes.

* Publicación con un solo clic (mediante **[!UICONTROL Publicación]** rápida en la barra de herramientas) de recursos 3D para generar una URL.
* Compatibilidad optimizada para ver recursos 3D con el ajuste preestablecido de visor de dimensiones interactivo y de alta calidad con tecnología Adobe Dimension.
* El componente WCM de medios 3D permite añadir fácilmente recursos 3D a las páginas de AEM Sites.

No se requiere una instalación adicional para utilizar recursos 3D en Dynamic Media.

![zapato en 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes.](/help/release-notes/aem3d-release-notes.md) -->

## Formatos 3D compatibles con Dynamic Media {#supported-three-d-file-formats-in-dm}

Dynamic Media admite los siguientes formatos de archivo 3D.

Consulte también Formatos [3D admitidos](/help/assets/file-format-support.md#supported-3d-formats)

| Extensión de archivo 3D | Formato de archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria de GL | model/gltf-binary | Incluye los materiales y las texturas como un único recurso. |
| OBJ | Archivo de objeto WaveFront 3D | application/x-tgif |  |
| STL | Esteroolitografía | application/vnd.ms-pki.stl |  |
| USDZ | Archivo zip de descripción de escena universal | model/vnd.usdz+zip | *Apoyo a la ingestión únicamente; no hay visualización ni interacción disponibles.* USDZ es un formato 3D propio que Safari o iOS pueden ver de forma nativa. |

## Inicio rápido: Recursos 3D en Dynamic Media {#quick-start-three-d}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle en el uso inicial de los recursos 3D en Dynamic Media.

Antes de trabajar con recursos 3D en Dynamic Media, asegúrese de que el administrador de AEM ya ha habilitado y configurado Cloud Service de Dynamic Media.

Consulte [Configuración de Cloud Service de Dynamic Media.](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

1. **Carga de recursos 3D**

   * [Carga de recursos 3D para su uso en Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de archivo 3D compatibles para cargar en Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gestión de recursos 3D**

   * Organización y búsqueda de recursos 3D

      * [Organización de recursos digitales](/help/assets/organize-assets.md)
      * [Búsqueda de recursos 3D](/help/assets/search-assets.md)
   * Recursos 3D de Vista

      * [Visualización e interacción con recursos 3D](#viewing-three-d-assets)
      * [Administración del ajuste preestablecido de visor dimensional](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabajo con metadatos de recursos 3D

      * [Gestión de metadatos para recursos digitales](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md)



1. **Publicación de recursos 3D**

   * [Publicación de recursos estáticos de Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar recursos Dynamic Media 3D con el visor de dimensiones](#alternate-publish-methods)

## Visualización e interacción con recursos 3D {#viewing-three-d-assets}

En esta sección se describe cómo vista e interacción con recursos 3D de dos formas diferentes: desde la página de detalles del recurso y desde el componente de medios 3D en Sitios.

El visor 3D interactivo incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, aplicar zoom y recorrer el recurso 3D.

Tenga en cuenta que el tiempo que tarda en abrir un recurso 3D en la vista de la página Detalles del recurso depende de varios factores. Estos factores incluyen elementos como los siguientes:

* Ancho de banda del servidor.
* Latencias en el servidor
* Complejidad de la imagen.

Además, las capacidades del ordenador cliente, como una estación de trabajo, un ordenador portátil o un dispositivo móvil táctil, también son importantes para tener en cuenta al manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización interactiva en 3D sea más cómoda y agradable.

>[!TIP]
>
>Puede abrir el ajuste preestablecido de visor de dimensiones en el Editor de ajustes preestablecidos de visor para practicar la navegación por un recurso 3D sin necesidad de cargar primero ningún archivo 3D. El ajuste preestablecido de visor de dimensiones tiene un recurso 3D integrado con el que interactuar.
>
>See [Managing viewer presets.](/help/assets/dynamic-media/managing-viewer-presets.md)

## Visualización e interacción con un recurso 3D desde la página de detalles del recurso {#viewing-three-d-assets-from-asset-details-page}

Consulte también [Vista previa de recursos mediante la interfaz de software.](/help/assets/dynamic-media/previewing-assets.md)

**vista e interacción con un recurso 3D desde la página de detalles del recurso**

1. Asegúrese de que ha cargado los recursos 3D en AEM.

   Consulte [Carga de recursos 3D para su uso en Dynamic Media.](/help/assets/add-assets.md#upload-assets)

1. En AEM, en la página **[!UICONTROL Navegación]** , toque **[!UICONTROL Recursos > Archivos]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Vaya a un recurso 3D que desee ver.
1. Toque la tarjeta del recurso 3D para abrirlo en la página de información del recurso.
1. En la página de vista de detalles del recurso 3D, realice una de las siguientes acciones:

   * **Gire la cámara** : ordene la vista alrededor de la escena y los objetos 3D.
      * _Ratón_: Haga clic y arrastre.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Recorra la cámara** : deslice la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Ratón_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione dos dedos y arrastre.
   * **Zoom en la cámara** : haga zoom en la cámara para entrar y salir de áreas de la escena 3D.
      * _Ratón_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Volver a introducir la cámara** : vuelva a introducir la cámara en un punto de la escena 3D.
      * _Ratón_: Haga clic con el Doble.
      * _Pantalla_ táctil: Toque el Doble.
   * **Restaurar** : cerca de la esquina inferior derecha de la página, toque el icono Restablecer para restaurar el punto de destinatario de vista al centro del recurso 3D. El reinicio también hace que la cámara se acerque o se aleje para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa: para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, toque el icono de pantalla completa.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Cerrar]** para volver a la página Recursos.

## Visualización e interacción con un recurso 3D dentro de un componente de medios 3D {#interacting-with-asset-inside-three-d-media-component}

Cuando una página web está en modo de **[!UICONTROL edición]** , no es posible interactuar con un recurso 3D. Para que el recurso sea interactivo, puede utilizar la función de **[!UICONTROL Previsualización]** para vista de la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

>[!IMPORTANT]
>
>Esta tarea solo se puede realizar una vez que haya agregado un componente de medios 3D a una página web y haya asignado un recurso 3D al componente. Consulte [Añadir el componente de medios 3D en una página](#adding-the-three-d-media-component-to-a-web-page) web y [Asignación de un recurso 3D a un componente de medios 3D.](#assigning-a-three-d-asset-to-the-component)

Consulte también [Vista previa de recursos mediante la interfaz de software.](/help/assets/dynamic-media/previewing-assets.md)

**vista e interacción con un recurso 3D dentro de un componente de medios 3D**

1. Mientras una página web está en modo de **[!UICONTROL edición]** , realice una de las siguientes acciones:

   * Cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Previsualización]** para acceder al modo de **[!UICONTROL Previsualización]** .
   * Elimine `/editor.html` de la dirección URL de la página en el explorador.

Un recurso 3D completamente interactivo, tal como se muestra en    ![Recurso 3D que se muestra dentro del componente](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)Medios 3D Un recurso 3D completamente interactivo, tal como se muestra en el modo de **[!UICONTROL Previsualización]** .

1. En el modo de **[!UICONTROL Previsualización]** , realice una de las siguientes acciones:

   * **Gire la cámara** : ordene la vista alrededor de la escena y los objetos 3D.
      * _Ratón_: Haga clic y arrastre.
      * _Pantalla_ táctil: Presione con un solo dedo y arrastre.
   * **Recorra la cámara** : deslice la vista hacia la izquierda, hacia la derecha, hacia arriba o hacia abajo.
      * _Ratón_: Haga clic con el botón derecho y arrastre.
      * _Pantalla_ táctil: Presione dos dedos y arrastre.
   * **Zoom en la cámara** : haga zoom en la cámara para entrar y salir de áreas de la escena 3D.
      * _Ratón_: Rueda de desplazamiento.
      * _Pantalla_ táctil: Pellizque con dos dedos.
   * **Volver a introducir la cámara** : vuelva a introducir la cámara en un punto de la escena 3D.
      * _Ratón_: Haga clic con el Doble.
      * _Pantalla_ táctil: Toque el Doble.
   * **Restaurar** : cerca de la esquina inferior derecha de la página, toque el icono Restablecer para restaurar el punto de destinatario de vista al centro del recurso 3D. El reinicio también hace que la cámara se acerque o se aleje para mostrar el recurso en su totalidad y con un tamaño de visualización razonable.
   * **Modo** de pantalla completa: para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, toque el icono de pantalla completa.

## Acerca del trabajo con el componente de medios 3D {#working-with-three-d-media-component}

Dynamic Media incluye un componente de medios 3D de Dynamic Media que puede utilizar en AEM Sites para permitir la visualización interactiva de modelos 3D en sus páginas web.

* [Añadir el componente de medios 3D en la plantilla de página](#adding-three-d-media-component-to-page-template)
* [Añadir el componente de medios 3D en una página web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional: Configuración del componente de medios 3D](#configuring-the-three-d-component)
* [Asignación de un recurso 3D al componente de medios 3D](#assigning-a-three-d-asset-to-the-component)


## Añadir el componente de medios 3D en la plantilla de página {#adding-three-d-media-component-to-page-template}

1. Vaya a **[!UICONTROL Herramientas > General > Plantillas]**.
1. Vaya a la plantilla de página en la que desea habilitar el componente 3D y seleccione la plantilla.
1. Toque **[!UICONTROL Editar]** para abrir la plantilla.
1. Cerca de la esquina superior derecha de la página, en el menú desplegable, seleccione el modo **[!UICONTROL Estructura]** , si aún no está activo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Toque un área vacía en la región del Contenedor **** Diseño para seleccionarla y abrir la barra de herramientas asociada.
1. En la barra de herramientas, toque el icono **[!UICONTROL Política]** para abrir el Editor **[!UICONTROL de directivas]**.
1. En la sección **[!UICONTROL Propiedades]** , en la ficha Componentes **** permitidos, desplácese hasta **[!UICONTROL Dynamic Media]** y, a continuación, expanda la lista y marque Medios **** 3D.
1. Toque **[!UICONTROL Listo]** para guardar los cambios y cerrar el Editor **[!UICONTROL de directivas]**.

   Ahora puede colocar el componente de medios 3D de Dynamic Media en todas las páginas que utilicen esta plantilla.

## Añadir el componente de medios 3D en una página web {#adding-the-three-d-media-component-to-a-web-page}

Si utiliza Adobe Experience Manager como sistema de gestor de contenido web, puede añadir recursos 3D a sus páginas web mediante el componente de medios 3D.

See also [Adding Dynamic Media assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

1. Abra AEM Sites y seleccione la página web a la que desea agregar el componente de medios 3D de Dynamic Media.
1. Toque el icono **[!UICONTROL Editar]** (lápiz) para abrir la página en el editor de páginas. Asegúrese de que el modo **[!UICONTROL Editar]** está seleccionado cerca de la esquina superior derecha de la página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. En la barra de herramientas, toque el icono del panel lateral para activar o desactivar la visualización del panel.

1. En el panel lateral, toque el icono de signo más para abrir la lista **[!UICONTROL Componentes]** .

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arrastre el componente **[!UICONTROL 3D Media]** de la lista **[!UICONTROL Componentes]** a la ubicación de la página en la que desea que aparezca el visor 3D.

Ya está listo para asignar un recurso 3D al componente.

Consulte [Asignación de un recurso 3D a un componente de medios 3D.](#assigning-a-three-d-asset-to-the-component)

### Opcional: Configuración del componente de medios 3D {#configuring-the-three-d-component}

1. En el editor de páginas AEM Sites, seleccione el componente de visor **[!UICONTROL de medios]** 3D que agregó anteriormente a la página.
1. Toque el icono **[!UICONTROL Configuración]** (llave inglesa) para abrir el cuadro de diálogo de configuración del componente.

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. En el cuadro de diálogo Medios 3D, en la lista desplegable Ajuste preestablecido de visor, seleccione **[!UICONTROL Dimensional]** para asignar el ajuste preestablecido de visor de dimensiones al componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. En la esquina superior derecha, toque la marca de verificación para guardar los cambios.

## Asignación de un recurso 3D al componente de medios 3D {#assigning-a-three-d-asset-to-the-component}

Después de agregar un componente de medios 3D a una página web, puede asignarle un recurso 3D.

Consulte [Añadir el componente de medios 3D en una página web.](#adding-the-three-d-media-component-to-a-web-page)

1. En el editor de páginas AEM Sites, haga clic en el icono **[!UICONTROL Recursos]** para abrir **[!UICONTROL Recursos]** en el panel lateral.
1. En la lista desplegable, seleccione **[!UICONTROL 3D]** para mostrar solo los tipos de archivo de recursos 3D.
1. En el panel lateral, busque o desplácese hasta el recurso 3D cuya vista desee realizar en la página que se esté editando.
1. Arrastre el recurso 3D desde el panel lateral Recursos y suéltelo en el componente Medios **** 3D que agregó anteriormente a la página.

   ![Asignación de un recurso 3d al componente de medios 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Mientras una página web está en el modo de **[!UICONTROL edición]** de AEM Sites, el componente de medios 3D muestra el recurso 3D, pero no es posible interactuar con el recurso. Para que el recurso sea interactivo, puede utilizar la función de **[!UICONTROL Previsualización]** para vista de la página web en el editor de páginas con acceso completo a la funcionalidad del componente de medios 3D.

## Publicación de recursos estáticos de Dynamic Media 3D {#publishing-three-d-assets}

Dynamic Media acepta diversos formatos de archivo 3D que se admiten como contenido ** estático en Dynamic Media. El contenido estático significa que se pueden cargar y publicar recursos 3D, pero no se admiten imágenes *dinámicas* ni redireccionamiento de imágenes asociados al recurso 3D. El motivo es que Dynamic Media Imaging Server no reconoce los formatos 3D. De este modo, después de publicar un recurso 3D en Dynamic Media, tiene una URL instantánea que puede copiar. La URL del recurso 3D sigue la estructura URL de Dynamic Media habitual. Sin embargo, no puede editar ningún parámetro en la URL del recurso, a diferencia de los recursos de imagen tradicionales de Dynamic Media.

Consulte también [Obtención de una URL para un recurso estático.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

En la Vista **[!UICONTROL de]** tarjeta, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

Si utiliza AEM como WCM, utilice este método de publicación para añadir los recursos de Dynamic Media 3D directamente en la página web.

Consulte también [Publicación de recursos de Dynamic Media.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

Consulte también [Publicación de páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

**Para publicar recursos estáticos de Dynamic Media 3D**

1. Abra un recurso 3D (formato de archivo GLB, OBJ o STL) para vista en la página de detalles del recurso.
1. En la barra de herramientas, toque **[!UICONTROL Publicación]** rápida.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Toque **[!UICONTROL Cerrar]** para salir del cuadro de diálogo y volver a la página de detalles del recurso.
1. En la lista desplegable situada a la izquierda del nombre de archivo del recurso 3D, toque **[!UICONTROL Representaciones]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Toque **[!UICONTROL original]**. Cuando se publica un recurso 3D (o se &quot;activa&quot;), el botón **[!UICONTROL URL]** aparece cerca de la esquina inferior izquierda de la página si se cumplen todas las condiciones de recursos 3D siguientes:
   * El recurso 3D es un formato admitido (GLB, OBJ, STL y USDZ).
   * El recurso 3D se ha ingerido en Dynamic Media Image Production System (IPS).
   * Se publica el recurso 3D.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Toque **[!UICONTROL URL]** para mostrar la URL de producción directa del recurso 3D, que puede copiar y utilizar en páginas web.

### Métodos alternativos para publicar recursos Dynamic Media 3D con el visor de dimensiones {#alternate-publish-methods}

Utilice los dos métodos siguientes para publicar recursos de Dynamic Media 3D si *no utiliza* AEM como WCM.

* **[!UICONTROL URL]** : utilice la **[!UICONTROL URL]** si utiliza un sistema de gestoras de contenido web de terceros y desea vincular recursos Dynamic Media 3D a sus páginas web mediante el visor de dimensiones.

   See [Linking URLs to your web application.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL Incrustar]** : utilice **[!UICONTROL Incrustar]** cuando desee realizar la vista de un recurso Dynamic Media 3D incrustado en una página web mediante el visor dimensional. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. Editing of the code is not permitted in the **[!UICONTROL Embed]** dialog box.

   Consulte [Incrustación de vídeos, visores de imágenes o visores dimensionales de Dynamic Media en una página web.](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)
