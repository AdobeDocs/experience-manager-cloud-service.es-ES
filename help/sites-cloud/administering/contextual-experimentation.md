---
title: Experimentación contextual en AEM as a Cloud Service
description: Aprenda a utilizar el complemento de experimentación para agregar capacidades de experimentación a sus sitios.
feature: Administering
role: Admin
source-git-commit: 1bb86516328d1405c1761f3c8b0494cc9cb64553
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 0%

---


# Información general {#overview}

>[!NOTE]
>Actualmente, la función de experimentación contextual solo está disponible a través del programa beta. Póngase en contacto con el servicio de asistencia de Adobe o con su administrador de cuentas para acceder al programa beta.

La experimentación es la práctica de probar el diseño, la funcionalidad y el código de su sitio para mejorar el rendimiento y hacer que el sitio sea más eficaz y optimizado. Esto se logra cambiando el contenido o la funcionalidad, comparando los resultados con una versión anterior y seleccionando las mejoras que tienen efectos mensurables.

Cuando se hace correctamente, es un patrón potente para mejorar las conversiones, la participación y la experiencia del visitante. En general, hay un par de problemas que se deben evitar al intentar adoptar la práctica:

* **Demasiado poco**: la mayoría de las empresas no están experimentando lo suficiente y, cuando lo hacen, experimentan con muy poco tráfico para obtener resultados significativos.
* **Demasiado lento**: muchos marcos de experimentación ralentizan tanto el sitio que las posibles nuevas conversiones no pueden compensar el tráfico perdido y las devoluciones debido a la lentitud del procesamiento.
* **Demasiado complejo**: si se tarda demasiado en configurar un experimento nuevo, se ejecutarán menos experimentos.

Para los sitios que se ejecutan en Adobe Experience Manager, existe el **complemento de experimentación** &quot;predeterminado&quot; que permite a los desarrolladores agregar una capacidad de experimentación a sus sitios. Tres cosas hacen que este enfoque sea diferente de otros marcos de experimentación:

* Es fácil configurar pruebas con las herramientas con las que los autores ya están familiarizados y no se necesita un inicio de sesión independiente.
* Está profundamente integrado en el sistema de entrega de AEM, no ralentiza el sitio y es resistente a los cambios en el código y el contenido.
* Permite probar cambios de contenido sencillos, así como experimentos que abarcan diseño, funcionalidad y código.

## Antes de comenzar {#before-start}

El complemento de experimentación se usa en el contexto de [Edge Delivery Services](/help/edge/overview.md), por lo que necesitarás una cuenta de Github, un repositorio de contenido como SharePoint o Google Drive, y también necesitarás [AEM Sidekick](https://www.aem.live/docs/sidekick). Consulte también la [Página de introducción - Tutorial para desarrolladores de Universal Editor](https://www.aem.live/developer/tutorial) y [Introducción - Tutorial para desarrolladores](https://www.aem.live/developer/tutorial).

Después de configurar todo, **vea este vídeo** titulado [Experimentación instantánea](https://business.adobe.com/products/experience-manager/sites/testing-optimization.html) para ver una breve demostración del funcionamiento del complemento de experimentación.

## Términos más utilizados {#frequently-used-terms}

Antes de seguir el resto de la guía para configurar el primer experimento, hay algunos términos utilizados con frecuencia que debe conocer:

* **Control**: la experiencia antes de ejecutar el experimento. Todos los experimentos intentan probar y demostrar una mejora sobre la experiencia de control.
* **Challenger**: una experiencia que es diferente de la experiencia de control y que se &quot;prueba&quot; junto a ella o con ella.
* **Variants**: el control y el aspirante son variantes de un experimento.
* **Relevancia estadística**: Evaluando si el aspirante es realmente mejor que el control. El cálculo de la relevancia estadística permite descartar la suerte y concentrarse en los resultados que tienen un efecto real.

## Variantes de experimento y flujo de trabajo general {#experiment-variants-workflow}

En términos generales, al configurar un experimento se utiliza una página preexistente como página de control. A continuación, creará una página de aspirante que reemplazará la página de control de algunos de los visitantes. En la página del aspirante, puede probar diferentes elementos, como variantes de contenido, diseños de página diferentes, call-to-action (CTA), etc. Puede configurar estas variantes de experimento añadiendo parámetros de metadatos en la página de control (a continuación).

A continuación, el [servicio de telemetría operativa](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) recopila datos, por ejemplo, el número de visitantes en la página de control en comparación con la página del aspirante. A continuación, utilice estos datos para elegir las mejoras necesarias para el sitio. Siempre y cuando se mantenga dentro del lenguaje de diseño establecido en el sitio web y utilice la funcionalidad de bloque existente, debe poder configurar una variante de experimento y enviarla a producción en cuestión de minutos.

>[!NOTE]
>Tenga en cuenta que el complemento no utiliza ni conserva datos del usuario final que puedan facilitar su identificación. No se requiere la inclusión del usuario final ni el consentimiento de cookies al utilizar la configuración predeterminada que utiliza el servicio de telemetría operativa [en AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md)

### Identificador de experimento {#experiment-identifier}

Antes de comenzar, cada experimento debe tener su propio identificador para fines de seguimiento y análisis. Un buen punto de partida es crear un buen identificador único para el experimento, que será el &quot;ID del experimento&quot;. Los experimentos suelen numerarse linealmente o correlacionarse con su ID de problema en un rastreador de problemas o un sistema de administración. Los ID de experimento suelen utilizar un prefijo para el proyecto, por ejemplo: OPT-0134, EXP0004 o CCX0076.

### Crear su página de Challenger {#create-challenger-page}

Por convención, se recomienda crear una carpeta con un ID de experimento en minúsculas en su `/experiments/ folder` (por ejemplo /experiments/ccx0076/). Todas las páginas de las variantes del aspirante se encuentran en esta carpeta. Puede crear esta carpeta en el repositorio local, por ejemplo, Sharepoint o Goggle Drive.

La carpeta de experimentos debería tener un aspecto similar al siguiente:

![carpeta de experimentos](/help/sites-cloud/administering/assets/experiments-folder.png)

Una vez creada la carpeta, coloque una copia de la página de control en esa carpeta y aplique los cambios en la página que desee probar como parte de la variante del experimento (consulte el vídeo anterior). Por ejemplo, supongamos que tenemos la siguiente página en el sitio web en la que queremos ejecutar un experimento:

![página de control](/help/sites-cloud/administering/assets/control-page.png)

Su copia del aspirante colocada en la carpeta `experiments/<experiment-id>` puede tener este aspecto:

![página-aspirante](/help/sites-cloud/administering/assets/challenger-page.png)

Obtenga una vista previa de la página del aspirante y publíquela con la barra de tareas y cuando haya terminado de crear la página del aspirante. La URL del aspirante publicado se utilizará en la siguiente sección: Configuración del experimento.

### Configuración del experimento {#configure-experiment}

Tan pronto como las páginas del aspirante estén listas, deberá volver a la página de control y agregar metadatos para indicar que las páginas forman parte de la prueba.

Hay dos filas de metadatos que deben agregarse para una variante de experimento.

* **Experimento**: contiene su ID de experimento.

* **Variantes de experimento**: contiene direcciones URL de todos los aspirantes de esta página, separadas por saltos de línea si tiene más de un aspirante.

Consulte el ejemplo siguiente:

![página-metadatos](/help/sites-cloud/administering/assets/metadata-page.png)

Para cada experimento, el tráfico se divide entre todas las variantes (control y aspirantes) y se establece automáticamente en una distribución par. Como tal, si tiene un aspirante, automáticamente habrá una división par 50/50 entre el control y el aspirante. Si tiene dos aspirantes, verá automáticamente un tercio del tráfico asignado al control y a cada aspirante, entre otros.

Puede anular la división de tráfico configurando los metadatos. Para obtener más información sobre cómo personalizar los metadatos utilizados en los experimentos, consulte la siguiente [página](https://github.com/adobe/aem-experience-decisioning/wiki/Experiments#authoring)

### Previsualización y ensayo de las variantes del experimento {#preview-stage-experiment}

Tan pronto como esté listo para previsualizar y montar el experimento, haga clic en Vista previa en la barra lateral izquierda. Siempre que esté previsualizando una página que tiene un experimento en ejecución, verá la superposición de experimentación en el entorno de vista previa `.aem.page`. La superposición de experimentación permite cambiar entre las variantes del experimento y también proporciona datos de tráfico.

<!--- ![experimentation-overlay](/help/sites-cloud/administering/assets/experimentation-overlay.png)

By using the experimentation overlay, authors can get quick insights on the performance of experiments being run on the production site. These insights are helpful in making a decision about the duration of the experiment, but also about which variant is best suited for production.-->

La recopilación de datos para medir la efectividad de cada variante se basa en el [servicio de telemetría operacional en AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md).

### Envíe la variante de experimento a producción {#production-experiment}

Seleccione las páginas del experimento y haga clic en Publicar en la barra de tareas para activar tanto la variante o variantes del control como las del aspirante.

### Ejemplos de casos de uso {#use-case-examples}

A continuación se presentan varios ejemplos de casos de uso de variantes de experimento. En términos generales, el flujo de trabajo básico es similar al descrito anteriormente, con cambios específicos para cada caso de uso (como el número de páginas del aspirante o cambios en los metadatos).

#### Experimento de página completa {#full-page}

Se utiliza un experimento de página completa para probar entre dos variantes de la misma página. Es una variante de página completa de una prueba A/B en la que tiene un control y una página de aspirante. Sustituirá todo el contenido de la página de control &quot;original&quot; en la variante del aspirante por un tipo de contenido diferente. Tenga en cuenta que, de forma predeterminada, el tráfico del cliente se divide uniformemente (50/50), pero puede crear divisiones personalizadas si lo desea.

<!--The metadata on the control page should look like this:

METADATA SETUP

#### Sections of the page Experiment {#sections-of-the-page}

This is experiment is similar to the full page one presented above but now the a/b test will contain changes to a section of the page instead of the whole content. For example, you can modify and test a carousel element, the call to action element and so on. As such, you will have a control and a challenger page, with the challenger page containing the modified elements. The metadata on the control page should look like this:

METADATA SETUP

#### Multi-path Experiment {#multi-path}

By leveraging the experimentation plug-in, you can set up a/b tests on several pages of your website at once. For example, on all product pages, photo galleries, all blog posts and so on.

The configuration logic is the same as above - you will create a control page and one or more challenger variants of that page. What changes in the multi-page use-case, is the following:

• You will create multiple control pages each with one or more variants.
• The control pages must have the same experiment ID in metadata field.

For example: We have 5 different production pages for which we need to set up an a/b test. We create 5 control pages (as detailed in the chapters above) and 5 (or more) challenger variants.

We then create an experiment ID, let’s say `prod-exp` and add this ID in the experiment metadata field for each control page. This basically means that all pages with the same ID are now “grouped”. We then assign the challenger variants for each control page, taking care to sequence them properly in case we have more than one variant for each control.

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

Once the audiences have been defined you are ready to author the experiment. As stated previously, let’s say you want to create a Firefox versus Chrome experiment where you will serve different pages depending on the browser.

You need two different challenger pages, so set up the experiment as follows:

1.Duplicate the Control page by right-clicking and copying it to the experiment folder. You need to copies, one for Firefox and one for Chrome.
2.Rename the copies. Give them specific names like “page-for-firefox”.
3.Change the content of the pages depending on what you need to serve on Firefox versus Chrome.
4.Change the metadata as explained in the section below.
5.Click Preview from the side-kick in the upper left side, to preview the changes.

The most important part when authoring this experiment is to change the metadata in the control page. Let’s say you defined the browser audiences in the codebase as: Audience: Firefox and Audience: Chrome. You need to edit the control page and add these audiences and point to the appropriate challenge page you set up previously. It should look similar to this:

Metadata
Title Control Page
Description This is the control page.
Experiment ExpBrowser
Experiment Variants `https://{ref}--{repo}--{org}.hlx.page/my-page-for-firefox https://{ref}--{repo}--{org}.hlx.page/my-page-for-chrome`
Audience: Firefox `https://{ref}--{repo}--{org}.hlx.page/page-for-firefox`
Audience: Chrome `https://{ref}--{repo}--{org}.hlx.page/page-for-chrome`

After this configuration, the users will be triaged based on the browser they connect with and the appropriate challenger page will be served.

Please keep in mind that the names above are only for illustration purposes. You can define the Audiences parameter and the challenger pages according to your needs, for example: Audience (Firefox) or Audience Firefox.-->

## Otras consideraciones {#other-considerations}

A continuación se presentan otros aspectos que debe tener en cuenta al utilizar la experimentación de contexto.

### Conversión {#conversion}

Los experimentos están configurados para abordar la conversión (rastrea los elementos en los que se puede hacer clic en la página). Todos los experimentos deben definirse para lo siguiente:

* Tipo de experimento
* A qué bloque de experiencia se aplicará el experimento
* Cuántas variantes contendrá el experimento
* ¿Cuál es la composición de cada variante

### Asegúrese de que las variantes del experimento no estén indexadas {#experiment-not-indexed}

Al ejecutar experimentos, normalmente se recomienda excluir las variantes del mapa del sitio y asegurarse de que los motores de búsqueda no las indexen. Esto se debe a que la página de variante podría verse como contenido duplicado y afectar negativamente al SEO.

Para ello, utilice uno de los dos métodos siguientes:

* Si centraliza todos los experimentos en una carpeta dedicada, como `/experiments`: asegúrese de que la hoja `metadata.xlsx` masiva contenga una fila con `/experiments/**` como ruta de acceso y una columna de robots con los valores `noindex`, `nofollow`.
* Si mantiene el control del experimento y las variantes con el contenido normal: agregue una entrada de robots en los metadatos de página para cada variante, con el valor `noindex`, `nofollow`.

## Desarrollador y recursos técnicos {#dev-resources}

Adobe Experience Manager usa [telemetría operativa]&#x200B;(/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md

) para recopilar los datos de operaciones estrictamente necesarios para detectar y corregir problemas funcionales y de rendimiento en sitios con tecnología de Adobe Experience Manager. Los datos de telemetría operativa se pueden utilizar para diagnosticar problemas de rendimiento. La telemetría operativa preserva la privacidad de los visitantes a través del muestreo (solo se monitorizará una pequeña porción de todas las vistas de página).

### Privacidad {#privacy-experimentation}

El servicio de telemetría operativa [de AEM as a Cloud Service](/help/sites-cloud/administering/operational-telemetry-for-aem-as-a-cloud-service.md) está diseñado para preservar la privacidad de los visitantes y minimizar la recopilación de datos. Como visitante, esto significa que Adobe no intentará recopilar información personal sobre usted o información de la que se pueda realizar un seguimiento. Como operador de sitio, revise los elementos de datos recopilados a continuación para comprender si requieren consentimiento.
La telemetría operativa de AEM no utiliza ningún estado o ID del lado del cliente, como cookies o `localStorage`, `sessionStorage` o similar, para recopilar métricas de uso. Los datos se envían de forma transparente a través de una llamada de `Navigator.sendBeacon`, no a través de píxeles o técnicas similares. No hay ninguna &quot;huella digital&quot; de dispositivos o personas a través de su dirección IP, cadena del agente de usuario ni ningún otro dato con el fin de capturar datos de muestra.

No está permitido añadir datos personales a la recopilación de datos de Telemetría Operativa ni se pueden utilizar datos de Telemetría Operativa para casos de uso que vayan más allá de lo estrictamente necesario.

### Preguntas frecuentes {#faq}

A continuación se presenta una lista de las preguntas más frecuentes:

P: ¿Puedo ajustar la proporción de división entre las variantes de mi experimento, por ejemplo, un 10 % en el control y un 90 % en el aspirante?

Sí, la proporción de división se puede configurar mediante [metadatos](#configure-experiment).

P: ¿Puedo experimentar tanto con texto como con imágenes?

Sí, la variante puede ser una página completamente diferente, por lo que puede incluso probar los cambios de diseño.
