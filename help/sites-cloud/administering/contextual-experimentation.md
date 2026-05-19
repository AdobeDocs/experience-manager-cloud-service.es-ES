---
title: Experimentación contextual en AEM as a Cloud Service
description: Aprenda a utilizar el carril de experimentación para añadir capacidades de experimentación al sitio.
feature: Administering
role: Admin
exl-id: 420f8d5e-27f9-4081-b174-b2d7752779f7
source-git-commit: ca9d8326f1c628bd3129aeda1f2d0d0c3386d60e
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 2%

---

# Experimentación contextual en AEM as a Cloud Service {#contextual-experimentation}

La experimentación es la práctica de probar el diseño, la funcionalidad y el código del sitio para mejorar el rendimiento y hacer que el sitio sea más eficaz y optimizado. Esto se logra cambiando el contenido o la funcionalidad, comparando los resultados con una versión anterior y seleccionando las mejoras que tienen efectos mensurables.

Cuando se hace correctamente, es un patrón potente para mejorar las conversiones, la participación y la experiencia del visitante. En general, hay un par de problemas que se deben evitar al intentar adoptar la práctica:

* **Demasiado poco**: la mayoría de las empresas no están experimentando lo suficiente y, cuando lo hacen, experimentan con muy poco tráfico para obtener resultados significativos.
* **Demasiado lento**: muchos marcos de experimentación ralentizan tanto el sitio que las posibles nuevas conversiones no pueden compensar el tráfico perdido y las devoluciones debido a la lentitud del procesamiento.
* **Demasiado complejo**: si se tarda demasiado en configurar un experimento nuevo, se ejecutarán menos experimentos.

Para los sitios que se ejecutan en Adobe Experience Manager, los desarrolladores tienen la opción de agregar una nueva capacidad de experimentación a sus sitios. Tres cosas hacen que este enfoque sea diferente de otros marcos de experimentación:

* Es fácil configurar pruebas con las herramientas con las que los autores ya están familiarizados y no se necesita un inicio de sesión independiente.
* Está profundamente integrado en el sistema de entrega de AEM, no ralentiza el sitio y es resistente a los cambios en el código y el contenido.
* Permite probar cambios de contenido sencillos, así como experimentos que abarcan diseño, funcionalidad y código.

## Carril de experimentación {#experimentation-rail}

El carril de experimentación es la forma principal de configurar experimentos. Se puede usar con su proyecto en un contexto [Edge Delivery Services](/help/edge/overview.md) o en el [Editor universal](/help/implementing/universal-editor/introduction.md). Como tal, necesitarás una cuenta de Github, un repositorio de contenido como SharePoint o Google Drive, y también el complemento [AEM Sidekick](https://www.aem.live/docs/sidekick). Si desea usar el editor universal, también necesitará acceso a un [entorno de AEM as a Cloud Service](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Consulte también la [página Introducción: Tutorial para desarrolladores de Universal Editor](https://www.aem.live/developer/tutorial).

>[!WARNING]
>Se requiere el motor de experimentación para utilizar la capacidad de experimentación. Asegúrese de que el motor esté instalado y actualizado correctamente antes de implementar los pasos siguientes. Consulte la siguiente [página de instalación](https://github.com/adobe/aem-experimentation/tree/v2?tab=readme-ov-file#installation) para obtener más información.

### Configuración de la experimentación mediante AEM Sidekick en Edge Delivery Services

Para acceder a las funcionalidades del carril de experimentación dentro de su proyecto de Edge Delivery Services, necesitará el complemento [AEM Sidekick](https://www.aem.live/docs/sidekick). Para configurar la barra de tareas, siga estos pasos:

1. Agregue la [extensión de la barra de tareas de AEM](https://chromewebstore.google.com/search/AEM%20Sidekick?hl=en-US&utm_source=ext_sidebar) y ancla en su explorador.
1. Abra la página del proyecto en el modo de vista previa.
1. En la barra de AEM Sidekick, haga clic en el icono de configuración ![Configuración](/help/sites-cloud/administering/assets/settings-1.png) y seleccione **Agregar este proyecto**.
1. Haga clic en la pestaña Experimentación para abrir el carril de experimentación.

### Configuración de la experimentación en el editor universal

Antes de configurar experimentos, tenga en cuenta que deberá utilizar sitios de AEM como fuente de contenido para poder crear en el editor universal. Si es necesario, puede convertir el proyecto existente en sitios de AEM como fuente de contenido siguiendo el tutorial presentado en la página [Configurar AEM Sites como Source de contenido](https://www.aem.live/developer/ue-tutorial). Cuando esté listo para configurar experimentos en el Editor universal, siga estos pasos:

1. Abra el proyecto en el editor universal y marque la extensión de icono **A/B**. Si el icono no está visible, confirme si ha habilitado la función en el administrador de extensiones. Si no está activada, actívela o solicite acceso.
1. Apunte la configuración de `fstab.yaml` a la configuración del proyecto y vincúlelo a la instancia de autor de AEM. Ver también [Conecte su código al contenido](https://www.aem.live/developer/ue-tutorial#connect-your-code-to-your-content)
1. Abra la instancia de AEM y, si tiene el proyecto listo, ábralo directamente en el editor universal.
1. Abra el proyecto y la página de índice donde desee ejecutar los experimentos y haga clic en **Editar** en la barra superior.
1. Haga clic en el icono A/B para abrir la extensión de experimentación.

>[!NOTE]
>Si tiene problemas para configurar la experimentación para su proyecto, póngase en contacto con `aem-contextual-experimentation@adobe.com`.

>[!NOTE]
>Para obtener más información sobre cómo configurar el motor de experimentación, consulte la sección de documentación del siguiente [repositorio](https://github.com/adobe/aem-experimentation/tree/v2-ui) .

## Variantes de experimento y flujo de trabajo general {#experiment-variants-workflow}

Antes de seguir el resto de la guía para configurar el primer experimento, hay algunos términos utilizados con frecuencia que debe estar familiarizado con:

* **Control**: la experiencia antes de ejecutar el experimento. Todos los experimentos intentan probar y demostrar una mejora sobre la experiencia de control.
* **Challenger**: una experiencia que es diferente de la experiencia de control y que se &quot;prueba&quot; junto a ella o frente a ella.
* **Variants**: el control y el aspirante son variantes de un experimento.
* **Relevancia estadística**: se evalúa si el aspirante es realmente mejor que el control. El cálculo de la relevancia estadística permite descartar la suerte y concentrarse en los resultados que tienen un efecto real.

En términos generales, al configurar un experimento se utiliza una página preexistente como página de control. Mediante el carril de experimentación, se crea una página de aspirante que es inicialmente una copia de la página de control. En la página del aspirante, puede probar diferentes elementos, como variantes de contenido, diseños de página diferentes, call-to-action (CTA), etc. También puede usar variantes generadas por IA usando la funcionalidad **Generar variación** en el carril de experimentación.

Para cada experimento, el tráfico se divide inicialmente al 50 % entre el control y el aspirante, pero se puede configurar cómo se divide el tráfico según sea necesario. Después de activar el experimento, recibirá datos a través del servicio de telemetría operativa.

El [servicio de telemetría operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) recopila datos, por ejemplo, el número de visitantes en la página de control en comparación con la página del aspirante. A continuación, utilice estos datos para elegir las mejoras necesarias para el sitio. Siempre y cuando se mantenga dentro del lenguaje de diseño establecido en el sitio web y utilice la funcionalidad existente, debe poder configurar una variante de experimento y enviarla a producción en cuestión de minutos.

>[!NOTE]
>Tenga en cuenta que el complemento no utiliza ni conserva datos del usuario final que puedan facilitar su identificación. No se requiere la inclusión del usuario final ni el consentimiento de cookies al usar la configuración predeterminada que usa el servicio de telemetría operativa [de AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

<!--
### Frequently used terms {#frequently-used-terms}

Before following the rest of the guide to set up your first experiment, there are a few frequently used terms that you should be familiar with:

* **Control**: the experience prior to running the experiment. All experiments try to test and demonstrate an improvement over the control experience.
* **Challenger**: an experience that is different from the control experience and is "tested" against it or alongside it.
* **Variants**: control and challenger are all variants of an experiment.
* **Statistical Significance**: Evaluating if your challenger is really better than the control. Calculating statistical significance allows you to rule out luck and concentrate on the results that have a real effect. 
-->

### Creación de experimentos en el editor universal

Para utilizar las funcionalidades de experimentación en el editor universal, primero debe configurar el carril de experimentación como se detalla en los capítulos presentados anteriormente y asegurarse de utilizar los sitios de AEM como fuente de contenido. Después de configurar todo, siga estos pasos.

### Empezar a editar el proyecto en el editor universal

Abra la instancia de AEM y, si tiene el proyecto listo, ábralo directamente en el editor universal. Si no tiene un proyecto listo y los sitios de AEM están configurados como origen de contenido, cree un nuevo proyecto de plantillas a partir de la plantilla proporcionada. Puede vincular su repositorio o nuestro repositorio de muestra para dirigirlo [https://github.com/sudo-buddy/ue-experimentation](https://github.com/sudo-buddy/ue-experimentation). Consulte también la página [Configurar AEM Sites as a Content Source](https://www.aem.live/developer/ue-tutorial). Una vez configurado el proyecto, ábralo junto con la página de índice donde quiera ejecutar los experimentos y haga clic en **Editar** en la barra superior.

### Inicio de la extensión A/B

Haga clic en el icono **A/B** para abrir la extensión de experimentación. La interfaz estará vacía la primera vez que la use. Haz clic en **Crear nuevo** para iniciar un nuevo experimento.

![a-b](/help/sites-cloud/administering/assets/a-b.png)

### Configuración de los detalles del experimento

Algunos de los valores del experimento están predefinidos de la siguiente manera:

**Tipo de experimento**: prueba A/B (solo se admite el tipo por ahora)
**Optimizando para**: conversión (solo se admite el tipo por ahora)

También puede cambiar el nombre del experimento por otro más descriptivo, por ejemplo, `homepage-head-experiment`.

![Detalles del experimento](/help/sites-cloud/administering/assets/exp-values.png)

### Agregar y editar variantes

Asegúrese de comprender los conceptos de aspirante y variante tal como se ha presentado anteriormente antes de continuar. Haga clic en **Agregar nuevo** para crear una variante de aspirante:

* Se le redirigirá a la página del aspirante en la misma ficha; inicialmente es sólo una copia del control.
* Edite la página directamente en contexto o haga clic en **Generar variación** para usar la asistencia de IA.
* Después de realizar cambios, vuelva a la extensión para continuar.

![Variante de control](/help/sites-cloud/administering/assets/control-variant.png)

### Definir otras propiedades y guardar como borrador

En el carril de experimentación puede establecer una fecha de inicio y de finalización (ambas opcionales). Si no se proporciona ninguna fecha de inicio, la prueba comienza una vez publicada. Si no se proporciona ninguna fecha de finalización, la prueba se ejecuta indefinidamente. También puede ajustar la división de tráfico, le recomendamos empezar con una división par 50/50.

Una vez que haya terminado, haga clic en **Guardar**; esto guardará el experimento como borrador. Tenga en cuenta que el experimento aún no está activo. Puede volver a la descripción general haciendo clic en **Volver al experimento** o puede permanecer en la interfaz de edición para activar el experimento.

![Borrador](/help/sites-cloud/administering/assets/draft-save.png)

### Activación del experimento

Cuando esté listo, haga clic en **Activar** para iniciar el experimento y publicar la página del experimento. La prueba comenzará a recopilar datos de telemetría operativa (RUM) (consulte más detalles en los capítulos siguientes).

![Activar](/help/sites-cloud/administering/assets/activate.png)

### Monitorización y promoción

Una vez que el experimento alcance la relevancia estadística, haga clic en **Promocionar** para convertir la variante deseada en el nuevo control. Tenga en cuenta que puede promocionar la variante del experimento en cualquier momento después de la activación, incluso si no alcanza la relevancia estadística.

### Uso de la experimentación con AEM Sidekick en Edge Delivery Services

Si tiene instalada la barra de tareas de AEM, puede utilizar el carril de experimentación directamente con el proyecto en el servicio de Edge Delivery sin utilizar el editor universal. La funcionalidad es esencialmente la misma que la prueba A/B descrita anteriormente; solo tenga en cuenta que necesita estar en modo **Vista previa** para editar y configurar la prueba. Una vez que termine de configurar la prueba, haga clic en **Activar** para activar el control y la variante del aspirante y comenzar a recopilar datos de telemetría.

<!--
### Experiment Identifier {#experiment-identifier}

Before you start, every experiment should have its own identifier for tracking and analytics purposes. A good starting point is to come up with a good, unique identifier for your experiment which will be the "Experiment ID". Experiments are often numbered linearly or correlated to their Issue ID in an issue tracker or management system. Experiment IDs often use a prefix for the project, for example: `OPT-0134`, `EXP0004` or `CCX0076`.

### Create your Challenger Page {#create-challenger-page}

By convention, it is recommended to create a folder with a lowercase experiment ID in your `/experiments/ folder` (for example /experiments/ccx0076/). All the pages for the challenger variants are located in this folder. You create this folder in your local repository, for example, Sharepoint or Goggle Drive.

Your experiments folder should look something like this:

![experiments-folder](/help/sites-cloud/administering/assets/experiments-folder.png)

Once the folder is created, put a copy of your control page into that folder, and apply the changes on the page that you would like to test as part of your experiment variant (see video above). As an example let's assume we have the following page on the website that we want to run an experiment on:

![control-page](/help/sites-cloud/administering/assets/control-page.png)

Your copy of the challenger placed in the experiments/experiment-id folder might look like this:

![challenger-page](/help/sites-cloud/administering/assets/challenger-page.png)

Preview and publish the challenger page using the sidekick and when you are done authoring the challenger page. The URL of the published challenger will be used in the next section - configuring the experiment.

### Configuring the experiment {#configure-experiment}

As soon as the challenger pages are ready to go, you need to go back to the control page and add metadata indicating that the page(s) are now part of the test.

There are two metadata rows that need to be added for an experiment variant.

* **Experiment**: containing your experiment ID.

* **Experiment Variants**: containing URLs for all the challengers of this page, separated by line breaks if you have more than one challenger.

See the example below:

![metadata-page](/help/sites-cloud/administering/assets/metadata-page.png)

For each experiment, the traffic is split between all the variants (control and challengers) and is automatically set to an even distribution. As such, if you have one challenger, there will automatically be an even 50/50 split between control and the challenger. If you have two challengers, you will automatically see a third of the traffic allocated to control and each challenger and so on.

You can override the traffic split by configuring the metadata. For more information on how you can customize the metadata used in your experiments, see the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

### Preview and Stage your Experiment Variants {#preview-stage-experiment}

As soon as you are ready to preview and stage your experiment, click Preview from the side-kick in the upper left side. Whenever you are previewing a page that has a running experiment, you will see the experimentation overlay in your `.aem.page` preview environment. The experimentation overlay lets you switch between the experiment variants and also provides traffic data.

![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.

The data collection to measure the effectiveness of each variant is based on the [Operational Telemetry service in AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Send your Experiment Variant to Production {#production-experiment}

Select the experiment pages and click Publish from the side-kick to push both the control and the challenger variant(s) live.

### Use Case Examples {#use-case-examples}

Presented below are several use case examples for experiment variants. Generally speaking, the basic worklflow will be similar to the one described above, with particular changes for each use case (like the number of challenger pages or metadata changes).

#### Full Page Experiment {#full-page}

You use a full page experiment to test between two variants of the same page. This is a full page variant of an a/b test where you have a control and a challenger page. You will replace the whole content of the "original" control page in the challenger variant with a different type of content. Keep in mind that by default the customer traffic is split evenly (50/50), but you can create custom splits if you like.

The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

* You will create multiple control pages each with one or more variants.
* The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let's say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now "grouped". We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

The metadata on the control page should look like this:

METADATA SETUP

#### Code-level experiments {#code-level}

Note that the examples above assume you have different content variants to serve, but if you want to run a pure code-based a/b test, this is achievable via:

Metadata

Experiment    Hero Test
Experiment Variants    2

This will create just two variants, without touching the content, and you'll be able to target those based on the `experiment-hero-test` and `variant-control/variant-challenger-1/variant-challenger-`2 CSS classes that will be set on the `<body>` element.

#### Browser based audience experiment {#browser-based}

You can create browser based experiments, where you deliver separate challenger pages depending on the browser used. You can, for example, serve a different challenger page to a Firefox user as opposed to a Chrome user. This is achieved by leveraging the audience parameter.

Once you configure the experiment, the target audience will be evaluated based on the context of the browser (client side) and limited to the browser APIs available. As such, you do not need to use server side third-party systems or customer profile data for your experiment.

Before you start authoring this experiment variant, the audience parameter needs to be defined in the project codebase. For more details, see ee the following [page](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring).

Once the audiences have been defined you are ready to author the experiment. As stated previously, let's say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like "page-for-firefox".
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let's say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.
-->

## Otras consideraciones {#other-considerations}

A continuación se presentan varios aspectos que debe tener en cuenta al utilizar la experimentación de contexto.

### Conversión {#conversion}

Los experimentos están configurados para abordar la conversión (rastrea los elementos en los que se puede hacer clic en la página). Actualmente, se admiten experimentos a nivel de página con un experimento por página.

<!--
### Make sure experiment Variants are not indexed {#experiment-not-indexed}

When running experiments, it is usually best practice to exclude the variants from the sitemap and ensure they are not indexed by search engines. This is because the variant page could be seen as duplicate content and negatively impact SEO.

You can do this by using either of the following two methods:

* If you centralize all experiments in a dedicated folder, like `/experiments`: make sure your bulk `metadata.xlsx` sheet contains a row with `/experiments/**` as path, and a robots column with the values `noindex`, `nofollow`.
* If you keep the experiment control and variants with the regular content: add a robots entry in the page metadata for each variant, with the value `noindex`, `nofollow`.
-->

## Desarrollador y recursos técnicos {#dev-resources}

Adobe Experience Manager utiliza la [telemetría operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) para recopilar los datos de operaciones que son estrictamente necesarios para detectar y corregir problemas funcionales y de rendimiento en sitios con tecnología de Adobe Experience Manager. Los datos de telemetría operativa se pueden utilizar para diagnosticar problemas de rendimiento. La telemetría operativa preserva la privacidad de los visitantes a través del muestreo (solo se monitorizará una pequeña porción de todas las vistas de página).

### Privacidad {#privacy-experimentation}

El servicio de telemetría operativa [de AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) está diseñado para preservar la privacidad de los visitantes y minimizar la recopilación de datos. Como visitante, esto significa que Adobe no intentará recopilar información personal sobre usted o información de la que se pueda realizar un seguimiento. Como operador de sitio, revise los elementos de datos recopilados a continuación para comprender si requieren consentimiento.

La telemetría operativa de AEM no utiliza ningún estado o ID del lado del cliente, como cookies o `localStorage`, `sessionStorage` o similar, para recopilar métricas de uso. Los datos se envían de forma transparente a través de una llamada de `Navigator.sendBeacon`, no a través de píxeles o técnicas similares. No hay ninguna &quot;huella digital&quot; de dispositivos o personas a través de su dirección IP, cadena del agente de usuario ni ningún otro dato con el fin de capturar datos de muestra.

No está permitido añadir datos personales a la recopilación de datos de Telemetría Operativa ni se pueden utilizar datos de Telemetría Operativa para casos de uso que vayan más allá de lo estrictamente necesario.
