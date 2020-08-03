---
title: Personalizar componentes principales de CIF
description: Personalizar componentes principales de CIF
translation-type: tm+mt
source-git-commit: dd6973085ae34dd6ea7296c36d0a14f699440269
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---


# Personalizar componentes principales de AEM CIF {#customize-cif-components}

[AEM componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF proporciona un conjunto estándar de componentes de comercio que pueden utilizarse para acelerar un proyecto que integra soluciones de Adobe Experience Manager (AEM) y Magento. Estos componentes están listos para la producción y se pueden diseñar [fácilmente con CSS](style-cif-component.md). Muchas implementaciones también desean ampliar estos componentes para satisfacer los requerimientos específicos del negocio.

En este tutorial analizaremos varios puntos de extensión diferentes proporcionados por AEM componentes principales de CIF y AEM en general. Para ello, ampliaremos las capacidades del componente [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para incluir la capacidad de procesar un letrero &quot;Nuevo&quot;. Los autores de contenido tendrán la capacidad de alternar este letrero y determinar cuánto tiempo se mostrará. La &quot;edad&quot; del producto se basará en su fecha de creación en el catálogo del Magento. Una vez que un producto tiene una cierta cantidad de días, la pancarta &quot;Nuevo&quot; debe desaparecer automáticamente.

![Nueva pancarta extendida](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Requisitos previos {#prerequisites}

Se requieren las siguientes herramientas y tecnologías:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 o posterior)
* [AEM Cloud SKD con complemento CIF](../develop.md)
* Magento compatible con los componentes principales de CIF

Se recomienda revisar el siguiente contenido antes de continuar con este tutorial:

* [Introducción a Commerce Integration Framework en AEM como Cloud Service](/help/commerce-cloud/overview.md)
* [Componentes principales de CIF de estilo AEM - Tutorial](style-cif-component.md)

## Proyecto de inicio

Hemos proporcionado un proyecto de inicio para utilizarlo con este tutorial. El proyecto se generó usando la [versión 0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) del Arquetipo del Proyecto CIF. Se considera una práctica recomendada utilizar siempre la [última versión](https://github.com/adobe/aem-cif-project-archetype/releases/latest) del arquetipo al iniciar un nuevo proyecto.

1. Descargue [**acme-store.zip **](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)del proyecto de inicio en su escritorio.

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

1. Añada las configuraciones de OSGi necesarias para conectar la instancia de AEM a una instancia de Magento o agregar las configuraciones al proyecto recién creado.

1. En este punto, debería tener una versión de trabajo de una tienda conectada a una instancia de Magento. Vaya a la página `US` > `Home` en: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Hay que ver que la tienda está usando actualmente el tema de Venia. Al expandir el menú principal de la tienda, verá varias categorías que indican que el Magento de conexión está funcionando.

   ![Tienda configurada con tema de Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Creación del teaser de productos {#author-product-teaser}

Ampliaremos el componente teaser de producto a través de este tutorial. Como primer paso, agregaremos una nueva instancia del teaser de productos a la Página de inicio para comprender la funcionalidad básica.

1. Navegue hasta la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Inserte un nuevo componente **de teaser** de producto en el contenedor de diseño principal de la página.

   ![Insertar teaser de productos](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Expanda el panel lateral (si no está activado) y cambie el menú desplegable del buscador de recursos a **Productos**. Esto debería mostrar una lista de los productos disponibles de una instancia de Magento conectada. Seleccione un producto y **arrástrelo y suéltelo** en el componente **Product Teaser** de la página.

   ![Arrastrar y soltar teaser de producto](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Tenga en cuenta que también puede configurar el producto mostrado configurando el componente mediante el cuadro de diálogo (haciendo clic en el icono de *llave inglesa* ).

1. Ahora debería ver un producto que está mostrando el teaser de productos. El nombre del producto y el precio del producto son atributos predeterminados que se muestran.

   ![Teaser de productos: estilo predeterminado](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalización del marcado del teaser de productos {#customize-markup-product-teaser}

Una extensión común de AEM componentes es modificar el marcado generado por el componente. Esto se realiza anulando la secuencia de comandos [](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) HTL que utiliza el componente para representar su marcado. HTML Template Language (HTL) es un lenguaje de plantilla ligero que AEM los componentes utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite reutilizar los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En nuestro caso, queremos mostrar un letrero encima del teaser para indicar que el producto es &quot;Nuevo&quot; y que se ha agregado recientemente al catálogo. El patrón de diseño para [personalizar el marcado](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de un componente es en realidad estándar para todos los componentes AEM, no solo para los componentes principales de CIF AEM.

Utilice el IDE de su elección para [abrir el proyecto de inicio descargado](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) al principio del tutorial.

1. Navegue y expanda el módulo **ui.apps** y expanda la jerarquía de carpetas a: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e inspeccione el `.content.xml` archivo.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Arriba se encuentra la definición de componentes para el componente teaser de productos en nuestro proyecto. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este es un ejemplo de creación de un componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)Proxy. En lugar de copiar y pegar todas las secuencias de comandos HTL de teaser de productos de los componentes principales de CIF de AEM, podemos usar `sling:resourceSuperType` para heredar toda la funcionalidad.

1. Abra un navegador nuevo y vaya a [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) en AEM. Expanda el árbol para vista del `productteaser` componente en: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`::

   ![Teaser de producto CRXDE Lite](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Es la definición completa del componente para el componente teaser de producto.

1. Vuelva a su IDE y al proyecto de Acme Store. Cree un nuevo archivo con el nombre `productteaser.html` debajo de `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copie el contenido de `productteaser.html` CRXDE- [Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) y péguelo en el proyecto Acme-Store en el `productteaser.html` archivo recién creado.

   ![Sobrescritura HTML de teaser de productos](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. En el proyecto Acme-Store, modifique el `productteaser.html` archivo e inserte un nuevo div que represente un distintivo sobre el marcado de imagen del producto:

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

1. Implemente el código actualizado en la instancia local de AEM con sus habilidades o con [las características de su IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. En el navegador, vuelva a la [página principal de la tienda](http://localhost:4502/editor.html/content/acme/us/en.html) en AEM. Actualice y verá que aparece un letrero &quot;nuevo&quot; en la esquina superior derecha del componente.

   ![Nueva pancarta extendida](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   Actualmente no hay ninguna lógica detrás de cuándo se mostrará la pancarta. En los próximos ejercicios corregiremos eso.

   > Tenga en cuenta que el CSS para procesar la pancarta se proporcionó como parte del proyecto de inicio y se puede encontrar en: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Para obtener más información, consulte el tutorial [Estilo de los componentes principales de CIF](style-cif-component.md).

## Personalización del cuadro de diálogo del teaser de productos {#customize-dialog-product-teaser}

A continuación, personalizaremos el cuadro de diálogo del componente Product Teaser para permitir que un Autor determine el intervalo de fechas para el cual un producto se considera &quot;nuevo&quot; y si se debe mostrar la pancarta. Para ello, [personalizaremos el cuadro de diálogo](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) de Product Teaser como parte del proyecto Acme Store.

1. Abra el proyecto de la tienda Acme en el IDE que desee y vaya a `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Debajo de la `productteaser` carpeta, agregue una nueva carpeta denominada `_cq_dialog`. Añada un nuevo archivo a la `_cq_dialog` carpeta denominada `.content.xml`. Ahora debe tener la siguiente estructura de archivos:

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

   Arriba hemos agregado 2 campos adicionales como parte de una nueva ficha y un único campo oculto.

   1. Casilla de verificación para mostrar el distintivo &#39;Nuevo&#39;
   2. Campo de número para definir la edad máxima del producto
   3. Campo oculto para asegurarse de que la edad máxima del producto se guarda como una longitud (consulte [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) para obtener más información)

   Los cuadros de diálogo definidos como parte de un componente proxy heredan todos los campos de diálogo existentes con una función conocida como Fusión [de recursos](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)Sling. Por lo tanto, no es necesario redefinir los campos existentes que forman parte del teaser de productos.

1. Actualice `productteaser.html` y agregue un `data-sly-test` al `<div>` para el distintivo. Será una prueba sencilla para decidir procesar el distintivo si el usuario ha marcado &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Implemente el código actualizado en la instancia local de AEM mediante las funciones de su IDE o con sus habilidades principales:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Vuelva al componente Product Teaser y haga clic en el icono de la *llave inglesa* para abrir el cuadro de diálogo. Ahora debería ver una ficha para el **distintivo** con dos campos adicionales. Al actualizar estos campos, los valores se mantendrán en AEM. Debe poder activar o desactivar el distintivo con la casilla de verificación:

   ![Alternar distintivo](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Esto le da al autor cierto control sobre cuándo aparece el distintivo. Sin embargo, sería ideal que la insignia desapareciera automáticamente una vez que el producto haya alcanzado una cierta edad en el día según la entrada de la edad **** máxima del producto. Para ello, tendremos que implementar una lógica de backend.

## Actualización del modelo Sling para el teaser de producto {#updating-sling-model-product-teaser}

A continuación, ampliaremos la lógica empresarial del teaser de productos implementando un modelo Sling. [Los modelos](https://sling.apache.org/documentation/bundles/models.html)de Sling son &quot;POJO&quot; (objetos Java antiguos comunes) impulsados por anotaciones que implementan cualquier lógica comercial necesaria para el componente. Los modelos Sling se utilizan junto con las secuencias de comandos HTL como parte del componente. Seguiremos el patrón de [delegación de modelos](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling para que podamos extender partes del modelo existente de teaser de producto.

Los modelos Sling se implementan como Java y se pueden encontrar en el módulo **principal** del proyecto generado.

1. Abra el proyecto de Acme Store en el IDE que desee y navegue bajo el módulo **principal** para: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** es una interfaz de Java que hemos creado previamente y que amplía la interfaz CIF **ProductTeaser** .

1. A continuación, abra el archivo **MyProductTeaserImpl.java** ubicado en: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` es la clase de implementación para la interfaz `MyProductTeaser`.

   Utilizando el patrón de [delegación para modelos](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling, podemos hacer referencia a la `ProductTeaser` clase mediante la `sling:resourceSuperType` propiedad:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos los métodos que no queremos anular o cambiar, simplemente podemos devolver el valor que devuelve el `ProductTeaser` :

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. Uno de los puntos de extensión adicionales que proporciona AEM componentes principales de CIF es el `AbstractProductRetriever` que nos permite tener acceso a atributos de producto específicos. Añada el siguiente método para inicializar el `AbstractProductRetriever` en el `init()` método:

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

1. Pruebe estos cambios modificando el precio con formato y anulando la lógica en `getFormattedPrice()`. Realice las siguientes actualizaciones para dar formato explícito al precio en función de la configuración regional alemana. (¡o elegir otro país!)

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

   Observe cómo el `productRetriever` objeto nos da acceso al `ProductInterface` objeto mediante el `fetchProduct()` método . Puede ver todos los métodos [disponibles aquí](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Nota* modificar la configuración regional a alemán es solo un ejemplo divertido para ver la anulación. En realidad, ProductTeaser utiliza la configuración regional de la [página para determinar el formato](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. A continuación, debemos actualizar **productEaser.html** en el módulo **ui.apps** para hacer referencia a nuestro nuevo modelo Sling en: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
       ...
   ```

   Guarde los cambios en `productteaser.html`.

1. Implemente el código base en la instancia local de AEM. Dado que se han realizado cambios en los módulos **ui.apps** y **core** , cree e implemente el proyecto desde la raíz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Abra un explorador y vaya a: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Esta consola muestra todos los modelos Sling registrados en el sistema. Comprobación de Dobles para garantizar que MyTeaserModelImpl se implementó y se asignó correctamente. Debería poder ver algo como:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Por último, navegue hasta el lugar en el que creó el componente Product Teaser y debería ver el precio con el formato de moneda alemán:

   ![Formato de precio actualizado](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementar la lógica isShowBadge {#implement-isshowbadge}

Ahora que hemos tenido la oportunidad de experimentar con la anulación de los métodos del modelo de Sling, vamos a implementar la lógica de cuándo mostrar la insignia &quot;nueva&quot;.

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

1. La lógica de cuánto tiempo se mostrará el distintivo &quot;nuevo&quot; se basará en el `created_at` atributo del Producto. Para tener acceso a ese atributo, necesitamos extender la consulta **GraphQL** realizada por ProductTeaser. Podemos hacerlo actualizando el `init()` método en **MyProductTeaserImpl.java**:

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

   Añadir al `extendProductQueryWith` método es una manera eficaz de garantizar que el resto del modelo disponga de atributos de producto adicionales. También minimiza el número de consultas ejecutadas.

   >[!NOTE]
   >En el código anterior utilizamos los`addCustomSimpleField` para recuperar la `created_at` propiedad. Esto ilustra cómo se puede realizar la consulta de cualquier atributo personalizado que forme parte del esquema del Magento.
   >
   > Sin embargo, la `created_at` propiedad se ha implementado realmente como parte de la interfaz [de](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) producto y una mejor práctica sería reutilizar el método como el así: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. A continuación, implementaremos el `isShowBadge()` método:

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

   En el método anterior comprobamos primero si el autor ha habilitado la funcionalidad de distintivo con la casilla de verificación. A continuación, leemos el valor de la propiedad `age` que se establece como parte del cuadro de diálogo y representa el número máximo de días de antigüedad que debe tener un producto hasta que desaparezca el letrero. Finalmente calculamos la antigüedad del producto en base a la `created_at` fecha. Si después de comparar los dos valores regresamos `true` para mostrar el distintivo, `false` en todos los demás casos.

1. Finalmente, se necesita agregar más a la `productteaser.html` secuencia de comandos para llamar al `isShowBadge()` método. Abra el archivo en `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Realice la siguiente actualización:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Implemente el código base en la instancia local de AEM. Dado que se han realizado cambios en los módulos **ui.apps** y **core** , cree e implemente el proyecto desde la raíz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Regrese a AEM y al componente ProductTeaser y experimente con números diferentes para mostrar la edad máxima del producto. Dependiendo de la antigüedad del producto, es posible que deba introducir números muy grandes para que se muestre el distintivo.

   ![Edad máxima del producto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Finalmente, busque los registros de AEM para ver la sentencia de registro ingresada en el paso 5 anterior. Debe imprimir el valor de la `created_at` propiedad que proviene del Magento. Puede vista de los registros de AEM abriendo el `error.log` archivo. Este archivo se encuentra debajo del `crx-quickstart/logs/error.log` lugar donde se ha instalado el tarro de AEM. Puede esperar ver un elemento de línea como el siguiente:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Ahora puede verificar que la lógica que implementamos es correcta.

### Felicitaciones {#congratulations}

¡Acaba de personalizar su primer componente AEM CIF! Descargue el paquete de solución [terminado aquí](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Recursos adicionales {#additional-resources}

* [AEM Arquetipo](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components)
* [Personalización de los componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalización de componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
