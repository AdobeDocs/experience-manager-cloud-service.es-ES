---
title: Crear y administrar recursos digitales en varios idiomas
description: Aprenda a automatizar los flujos de trabajo para traducir recursos, incluidos binarios, metadatos y etiquetas a varios idiomas.
contentOwner: AG
feature: Administración de activos,Traducción
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '2587'
ht-degree: 24%

---

# Recursos multilingües {#multilingual-assets}

Recursos multilingües significa recursos con binarios, metadatos y etiquetas en varios idiomas. Por lo general, los binarios, los metadatos y las etiquetas de los recursos existen en un idioma, y luego se traducen a otros idiomas para su uso en proyectos multilingües. Adobe Experience Manager Assets permite automatizar los flujos de trabajo de traducción en recursos (incluidos binarios, metadatos y etiquetas) para generar recursos en otros idiomas y utilizarlos en proyectos multilingües.

Para automatizar los flujos de trabajo de traducción, integre los proveedores de servicios de traducción con el Experience Manager y cree proyectos para traducir recursos a varios idiomas. Experience Manager admite flujos de trabajo de traducción automática y humana.

Traducción humana: Los recursos traducidos se devuelven y se importan al Experience Manager. Cuando el proveedor de traducción está integrado con el Experience Manager, los recursos se envían automáticamente entre el Experience Manager y el proveedor de traducción.

Traducción automática: El servicio de traducción automática traduce inmediatamente los metadatos y las etiquetas de los recursos.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparación de recursos para su traducción {#prepare-assets-for-translation}

Recursos multilingües significa recursos con binarios, metadatos y etiquetas en varios idiomas. Por lo general, los binarios, los metadatos y las etiquetas de los recursos existen en un idioma, y luego se traducen a otros idiomas para su uso en proyectos multilingües.

En Adobe Experience Manager Assets, los recursos multilingües se incluyen en las carpetas, donde cada carpeta contiene los recursos en un idioma diferente.

Cada carpeta de idioma se denomina copia de idioma. La carpeta raíz de una copia de idioma, conocida como raíz de idioma, identifica el idioma del contenido en la copia de idioma. Por ejemplo, `/content/dam/it` es la raíz del idioma italiano para la copia en idioma italiano. Las copias de idioma deben utilizar una [raíz de idioma configurada correctamente](#create-a-language-root) para que se oriente al idioma correcto cuando se realicen traducciones de recursos de origen.

La copia de idioma para la que se agregaron recursos originalmente es el idioma principal. El idioma principal es la fuente que se traduce a otros idiomas. Una jerarquía de carpetas de ejemplo incluye varias raíces de idioma:

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

Siga estos pasos para preparar los recursos para la traducción:

1. Cree la raíz de idioma de la principal del idioma. Por ejemplo, la raíz de idioma de la copia en inglés en la jerarquía de carpetas de ejemplo es `/content/dam/en`. Asegúrese de que la raíz del idioma esté configurada correctamente según la información de [Create a language root](#create-a-language-root).

1. Añada recursos al idioma principal.
1. Cree la raíz de idioma de cada idioma de destino para el que necesite una copia de idioma.

### Crear una raíz de idioma {#create-a-language-root}

Para crear la raíz del idioma, cree una carpeta y utilice un código de idioma ISO como valor de la propiedad Name . Después de crear la raíz del idioma, puede crear una copia del idioma en cualquier nivel dentro de la raíz del idioma.

Por ejemplo, la página raíz de la copia en idioma italiano de la jerarquía de ejemplo tiene `it` como propiedad Name . La propiedad Name se utiliza como nombre del nodo de recursos en el repositorio y, por lo tanto, determina la ruta de los recursos. (*&lt;server>:&lt;port>/assets.html/content/dam/it/*)

1. En la consola de Assets, pulse o haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Carpeta]** en el menú.
1. En el campo Nombre , escriba el código de país con el formato `<language-code>`.
1. Haga clic o pulse **[!UICONTROL Crear]**. La raíz del idioma se crea en la consola Recursos.

### Ver raíces de idioma {#view-language-roots}

La IU táctil proporciona un panel Referencias que muestra una lista de las raíces de idioma que se han creado en [!DNL Assets].

1. En la consola Assets, seleccione el idioma principal para el que desea crear copias de idioma.
1. Toque o haga clic en el icono de navegación global y elija **[!UICONTROL Referencias]** para abrir el panel Referencia.
1. En el panel Referencias, pulse o haga clic en **[!UICONTROL Textos en idiomas]**. El panel Textos en idiomas muestra las copias de idioma de los recursos.

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project}

Si utiliza esta opción, los recursos que desea traducir se copian en la raíz del idioma al que desea traducir. Según las opciones que elija, se crea un proyecto de traducción para los recursos en la consola Proyectos . Según la configuración, el proyecto de traducción se puede iniciar manualmente o se ejecuta automáticamente en cuanto se crea el proyecto de traducción.

1. En la interfaz de usuario de Assets, seleccione la carpeta de origen para la que desea crear una copia de idioma.
1. Abra el panel **[!UICONTROL Referencias]** y pulse o haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**.
1. Pulse o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear un nuevo proyecto de traducción]**.
1. En el campo **[!UICONTROL Título del proyecto]**, introduzca un título.
1. Toque o haga clic en **[!UICONTROL Crear]**. Los recursos de la carpeta de origen se copian en las carpetas de destino para las configuraciones regionales seleccionadas en el paso 4.
1. Para desplazarse a la carpeta, seleccione la copia de idioma y haga clic en **[!UICONTROL Mostrar en Assets]**.
1. Vaya a la consola Proyectos . La carpeta de traducción se copia en la consola Proyectos .
1. Abra la carpeta para ver el proyecto de traducción.
1. Toque o haga clic en el proyecto para abrir la página de detalles.
1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. En la interfaz de usuario de Assets, abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

>[!NOTE]
>
>Esta función está disponible tanto para recursos como para carpetas. Cuando se selecciona un recurso en lugar de una carpeta, toda la jerarquía de carpetas hasta la raíz del idioma se copia para crear una copia de idioma para el recurso.

### Agregar a un proyecto de traducción existente {#add-to-existing-translation-project}

Si utiliza esta opción, el flujo de trabajo de traducción se ejecuta para los recursos que agregue a la carpeta de origen después de ejecutar un flujo de trabajo de traducción anterior. Solo los recursos recién añadidos se copian en la carpeta de destino que contiene recursos traducidos anteriormente. En este caso no se crea ningún proyecto de traducción nuevo.

1. En la interfaz de usuario de Assets, vaya a la carpeta de origen que contiene recursos sin traducir.
1. Seleccione un recurso que desee traducir y abra el **[!UICONTROL panel Referencias]**. La sección **[!UICONTROL Textos en idiomas]** muestra el número de traducciones disponibles en ese momento.
1. Pulse o haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**. Se muestra una lista de las traducciones disponibles.
1. Pulse o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione los idiomas para los que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Agregar a proyecto de traducción]** existente para ejecutar el flujo de trabajo de traducción en la carpeta.
   >[!NOTE]
   >
   >Si elige la opción **[!UICONTROL Add to existing translation project]** , el proyecto de traducción se agregará a un proyecto preexistente solo si la configuración del proyecto coincide exactamente con la configuración del proyecto preexistente. De lo contrario, se crea un nuevo proyecto.
1. En la lista **[!UICONTROL Existing translation project]**, seleccione un proyecto para agregar el recurso para su traducción.
1. Pulse o haga clic en **[!UICONTROL Crear]**. Los recursos que se van a traducir se agregan a la carpeta de destino. La carpeta actualizada se muestra en la sección **[!UICONTROL Textos en idiomas]**.
1. Vaya a la consola Proyectos y abra el proyecto de traducción existente que ha agregado a.
1. Toque o haga clic en el proyecto de traducción para ver la página de detalles del proyecto.
1. Pulse o haga clic en los puntos suspensivos en la parte inferior del mosaico **Trabajo de traducción** para ver los recursos en el flujo de trabajo de traducción. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

   >[!NOTE]
   >
   >* Si elimina la entrada de etiquetas o metadatos, no se traducirá ninguna etiqueta ni metadatos para ninguno de los recursos.
   >* Si utiliza la traducción automática, los binarios de recursos no se traducen.
   >* Si el recurso que agrega al trabajo de traducción incluye subrecursos, selecciónelos y elimínelos para que la traducción continúe sin problemas.


1. Para iniciar la traducción de los recursos, toque o haga clic en la flecha del mosaico **[!UICONTROL Trabajo de traducción]** y seleccione **[!UICONTROL Inicio]** en la lista. Un mensaje notifica el inicio del trabajo de traducción.
1. Para ver el estado del trabajo de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Una vez finalizada la traducción, el estado cambia a Listo para revisión. Vaya a la interfaz de usuario de Assets y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

### Actualizar copias de idioma {#update-language-copies}

Ejecute este flujo de trabajo para traducir cualquier conjunto adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene recursos traducidos anteriormente. Según la elección de opciones, se crea un proyecto de traducción o se actualiza un proyecto de traducción existente para los nuevos recursos. El flujo de trabajo Update language Copies incluye las siguientes opciones:

* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project-1}

Si utiliza esta opción, el conjunto de recursos se agregará a un proyecto de traducción existente para actualizar la copia de idioma para la configuración regional que elija.

1. En la interfaz de usuario de Assets, seleccione la carpeta de origen en la que ha añadido una carpeta de recursos.
1. Abra el **[!UICONTROL panel Referencias]** y pulse o haga clic en **[!UICONTROL Textos en idiomas]**, situado en el apartado **[!UICONTROL Textos]** para mostrar la lista de textos en diferentes idiomas.
1. Seleccione la casilla de verificación que se encuentra delante de **[!UICONTROL Textos en idiomas]**, de esta forma, selecciona los textos disponibles en diferentes idiomas. Anule la selección de otros textos excepto el texto (textos) en el idioma correspondiente a las configuraciones regionales a las que desea traducir.
1. Toque o haga clic en **[!UICONTROL Actualizar copias de idioma]** en la parte inferior.
1. En la lista **[!UICONTROL Proyecto]**, elija **[!UICONTROL Agregar al proyecto de traducción existente]**.
1. En la lista **[!UICONTROL Existing translation project]**, seleccione un proyecto para agregar el recurso para su traducción.
1. Pulse o haga clic en **[!UICONTROL Iniciar]**.
1. Consulte los pasos 9-14 de [Agregar al proyecto de traducción existente](#add-to-existing-translation-project) para completar el resto del procedimiento.

### Crear copias de idioma temporales {#creating-temporary-language-copies}

Cuando se ejecuta un flujo de trabajo de traducción para actualizar una copia de idioma con versiones editadas de los recursos originales, la copia de idioma existente se conserva hasta que se aprueban los recursos traducidos. [!DNL Assets] almacena los recursos recién traducidos en una ubicación temporal y actualiza la copia de idioma existente después de aprobar explícitamente los recursos. Si rechaza los recursos, la copia de idioma permanece sin cambios.

1. Pulse o haga clic en la carpeta raíz de origen en **[!UICONTROL Textos en idiomas]** para la que ya ha creado un texto en un idioma y, a continuación, pulse o haga clic en **[!UICONTROL Mostrar en Assets]** para abrir la carpeta en [!DNL Assets].
1. En la interfaz de usuario de Assets, seleccione un recurso que ya haya traducido y pulse o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas para abrir el recurso en modo de edición.
1. Edite el recurso y, a continuación, guarde los cambios.
1. Realice los pasos 2-14 del procedimiento [Add to existing translation project](#add-to-existing-translation-project) para actualizar la copia de idioma.
1. Pulse o haga clic en los puntos suspensivos en la parte inferior del mosaico **[!UICONTROL Trabajo de traducción]**. Desde la lista de recursos de la página **[!UICONTROL Trabajo de traducción]**, puede ver claramente la ubicación temporal en la que se almacena la versión traducida del recurso.
1. Seleccione la casilla de verificación situada junto a **[!UICONTROL Title]**.
1. En la barra de herramientas, pulse o haga clic en **[!UICONTROL Aceptar traducción]** y, a continuación, pulse o haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para sobrescribir el recurso traducido en la carpeta de destino con la versión traducida del recurso editado.

   >[!NOTE]
   >
   >Para permitir que el flujo de trabajo de traducción actualice los recursos de destino, acepte el recurso y los metadatos.

   Pulse o haga clic en **[!UICONTROL Rechazar traducción]** para conservar la versión traducida originalmente del recurso en la raíz de configuración regional de destino y rechace la versión editada.

1. Vaya a la consola Recursos y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## Crear proyectos de traducción {#creating-translation-projects}

Para crear una copia de idioma, asigne un déclencheur a uno de los siguientes flujos de trabajo de copia de idioma disponibles en el carril Referencias de la interfaz de usuario de Assets:

**Crear y traducir**

En este flujo de trabajo, los recursos que se van a traducir se copian en la raíz del idioma al que se desea traducir. Además, según las opciones que elija, se crea un proyecto de traducción para los recursos en la consola Proyectos . Según la configuración, el proyecto de traducción se puede iniciar manualmente o se le puede permitir que se ejecute automáticamente en cuanto se cree el proyecto de traducción.

**Actualizar copias de idioma**

Ejecute este flujo de trabajo para traducir un grupo adicional de recursos e incluirlos en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se añaden a la carpeta de destino que ya contiene recursos traducidos anteriormente.

>[!NOTE]
>
>Los binarios de recursos solo se traducen si el proveedor de servicios de traducción admite la traducción de binarios.

>[!NOTE]
>
>Si inicia un flujo de trabajo de traducción para recursos complejos, como archivos PDF y archivos Adobe InDesign, sus subrecursos o representaciones (si hay) no se envían para su traducción.

### Creación y traducción de flujos de trabajo {#create-and-translate-workflow}

Utilice el flujo de trabajo crear y traducir para generar copias de idioma para un idioma en particular por primera vez. El flujo de trabajo ofrece las siguientes opciones:

* Crear solo una estructura
* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Crear solo una estructura {#create-structure-only}

Utilice la opción **Crear solo estructura** para diseñar una jerarquía de carpetas de destino dentro de la raíz del idioma de destino para que coincida con la jerarquía de la carpeta de origen dentro de la raíz del idioma de origen. En este caso, los recursos de origen se copian en la carpeta de destino. Sin embargo, no se genera ningún proyecto de traducción.

1. En la interfaz de usuario de Assets, seleccione la carpeta de origen para la que desea crear una estructura en la raíz del idioma de destino.
1. Abra el panel **[!UICONTROL Referencias]** y pulse o haga clic en **[!UICONTROL Textos en idiomas]** en **[!UICONTROL Textos]**.
1. Pulse o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista **[!UICONTROL Idiomas de destino]**, seleccione el idioma para el que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]**, seleccione **[!UICONTROL Crear estructura únicamente]**.
1. Pulse o haga clic en **[!UICONTROL Crear]**. La nueva estructura para el idioma de destino se muestra en **[!UICONTROL Textos en idiomas]**.
1. Pulse o haga clic en la estructura de la lista y, a continuación, pulse o haga clic en **[!UICONTROL Mostrar en recursos]** para desplazarse a la estructura de carpetas dentro del idioma de destino.

## Aplicar servicios de nube de traducción a carpetas {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager le permite utilizar los servicios de traducción basados en la nube del proveedor de traducción que elija para garantizar que sus recursos se traduzcan según sus necesidades.

Puede aplicar el servicio de nube de traducción directamente a la carpeta de recursos para que se puedan utilizar durante los flujos de trabajo de traducción.

### Aplique los servicios de traducción {#applying-the-translation-services}

La aplicación de servicios de traducción en la nube directamente a la carpeta de recursos elimina la necesidad de configurar servicios de traducción al crear o actualizar flujos de trabajo de traducción.

1. En la interfaz de usuario de Assets, seleccione la carpeta a la que desea aplicar los servicios de traducción.
1. En la barra de herramientas, pulse o haga clic en el icono **[!UICONTROL Propiedades]** para mostrar la página **[!UICONTROL Propiedades de la carpeta]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vaya a la pestaña **[!UICONTROL Cloud Services]**.
1. En la lista Configuraciones del Cloud Service , elija el proveedor de traducción deseado. Por ejemplo, si desea utilizar servicios de traducción de Microsoft, elija **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Seleccione el conector para el proveedor de traducción.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. En la barra de herramientas, pulse o haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. El servicio de traducción se aplica a la carpeta.

### Aplicar conector de traducción personalizado {#applying-custom-translation-connector}

Si desea aplicar un conector personalizado para los servicios de traducción que desea utilizar en los flujos de trabajo de traducción. Para aplicar un conector personalizado, primero instale el conector desde el Administrador de paquetes. A continuación, configure el conector desde la consola de Cloud Services. Después de configurar el conector, estará disponible en la lista de conectores de la pestaña Cloud Services que se describe en [Aplicación de los serviciosde traducción](#applying-the-translation-services). Después de aplicar el conector personalizado y ejecutar los flujos de trabajo de traducción, el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción muestra los detalles del conector en los encabezados **[!UICONTROL Proveedor]** y **[!UICONTROL Método]**.

1. Instale el conector desde el Administrador de paquetes.
1. Pulse o haga clic en el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas > Implementación > Cloud Services]**.
1. Coloque el conector que instaló en **[!UICONTROL Servicios de terceros]** en la página **[!UICONTROL Cloud Services]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Pulse o haga clic en el enlace **[!UICONTROL Configurar ahora]** para abrir el cuadro de diálogo **[!UICONTROL Crear configuración]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique un título y un nombre para el conector y, a continuación, pulse o haga clic en **[!UICONTROL Crear]**. El conector personalizado está disponible en la lista de conectores de la pestaña **[!UICONTROL Cloud Services]** que se describe en el paso 5 de [Aplicación de los servicios de traducción](#applying-the-translation-services).
1. Ejecute cualquier flujo de trabajo de traducción descrito en Creación de proyectos de traducción después de aplicar el conector personalizado. Compruebe los detalles del conector en el mosaico **[!UICONTROL Resumen de traducción]** del proyecto de traducción en la consola **[!UICONTROL Proyectos]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
