---
title: Diseño de los componentes principales del CIF de AEM
description: Aprenda a aplicar estilo a AEM componentes principales del CIF. El tutorial explica cómo se utilizan las bibliotecas del lado del cliente o clientlibs para implementar y administrar CSS y Javascript para una implementación de Adobe Experience Manager (AEM) Commerce. Este tutorial también tratará cómo el módulo ui.frontend y un proyecto de webpack están integrados en el proceso de compilación de extremo a extremo.
sub-product: Commerce
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 521c1bb8-7326-4ee8-aba3-f386727e2b34,75df606f-b22f-4f7e-bd8a-576d215f72bc
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 29%

---

# Diseño de los componentes principales del CIF de AEM {#style-aem-cif-core-components}

La variable [Proyecto de CIF Venia](https://github.com/adobe/aem-cif-guides-venia) es una base de código de referencia para usar [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components). En este tutorial, inspeccionará el proyecto de referencia de Venia y comprenderá cómo se organizan los componentes principales de AEM CIF y CSS y JavaScript. También creará un nuevo estilo con CSS para actualizar el estilo predeterminado del **Teaser de productos** componente.

>[!TIP]
>
> Utilice la variable [AEM tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) al iniciar su propia implementación de comercio.

## Qué va a generar

En este tutorial, se implementará un nuevo estilo para el componente teaser de productos que se asemeje a una tarjeta. Las lecciones aprendidas en el tutorial se pueden aplicar a otros componentes principales del CIF.

![Qué va a generar](../assets/style-cif-component/what-you-will-build.png)

## Requisitos previos {#prerequisites}

Se requiere un entorno de desarrollo local para completar este tutorial. Esto incluye una instancia de AEM en ejecución configurada y conectada a una instancia de Adobe Commerce. Consulte los requisitos y pasos para [configuración de un desarrollo local con AEM SDK as a Cloud Service](../develop.md).

## Clonar el proyecto de Venia {#clone-venia-project}

Clonaremos el [Proyecto Venia](https://github.com/adobe/aem-cif-guides-venia) y, a continuación, anule los estilos predeterminados.

>[!NOTE]
>
> **Siéntase libre de usar un proyecto existente** (basado en el tipo de archivo del proyecto AEM con CIF incluido) y omita esta sección.

1. Ejecute el siguiente comando git para clonar el proyecto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Agregue las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Adobe Commerce o agregue las configuraciones al proyecto recién creado.

1. En este punto debe tener una versión de trabajo de una tienda conectada a una instancia de Adobe Commerce. Vaya a la `US` > `Home` en: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, debería ver varias categorías que indican que la conexión a Adobe Commerce está funcionando.

   ![Tienda configurada con tema de Venia](../assets/style-cif-component/venia-store-configured.png)

## Bibliotecas de cliente y módulo ui.frontend {#introduction-to-client-libraries}

CSS y JavaScript responsables de procesar el tema o los estilos de la tienda se gestionan en AEM en una [biblioteca de cliente](/help/implementing/developing/introduction/clientlibs.md) o clientlibs para abreviar. Las bibliotecas de cliente proporcionan un mecanismo para organizar CSS y Javascript en el código de un proyecto y luego distribuirlas en la página.

Los estilos específicos de marca se pueden aplicar a AEM componentes principales del CIF añadiendo y anulando el CSS administrado por estas bibliotecas de cliente. Es fundamental comprender cómo se estructuran e incluyen las bibliotecas de cliente en la página.

La variable [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) es un [webpack](https://webpack.js.org/) para administrar todos los recursos front-end de un proyecto. Esto permite a los desarrolladores de front-end utilizar cualquier cantidad de idiomas y tecnologías como [TypeScript](https://www.typescriptlang.org/), [Sass](https://sass-lang.com/) y mucho más.

La variable `ui.frontend` es también un módulo Maven e integrado con el proyecto más grande mediante el uso de un módulo NPM en [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). Durante una compilación, la variable `aem-clientlib-generator` copia los archivos CSS y JavaScript compilados en una biblioteca de cliente de la `ui.apps` módulo.

![ui.frontend para la arquitectura ui.apps](../assets/style-cif-component/ui-frontend-architecture.png)

*Los archivos CSS y Javascript compilados se copian desde el `ui.frontend` en el `ui.apps` módulo como biblioteca de cliente durante una compilación de Maven*

## Actualizar el estilo del teaser {#ui-frontend-module}

A continuación, realice un pequeño cambio en el estilo del teaser para ver cómo se llama a la función `ui.frontend` las bibliotecas de módulos y clientes funcionan. Uso [el IDE que elija](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar el proyecto Venia. Las capturas de pantalla utilizadas son de la [Código IDE de Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. Navegue y amplíe el **ui.frontend** y expanda la jerarquía de carpetas a: `ui.frontend/src/main/styles/commerce`:

   ![carpeta de comercio ui.frontend](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   Tenga en cuenta que hay varios Sass (`.scss`) debajo de la carpeta . Son los estilos específicos de comercio para cada uno de los componentes de comercio.

1. Abra el archivo `_productteaser.scss`.

1. Actualice el `.item__image` y modificar la regla de borde:

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
   }
   ```

   La regla anterior debe añadir un borde rosa muy negrita al componente teaser de productos.

1. Abra una nueva ventana de terminal y vaya a la `ui.frontend` carpeta:

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. Ejecute el siguiente comando Maven:

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect la salida de terminal. Verá que el comando Maven ejecutó varias secuencias de comandos NPM, incluidas `npm run build`. La variable `npm run build` se define en la variable `package.json` y tiene el efecto de compilar el proyecto webpack y activar la generación de la biblioteca cliente.

1. Inspect el archivo `ui.frontend/dist/clientlib-site/site.css`:

   ![CSS del sitio compilado](../assets/style-cif-component/comiled-site-css.png)

   El archivo es la versión compilada y minificada de todos los archivos Sass del proyecto.

   >[!NOTE]
   >
   > Los archivos como este se omiten del control de código fuente, ya que deben generarse durante el tiempo de compilación.

1. Inspect el archivo `ui.frontend/clientlib.config.js`.

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   Este es el archivo de configuración para [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) y determina dónde y cómo se transformarán la CSS y JavaScript compiladas en una biblioteca de cliente AEM.

1. En el `ui.apps` inspeccione el archivo: `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![CSS del sitio compilado en ui.apps](../assets/style-cif-component/comiled-css-ui-apps.png)

   Esta es la copia `site.css` en el `ui.apps` proyecto. Ahora forma parte de una clientlibrary denominada `clientlib-site` con una categoría de `venia.site`. Una vez que el archivo forma parte de la variable `ui.apps` se puede implementar en AEM.

   >[!NOTE]
   >
   > Los archivos como este también se omiten del control de código fuente, ya que deben generarse durante la hora de compilación.

1. A continuación, revise las otras bibliotecas de cliente generadas por el proyecto:

   ![Otras bibliotecas de cliente](../assets/style-cif-component/other-clientlibs.png)

   Estas bibliotecas de cliente no están administradas por el `ui.frontend` módulo. En su lugar, estas bibliotecas de cliente incluyen dependencias CSS y JavaScript proporcionadas por Adobe. La definición de estas bibliotecas de cliente se encuentra en la variable `.content.xml` debajo de cada carpeta.

   **clientlib-base**: es una biblioteca de cliente vacía que simplemente incrusta las dependencias necesarias de los [componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es). La categoría es `venia.base`.

   **clientlib-cif** : también es una biblioteca de cliente vacía que simplemente incrusta las dependencias necesarias de [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components). La categoría es `venia.cif`.

   **clientlib-grid** - Esto incluye el CSS necesario para habilitar AEM función de cuadrícula interactiva. El uso de la cuadrícula AEM habilita [Modo de diseño](/help/sites-cloud/authoring/features/responsive-layout.md) en el editor de AEM y permite a los autores de contenido cambiar el tamaño de los componentes. La categoría es `venia.grid` y está incrustado en la variable `venia.base` biblioteca.

1. Inspect los archivos `customheaderlibs.html` y `customfooterlibs.html` below `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![Secuencias de comandos de Encabezado y Pie de página personalizadas](../assets/style-cif-component/custom-header-footer-script.png)

   Estas secuencias de comandos incluyen **venia.base** y **venia.cif** como parte de todas las páginas.

   >[!NOTE]
   >
   > Solo las bibliotecas base están &quot;codificadas&quot; como parte de los scripts de página. `venia.site` no se incluye en estos archivos y, en su lugar, se incluye como parte de la plantilla de página para una buena flexibilidad. Esto se inspeccionará más adelante.

1. Desde la terminal, cree e implemente todo el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## Creación de un teaser de productos {#author-product-teaser}

Ahora que se han implementado las actualizaciones de código, agregue una nueva instancia del componente teaser de productos a la página principal del sitio con las herramientas de creación de AEM. Esto nos permitirá ver los estilos actualizados.

1. Abra una nueva pestaña del explorador y vaya a la **Página principal** del sitio: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Expanda el buscador de recursos (el carril lateral) en **Editar** en el menú contextual. Cambie el filtro Recurso a **Productos**.

   ![Expanda el Buscador de recursos y filtre por Productos](../assets/style-cif-component/drag-drop-product-page.png)

1. Arrastre y suelte un nuevo producto en la página principal del contenedor de diseño principal:

   ![Teaser de productos con borde rosa](../assets/style-cif-component/pink-border-product-teaser.png)

   Debería ver que el teaser de productos ahora tiene un borde rosa claro basado en el cambio de regla CSS creado anteriormente.

## Verificación de las bibliotecas de cliente en la página {#verify-client-libraries}

A continuación, verifique la inclusión de las bibliotecas de cliente en la página.

1. Vaya a la **Página principal** del sitio: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleccione el menú **Información de página** y haga clic en **Ver tal y como aparece publicado**:

   ![Ver como aparece publicado](../assets/style-cif-component/view-as-published.png)

   De este modo se abre la página sin que se hayan cargado los archivos JavaScript del Autor de AEM, ya que aparecería en el sitio publicado. Observe que la dirección URL tiene el parámetro de consulta . `?wcmmode=disabled` anexado. Al desarrollar CSS y Javascript, se recomienda utilizar este parámetro para simplificar la página sin ningún elemento del Autor de AEM.

1. Vea el origen de la página y debe poder identificar varias bibliotecas de cliente incluidas:

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   A las bibliotecas de cliente que se envíen a la página se les agregará el prefijo `/etc.clientlibs` y se sirven a través de un [proxy](/help/implementing/developing/introduction/clientlibs.md) para evitar exponer cualquier elemento sensible en `/apps` o `/libs`.

   Aviso `venia/clientlibs/clientlib-site.min.css` y `venia/clientlibs/clientlib-site.min.js`. Estos son los archivos CSS y Javascript compilados derivados de la variable `ui.frontend` módulo.

## Inclusión de la biblioteca de cliente con plantillas de página {#client-library-inclusion-pagetemplates}

Existen varias opciones para incluir una biblioteca del lado del cliente. A continuación, revise cómo el proyecto generado incluye el `clientlib-site` bibliotecas mediante [Plantillas de página](/help/implementing/developing/components/templates.md).

1. Vaya a la **Página principal** del sitio dentro del Editor de AEM: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleccione el **Información de la página** y haga clic en **Editar plantilla**:

   ![Editar la plantilla](../assets/style-cif-component/edit-template.png)

   Se abrirá la variable **Página de aterrizaje** plantilla de **Página principal** se basa en

   >[!NOTE]
   >
   > Para ver todas las plantillas disponibles en la pantalla Inicio de AEM, vaya a **Herramientas** > **General** > **Plantillas**.

1. En la esquina superior izquierda, seleccione el icono **Información de página** y haga clic en **Política de página**.

   ![Elemento de menú de directiva de página](../assets/style-cif-component/page-policy-menu.png)

1. Se abrirá la directiva de página para la plantilla Página de aterrizaje:

   ![Política de página: página de aterrizaje](../assets/style-cif-component/page-policy-properties.png)

   A la derecha puede ver una lista de **categorías** de bibliotecas de clientes que se incluirán en todas las páginas que utilicen esta plantilla.

   * `venia.dependencies` - Proporciona cualquier biblioteca de proveedor que `venia.site` depende de.
   * `venia.site` - Esta es la categoría para `clientlib-site` que `ui.frontend` genera el módulo.

   Tenga en cuenta que otras plantillas utilizan la misma directiva, la **página de contenido**, la **página de aterrizaje**, etc. Al reutilizar la misma directiva, podemos garantizar que se incluyan las mismas bibliotecas de cliente en todas las páginas.

   La ventaja de utilizar las plantillas y las directivas de página para administrar la inclusión de bibliotecas de cliente es que puede cambiar la directiva por plantilla. Por ejemplo: quizás esté administrando dos marcas diferentes dentro de la misma instancia de AEM. Cada marca tendrá su propio estilo o *tema* único, pero las bibliotecas base y el código serán los mismos. Otro ejemplo: si tiene una biblioteca de cliente más grande que solo desea que aparezca en determinadas páginas, puede crear una directiva de página única solo para esa plantilla.

## Desarrollo de Webpack local {#local-webpack-development}

En el ejercicio anterior, se actualizó la información de los archivos Sass de la `ui.frontend` y después de realizar una compilación de Maven, los cambios se implementan en AEM. A continuación, analizaremos cómo aprovechar un webpack-dev-server para desarrollar rápidamente los estilos front-end.

El webpack-dev-server proxies imágenes y parte del CSS/JavaScript de la instancia local de AEM, pero permite al desarrollador modificar los estilos y JavaScript en la variable `ui.frontend` módulo.

1. En el navegador, vaya a la **Página principal** página y **Ver tal y como aparece publicado**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. Ver el origen de la página y el **copy** el HTML sin procesar de la página.

1. Vuelva al IDE que elija debajo de la `ui.frontend` abra el archivo : `ui.frontend/src/main/static/index.html`

   ![Archivo de HTML estático](../assets/style-cif-component/static-index-html.png)

1. Sobrescribir el contenido de `index.html` y **pegar** el HTML copiado en el paso anterior.

1. Busque las inclusiones para `clientlib-site.min.css`, `clientlib-site.min.js` y **remove** ellos.

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   Se eliminan porque representan la versión compilada de CSS y JavaScript que genera el `ui.frontend` módulo. Deje las otras bibliotecas de cliente como se sustituirán desde la instancia de AEM en ejecución.

1. Abra una nueva ventana de terminal y vaya a la `ui.frontend` carpeta. Ejecutar el comando `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   Esto iniciará el webpack-dev-server en [http://localhost:8080/](http://localhost:8080/)

   >[!CAUTION]
   >
   > Si aparece un error relacionado con Sass, detenga el servidor y ejecute el comando `npm rebuild node-sass` y repita los pasos anteriores. Esto puede ocurrir si se tiene una versión diferente de `npm` y `node` a continuación especificado en el proyecto `aem-cif-guides-venia/pom.xml`.

1. Vaya a la [http://localhost:8080/](http://localhost:8080/) en una pestaña nueva con el mismo explorador que un registrado en la instancia de AEM. Debería ver la página de inicio de Venia a través del webpack-dev-server:

   ![Servidor de desarrollo de Webpack en el puerto 80](../assets/style-cif-component/webpack-dev-server-port80.png)

   Deje webpack-dev-server en ejecución. Se utilizará en el próximo ejercicio.

## Implementación del estilo de tarjeta para el teaser de productos {#update-css-product-teaser}

A continuación, modifique los archivos Sass en la variable `ui.frontend` para implementar un estilo de tarjeta para el teaser de productos. El webpack-dev-server será usado para ver rápidamente los cambios.

Vuelva al IDE y al proyecto generado.

1. En el **ui.frontend** volver a abrir el archivo `_productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

1. Realice los siguientes cambios en el borde del teaser de productos:

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
           display: block;
           grid-area: main;
           height: auto;
           opacity: 1;
           transition-duration: 512ms;
           transition-property: opacity, visibility;
           transition-timing-function: ease-out;
           visibility: visible;
           width: 100%;
       }
   ```

   Guarde los cambios y el webpack-dev-server se actualizará automáticamente con los nuevos estilos.

1. En el teaser de productos, añada una sombra paralela e incluya esquinas redondeadas.

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. Actualice el nombre del producto para que aparezca en la parte inferior del teaser y modifique el color del texto.

   ```css
   .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

1. Actualice el precio del producto para que también aparezca en la parte inferior del teaser y modifique el color del texto.

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. Actualice la consulta de medios en la parte inferior para apilar el nombre y el precio en pantallas menores que **992px**.

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   Ahora debería ver el estilo de tarjeta reflejado en el webpack-dev-server:

   ![Cambios en el teaser del servidor de desarrollo de Webpack](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   Sin embargo, los cambios aún no se han implementado en AEM. Puede descargar el archivo [solution aquí](../assets/style-cif-component/_productteaser.scss).

1. Implemente las actualizaciones en AEM con sus habilidades con Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >Existen [herramientas y configuración IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) adicionales que pueden sincronizar los archivos de proyecto directamente con una instancia de AEM local sin tener que realizar una compilación completa de Maven.

## Visualización de teaser de productos actualizado {#view-updated-product-teaser}

Una vez que el código del proyecto se haya implementado en AEM, debería poder ver los cambios en el teaser de productos.

1. Vuelva al explorador y vuelva a actualizar la página principal: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). Debe ver los estilos aplicados del teaser de productos actualizado.

   ![Estilo del teaser de productos actualizado](../assets/style-cif-component/product-teaser-new-style.png)

1. Experimente añadiendo teaser de productos adicionales. Utilice el modo Diseño para cambiar la anchura y el desplazamiento de los componentes a fin de mostrar varios teasers en una fila.

   ![Varios teasers de producto](../assets/style-cif-component/multiple-teasers-final.png)

## Solución de problemas {#troubleshooting}

Puede verificar en [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) que se ha implementado el archivo CSS actualizado: [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

Al implementar nuevos archivos CSS o JavaScript, también es importante asegurarse de que el explorador no muestre archivos antiguos. Se pueden eliminar borrando la caché del explorador o iniciando una nueva sesión del explorador.

AEM también intenta almacenar en caché las bibliotecas de cliente para el rendimiento. En ocasiones, tras una implementación de código, se muestran los archivos más antiguos. Puede invalidar manualmente la caché de la biblioteca de cliente de AEM con la herramienta [Reconstruir bibliotecas de cliente](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Invalidar cachés es el método preferido si sospecha que AEM ha almacenado en caché una versión antigua de una biblioteca de cliente. La reconstrucción de bibliotecas es ineficiente y lleva mucho tiempo.*

## Felicitaciones {#congratulations}

Acaba de diseñar su primer componente principal AEM CIF y utilizó un servidor de desarrollo de webpack.

## Desafío para una bonificación {#bonus-challenge}

Utilice el [sistema de estilos de AEM](/help/sites-cloud/authoring/features/style-system.md) para crear dos estilos que se puedan activar o desactivar con el autor de contenido. [El desarrollo con el sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html?lang=es) incluye pasos detallados e información sobre cómo hacerlo.

![Desafío para una bonificación: Sistema de estilos](../assets/style-cif-component/bonus-challenge.png)

## Recursos adicionales {#additional-resources}

* [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
* [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
* [Configuración de un Entorno de desarrollo de AEM local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [Bibliotecas de cliente](/help/implementing/developing/introduction/clientlibs.md)
* [Introducción a AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)
* [Desarrollo con el sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
