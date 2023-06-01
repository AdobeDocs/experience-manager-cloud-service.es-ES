---
title: Crear o agregar un formulario adaptable a la página de AEM Sites
description: Descubra cómo crear o agregar fácilmente un formulario adaptable a su página de AEM Sites. Conozca las técnicas paso a paso y las prácticas recomendadas para integrar formularios dinámicos y personalizables en su sitio web, optimizando las experiencias digitales para lograr el máximo impacto.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 3%

---


# Crear o agregar un formulario adaptable a la página de AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

Con AEM Forms, puede incorporar fácilmente formularios adaptables a sus páginas web. Esto permite a los visitantes rellenar y enviar formularios cómodamente sin salir de la página en la que se encuentran. Al hacerlo, pueden interactuar fácilmente con otros elementos del sitio web e interactuar activamente con el formulario.

Puede aprovechar al máximo esta función utilizando las siguientes opciones:

* **Agregar un formulario personalizado:** Cree un formulario nuevo desde cero y adáptelo específicamente a sus necesidades y preferencias de diseño.

* **Mejore los fragmentos de experiencias:** AEM Amplíe el alcance de los formularios añadiéndolos a los fragmentos de experiencias de la, lo que permite una reutilización perfecta en varias páginas o sitios.

* **Utilizar plantillas aprobadas:** Aproveche las plantillas aprobadas previamente para crear rápidamente formularios que se ajusten a las directrices de promoción de la marca y a los estándares de diseño de su organización.

* **Agregar formularios existentes:** Integre fácilmente formularios que ya haya creado en sus sitios web, lo que permite a los visitantes interactuar con ellos directamente.

* **Agregar varios formularios:**  Agregue varios formularios a una página para proporcionar varias opciones a los usuarios en función de sus preferencias y requisitos. Pueden ser una combinación de formularios nuevos desde cero y formularios existentes.

Puede utilizar el editor de AEM Sites para crear y agregar rápidamente varios formularios a las páginas de AEM Sites. El uso del editor de AEM Sites permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de una página de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de los procesos empresariales. También le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

## Objetivo

* Aprenda a crear un formulario adaptable mediante el editor de AEM Sites y el fragmento de experiencia
* Obtenga información sobre cómo establecer el diseño y la temática de un formulario adaptable agregado a una página de AEM Sites y
* Crear un formulario adaptable mediante el editor de AEM Sites y el fragmento de experiencia


## Consideraciones {#consideration}

AEM Forms proporciona el contenedor del formulario adaptable y los componentes incrustados de Forms adaptable. Puede utilizar el contenedor de formulario adaptable para crear y agregar un nuevo formulario en un fragmento de experiencia o una página de AEM Sites, mientras que el componente Forms adaptable incrustado le permite agregar un formulario adaptable existente o crear un nuevo formulario con el editor de Forms adaptable.

Cuando se utiliza el contenedor de formulario adaptable para crear o agregar un formulario, este se traduce y localiza a través del flujo de traducción de AEM Sites. Para cada idioma, se genera una copia independiente (copia de idioma) de la página de Sites y de los formularios correspondientes y, cuando un autor de contenido modifica una regla en un formulario de la página principal, se deben realizar los mismos cambios en todas las copias de idioma del formulario. El contenedor de formulario adaptable también le permite utilizar varias funciones de las páginas de AEM Sites, como versiones, segmentación, traducción y administrador de varios sitios.

Cuando se crea o se agrega un formulario con el componente incrustado del formulario adaptable, los formularios se traducen y localizan mediante el flujo de traducción de AEM Forms. En este caso, se mantiene un único formulario y se hace referencia a él en todas las copias de idioma de las páginas de Sites. El componente incrustado en el formulario adaptable no proporciona acceso a varias funciones de páginas de AEM Sites, como control de versiones, direccionamiento, traducción y administrador de varios sitios.


## Antes de comenzar {#before-you-start}

+++  Habilitar los componentes principales de Forms adaptables para su entorno

Asegúrese de que la variable [Los componentes principales de Forms adaptables están habilitados para su entorno as a Cloud Service de AEM Forms](enable-adaptive-forms-core-components.md).

+++

+++ Habilitar **[!UICONTROL Contenedor de Forms adaptable]

Para habilitar el [!UICONTROL Contenedor de formularios adaptables] en la política de la plantilla, siga los siguientes pasos:

1. Abra la página de AEM Sites para editarla. Para abrir la página y editarla, selecciónela y haga clic en Editar.
1. Abra la plantilla de la página de Sites. Para abrir la plantilla, vaya a [!UICONTROL Información de página] ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar plantilla]. Se abrirá la plantilla correspondiente en el editor de plantillas.
1. En la vista Estructura, haga clic en **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) en la barra de menús. En el **[!UICONTROL Componentes permitidos]** y seleccione la **[!UICONTROL Contenedor de Forms adaptable]**  en la casilla de verificación **[AEM Nombre de proyecto de tipo de archivo] - Formulario adaptable**.
1. Haga clic en **[!UICONTROL Listo]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  Añadir bibliotecas de cliente de Forms adaptables a la página de AEM Sites

Para habilitar la funcionalidad completa del componente Contenedor de Forms adaptable, agregue las bibliotecas de cliente Customheaderlibs y Customfooterlibs a la página de AEM Sites mediante la canalización de implementación. Para añadir las bibliotecas:

1. Acceso y clonación de su [Repositorio de Git de AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Abra la carpeta Repositorio de Git de AEM Cloud Service en un editor de texto de plan. Por ejemplo, Microsoft Visual Code.
1. Abra el `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` archivo para editar y anote el valor de `sling:resourceSuperType`. Por ejemplo, anote el valor `core/wcm/components/page/v3/page`.


   ![recurso de sling](/help/forms/assets/slingresource.png)

1. Vaya a `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` y cree una estructura de carpetas idéntica al valor anotado en el paso anterior. Por ejemplo, si el valor es similar al del paso anterior, la estructura final del nodo es `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![estructura de superposición](/help/forms/assets/overlaystructure.png)

1. Crear `customheaderlibs.html` y `customfooterlibs.html` archivos en la estructura de nodos creada en el paso anterior y agregue el siguiente contenido a los archivos:

   ```
        //Customheaderlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
        </sly> 
   
        //customfooterlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
        </sly> 
   ```

1. [Ejecutar la canalización de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) AEM para implementar las bibliotecas de cliente en el entorno as a Cloud Service.

+++

## Crear un formulario adaptable {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

AEM Puede crear un formulario completamente nuevo desde cero y adaptarlo específicamente a sus necesidades y preferencias de diseño, directamente en una página de sitios de o en un fragmento de experiencia. AEM Para los formularios de un solo uso, se recomienda la creación directa en una página de sitios de, mientras que los fragmentos de experiencias son ideales para los formularios que deben reutilizarse en varias páginas del sitio web.

* [Creación de un formulario en una página de AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creación de un formulario en un fragmento de experiencia](#create-an-adaptive-form-in-experience-fragment)

### Creación de un formulario en una página de AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puede utilizar el componente Contenedor de formulario adaptable en el editor de AEM Sites para crear un formulario personalizado. El componente le permite crear un formulario arrastrando y soltando sus componentes. Los componentes de formulario se basan en los componentes principales. Puede personalizarlos fácilmente según los requisitos de su organización.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para crear un formulario adaptable en una página de Sites:

1. Abra la página de AEM Sites en el modo de edición.
1. Arrastre y suelte el **[!UICONTROL Contenedor de Forms adaptable]** de Navegador de componentes a la página Sitios. Esto crea un espacio en la página para el formulario. Puede utilizar el modo Diseño para cambiar el tamaño del espacio del contenedor.
1. Arrastre y suelte los componentes principales del formulario adaptable en el espacio contenedor para crear el formulario.
1. Agregue el botón Enviar.

A continuación, establezca la acción de envío y las propiedades avanzadas.

### Creación de un formulario en un fragmento de experiencia {#create-an-adaptive-form-in-experience-fragment}

AEM Puede ampliar el alcance de los formularios añadiéndolos a los fragmentos de experiencias de la aplicación, lo que permite una reutilización perfecta en varias páginas o sitios. Por ejemplo, puede incluir un formulario de suscripción a un boletín informativo dentro de un Fragmento de experiencia. Esto le permite reutilizar convenientemente el fragmento en varias páginas del sitio web, lo que elimina la necesidad de volver a crear el formulario repetidamente. Las actualizaciones o modificaciones realizadas en el formulario de suscripción al boletín informativo dentro del fragmento de experiencia se propagan automáticamente a todas las páginas donde se utiliza. Esto optimiza el proceso y garantiza una experiencia de usuario perfecta a la vez que simplifica la administración de los formularios del sitio web.

Para crear un formulario adaptable en un fragmento de experiencia:

## Cambiar el diseño de un formulario adaptable {#change-layout-of-an-adaptive-form}

En la página de AEM Sites, utilice el [Modo Diseño](/help/sites-cloud/authoring/features/responsive-layout.md) para cambiar el tamaño de un componente Contenedor de formulario adaptable agregado a una página de AEM Sites.
