---
title: Cómo añadir un formulario adaptable a la página de AEM Sites
description: Descubra cómo crear o agregar fácilmente un formulario adaptable a su página de AEM Sites. Conozca las técnicas paso a paso y las prácticas recomendadas para integrar formularios en su sitio web y optimizar sus experiencias digitales para lograr el máximo impacto.
feature: Adaptive Forms, Page Editor, Authoring
Keywords: adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
source-git-commit: 53997540cc469f4cc2ad747ca4e52b531a7b193e
workflow-type: tm+mt
source-wordcount: '3232'
ht-degree: 70%

---


# Agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |
| AEM as a Cloud Service | Este artículo |

Con AEM Forms, puede agregar fácilmente un formulario a su página de AEM Sites. Esto permite a los visitantes rellenar y enviar formularios cómodamente sin salir de la página en la que se encuentran. Al hacerlo, pueden interactuar fácilmente con otros elementos del sitio web e interactuar activamente con el formulario.

Puede utilizar el Editor de páginas de AEM para crear y agregar rápidamente varios formularios a las páginas de AEM Sites. AEM El uso del editor de páginas de permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de una página de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de los procesos empresariales. También le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

El Cloud Service de AEM Forms proporciona el contenedor de formulario adaptable y los componentes incrustados de Forms adaptable. Puede utilizar el contenedor de formulario adaptable para crear un nuevo formulario en una página de AEM Sites o un fragmento de experiencia, mientras que el componente Forms adaptable incrustado le permite agregar un formulario adaptable existente o crear un nuevo formulario con el editor de Forms adaptable.

![Ejemplo de un formulario adaptable en una página de AEM Sites](/help/forms/assets/adaptive-form-in-sites-page.png)

## ¿Por qué utilizar los componentes principales de Forms adaptable para crear un formulario adaptable en una página de AEM Sites o un fragmento de experiencia?

Si ha creado formularios adaptables basados en Forms Foundation o en HTML simples para sus sitios en el pasado, Adobe recomienda utilizar los componentes principales de Forms adaptables para crear un formulario adaptable en una página de AEM Sites o un fragmento de experiencia. Permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios, lo que mejora la experiencia general de creación y administración de formularios para Forms adaptable. Vamos a explorar algunas de estas características:

* **Versiones:** Las páginas de AEM Sites ofrecen [sólidas capacidades de versiones](/help/sites-cloud/authoring/features/page-versions.md), lo que le permite realizar un seguimiento y administrar diferentes versiones de los formularios. Esto le permite realizar cambios y mejoras en los formularios al tiempo que se mantiene la capacidad de revertir a versiones anteriores si es necesario. El control de versiones garantiza un enfoque controlado y organizado del desarrollo y la evolución de los formularios.
* **Segmentación (integración con Adobe Target):** Con las funcionalidades de segmentación de páginas de AEM Sites, también puede [personalizar la experiencia del formulario para diferentes audiencias](/help/sites-cloud/integrating/integration-adobe-target-ims.md). Al aprovechar los segmentos de usuario y los criterios de segmentación, puede adaptar el contenido, diseño o comportamiento del formulario a grupos específicos de usuarios. Esto le permite proporcionar una experiencia de formulario personalizada y relevante, lo que aumenta las tasas de participación y conversión.
* **Traducción: Integración perfecta de** AEM Sites [con los servicios de traducción](/help/sites-cloud/administering/translation/overview.md), lo que le permite traducir fácilmente formularios a varios idiomas. Esta función simplifica el proceso de localización y garantiza que los formularios sean accesibles para una audiencia global. Puede administrar las traducciones de forma eficaz dentro de los proyectos de traducción de AEM, lo que reduce el tiempo y el esfuerzo necesarios para la asistencia con formularios multilingües. Consulte la sección Consideraciones para obtener más información sobre la traducción.
* **Administración de varios sitios y Live Copy:** AEM Sites proporciona [Funciones de administración de varios sitios y Live Copy](/help/sites-cloud/administering/msm/overview.md) sólidas, lo que permite crear y administrar varios sitios web en un único entorno. Ahora esta función le permite reutilizar formularios en diferentes sitios, lo que garantiza la consistencia y reduce los esfuerzos de duplicación. Con el control y la administración centralizados, puede mantener y actualizar de forma eficaz los formularios en varios sitios web.
* **Temáticas:** Las páginas de AEM Sites proporcionan un marco de trabajo para diseñar y mantener estilos visuales coherentes en varias páginas web. Estas definen colores, fuentes, hojas de estilo y otros elementos visuales que contribuyen a la apariencia general del sitio web. [Puede utilizar las temáticas diseñadas para una página de AEM Sites para un formulario adaptable, lo que ahorra tiempo y esfuerzo](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Etiquetado:** Las páginas de AEM Sites le permiten [asignar etiquetas a una página, a un recurso o a otro contenido](/help/implementing/developing/introduction/tagging-framework.md). Las etiquetas son palabras clave o etiquetas de metadatos que proporcionan una forma de categorizar y organizar el contenido en función de criterios específicos. Puede asignar una o más etiquetas a páginas, recursos o a cualquier otro elemento de contenido dentro de AEM para mejorar la búsqueda y la clasificación de los archivos.
* **Bloquear y desbloquear contenido:** AEM Sites permite a los usuarios [controlar el acceso y las modificaciones de páginas](/help/sites-cloud/authoring/fundamentals/editing-content.md) dentro del entorno de AEM Sites. Cuando una página está bloqueada, significa que está protegida contra cambios o ediciones no autorizados por parte de otros usuarios. Solo el usuario que ha bloqueado el contenido o un administrador designado pueden desbloquearlo para permitir modificaciones.

Además, Forms AEM adaptable en el editor de páginas de utiliza [Componentes principales de Forms adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es#features). Estos componentes principales proporcionan métodos estándar y más sencillos para aplicar estilos y personalizar los componentes, idénticos a los siguientes [Componentes de AEM Sites WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es).


## ¿Cómo se crea o se agrega un formulario adaptable en una página de AEM Sites AEM o en un fragmento de experiencia de la? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Puede aprovechar al máximo esta función utilizando las siguientes opciones:

* **[Crear y agregar un formulario adaptable personalizado a una página de AEM Sites](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Puede utilizar el componente Contenedor de formulario adaptable para crear un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño.

* **[Crear y agregar un formulario adaptable personalizado a un fragmento de experiencia](#create-an-adaptive-form-in-sites-editor):** AEM Puede ampliar el alcance de los formularios añadiéndolos a los fragmentos de experiencias de la aplicación, lo que permite una reutilización perfecta en varias páginas o sitios.

* **[Conversión de un formulario adaptable en un fragmento de experiencia](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Convertir un formulario adaptable agregado a una página de AEM Sites en un fragmento de experiencia para reutilizar el formulario en varias páginas de AEM Sites.

* **Agregar varios formularios a una página de AEM Sites o a un fragmento de experiencia:**  Puede crear o agregar varios Forms adaptables a una página de AEM Sites para proporcionar varias opciones a los usuarios en función de sus preferencias y requisitos. Pueden ser una combinación de formularios nuevos desde cero y formularios existentes.

* **Cree y agregue formularios basados en plantillas aprobadas a una página de AEM Sites:** Puede aprovechar las plantillas aprobadas previamente para crear rápidamente Forms adaptable que se ajuste a las directrices de promoción de la marca y a los estándares de diseño de su organización. La opción solo está disponible para los formularios adaptables creados con el Editor de formularios adaptables o Formularios adaptables: componente incrustado.

* **Agregar formularios existentes a una página de AEM Sites:** Puede integrar fácilmente formularios que ya haya creado en sus sitios web, lo que permite a los visitantes interactuar con ellos directamente. La opción solo está disponible para los formularios adaptables creados con el Editor de formularios adaptables o Formularios adaptables: componente incrustado.

## Consideraciones para crear un formulario adaptable en una página de AEM Sites AEM o un fragmento de experiencia de la {#consideration}

* Cuando se utiliza el Contenedor de formularios adaptables para crear o añadir un formulario, los formularios pasan por un proceso de traducción y localización a través del flujo de traducción de AEM Sites. Para cada idioma, se genera una copia independiente (copia de idioma) de la página de Sites y de los formularios correspondientes y, cuando un autor de contenido modifica una regla en un formulario de la página principal, se deben realizar los mismos cambios en todas las copias de idioma del formulario. El Contenedor de formularios adaptables también permite utilizar varias funcionalidades de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

* Cuando se crea o se añade un formulario utilizando el Formulario adaptable: componente incrustado, los formularios pasan por un proceso de traducción y localización utilizando el flujo de traducción de AEM Forms. En este caso, se mantiene un único formulario y se hace referencia a él en todas las copias de idioma de las páginas de Sites. El Formulario adaptable: componente incrustado no proporciona acceso a varias funcionalidades de páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.


## Requisitos para crear o agregar un formulario adaptable en una página de AEM Sites AEM o en un fragmento de experiencia de la aplicación de {#before-you-start-creating-an-adaptive-form}

Antes de empezar a crear o a crear un formulario adaptable, habilite los componentes principales de Forms adaptable y agregue las bibliotecas de cliente de Forms adaptables a su página de AEM Sites:

+++  Habilitar los componentes principales de Forms adaptables para su entorno de AEM Cloud Service

Asegúrese de que los [componentes principales de formularios adaptables estén habilitados para su entorno de AEM Forms as a Cloud Service](enable-adaptive-forms-core-components.md).

+++

+++  Añadir bibliotecas de cliente de Forms adaptables a su página de AEM Sites o fragmento de experiencia

Para habilitar la funcionalidad completa del componente Contenedor de formularios adaptables, añada las bibliotecas de cliente Customheaderlibs y Customfooterlibs a la página de AEM Sites mediante la canalización de implementación. Para añadir las bibliotecas:

1. Acceda a [Repositorio de Git de AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=es) y clónelo.
1. Abra la carpeta Repositorio de Git de AEM Cloud Service en un editor de texto del plan. Por ejemplo, Microsoft Visual Code.
1. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` y añada el siguiente código al archivo:

       ```
     //Customheaderlibs.html
     &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
     &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&#39;core.forms.components.runtime.all&#39;}&quot;/>
     &lt;/sly>
     
     ```
   
1. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` y añada el siguiente código al archivo:

       ```
     
     //customfooterlibs.html
     &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
     &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&#39;core.forms.components.runtime.all&#39;, async=true}&quot;/>
     &lt;/sly>
     ```
   
1. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` y añada el siguiente código al archivo:

       ```
     //Customheaderlibs.html
     &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
     &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&#39;core.forms.components.runtime.all&#39;}&quot;/>
     &lt;/sly>
     
     ```
   
1. Abra el archivo `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` y añada el siguiente código al archivo:

       ```
     
     //customfooterlibs.html
     &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
     &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&#39;core.forms.components.runtime.all&#39;, async=true}&quot;/>
     &lt;/sly>
     ```
   
1. [Ejecute la canalización de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) para implementar las bibliotecas de cliente en el entorno de AEM as a Cloud Service.

+++

+++ Habilitar el contenedor de formularios adaptables para su página de AEM Sites o fragmento de experiencia

Para habilitar el [!UICONTROL Contenedor de formularios adaptables] en la política de la plantilla, siga los siguientes pasos:

1. Abra la página de AEM Sites o el Fragmento de experiencia para editarlos. Para abrir la página para editarla, selecciónela y haga clic en Editar.
1. Abra la plantilla de su página Sites o Fragmento de experiencia. Para abrir la plantilla, vaya a [!UICONTROL Información de página] ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar plantilla]. Se abre la plantilla correspondiente en el editor de plantillas.
1. En la vista Estructura, haga clic en el icono **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) en la barra de menús. En la lista **[!UICONTROL Componentes permitidos]**, seleccione la casilla de verificación **[!UICONTROL Contenedor de formularios adaptables]** en **[Nombre de proyecto de tipo de archivo de AEM] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Crear un formulario adaptable {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puede crear un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño, directamente en una página de AEM Sites o en un Fragmento de experiencia. Para formularios de un solo uso, se recomienda la creación directa en una página de AEM Sites, mientras que los Fragmentos de experiencias son ideales para formularios que deben reutilizarse en varias páginas del sitio web.

* [Creación de un formulario en una página de AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creación de un formulario en un Fragmento de experiencia](#create-an-adaptive-form-in-experience-fragment)
* [Conversión de un formulario adaptable en una página de AEM Sites a un Fragmento de experiencia](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Creación de un formulario en una página de AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puede utilizar el componente Contenedor de formularios adaptables en el Editor de páginas de AEM para crear un formulario personalizado. El componente permite crear un formulario arrastrando y soltando los componentes del formulario. Los componentes de formulario se basan en los componentes principales. Puede personalizarlos fácilmente según los requisitos de su organización.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para crear un formulario adaptable en una página de Sites:

1. Abra la página de AEM Sites en el modo de edición.
1. Arrastre y suelte el componente **[!UICONTROL Contenedor de formularios adaptables]** del explorador de componentes a la página de Sites. Se creará un espacio en la página para el formulario. Puede utilizar el modo de diseño para cambiar el tamaño del espacio del contenedor.
1. Arrastre y suelte los componentes principales del formulario adaptable en el espacio del contenedor para crear el formulario.
1. Agregue el botón Enviar.

A continuación, [establezca la acción de envío](#configure-submit-action-for-form) y las propiedades avanzadas.

### Creación de un formulario en un Fragmento de experiencia {#create-an-adaptive-form-in-experience-fragment}

Puede ampliar el alcance de los formularios añadiéndolos a los Fragmentos de experiencias de AEM, lo que permite una reutilización perfecta en varias páginas o sitios. Por ejemplo, puede incluir un formulario de suscripción a una newsletter dentro de un Fragmento de experiencia. Esto le permite reutilizar convenientemente el fragmento en varias páginas del sitio web, lo que elimina la necesidad de volver a crear el formulario repetidamente. Las actualizaciones o modificaciones realizadas en el formulario de suscripción a la newsletter dentro del Fragmento de experiencia se propagan automáticamente a todas las páginas donde se utiliza. Esto optimiza el proceso y garantiza una experiencia de usuario perfecta a la vez que simplifica la administración de sus formularios del sitio web.

Para crear un formulario adaptable en un Fragmento de experiencia:

1. Abra un Fragmento de experiencia.
1. Arrastre y suelte el componente de **[!UICONTROL Contenedor de formularios adaptables]** del Explorador de componentes al Fragmento de experiencia.
1. Arrastre y suelte los componentes principales del formulario adaptable en el espacio contenedor del fragmento de experiencia para crear el formulario.
1. Agregue el botón Enviar.

A continuación, [establezca la acción de envío](#configure-submit-action-for-form) y las propiedades avanzadas.

### Conversión de un formulario en una página de AEM Sites en un fragmento de experiencia {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Puede convertir un formulario adaptable existente en un editor de páginas de Sites a un Fragmento de experiencia para reutilizar el formulario en varias páginas o sitios.

Para convertir un formulario adaptable en una página de AEM Sites en un Fragmento de experiencia:

1. Abra la página de AEM Sites que contiene el formulario adaptable (en el componente Contenedor de formularios adaptables) en el modo Editar.
1. Abra el árbol de contenido y seleccione el **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. En la barra de menús, seleccione el ![Icono Convertir para la variación del fragmento de experiencia](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Icono Convertir en variación de Fragmento de experiencia.
   ![Haga clic en el logotipo del archivador para convertir un formulario adaptable de la página de AEM Sites en un fragmento de experiencia](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Aparece un cuadro de diálogo para convertir el contenedor del formulario adaptable a un nuevo fragmento de experiencia o agregar a un fragmento de experiencia existente
1. En el cuadro de diálogo Convertir en variación de Fragmento de experiencia, establezca los valores de las siguientes opciones:

   * **Acción:** Seleccione para crear un nuevo fragmento de experiencia o Añadir a un Fragmento de experiencia existente.
   * **Ruta principal:** Especifique la ruta de la carpeta en la que se alojará el Fragmento de experiencia. La opción solo está disponible para crear un nuevo Fragmento de experiencia.
   * **Plantilla:** Especifique la ruta de la plantilla del Fragmento de experiencia. Si no tiene una plantilla de fragmento de experiencia, [crearlo](/help/implementing/developing/extending/experience-fragments.md). La opción solo está disponible para agregar formularios adaptables a un Fragmento de experiencia existente.
   * **Título del fragmento:** Especifique el título del Fragmento de experiencia. El título identifica de forma exclusiva un Fragmento de experiencia


## Configurar la acción de envío para un formulario en una página de AEM Sites o un fragmento de experiencia {#configure-submit-action-for-form}

Una acción de envío permite elegir el destino de los datos capturados mediante un formulario adaptable. Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Los formularios adaptables incluyen algunas acciones de envío listas para usar. También puede ampliar las acciones de envío predeterminadas para crear su propia acción de envío personalizada. Para configurar una acción de envío para el formulario:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de las propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar las acciones de envío.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una acción de envío](/help/forms/assets/adaptive-forms-container.png)
1. Seleccione y configure una acción de envío según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](/help/forms/configuring-submit-actions.md)


## Configurar un esquema o un modelo de datos de formulario para un formulario en página de AEM Sites o fragmento de experiencia {#configure-schema-or-data-model-for-form}

Puede utilizar el modelo de datos del formulario para conectar un formulario a una fuente de datos para enviar y recibir datos en función de las acciones del usuario. También puede conectar un formulario a un esquema JSON para recibir los datos enviados en un formato predefinido. En función del requisito, conecte el formulario a un esquema JSON o a un modelo de datos de formulario:

* [Crear un esquema JSON y cargarlo en su entorno](/help/forms/adaptive-form-json-schema-form-model.md)  o,
* [Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)

Para configurar un esquema JSON o un modelo de datos de formulario para su formulario:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar un modelo de datos para el formulario adaptable](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Seleccione y configure un esquema JSON o un modelo de datos de formulario según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](/help/forms/configuring-submit-actions.md).

   * Al seleccionar la variable **[!UICONTROL Modelo de formulario]**, utilice la opción **[!UICONTROL Seleccionar modelo de datos de formulario]** para seleccionar un modelo de datos de formulario preconfigurado.
   * Al seleccionar la opción **[!UICONTROL Esquema]**, utilice la opción **[!UICONTROL Esquema]** para seleccionar un esquema JSON para el formulario.

1. Haga clic en **[!UICONTROL Listo]**.

## Configurar un servicio de rellenado previo para un formulario en página de AEM Sites o fragmento de experiencia {#configure-prefill-service-for-form}

Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Puede hacer lo siguiente:

* [Crear un servicio de rellenado previo personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Servicio de rellenado previo de modelo de datos de formulario](#fdm-prefill-service)

### Utilice el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario en la página de AEM Sites o en el fragmento de experiencia {#fdm-prefill-service}

Puede utilizar el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable en una página de AEM Sites o un fragmento de experiencia mediante un modelo de datos de formulario o un servicio de prerrellenado personalizado. El servicio de rellenado previo del modelo de datos de formulario utiliza el [Obtener servicio del modelo de datos de formulario configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar datos. Para utilizar el servicio de rellenado previo del modelo de datos de formulario de un formulario adaptable, haga lo siguiente:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.
1. Haga clic en el icono de propiedades del contenedor del formulario adaptable ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar el servicio de rellenado previo](/help/forms/assets/adaptive-forms-container.png)
1. Seleccionar modelo de datos de formulario. Abra la pestaña **[!UICONTROL Básico]**. En el servicio de relleno previo, seleccione **[!UICONTROL Servicio de prerrellenado del modelo de datos de formulario]**.
1. Haga clic en **[!UICONTROL Listo]**. El formulario adaptable ahora está configurado para utilizar el prerrellenado del modelo de datos de formulario. Ahora puede usar la variable [editor de reglas](rule-editor.md) para crear reglas para rellenar previamente los campos del formulario.


## Redirigir al usuario a una página o mostrar un mensaje de agradecimiento al enviar el formulario

Al enviar un formulario, puede redirigir al usuario a otra página web o a un mensaje. Para redirigir al usuario o configurar el mensaje de agradecimiento:

1. Abra el Editor de páginas de AEM o el Fragmento de experiencia que contiene el formulario adaptable.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de formularios adaptables]** que aloja su formulario adaptable. Una página de AEM Sites puede alojar varios formularios adaptables. Por lo tanto, seleccione cuidadosamente el contenedor de formularios adaptables correcto.

1. Abra la pestaña **[!UICONTROL Envío]**.

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione **[!UICONTROL Redirigir a URL]** y examine y seleccione una página de AEM Sites, o proporcione la URL de una página externa.

   * Para configurar un mensaje personalizado o de agradecimiento, para en la opción Enviar, seleccione **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en la **[!UICONTROL Contenido del mensaje]** cuadro. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

## Ver siguiente

* [Crear estilos o temáticas para los formularios](using-themes-in-core-components.md)
* [Agregar un comportamiento dinámico a los formularios mediante el editor de reglas](rule-editor.md)
* [Definir la presentación de los formularios para diferentes tamaños de pantalla y tipos de dispositivos](/help/sites-cloud/authoring/features/responsive-layout.md)


## Artículo relacionado {#related-article}

* [Crear un formulario adaptable independiente basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es)

