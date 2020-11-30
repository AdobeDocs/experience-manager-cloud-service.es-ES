---
title: SPA Introducción y Tutorial
description: En este artículo se introducen los conceptos de SPA y se pasa por una aplicación básica de SPA para la creación, mostrando cómo se relaciona con el AEM SPA Editor subyacente.
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---


# SPA Introducción y Tutorial {#spa-introduction}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

El Editor SPA oferta una solución integral para admitir SPA dentro de AEM. En este artículo se explica el uso de una aplicación de SPA básica para la creación y se muestra cómo se relaciona con el editor de SPA de AEM subyacente.

## Introducción {#introduction}

### Objetivo del artículo {#article-objective}

Este artículo presenta los conceptos básicos de SPA antes de guiar al lector a través de un tutorial del editor de SPA mediante una aplicación SPA sencilla para mostrar la edición básica del contenido. A continuación, profundiza en la construcción de la página y en cómo se relaciona la aplicación SPA con el Editor de SPA de AEM y cómo interactúa con él.

El objetivo de esta introducción y tutorial es demostrar a un desarrollador AEM por qué SPA son relevantes, cómo funcionan en general, cómo gestiona un SPA el Editor AEM y cómo es diferente de una aplicación AEM estándar.

El tutorial se basa en la funcionalidad de AEM estándar y en la aplicación de proyecto WKND SPA de muestra. Para continuar, [descargue e instale la aplicación de muestra de WKND SPA Project desde GitHub aquí.](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>Este documento solo utiliza la aplicación [de proyecto](https://github.com/adobe/aem-guides-wknd-spa) WKND SPA para fines de demostración. No debe utilizarse para ningún trabajo de proyecto.

>[!TIP]
>
>Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)de proyecto, que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

### ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y se dirige principalmente a JavaScript, y depende de las llamadas de Ajax para cargar datos y actualizar la página de forma dinámica. La mayor parte o la totalidad del contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario según la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, permitiendo a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

### ¿Por qué un SPA? {#why-a-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no sólo para el visitante de la página web, sino también para los especialistas en mercadotecnia y desarrolladores debido a la naturaleza de SPA trabajo.

![SPA beneficios](assets/spa-benefits.png)

#### Visitantes {#visitors}

* Los visitantes desean experiencias nativas cuando interactúan con el contenido.
* Hay datos claros de que cuanto más rápida sea una página, más probabilidad habrá de producirse una conversión.

#### Especialistas en mercadotecnia {#marketers}

* Los especialistas en marketing desean oferta de experiencias ricas y nativas para atraer a visitantes a fin de que se comprometan plenamente con el contenido.
* La personalización puede hacer que estas experiencias sean aún más atractivas.

#### Desarrolladores {#developers}

* Los desarrolladores quieren una clara separación de las preocupaciones entre el contenido y la presentación.
* La separación limpia hace que el sistema sea más extensible y permite el desarrollo independiente del front-end.

### ¿Cómo funciona un SPA? {#how-does-a-spa-work}

La idea principal detrás de una SPA es que las llamadas a un servidor y la dependencia de un servidor se reducen para minimizar los retrasos causados por la latencia del servidor de modo que el SPA se aproxime a la capacidad de respuesta de una aplicación nativa.

En una página web secuencial tradicional, solo se cargan los datos necesarios para la página inmediata. Esto significa que cuando el visitante se mueve a otra página, se llama al servidor para obtener los recursos adicionales. Es posible que sean necesarias llamadas adicionales a medida que el visitante interactúa con los elementos de la página. Estas llamadas múltiples pueden dar una sensación de retraso o retraso, ya que la página tiene que responder a las solicitudes del visitante.

![Experiencias secuenciales frente a fluidas](assets/spa-sequential-vs-fluid.png)

Para una experiencia más fluida, que se aproxima a lo que espera un visitante de las aplicaciones móviles nativas, un SPA carga todos los datos necesarios para el visitante en la primera carga. Aunque esto puede tardar un poco más al principio, elimina la necesidad de realizar llamadas al servidor adicionales.

Al realizar el procesamiento en el lado del cliente, los elementos de la página reaccionan más rápidamente y las interacciones con la página por parte del visitante son inmediatas. Cualquier dato adicional que se necesite se llama de forma asíncrona para maximizar la velocidad de la página.

>[!TIP]
>
>Para obtener detalles técnicos sobre cómo SPA trabajar en AEM, consulte los artículos:
>* [Introducción a SPA en AEM con React](getting-started-react.md)
>* [Introducción a SPA en AEM con Angular](getting-started-angular.md)

>
>
Para ver más de cerca el diseño, la arquitectura y el flujo de trabajo técnico del Editor de SPA, consulte el artículo:
>* [Información general](editor-overview.md)del Editor de SPA.


## Experiencia de edición de contenido con SPA {#content-editing-experience-with-spa}

Cuando se crea un SPA para aprovechar el Editor de SPA de AEM, el autor del contenido no observa ninguna diferencia al editar y crear contenido. La funcionalidad de AEM común está disponible y no se requieren cambios en el flujo de trabajo del autor.

1. Edite la aplicación WKND SPA Project en AEM.

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Inicio del proyecto WKND SPA](assets/wknd-home.png)

1. Seleccione un componente de texto y observe que aparece una barra de herramientas como cualquier otro componente. Seleccione **Editar**.

   ![Seleccionar componente de texto](assets/wknd-text.png)

1. Edite el contenido como si fuera normal dentro de AEM y tenga en cuenta que los cambios se mantienen.

   ![Editar texto](assets/wknd-edit-text.png)

1. Utilice el navegador de recursos para arrastrar y soltar una imagen nueva en un componente de imagen.

   ![Colocación de un recurso de imagen](assets/wkdn-drop-image.png)

1. El cambio se mantiene.

   ![Imagen persistente](assets/wknd-change-persisted.png)

Se admiten herramientas de creación adicionales como arrastrar y soltar componentes adicionales en la página, reorganizar componentes y modificar el diseño, como en cualquier aplicación AEM que no sea SPA.

>[!NOTE]
>
>El Editor de SPA no modifica el DOM de la aplicación. El propio SPA es responsable del DOM.
>
>Para ver cómo funciona, continúe con la siguiente sección de este artículo [SPA Aplicaciones y el AEM SPA Editor](#spa-apps-and-the-aem-spa-editor).

## Aplicaciones SPA y el AEM Editor SPA {#spa-apps-and-the-aem-spa-editor}

La experiencia de cómo se comporta un SPA para el usuario final y, a continuación, la inspección de la página de SPA ayuda a comprender mejor cómo funciona una aplicación SAP con el Editor de SPA en AEM.

### Uso de una aplicación SPA {#using-an-spa-application}

1. Cargue la aplicación WKND SPA Project en el servidor de publicación o mediante la **Vista de opciones tal como se ha publicado** desde el menú Información **de** página del editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Previsualización del hogar del proyecto WKND SPA](assets/wknd-preview.png)

   Tenga en cuenta la estructura de las páginas, incluida la navegación a páginas secundarias, menús y tarjetas de artículos.

1. Navegue a una página secundaria mediante el menú y observe que la página se carga inmediatamente sin necesidad de actualizar.

   ![Página 1 del proyecto de WKND SPA](assets/wknd-page1.png)

1. Abra las herramientas de desarrollador integradas de su navegador y supervise la actividad de red a medida que navega por las páginas secundarias.

   ![Actividad de red](assets/wknd-network-activity.png)

   Hay muy poco tráfico a medida que se mueve de una página a otra en la aplicación. La página no se vuelve a cargar y solo se solicitan las imágenes nuevas.

   El SPA administra el contenido y el enrutamiento por completo en el lado del cliente.

Por lo tanto, si la página no se recarga al navegar por las páginas secundarias, ¿cómo se carga?

La siguiente sección, [Carga de una aplicación](#loading-a-spa-application)SPA, profundiza en la mecánica de carga del SPA y en cómo se puede cargar el contenido sincrónica y asincrónicamente.

### Carga de una aplicación SPA {#loading-a-spa-application}

1. Si aún no se ha cargado, cargue la aplicación de Historial We.Retail en el servidor de publicación o mediante la **Vista de opciones tal como se ha publicado** desde el menú Información **de** página del editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![WKND SPA previsualización del proyecto](assets/wknd-preview.png)

1. Utilice la herramienta integrada de su navegador para vista del origen de la página.
1. Tenga en cuenta que el contenido de la fuente es limitado.

   ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>WKND SPA React Home Page</title>
   
        <meta name="template" content="spa-page-template"/>
        <meta name="viewport" content="width=device-width, initial-scale=1"/>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.css" type="text/css">
   
    <meta name="theme-color" content="#000000"/>
    <link rel="icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/favicon.ico"/>
    <link rel="apple-touch-icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/logo192.png"/>
    <link rel="manifest" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/manifest.json"/>
   
    <!-- AEM page model -->
    <meta property="cq:pagemodel_root_url" content="/content/wknd-spa-react/us/en.model.json"/>
    <link href="//fonts.googleapis.com/css?family=Source+Sans+Pro:400,600|Asar&display=swap" rel="stylesheet"/>
    <meta property="cq:datatype" content="JSON"/>
    <meta property="cq:wcmmode" content="edit"/>
   
    <link rel="stylesheet" href="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.css" type="text/css">
    <link rel="stylesheet" href="/etc.clientlibs/wcm/foundation/clientlibs/main.min.css" type="text/css">
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/messaging.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/utils.min.js"></script>
    <script type="text/javascript" src="/libs/granite/author/deviceemulator/clientlibs.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wcm/foundation/clientlibs/main.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/utils.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery/granite.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/shared.min.js"></script>
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/header","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/header/header.html","totalTime":2,"selfTime":2}-->
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.css" type="text/css">
   
    </head>
   
    <body class="page basicpage">
        <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="spa-root"></div>
   
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.js"></script>
   
    <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.js"></script>
   
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/pagemodel/messaging.min.js"></script>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-author.min.css" type="text/css">
   
    <!--cq{"decorated":true,"type":"cq/cloudserviceconfigs/components/servicecomponents","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudservices","selectors":null,"servlet":"Script /libs/cq/cloudserviceconfigs/components/servicecomponents/servicecomponents.jsp","totalTime":2,"selfTime":2}-->
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/footer","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/footer/footer.html","totalTime":2,"selfTime":2}-->
   
    </body>
    </html>
    <!--cq{"decorated":false,"type":"wknd-spa-react/components/page","path":"/content/wknd-spa-react/us/en/home/jcr:content","selectors":null,"servlet":"Script /apps/spa-project-core/components/page/page.html","totalTime":39,"selfTime":33}-->
   ```

   La página no tiene contenido dentro de su cuerpo. Se compone principalmente de hojas de estilo y una llamada a varios scripts como `clientlib-react.min.js`.

   Estos scripts son los principales controladores de esta aplicación y son responsables de procesar todo el contenido.

1. Utilice las herramientas integradas del explorador para inspeccionar la página. Consulte el contenido del DOM completamente cargado.

   ![DOM del proyecto WKND SPA](assets/wknd-dom.png)

1. Cambie a la ficha Red del Inspector y vuelva a cargar la página.

   Al omitir las solicitudes de imagen, tenga en cuenta que los recursos principales cargados para la página son la propia página, CSS, React Javascript, sus dependencias y los datos JSON de la página.

   ![WKND SPA actividad de red del proyecto](assets/wknd-network.png)

1. Cargue el `home.model.json` en una nueva ficha.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON de la página de inicio del proyecto WKND SPA](assets/wknd-json.png)

   El Editor de SPA de AEM aprovecha [AEM Content Services](/help/assets/content-fragments/content-fragments.md) para entregar todo el contenido de la página como un modelo JSON.

   Al implementar interfaces específicas, los modelos Sling proporcionan la información necesaria para el SPA. El envío de los datos de JSON se delega hacia abajo en cada componente (de página, párrafo, componente, etc.).

   Cada componente elige lo que expone y cómo se procesa (lado del servidor con HTL o lado del cliente con React o Angular). Este artículo se centra en la representación del lado del cliente con React.

1. El modelo también puede agrupar las páginas para que se carguen sincrónicamente, reduciendo el número de recargas de página necesarias.

   En el ejemplo de Historial We.Retail, las páginas `home`, `page-1`, `page-2`y `page-3` se cargan sincrónicamente, ya que los visitantes suelen visitar todas esas páginas.

   Este comportamiento no es obligatorio y es totalmente definible.

   ![WKND SPA Agrupación de elementos del proyecto](assets/wknd-pages.png)

1. Para vista de esta diferencia de comportamiento, vuelva a cargar la `home` página y borre la actividad de red del inspector. Vaya a `page-1` en el menú de la página y vea que la única actividad de red es una solicitud de imagen de `page-1`. `page-1` no necesita cargarse.

   ![WKND SPA Project page-1 actividad de red](assets/wknd-page1-network.png)

### Interacción con el Editor de SPA {#interaction-with-the-spa-editor}

Con la aplicación de ejemplo WKND SPA Project, queda claro cómo se comporta y se carga la aplicación cuando se publica, aprovechando los servicios de contenido para el envío de contenido JSON así como la carga asincrónica de recursos.

Además, para el autor del contenido, la creación de contenido mediante un editor de SPA es perfecta dentro de AEM.

En la siguiente sección analizaremos el contrato que permite al Editor de SPA relacionar componentes dentro del SPA con AEM componentes y lograr esta experiencia de edición sin problemas.

1. Cargue la aplicación WKND SPA Project en el editor y cambie al modo de **Previsualización** .

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Con las herramientas de desarrollador integradas del explorador, inspeccione el contenido de la página. Con la herramienta de selección, seleccione un componente editable en la página y vista los detalles del elemento.

   Tenga en cuenta que el componente tiene un nuevo atributo de datos `data-cq-data-path`.

   ![Inspección de elementos del proyecto WKND SPA](assets/wknd-inspector.png)

   Por ejemplo

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Esta ruta permite recuperar y asociar el objeto de configuración de contexto de edición de cada componente.

   Este es el único atributo de marcado necesario para que el editor reconozca este componente como un componente editable dentro del SPA. Según este atributo, el Editor de SPA determinará qué configuración editable está asociada al componente, de modo que el marco, la barra de herramientas, etc. correctos. está cargado.

   Algunos nombres de clase específicos también se agregan para marcar marcadores de posición y para la funcionalidad de arrastrar y soltar recursos.

   >[!NOTE]
   >
   >Este comportamiento difiere de las páginas procesadas del lado del servidor en AEM, donde hay un `cq` elemento insertado para cada componente editable.
   >
   >Este método en el Editor de SPA elimina la necesidad de insertar elementos personalizados, confiando únicamente en un atributo de datos adicional, lo que simplifica el marcado para el desarrollador de front-end.

## Próximos pasos {#next-steps}

Ahora que comprende la experiencia de edición SPA en AEM y cómo se relaciona un SPA con el Editor de SPA, indíquese más profundamente en la comprensión de cómo se crea un SPA.

* [Introducción a SPA en AEM con React](getting-started-react.md) muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con React
* [Introducción a SPA en AEM con Angular](getting-started-angular.md) muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con Angular
* [SPA información general](editor-overview.md) del Editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [Desarrollar SPA para AEM](developing.md) describe cómo involucrar a los desarrolladores front-end para desarrollar un SPA para AEM así como también cómo SPA interactuar con la arquitectura AEM.
