---
title: Componentes principales de AEM CIF de estilo
description: Componentes principales de AEM CIF de estilo
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---


# Componentes principales de AEM CIF de estilo {#style-aem-cif-core-components}

El arquetipo [del proyecto](https://github.com/adobe/aem-cif-project-archetype) CIF crea un proyecto CIF de Adobe Experience Manager mínimo (AEM) como punto de partida para los proyectos de clientes que utilizan [AEM componentes](https://github.com/adobe/aem-core-cif-components)principales CIF. Inicialmente se aplica al sitio un estilo predeterminado, conocido como la marca Venia. En este tutorial, inspeccionará un nuevo proyecto de CIF de AEM, generado por el arquetipo, y comprenderá cómo se organizan los componentes principales de CIF y CSS y JavaScript utilizados por AEM. También creará un nuevo estilo con CSS para reemplazar el estilo predeterminado del componente teaser de producto.

![Qué va a generar](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> Se implementará un nuevo estilo para el componente Product Teaser que se asemeje a una tarjeta.

## Requisitos previos {#prerequisites}

Se requieren las siguientes herramientas y tecnologías:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (solo AEM 6.5 o posterior)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
* Adobe Experience Manager (instancia local)
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* Magento que ejecuta una [versión compatible con el arquetipo](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Generar un proyecto {#generate-project}

Generaremos un nuevo proyecto de CIF AEM usando el arquetipo [del proyecto](https://github.com/adobe/aem-cif-project-archetype) CIF y luego anularemos los estilos predeterminados.

**Siéntase libre de usar un proyecto** existente (basado en el arquetipo del proyecto CIF) y omita esta sección.

1. Determine la versión más reciente del Arquetipo de proyecto CIF consultando [la última versión en GitHub](https://github.com/adobe/aem-cif-project-archetype/releases/latest). En el siguiente paso, reemplace `x.y.z` por la versión de la última versión.

1. Ejecute el siguiente comando Maven para generar un nuevo proyecto en modo [](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)por lotes.

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Añada las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Magento o agregar las configuraciones al proyecto recién creado.

1. En este punto, debería tener una versión de trabajo de una tienda conectada a una instancia de Magento. Vaya a la página `US` > `Home` en: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Hay que ver que la tienda está usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, verá varias categorías que indican que el Magento de conexión está funcionando.

   ![Tienda configurada con tema de Venia](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introducción a las bibliotecas de clientes {#introduction-to-client-libraries}

La CSS y JavaScript responsables de procesar el tema o los estilos de la tienda son administrados en AEM por una biblioteca [](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) cliente o clientlibs para abreviar. Las bibliotecas de cliente proporcionan un mecanismo para organizar CSS y Javascript en el código de un proyecto y luego distribuirlas en la página.

La manera en que podemos aplicar estilos específicos de marca a AEM componentes principales de CIF es agregando y anulando el CSS administrado por estas bibliotecas de clientes. Es fundamental comprender cómo se estructuran e incluyen las bibliotecas de cliente en la página.

### Bibliotecas del cliente del proyecto {#project-client-libraries}

Luego analizaremos las bibliotecas de cliente generadas automáticamente por el arquetipo. Utilice el IDE de su elección para [importar el proyecto generado en el ejercicio](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)anterior.

1. Navegue y expanda el módulo **ui.apps** y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`::

   ![clientlibs de ui.apps](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Hay dos carpetas debajo, **clientlib-base** y **topic**.

1. **clientlib-base** : es una biblioteca de cliente vacía que simplemente incrusta las dependencias necesarias de [AEM componentes](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html)principales.

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   A continuación se muestra la definición XML de **clientlib-base** (el `.content.xml` archivo):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` es la categoría para esta biblioteca de cliente. Considere una categoría como una etiqueta. Se utilizará para incluir o incrustar la biblioteca en la página.

   Observe la propiedad `embed` y la matriz de otras categorías clientlib. Cada una de estas categorías representa una biblioteca de cliente. Por ejemplo, `core.wcm.components.accordion.v1` incluye el código JavaScript necesario para que funcione el componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) Acordeón.

   Mediante las propiedades `embed` y `categories` puede administrar e incluir bibliotecas de cliente de diferentes proyectos.

   `allowProxy=true` garantiza que la biblioteca de cliente CSS y JavaScript se proporcionen desde una ruta con el prefijo: `/etc.clientlibs`. Esto garantiza que el código de la aplicación debajo `/apps` permanezca protegido de los usuarios finales, pero que CSS y JavaScript necesarios para que el sitio web funcione puedan servir de forma anónima. Encontrará más detalles sobre la propiedad [allowProxy aquí](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **tema** : es la biblioteca del cliente que contiene el tema de inicio y la CSS para el proyecto CIF. Esta biblioteca de cliente está diseñada para ser personalizada por cada implementación y resulta útil tener en inicio algunos estilos existentes para que los componentes sean funcionales para el inicio.

   ![topic clientlibrary](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   A continuación se muestra la definición XML del **tema**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` es la categoría de esta biblioteca de cliente y así es como se incluirá la biblioteca de cliente en la página.

1. Debajo de la biblioteca del cliente de **temas** debe ver un archivo llamado **css.txt** ubicado en: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`::

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   El **css.txt** (y **js.txt**) actúan como manifiestos que dictan el orden en que se incluyen los archivos individuales en el archivo CSS final. Los pedidos son importantes tanto para CSS como para JavaScript y es bueno poder crear varios archivos para administrar mejor el código. Si busca en el archivo **css.txt** , verá que los archivos están organizados por los componentes a los que se aplican los estilos.

1. Inspect utiliza los archivos CSS situados debajo del **tema o los componentes** para hacerse una idea de los estilos de los componentes ootb. Actualizaremos algunos de estos archivos más adelante en el tutorial.

### Inclusión de la biblioteca del cliente con el componente de página base

A continuación, analizaremos cómo se incluyen las bibliotecas de cliente en una página mediante [HTL](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) y el componente Página.

1. En el módulo **ui.apps** , vaya a la definición del `page` componente en: `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Este componente de **página** , generado por el arquetipo, es el punto de entrada utilizado para procesar todas las páginas del proyecto.

1. Si inspecciona la definición del componente de **página** (`page/.content.xml`), verá una propiedad `sling:resourceSuperType` que apunta a `core/cif/components/structure/page/v1/page`. Esto significa que el componente de **página** de nuestro proyecto (Acme) heredará toda la funcionalidad del componente de página [principal de](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) CIF y nos permitirá administrar menos código.

1. Debajo del componente de **página** encontrará dos archivos: **customheaderlibs.html** y **customfoterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** es una secuencia de comandos HTL que se procesará al principio de la página. Es una secuencia de comandos común para sobrescribir y agregar lógica específica del proyecto. En este caso lo estamos utilizando para incluir la biblioteca cliente con una categoría de `acme.wcm.base`. Siguiendo las optimizaciones de desarrollo web, solo incluimos la CSS en el encabezado de la página.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfoterlibs.html** es un script HTL que se procesará en la parte inferior de la página, justo antes de la `</body>` etiqueta de cierre. Nuevamente se utiliza la categoría de `acme.wcm.base` pero esta vez sólo se cargará el JavaScript de la biblioteca del cliente.

La modificación de las secuencias de comandos HTML del componente de **página** es la forma en que `acme.wcm.base` se incluye en todas las páginas. Sin embargo, ¿qué hay de `acme.theme`? En el próximo ejercicio analizaremos otra opción para incluir bibliotecas de clientes.

### Inclusión de la biblioteca de clientes con plantillas de página {#client-library-inclusion-pagetemplates}

Existen varias opciones para incluir una biblioteca del lado del cliente. A continuación, analizaremos cómo el proyecto generado incluye las bibliotecas de temas del lado del cliente a través de las plantillas [de página](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html).

Abra un navegador nuevo e inicie sesión en la instancia de AEM en la que ha implementado el proyecto al principio de este tutorial.

1. En la pantalla del Inicio de AEM, vaya a **Herramientas** > **General** > **Plantillas**.

   ![Navegación de plantilla](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Vaya a la carpeta **Configuración** del almacén de acúmenes. Abra la plantilla **de página de** Categoría seleccionando el icono de *lápiz* .

   ![Tarjeta de plantilla de página de categoría](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. En la esquina superior izquierda, seleccione el icono Información **de** página y haga clic en Política **de** página.

   ![Elemento de menú de directiva de página](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. Se abrirá la directiva de página para la plantilla Página de catálogo:

   ![Directiva de página: página de catálogo](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   A la derecha puede ver una lista de **categorías** de bibliotecas de clientes que se incluirán en todas las páginas que utilicen esta plantilla.

   * **wcm.foundation.components.page.adaptable** : Proporciona la CSS necesaria para que los autores puedan habilitar los controles de diseño [](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) interactivos.
   * **acme.topic** : es el tema de inicio que el arquetipo genera automáticamente. De forma predeterminada, este estilo es similar al almacén de demostración de Venia. Sin embargo, como se puede ver en el nombre, la implementación del proyecto pretende personalizarlo. *Esto es lo que vamos a modificar en la siguiente sección!*
   * **core.cif.components.response** : es una biblioteca de clientes compilada con varios componentes de React que se utilizan para funciones dinámicas como el carro de compras. Puede encontrar más [información aquí](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Tenga en cuenta que otras plantillas utilizan la misma directiva, página **** de contenido, **Página de aterrizaje**, etc. Al reutilizar la misma directiva, podemos garantizar que se incluyan las mismas bibliotecas de cliente en todas las páginas.

   La ventaja de utilizar las plantillas y las directivas de página para administrar la inclusión de bibliotecas de cliente es que puede cambiar la directiva por plantilla. Por ejemplo: quizás esté administrando dos marcas diferentes dentro de la misma instancia de AEM. Cada marca tendrá su propio estilo o *tema* único, pero las bibliotecas base y el código serán los mismos. Otro ejemplo: si tiene una biblioteca de cliente más grande que sólo desea que aparezca en determinadas páginas, puede crear una directiva de página única solo para esa plantilla. La otra ventaja

### Verificación de las bibliotecas de cliente en la página {#verify-client-libraries}

En este punto hemos revisado cómo incluir las bibliotecas de cliente que utilizan HTL con las secuencias de comandos **customheaderlibs.html** y **customfoterlibs.html** y cómo se puede utilizar una directiva de página de Plantilla para incluir bibliotecas de cliente adicionales. Luego verificaremos la inclusión de las bibliotecas cliente en el sitio.

1. En la pantalla del Inicio de AEM, vaya a **Sitios** > Tienda **de** Acme > Estados **** Unidos > **Inglés** y abra la página para editarla: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Seleccione el menú Información **de** página y haga clic en **Vista tal y como aparece publicado**:

   ![Ver tal y como aparece publicado](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   De este modo se abrirá la página sin que se haya cargado ninguno de los archivos javascript del autor de AEM, ya que aparecería en el sitio publicado. Observe que la dirección URL tiene el parámetro de consulta `?wcmmode=disabled` anexado. Al desarrollar CSS y Javascript, se recomienda utilizar este parámetro para simplificar la página sin ningún elemento de AEM autor.

1. Vista el origen de la página y debe poder identificar las siguientes bibliotecas de cliente: **acme.wcm.base**, **wcm.foundation.components.page.adaptable**, **acme.topic**, **core.cif.components.response**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## Estilo del teaser de productos {#style-product-teaser}

Ahora que entendemos la estructura de la biblioteca de cliente generada por el arquetipo, podemos empezar a personalizar los componentes principales de AEM CIF. Modificaremos los estilos del componente Product Teaser para que parezca más una &quot;tarjeta&quot;.

### Creación del teaser de productos {#author-product-teaser}

Como primer paso, agregaremos una nueva instancia del componente Product Teaser a la página de inicio de nuestro sitio con las herramientas de creación de AEM.

1. Abra una nueva ficha del explorador y vaya a la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Inserte un nuevo componente **de teaser** de producto en el contenedor de diseño principal de la página.

   ![Insertar teaser de productos](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Expanda el panel lateral (si no está activado) y cambie el menú desplegable del buscador de recursos a **Productos**. Esto debería mostrar una lista de los productos disponibles de una instancia de Magento conectada. Seleccione un producto y **arrástrelo y suéltelo** en el componente **Product Teaser** de la página.

   ![Arrastrar y soltar teaser de producto](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Tenga en cuenta que también puede configurar el producto mostrado configurando el componente mediante el cuadro de diálogo (haciendo clic en el icono de *llave inglesa* ).

1. Ahora debería ver un producto que está mostrando el teaser de productos. El nombre del producto y el precio del producto son atributos predeterminados que se muestran.

   ![Teaser de productos: estilo predeterminado](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Actualizar el CSS para el teaser de productos {#update-css-product-teaser}

A continuación, modificaremos la CSS en la biblioteca del cliente del **tema** para implementar un estilo de tarjeta para el teaser del producto.

Vuelva al IDE y al proyecto generado.

1. En el módulo **ui.apps** , vaya a la carpeta: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. Aquí es donde se definen todos los estilos del teaser de productos.

1. Abra el archivo **teaser.css** y actualice las reglas CSS correspondientes (o descargue el archivo [teaser.css de la](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) solución y sustitúyalo).

   Añada una sombra paralela e incluya esquinas redondeadas en el teaser de productos.

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   Cambie el borde de la imagen en el teaser de productos.

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
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

   Actualice el nombre del producto para que aparezca en la parte inferior del teaser y modifique el color del texto.

   ```css
   .productteaser .item__name {
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

   Actualice el precio del producto para que también aparezca en la parte inferior del teaser y modifique el color del texto.

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   Actualice la consulta de medios en la parte inferior para apilar el nombre y el precio en pantallas de menos de 992 píxeles.

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

   Guarde los cambios en **teaser.css**. Puede descargar el archivo [solution teaser.css aquí](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Implemente las actualizaciones del módulo **ui.apps** para AEM con sus habilidades Maven, desde un terminal de línea de comandos:

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >Existen herramientas [y configuración](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) IDE adicionales que pueden sincronizar los archivos de proyecto directamente con una instancia de AEM local sin tener que realizar una compilación completa de Maven.

### Teaser de producto actualizado de Vista {#view-updated-product-teaser}

Una vez que el código del proyecto se haya implementado en AEM, ahora deberíamos poder ver los cambios en el teaser de productos.

1. Vuelva al explorador y vuelva a actualizar la Página de inicio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). Debe ver los estilos de teaser de producto actualizados aplicados.

   ![Estilo teaser de producto actualizado](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Experimente agregando teasers de producto adicionales. Utilice el modo Diseño para cambiar la anchura y el desplazamiento de los componentes a fin de mostrar varios teasers en una fila.

   ![Varios teasers de producto](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Cada teaser de producto contiene el mismo estilo.

### Solución de problemas {#troubleshooting}

Puede comprobar en [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) que se ha implementado el archivo CSS actualizado: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

Al implementar nuevos archivos CSS y/o JavaScript, también es importante asegurarse de que el explorador no ofrezca archivos antiguos. Esto se puede eliminar borrando la caché del explorador o iniciando una nueva sesión del explorador.

AEM también intenta almacenar en caché las bibliotecas de cliente para obtener un rendimiento. En ocasiones, tras una implementación de código, se sirven los archivos más antiguos. Puede invalidar manualmente AEM caché de la biblioteca de cliente mediante la herramienta [](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)Reconstruir bibliotecas de cliente. *Invalidar cachés es el método preferido si sospecha que AEM ha almacenado en caché una versión antigua de una biblioteca de cliente. La reconstrucción de bibliotecas es ineficiente y lleva mucho tiempo.*

### Felicitaciones {#congratulations}

¡Acabas de diseñar tu primer componente principal AEM CIF!

### Desafío de bonos {#bonus-challenge}

Utilice el sistema [Estilo de](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) AEM para crear dos estilos que un autor de contenido puede activar o desactivar. [El desarrollo con el sistema](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) de estilos incluye pasos detallados e información sobre cómo hacerlo.

![Retos de bonificación - estilo de sistema](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Recursos adicionales {#additional-resources}

* [Arquetipo CIF AEM](https://github.com/adobe/aem-cif-project-archetype)

* [Componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components)

* [Configurar un Entorno de desarrollo de AEM local](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Bibliotecas del cliente](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [Introducción a los AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Desarrollo con el sistema de estilos](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
