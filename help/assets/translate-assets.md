---
title: Cree y gestione recursos digitales en varios idiomas y ejecute flujos de trabajo de traducción
description: Aprenda a automatizar los flujos de trabajo para traducir recursos, incluidos binarios, metadatos y etiquetas en varios idiomas.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Recursos multilingües {#multilingual-assets}

Recursos multilingües significa recursos con binarios, metadatos y etiquetas en varios idiomas. Generalmente, los binarios, metadatos y etiquetas de recursos existen en un idioma, que luego se traducen a otros idiomas para su uso en proyectos multilingües. Recursos Adobe Experience Manager (AEM) le permite automatizar los flujos de trabajo de traducción en recursos (incluidos binarios, metadatos y etiquetas) para generar recursos en otros idiomas y utilizarlos en proyectos multilingües.

Para automatizar los flujos de trabajo de traducción, integre proveedores de servicios de traducción con AEM y cree proyectos para traducir recursos a varios idiomas. AEM admite flujos de trabajo de traducción automática y humana.

Traducción humana: Los recursos traducidos se devuelven e importan en AEM. Cuando el proveedor de traducción está integrado con AEM, los recursos se envían automáticamente entre AEM y el proveedor de traducción.

Traducción automática: El servicio de traducción automática traduce inmediatamente los metadatos y las etiquetas de los recursos.

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only 1 master article.

https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/translation-projects.html
https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://docs.adobe.com/content/help/en/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting AEM with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## Preparación de recursos para su traducción {#prepare-assets-for-translation}

Recursos multilingües significa recursos con binarios, metadatos y etiquetas en varios idiomas. Generalmente, los binarios, metadatos y etiquetas de recursos existen en un idioma, que luego se traducen a otros idiomas para su uso en proyectos multilingües.

En Recursos Adobe Experience Manager (AEM), los recursos multilingües se incluyen en las carpetas, donde cada carpeta contiene los recursos en un idioma diferente.

Cada carpeta de idioma se denomina copia de idioma. La carpeta raíz de una copia de idioma, conocida como raíz de idioma, identifica el idioma del contenido en la copia de idioma. Por ejemplo, `/content/dam/it` es la raíz de idioma italiano para la copia en idioma italiano. Las copias de idioma deben utilizar una raíz [de idioma](#create-a-language-root) correctamente configurada para que el idioma correcto se dirija al realizar las traducciones de recursos de origen.

La copia de idioma para la que se agregaron recursos originalmente es el maestro de idioma. El maestro de idiomas es la fuente que se traduce a otros idiomas. Una jerarquía de carpetas de ejemplo incluye varias raíces de idioma:

```
/content
&nbsp; &nbsp; /- dam
&nbsp; &nbsp; &nbsp; |- en
&nbsp; &nbsp; &nbsp; |- fr
&nbsp; &nbsp; &nbsp; |- de
&nbsp; &nbsp; &nbsp; |- es
&nbsp; &nbsp; &nbsp; |- it
&nbsp; &nbsp; &nbsp; |- ja
&nbsp; &nbsp; &nbsp; |- zh
```

Realice los siguientes pasos para preparar los recursos para la traducción:

1. Cree la raíz del idioma del maestro de idioma. Por ejemplo, la raíz de idioma de la copia en inglés en la jerarquía de carpetas de ejemplo es */content/dam/en*. Asegúrese de que la raíz del idioma está configurada correctamente según la información de [Crear una raíz](#create-a-language-root)de idioma.

1. Agregue recursos al maestro de idioma.
1. Cree la raíz de idioma de cada idioma de destino para el que necesite una copia de idioma.

### Crear una raíz de idioma {#create-a-language-root}

Para crear la raíz de idioma, cree una carpeta y utilice un código de idioma ISO como valor para la propiedad Name. Después de crear la raíz del idioma, puede crear una copia del idioma en cualquier nivel dentro de la raíz del idioma.

Por ejemplo, la página raíz de la copia en idioma italiano de la jerarquía de muestra tiene `it` como propiedad Name. La propiedad Name se utiliza como nombre del nodo de recursos en el repositorio y, por lo tanto, determina la ruta de los recursos. (*&lt;servidor>:&lt;puerto>/assets.html/content/dam/it/*)

1. En la consola Recursos, toque o haga clic en **[!UICONTROL Crear]** y elija **[!UICONTROL Carpeta]** en el menú.
1. En el campo Nombre, escriba el código de país en el formato de `<language-code>`.
1. Haga clic o pulse **[!UICONTROL Crear]**. La raíz del idioma se crea en la consola Recursos.

### Ver las raíces del idioma {#view-language-roots}

La IU táctil proporciona un panel Referencias que muestra una lista de las raíces de idioma que se han creado en Recursos AEM.

1. En la consola Recursos, seleccione el maestro de idioma para el que desea crear copias de idioma.
1. Toque o haga clic en el icono de GlobalNav y elija **[!UICONTROL Referencias]** para abrir el panel Referencia.
1. En el panel Referencias, toque o haga clic en **[!UICONTROL Copias]** de idioma. El panel Copias de idioma muestra las copias de idioma de los recursos.

### Crear un nuevo proyecto de traducción {#create-a-new-translation-project}

Si utiliza esta opción, los recursos que se van a traducir se copian en la raíz del idioma en el que desea traducir. Según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción se puede iniciar manualmente o automáticamente en cuanto se cree el proyecto de traducción.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen para la que desea crear una copia de idioma.
1. Abra el panel **[!UICONTROL Referencias]** y toque o haga clic en **[!UICONTROL Copias]** de idioma en **[!UICONTROL Copias]**.
1. Toque o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista Idiomas **[!UICONTROL de]** destino, seleccione los idiomas para los que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]** , seleccione **[!UICONTROL Crear un nuevo proyecto]** de traducción.
1. En el campo Título **[!UICONTROL del]** proyecto, introduzca un título para el proyecto.
1. Toque o haga clic en **[!UICONTROL Crear]**. Los recursos de la carpeta de origen se copian en las carpetas de destino para las configuraciones regionales seleccionadas en el paso 4.
1. Para desplazarse a la carpeta, seleccione la copia de idioma y haga clic en **[!UICONTROL Mostrar en recursos]**.
1. Vaya a la consola Proyectos. La carpeta de traducción se copia en la consola Proyectos.
1. Abra la carpeta para ver el proyecto de traducción.
1. Toque o haga clic en el proyecto para abrir la página de detalles.
1. Para ver el estado del trabajo de traducción, haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción. <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. En la interfaz de usuario de Recursos, abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

>[!NOTE]
>
>Esta función está disponible para recursos y carpetas. Cuando se selecciona un recurso en lugar de una carpeta, se copia toda la jerarquía de carpetas hasta la raíz del idioma para crear una copia de idioma para el recurso.

### Add to an existing translation project {#add-to-existing-translation-project}

Si utiliza esta opción, el flujo de trabajo de traducción se ejecuta para los recursos que agregue a la carpeta de origen después de ejecutar un flujo de trabajo de traducción anterior. Solo los recursos recién añadidos se copian en la carpeta de destino que contiene recursos traducidos anteriormente. En este caso no se crea ningún proyecto de traducción nuevo.

1. En la interfaz de usuario de Recursos, navegue a la carpeta de origen que contenga recursos sin traducir.
1. Seleccione un recurso que desee traducir y abra el panel **** Referencia. La sección Copias **[!UICONTROL de]** idioma muestra el número de copias de traducción disponibles en ese momento.
1. Toque o haga clic en **[!UICONTROL Copias]** de idioma en **[!UICONTROL Copias]**. Se muestra una lista de las copias de traducción disponibles.
1. Toque o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista Idiomas **[!UICONTROL de]** destino, seleccione los idiomas para los que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]** , seleccione **[!UICONTROL Agregar a proyecto]** de traducción existente para ejecutar el flujo de trabajo de traducción en la carpeta.
   >[!NOTE]
   >
   >Si selecciona la opción **[!UICONTROL Agregar a proyecto]** de traducción existente, el proyecto de traducción se agrega a un proyecto preexistente solo si la configuración del proyecto coincide exactamente con la del proyecto preexistente. De lo contrario, se crea un nuevo proyecto.
1. En la lista de proyectos **[!UICONTROL de traducción]** existentes, seleccione un proyecto para agregar el recurso para la traducción.
1. Click/tap **[!UICONTROL Create]**. Los recursos que se van a traducir se agregan a la carpeta de destino. La carpeta actualizada se muestra en la sección Copias **[!UICONTROL de]** idioma.
1. Vaya a la consola Proyectos y abra el proyecto de traducción existente que ha agregado.
1. Toque o haga clic en el proyecto de traducción para ver la página de detalles del proyecto.
1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. En la lista de trabajos de traducción también se muestran las entradas para los metadatos y las etiquetas de los recursos. Estas entradas indican que los metadatos y las etiquetas de los recursos también se traducen.

   >[!NOTE]
   >
   >* Si elimina la entrada de etiquetas o metadatos, no se traducirá ninguna etiqueta o metadatos para ninguno de los recursos.
   >* Si utiliza Traducción automática, los binarios de recursos no se traducen.
   >* Si el recurso que agrega al trabajo de traducción incluye subrecursos, selecciónelos y elimínelos para que la traducción continúe sin problemas.


1. Para iniciar la traducción de los recursos, toque o haga clic en la flecha del mosaico Trabajo **[!UICONTROL de]** traducción y seleccione **[!UICONTROL Iniciar]** en la lista. Un mensaje notifica el inicio del trabajo de traducción.
1. Para ver el estado del trabajo de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción. <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. Una vez finalizada la traducción, el estado cambia a Listo para revisar. Vaya a la interfaz de usuario de Recursos y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

### Actualizar copias de idioma {#update-language-copies}

Ejecute este flujo de trabajo para traducir cualquier conjunto adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se agregan a la carpeta de destino que ya contiene recursos traducidos anteriormente. Según la elección de opciones, se crea un proyecto de traducción o se actualiza un proyecto de traducción existente para los nuevos recursos. El flujo de trabajo Actualizar copias de idioma incluye las siguientes opciones:

* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Añadir a un proyecto de traducción existente {#add-to-existing-translation-project-1}

Si utiliza esta opción, el conjunto de recursos se agrega a un proyecto de traducción existente para actualizar la copia de idioma de la configuración regional que elija.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen en la que ha agregado una carpeta de recursos.
1. Abra el panel **** Referencias y toque o haga clic en Copias **[!UICONTROL de]** idioma en **[!UICONTROL Copias]** para mostrar la lista de copias de idioma.
1. Seleccione la casilla de verificación antes de **[!UICONTROL Copias]** de idioma, que selecciona todas las copias de idioma. Anule la selección de otras copias excepto la copia del idioma (copias) correspondiente a las configuraciones regionales a las que desea traducir.
1. Toque o haga clic en **[!UICONTROL Actualizar copias]** de idioma en la parte inferior.
1. En la lista **[!UICONTROL Proyecto]** , elija **[!UICONTROL Agregar a proyecto]** de traducción existente.
1. En la lista de proyectos **[!UICONTROL de traducción]** existentes, seleccione un proyecto para agregar el recurso para la traducción.
1. Toque o haga clic en **[!UICONTROL Iniciar]**.
1. Consulte los pasos 9 a 14 de [Agregar al proyecto](#add-to-existing-translation-project) de traducción existente para completar el resto del procedimiento.

### Crear copias temporales de idioma {#creating-temporary-language-copies}

Cuando se ejecuta un flujo de trabajo de traducción para actualizar una copia de idioma con versiones editadas de los recursos originales, la copia de idioma existente se conserva hasta que se aprueban los recursos traducidos. AEM Assets almacena los recursos recién traducidos en una ubicación temporal y actualiza la copia de idioma existente después de aprobar explícitamente los recursos. Si rechaza los recursos, la copia de idioma permanece sin cambios.

1. Toque o haga clic en la carpeta raíz de origen en Copias **[!UICONTROL de]** idioma para la que ya ha creado una copia de idioma y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]** para abrir la carpeta en Recursos AEM.
1. En la interfaz de usuario de Recursos, seleccione un recurso que ya haya traducido y toque o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas para abrir el recurso en modo de edición.
1. Edite el recurso y guarde los cambios.
1. Realice los pasos 2 a 14 del procedimiento [Agregar al proyecto](#add-to-existing-translation-project) de traducción existente para actualizar la copia del idioma.
1. Toque o haga clic en los puntos suspensivos en la parte inferior del mosaico Trabajo **[!UICONTROL de]** traducción. En la lista de recursos de la página Trabajo **[!UICONTROL de]** traducción, puede ver claramente la ubicación temporal en la que se almacena la versión traducida del recurso.
1. Seleccione la casilla de verificación situada junto a **[!UICONTROL Título]**.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Aceptar traducción]** y, a continuación, toque o haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para sobrescribir el recurso traducido en la carpeta de destino con la versión traducida del recurso editado.

   >[!NOTE]
   >
   >Para habilitar el flujo de trabajo de traducción para actualizar los recursos de destino, acepte tanto el recurso como los metadatos.

   Toque o haga clic en **[!UICONTROL Rechazar traducción]** para conservar la versión traducida originalmente del recurso en la raíz de configuración regional de destino y rechazar la versión editada.

1. Vaya a la consola Recursos y abra la página Propiedades de cada uno de los recursos traducidos para ver los metadatos traducidos.

Para obtener sugerencias sobre la traducción eficiente de metadatos para recursos, consulte [5 pasos para traducir metadatos](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/)de forma eficaz.

## Creación de proyectos de traducción {#creating-translation-projects}

Para crear una copia de idioma, active uno de los siguientes flujos de trabajo de copia de idioma disponibles en el carril Referencias de la interfaz de usuario de Recursos:

**Crear y traducir**

En este flujo de trabajo, los recursos que se van a traducir se copian en la raíz de idioma del idioma al que se desea traducir. Además, según las opciones que elija, se creará un proyecto de traducción para los recursos en la consola Proyectos. Según la configuración, el proyecto de traducción puede iniciarse manualmente o puede ejecutarse automáticamente en cuanto se cree el proyecto de traducción.

**Actualizar copias de idioma**

Este flujo de trabajo se ejecuta para traducir un grupo adicional de recursos e incluirlo en una copia de idioma para una configuración regional concreta. En este caso, los recursos traducidos se agregan a la carpeta de destino que ya contiene recursos traducidos anteriormente.

>[!NOTE]
>
>Los binarios de recursos solo se traducen si el proveedor de servicios de traducción admite la traducción de binarios.

>[!NOTE]
>
>Si inicia un flujo de trabajo de traducción para recursos complejos, como archivos PDF y archivos de Adobe InDesign, sus subrecursos o representaciones (si los hay) no se envían para su traducción.

### Crear y traducir flujos de trabajo {#create-and-translate-workflow}

El flujo de trabajo de creación y traducción se utiliza para generar copias de idiomas para un idioma determinado por primera vez. El flujo de trabajo ofrece las siguientes opciones:

* Crear solo una estructura
* Crear un nuevo proyecto de traducción
* Añadir a un proyecto de traducción existente

### Crear solo una estructura {#create-structure-only}

Utilice la opción **Crear sólo** estructura para crear una jerarquía de carpetas de destino dentro de la raíz del idioma de destino para que coincida con la jerarquía de la carpeta de origen dentro de la raíz del idioma de origen. En este caso, los recursos de origen se copian en la carpeta de destino. Sin embargo, no se genera ningún proyecto de traducción.

1. En la interfaz de usuario de Recursos, seleccione la carpeta de origen para la que desea crear una estructura en la raíz del idioma de destino.
1. Abra el panel **[!UICONTROL Referencias]** y toque o haga clic en **[!UICONTROL Copias]** de idioma en **[!UICONTROL Copias]**.
1. Toque o haga clic en **[!UICONTROL Crear y traducir]** en la parte inferior.
1. En la lista Idiomas **[!UICONTROL de]** destino, seleccione el idioma para el que desea crear una estructura de carpetas.
1. En la lista **[!UICONTROL Proyecto]** , elija **[!UICONTROL Crear estructura únicamente]**.
1. Click/tap **[!UICONTROL Create]**. La nueva estructura del idioma de destino se muestra en Copias **[!UICONTROL de idioma]**.
1. Toque o haga clic en la estructura de la lista y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]** para desplazarse a la estructura de carpetas dentro del idioma de destino.

## Aplicar servicios de traducción en la nube a las carpetas {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager (AEM) le permite utilizar los servicios de traducción basados en la nube del proveedor de traducción que elija para garantizar que los recursos se traducen según sus necesidades.

Puede aplicar el servicio de traducción en la nube directamente a la carpeta de recursos para que se puedan utilizar durante los flujos de trabajo de traducción.

### Aplicar los servicios de traducción {#applying-the-translation-services}

La aplicación de servicios de traducción en la nube directamente a la carpeta de recursos elimina la necesidad de configurar servicios de traducción al crear o actualizar flujos de trabajo de traducción.

1. En la interfaz de usuario de Recursos, seleccione la carpeta a la que desea aplicar los servicios de traducción.
1. En la barra de herramientas, toque o haga clic en el icono **[!UICONTROL Propiedades]** para mostrar la página Propiedades **[!UICONTROL de la]** carpeta.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Vaya a la ficha **[!UICONTROL Cloud Services]** .
1. En la lista Configuraciones del servicio de nube, elija el proveedor de traducción deseado. Por ejemplo, si desea utilizar los servicios de traducción de Microsoft, elija **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Elija el conector para el proveedor de traducción.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo.El servicio de traducción se aplica a la carpeta.

### Aplicar conector de traducción personalizada {#applying-custom-translation-connector}

Si desea aplicar un conector personalizado para los servicios de traducción que desea utilizar en los flujos de trabajo de traducción. Para aplicar un conector personalizado, primero instale el conector desde el Administrador de paquetes. A continuación, configure el conector desde la consola de Cloud Services. Después de configurar el conector, estará disponible en la lista de conectores de la ficha Cloud Services que se describe en [Aplicación de los servicios](#applying-the-translation-services)de traducción. Después de aplicar el conector personalizado y ejecutar los flujos de trabajo de traducción, el mosaico Resumen **[!UICONTROL de]** traducción del proyecto de traducción muestra los detalles del conector en los encabezados **[!UICONTROL Proveedor]** y **[!UICONTROL Método]**.

1. Instale el conector desde el Administrador de paquetes.
1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas > Implementación > Servicios]** de nube.
1. Ubique el conector que instaló en Servicios **[!UICONTROL de]** terceros en la página Servicios **[!UICONTROL de]** nube.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Toque o haga clic en el vínculo **[!UICONTROL Configurar ahora]** para abrir el cuadro de diálogo **[!UICONTROL Crear configuración]** .

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Especifique un título y un nombre para el conector y, a continuación, toque o haga clic en **[!UICONTROL Crear]**. El conector personalizado está disponible en la lista de conectores de la ficha Servicios **[!UICONTROL de]** nube que se describe en el paso 5 de [Aplicación de los servicios](#applying-the-translation-services)de traducción.
1. Ejecute cualquier flujo de trabajo de traducción descrito en la creación de proyectos de traducción después de aplicar el conector personalizado. Compruebe los detalles del conector en el mosaico Resumen **[!UICONTROL de]** traducción del proyecto de traducción en la consola **[!UICONTROL Proyectos]** .

   ![chlimage_1-220](assets/chlimage_1-220.png)
