---
title: Personalice los componentes principales de CIF
description: Personalice los componentes principales de CIF
translation-type: ht
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: ht
source-wordcount: '2520'
ht-degree: 100%

---


# Personalización de los componentes principales del CIF de AEM {#customize-cif-components}

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) proporcionan un conjunto estándar de componentes de comercio que pueden utilizarse para acelerar un proyecto que integra soluciones de Adobe Experience Manager (AEM) y Magento. Estos componentes están listos para la producción y se pueden [diseñar fácilmente con CSS](style-cif-component.md). Muchas implementaciones también desean ampliar estos componentes para satisfacer los requerimientos específicos de la empresa.

En este tutorial analizaremos varios puntos de extensión diferentes proporcionados por los componentes principales del CIF de AEM y de AEM en general. Para ello, ampliaremos las funcionalidades del componente [teaser de productos](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para incluir la capacidad de renderizar un titular &quot;Nuevo&quot;. Los autores de contenido tendrán la capacidad de alternar este titular y determinar cuánto tiempo se mostrará. La &quot;edad&quot; del producto se basa en su fecha de creación en el catálogo de Magento. Una vez que un producto tiene una cierta cantidad de días, el titular &quot;Nuevo&quot; debe desaparecer automáticamente.

![Nuevo titular extendido](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Requisitos previos {#prerequisites}

Se requieren las siguientes herramientas y tecnologías:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
* [SKD de AEM Cloud con el complemento CIF](../develop.md)
* Compatibilidad de Magento con los componentes principales del CIF

Se recomienda revisar el siguiente contenido antes de continuar con este tutorial:

* [Presentación de Commerce Integration Framework en AEM as a Cloud Service.](/help/commerce-cloud/overview.md)
* [Diseño de los componentes principales del CIF de AEM: tutorial](style-cif-component.md)

## Proyecto de inicio

Hemos proporcionado un proyecto de inicio para utilizarlo con este tutorial. El proyecto se generó usando la [versión 0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) del tipo de archivo del proyecto CIF. Se considera una práctica recomendada utilizar siempre la [última versión](https://github.com/adobe/aem-cif-project-archetype/releases/latest) del tipo de archivo al iniciar un nuevo proyecto.

1. Descargue el proyecto de inicio [**acme-store.zip**](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip) a su escritorio.

1. Descomprima **acme-store.zip** y debería ver la siguiente estructura de carpetas:

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. Abra una nueva ventana de terminal y cree e implemente el proyecto en una instancia local de AEM;

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Añada las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Magento o añadir las configuraciones al proyecto recién creado.

1. En este punto, debería tener una versión de trabajo de una tienda conectada a una instancia de Magento. Vaya a la página `US` > `Home` en: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, verá varias categorías que indican que la conexión con Magento está funcionando.

   ![Tienda configurada con tema de Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Creación del teaser de productos {#author-product-teaser}

Ampliaremos el componente teaser de productos a través de este tutorial. Como primer paso, añadiremos una nueva instancia del teaser de productos a la página de inicio para entender la funcionalidad de línea de base.

1. Vaya hasta la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Inserte un nuevo componente **teaser de productos** en el contenedor del diseño principal de la página.

   ![Inserción del teaser de productos](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Expanda el panel lateral (si no está activado) y cambie desde menú desplegable del buscador de recursos a **Productos**. Esto debería mostrar una lista de los productos disponibles de una instancia conectada a Magento. Seleccione un producto y **arrástrelo y suéltelo** en el componente **teaser de productos** de la página.

   ![Arrastrar y soltar teaser de productos](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Tenga en cuenta que también puede configurar el producto mostrado configurando el componente con el cuadro de diálogo (haga clic en el icono de *llave inglesa*).

1. Ahora debería ver un producto que muestra el teaser de productos. Se muestran el nombre y el precio del producto ya que son atributos predeterminados.

   ![Teaser de productos: estilo predeterminado](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalización del marcado del teaser de productos {#customize-markup-product-teaser}

Una extensión común de los componentes de AEM es modificar el marcado que genera el componente. Esto se realiza anulando la [secuencia de comandos HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) que utiliza el componente para representar su marcado. La plantilla de idioma HTML (HTL) es un idioma de plantilla ligero que los componentes de AEM utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite la reutilización de los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En nuestro caso, queremos renderizar un titular sobre el teaser para indicar que el producto es &quot;Nuevo&quot; y que se ha añadido recientemente al catálogo. El patrón de diseño para [personalizar el marcado](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de un componente es en realidad estándar para todos los componentes AEM, no solo para los componentes principales del CIF de AEM.

Utilice el IDE de su elección para [abrir el proyecto de inicio descargado](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) al principio del tutorial.

1. Navegue y expanda el módulo **ui.apps** y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e inspeccione el archivo `.content.xml` .

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Arriba se encuentra la definición del componente para el componente teaser de productos en nuestro proyecto. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este es un ejemplo de creación de un [componente Proxy](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/get-started/using.html#create-proxy-components). En lugar de copiar y pegar todas las secuencias de comandos HTL del teaser de productos de los componentes principales del CIF de AEM, podemos usar `sling:resourceSuperType` para heredar todas las funcionalidades.

1. Abra un explorador nuevo y vaya a [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) en AEM. Expanda el árbol para ver el `productteaser` componente en: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![Teaser del producto CRXDE Lite](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Es la definición completa del componente para el componente teaser de productos.

1. Cambie a su IDE y al proyecto de Tienda Acme. Cree un nuevo archivo con el nombre `productteaser.html` debajo de `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copie el contenido de `productteaser.html` de [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) y péguelo en el proyecto Acme-Store en el `productteaser.html` archivo recién creado.

   ![Sobrescritura HTML del teaser de productos](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. En el proyecto Acme-Store, modifique el `productteaser.html` archivo e inserte un nuevo div que represente un distintivo sobre el marcado de la imagen del producto:

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. Implemente el código actualizado en la instancia local de AEM con sus habilidades con Maven o con [las características de su IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. En el explorador, vuelva a la [página principal de la tienda](http://localhost:4502/editor.html/content/acme/us/en.html) en AEM. Actualice y verá que aparece un titular &quot;nuevo&quot; en la esquina superior derecha del componente.

   ![Nuevo titular extendido](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   Actualmente no hay ninguna lógica detrás de cuándo se mostrará el titular. En los próximos ejercicios corregiremos eso.

   > Tenga en cuenta que el CSS para renderizar el titular se proporcionó como parte del proyecto de inicio y se puede encontrar en: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Para obtener más información, consulte el tutorial [Diseño de componentes principales del CIF](style-cif-component.md).

## Personalización del cuadro de diálogo del teaser de productos {#customize-dialog-product-teaser}

A continuación, personalizaremos el cuadro de diálogo del componente teaser de productos para permitir que un Autor determine el intervalo de fecha para el cual un producto se considera &quot;nuevo&quot; y si se debe mostrar el titular. Para ello, [personalizaremos el cuadro de diálogo](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) del teaser de productos como parte del proyecto de tienda Acme.

1. Abra el proyecto de la tienda Acme en el IDE que desee y vaya a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Debajo de la carpeta `productteaser`, añada una nueva carpeta denominada `_cq_dialog`. Añada un nuevo archivo a la `_cq_dialog` carpeta denominada `.content.xml`. Ahora debe tener la siguiente estructura de archivos:

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. Actualice `_cq_dialog/.content.xml` con el siguiente XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   Arriba hemos agregado dos campos adicionales como parte de una nueva pestaña y un único campo oculto.

   1. Casilla de verificación para mostrar el distintivo &quot;Nuevo&quot;
   2. Campo de número para definir la edad máxima del producto
   3. Campo oculto para asegurarse de que la edad máxima del producto se guarde con una longitud (consulte [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) para obtener más información).

   Los cuadros de diálogo definidos como parte de un componente proxy heredan todos los campos de diálogo existentes con una función conocida como [fusión de recursos de Sling](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html). Por lo tanto, no es necesario redefinir los campos existentes que forman parte del teaser de productos.

1. Actualice `productteaser.html` y añada un `data-sly-test` al `<div>` para el distintivo. Será una prueba sencilla para decidir procesar el distintivo si el usuario ha marcado &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Implemente el código actualizado en la instancia local de AEM mediante las funciones de su IDE o con sus habilidades con Maven:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Vuelva al componente teaser de productos y haga clic en el icono de la *llave inglesa* para abrir el cuadro de diálogo. Ahora debería ver una pestaña para el **distintivo** con dos campos adicionales. Al actualizar estos campos, los valores se mantienen en AEM. Debe poder activar o desactivar el distintivo con la casilla de verificación:

   ![Alternar distintivo](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Esto le da al autor cierto control sobre cuándo aparece el distintivo. Sin embargo, sería ideal que el distintivo desapareciera automáticamente una vez que el producto haya alcanzado una cierta edad en el día según la entrada de la **edad máxima del producto**. Para ello, tendremos que implementar una lógica de back-end.

## Actualización del modelo de Sling para el teaser de productos {#updating-sling-model-product-teaser}

A continuación, ampliaremos la lógica empresarial del teaser de productos implementando el modelo Sling. [Los modelos de Sling](https://sling.apache.org/documentation/bundles/models.html) son objetos Java antiguos comunes (&quot;POJO&quot;), impulsados por anotaciones que implementan cualquier lógica comercial necesaria para el componente. Los modelos Sling se utilizan junto con las secuencias de comandos HTL como parte del componente. Seguiremos el patrón de [delegación de modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que podamos extender las partes del modelo de teaser de productos existente.

Los modelos Sling se implementan como Java y se pueden encontrar en el módulo **principal** del proyecto generado.

1. Abra el proyecto de la tienda Acme en el IDE que desee y vaya al módulo **principal** a: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** es una interfaz de Java que hemos creado previamente y que amplía la interfaz **ProductTeaser** del CIF.

1. A continuación, abra el archivo **MyProductTeaserImpl.java** ubicado en: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` es la clase de implementación para la interfaz `MyProductTeaser`.

   Utilizando el patrón de [delegación para modelos Sling,](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) podemos hacer referencia a la clase `ProductTeaser`mediante la propiedad `sling:resourceSuperType`:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos los métodos que no queremos anular o cambiar, simplemente podemos devolver el valor que devuelve el `ProductTeaser`:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. Uno de los puntos de extensión adicionales que proporcionan los componentes principales del CIF de AEM es el `AbstractProductRetriever` que nos permite tener acceso a los atributos de productos específicos. Añada el siguiente método para inicializar el `AbstractProductRetriever` en el método `init()`:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
       }
   ...
   ```

1. Pruebe estos cambios modificando el precio con formato y anulando la lógica en `getFormattedPrice()`. Realice las siguientes actualizaciones para dar formato explícito al precio en función de la configuración regional en alemán (o elija otro país).

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   Observe cómo el objeto `productRetriever` nos da acceso al objeto `ProductInterface` mediante el método `fetchProduct()` . Puede ver todos los métodos [disponibles aquí](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Nota:* Modificar la configuración regional a alemán es solo un ejemplo divertido para ver la anulación. En realidad, ProductTeaser utiliza la configuración regional de la [página para determinar el formato](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. A continuación, debemos actualizar **productteaser.html** en el módulo **ui.apps** para hacer referencia a nuestro nuevo modelo Sling en: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   Guarde los cambios en `productteaser.html`.

1. Implemente el código base en la instancia local de AEM. Dado que se han realizado cambios en los módulos **ui.apps** y **core**, cree e implemente el proyecto desde la raíz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Abra un explorador y vaya a [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Esta consola muestra todos los modelos Sling registrados en el sistema. Compruebe que MyTeaserModelImpl se implementó y se asignó correctamente. Debería poder ver algo como:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Por último, navegue hasta el lugar en el que creó el componente teaser de productos y debería ver el precio con el formato de moneda alemán:

   ![Formato de precio actualizado](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementar la lógica isShowBadge {#implement-isshowbadge}

Ahora que hemos tenido la oportunidad de experimentar con la anulación de los métodos del modelo de Sling, vamos a implementar la lógica de cuándo mostrar el distintivo &quot;nuevo&quot;.

1. Vuelva a su IDE y abra el archivo **MyProductTeaser.java** en: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Añada un nuevo método `isShowBadge()` en la interfaz:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   Este es un nuevo método que introduciremos para encapsular la lógica de si mostrar o no el distintivo.

1. A continuación, vuelva a abrir **MyProductTeaserImpl.java** en `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. La lógica de cuánto tiempo se mostrará el distintivo &quot;nuevo&quot; se basará en el atributo `created_at` del Producto. Para tener acceso a ese atributo, necesitamos extender la consulta **GraphQL** realizada por ProductTeaser. Podemos hacerlo actualizando el `init()` método en **MyProductTeaserImpl.java**:

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   Añadir al método `extendProductQueryWith` es una manera eficaz de garantizar que el resto del modelo disponga de atributos de productos adicionales. También minimiza el número de consultas ejecutadas.

   >[!NOTE]
   >En el código anterior utilizamos los `addCustomSimpleField` para recuperar la propiedad `created_at`. Esto ilustra cómo se puede realizar la consulta de cualquier atributo personalizado que forme parte del esquema del Magento.
   >
   > Sin embargo, la propiedad `created_at` se ha implementado realmente como parte de la [interfaz de producto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) y una práctica recomendada sería reutilizar el método como el: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. A continuación, implementaremos el método `isShowBadge()`:

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   En el método anterior comprobamos primero si el autor ha habilitado la funcionalidad de distintivo con la casilla de verificación. A continuación, leemos el valor de la propiedad `age` que se establece como parte del cuadro de diálogo y representa el número máximo de días de antigüedad que debe tener un producto hasta que desaparezca el titular. Finalmente calculamos la antigüedad del producto en base a la `created_at` fecha. Si después de comparar los dos valores regresamos a `true` para mostrar el distintivo, `false` en todos los demás casos.

1. Finalmente, se necesita añadir más a la secuencia de comandos `productteaser.html` para llamar al método `isShowBadge()`. Abra el archivo en `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Realice la siguiente actualización:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Implemente el código base en la instancia local de AEM. Dado que se han realizado cambios en los módulos **ui.apps** y **core**, cree e implemente el proyecto desde la raíz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Regrese a AEM y al componente ProductTeaser y experimente con números diferentes para mostrar la edad máxima del producto. Según la edad del producto, es posible que deba introducir números muy grandes para que se muestre el distintivo.

   ![Edad máxima del producto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Finalmente, busque los registros de AEM para ver la sentencia de registro ingresada anteriormente en el paso 5. Debe imprimir el valor de la propiedad `created_at` que proviene del Magento. Puede vista de los registros de AEM abriendo el archivo `error.log`. Este archivo se encuentra debajo del `crx-quickstart/logs/error.log` donde se ha instalado el jar de AEM. Puede esperar ver un elemento de línea como el siguiente:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Ahora puede verificar que la lógica que implementamos es correcta.

### Felicitaciones {#congratulations}

Acaba de personalizar su primer componente del CIF de AEM. Descargue el paquete de solución [terminado aquí](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Recursos adicionales {#additional-resources}

* [Tipo de archivo de AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalización de los componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalización de componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/customizing.html)
