---
title: Personalice los componentes principales de CIF
description: Aprenda a personalizar AEM componentes principales de CIF. El tutorial cubre cómo extender de manera segura un CIF Core Componente para cumplir con los requisitos específicos del negocio. Aprenda a extender un consulta GraphQL para devolver un atributo personalizado y mostrar el nuevo atributo en un CIF Core Componente.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 9%

---

# Personalizar AEM componentes principales de CIF {#customize-cif-components}

El [Proyecto](https://github.com/adobe/aem-cif-guides-venia) CIF Venia es una base de código de referencia para el uso de los componentes](https://github.com/adobe/aem-core-cif-components) principales de [CIF. En este tutorial, ampliará aún más el [componente Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) de producto para mostrar un atributo personalizado de Adobe Systems Commerce. También obtenga más información sobre la integración de GraphQL entre AEM y Adobe Systems Commerce y los ganchos de extensión proporcionados por los componentes principales de CIF.

>[!TIP]
>
> Utilice el arquetipo](https://github.com/adobe/aem-project-archetype) de [AEM Project al iniciar su propia implementación comercial.

## Qué generará

El marca Venia recientemente comenzó a fabricar algunos productos utilizando materiales sostenibles y el negocio gustar mostraría una **insignia ecológica** como parte del avance del producto. Se crea un nuevo atributo personalizado en Adobe Systems Commerce para indicar si un producto utiliza el **material ecológico** . Este atributo personalizado se agrega como parte de la consulta de GraphQL y se muestra en el teaser de productos para productos especificados.

![Implementación final de la insignia ecológica](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Requisitos previos {#prerequisites}

Se requiere un entorno de desarrollo local para completar este tutorial. Este entorno incluye un instancia de AEM configurado y conectado a un instancia de Adobe Systems Commerce. Revise los requisitos y pasos para [configurar un desarrollo local con AEM como SDK](../develop.md) de Cloud Service. Para seguir completamente el tutorial, debe permiso agregar atributos a [un producto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) en Adobe Systems comercio.

También necesita el IDE de GraphQL como [GraphiQL](https://github.com/graphql/graphiql) o una extensión explorador para ejecutar los ejemplos de código y tutoriales. Si instala una extensión explorador, asegúrese de que pueda establecer encabezados solicitud. En Google Cromo, _Altair GraphQL Client_ es una extensión que puede hacer el trabajo.

## Clonar el Proyecto Venia {#clone-venia-project}

Clonar el [Proyecto](https://github.com/adobe/aem-cif-guides-venia) Venia y, a continuación, anular los estilos predeterminados.

>[!NOTE]
>
> **Siéntase gratuito usar un proyecto existente (basado en el arquetipo del proyecto** AEM con CIF incluido) y omita esta sección.

1. Ejecute el siguiente comando git para poder clonar el proyecto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Cree e implemente el proyecto en una instancia local de AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. añadir las configuraciones de OSGi necesarias para conectar su AEM instancia a una instancia de Adobe Systems Commerce o agregar las configuraciones al proyecto creado.

1. En este punto, debe tener una versión funcional de una tienda que esté conectada a una instancia de Adobe Systems Commerce. Vaya a la `US` > `Home` Página en: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Hay que ver que la tienda esté usando actualmente el tema de Venia. Al expandir el menú principal del escaparate, debería ver varias categorías, lo que indica que la conexión a Adobe Systems Commerce está funcionando.

   ![Tienda configurada con tema de Venia](../assets/customize-cif-components/venia-store-configured.png)

## Crear el teaser de productos {#author-product-teaser}

El componente teaser de productos se amplía a través de este tutorial. Como primer paso, añada una instancia del teaser de productos a la página de inicio para comprender la funcionalidad de línea de base.

1. Vaya hasta la **Página de inicio** del sitio: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserte un nuevo componente **teaser de productos** en el contenedor del diseño principal de la página.

   ![Inserción del teaser de productos](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expand the Side Panel (if not already toggled) and switch the asset finder drop-down list to **Productos**. Este lista debe mostrar una lista de productos disponibles de un instancia de Adobe Systems Commerce conectado. Seleccione un producto y **arrástrelo y suéltelo** en el componente **teaser de productos** de la página.

   ![Arrastrar y soltar teaser de productos](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Tenga en cuenta que también puede configurar el producto mostrado configurando el componente con el cuadro de diálogo (haga clic en el icono de _llave inglesa_).

4. Ahora debería ver un producto que muestra el teaser de productos. Se muestran el nombre y el precio del producto ya que son atributos predeterminados.

   ![Teaser de productos: estilo predeterminado](../assets/customize-cif-components/product-teaser-default-style.png)

## Añadir un atributo personalizado en Adobe Commerce {#add-custom-attribute}

AEM Los productos y los datos de productos que se muestran en la lista de productos se almacenan en Adobe Commerce. Next add an attribute for **Respetuoso con el medio ambiente** como parte del conjunto de atributos del producto mediante la interfaz de usuario de Adobe Commerce.

>[!TIP]
>
> Ya tiene un personalizado **Sí/No** como parte de su conjunto de atributos del producto? No dude en usarlo y saltarse esta sección.

1. Inicie sesión en su Adobe Systems Commerce instancia.
1. Vaya a **Catálogo** > **productos**.
1. Actualice el filtro búsqueda para que pueda encontrar el Producto **configurable utilizado cuando se añadió al componente Teaser en el** ejercicio anterior. Abra el producto en modo de edición.

   ![Search para el producto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. En la vista del producto, haga clic en **Añadir atributo** > **Crear nuevo atributo**.
1. Rellene el formulario Atributo **Nuevo con los siguientes valores (deje la** configuración predeterminada para otros valores):

   | Conjunto de campos | Etiqueta de campo | Valor |
   | ----------------------------- | ------------------ | ---------------- |
   | Atributo Propiedades | Atributo Etiquetar | **Ecológico** |
   | Atributo Propiedades | Tipo de entrada de catálogo | **Sí/No** |
   | Avanzadas atributo Propiedades | Code atributo | **eco_friendly** |

   ![Nuevo Formulario de atributo](../assets/customize-cif-components/attribute-new-form.png)

   Haga clic en **Guardar atributo** cuando termine.

1. Desplácese hasta la parte inferior del producto y amplíe el **encabezado Atributos** . Deberías ver el nuevo **campo Eco Friendly** . Cambie el interruptor a **Sí**.

   ![Cambiar a sí](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **** Guardar los cambios realizados en el producto.

   >[!TIP]
   >
   > Puede encontrar más detalles sobre la administración [de atributos de producto en el usuario guía de Adobe Systems](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html) Commerce.

1. Vaya a **>** sistema **Herramientas** > **Administración de** caché. Dado que se ha realizado una actualización del esquema de datos, debe invalidar algunos de los tipos de caché de Adobe Systems Commerce.
1. Marque la casilla junto a **Configuración** y envíe el tipo de caché para **Actualizar**

   ![Tipo de caché de configuración de Actualizar](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Puede encontrar más detalles sobre [la administración de caché en el usuario guía de Adobe Systems](https://docs.magento.com/user-guide/system/cache-management.html) Commerce.

## Usar un IDE de GraphQL para verificar el atributo {#use-graphql-ide}

Antes de saltar a AEM código, es útil explorar la descripción general](https://devdocs.magento.com/guides/v2.4/graphql/) de GraphQL utilizando un IDE de [GraphQL. La integración de Adobe Systems Commerce con AEM se realiza principalmente a través de una serie de consultas GraphQL. Comprender y modificar las consultas de GraphQL es una de las formas clave en que se pueden ampliar los componentes principales de CIF.

Siguiente, utilice un IDE de GraphQL para comprobar que el `eco_friendly` atributo se ha añadido al conjunto de atributos del producto. Las capturas de pantalla de este tutorial utilizan la extensión de Cromo de Google Altair _GraphQL Client_ .

1. Abra el IDE de GraphQL e introduzca el URL en la barra de URL `http://<commerce-server>/graphql` de su IDE o extensión.
2. añadir los siguientes [productos consulta](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) dónde `YOUR_SKU` es la **unidad de almacén** del producto utilizado en el ejercicio anterior:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Ejecute el consulta y obtendrá una respuesta gustar lo siguiente:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Ejemplo de respuesta de GraphQL](../assets/customize-cif-components/sample-graphql-query.png)

   El valor de Yes es un número entero de **** 1 **.** Este valor es útil cuando escribe el consulta GraphQL en Java™.

   >[!TIP]
   >
   > Lea documentación más detallada sobre [Adobe Systems Commerce GraphQL aquí](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Actualizar el modelo de Sling para el teaser del producto {#updating-sling-model-product-teaser}

Siguiente, amplíe el lógica empresarial del teaser del producto implementando un modelo Sling. [Los modelos](https://sling.apache.org/documentation/bundles/models.html) Sling son &quot;POJOs&quot; (Plain Old Java™ Objects) impulsados por anotación que implementar lógica empresarial que el componente lo necesita. Los modelos Sling se utilizan con los scripts HTL como parte del componente. Siga las [patrón de delegación para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) so you can extend parts of the existing Product Teaser model.

Los modelos Sling se implementan como Java™ y se pueden encontrar en la **núcleo** módulo del proyecto generado.

Uso [el IDE de su elección](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar el proyecto Venia. Las capturas de pantalla utilizadas son de [IDE de código de Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. En el IDE, vaya a **núcleo** módulo a: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de ubicación principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` es una interfaz Java™ que amplía la interfaz CIF [ProductTeser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) .

   Ya se ha agregado un nuevo método denominado `isShowBadge()` para mostrar un distintivo si el producto se considera &quot;Nuevo&quot;.

1. Añadir `isEcoFriendly()` a la interfaz:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   This new method is introduced to encapsulate the logic to indicate if the product has the `eco_friendly` atributo establecido en **Sí** o **No**.

1. A continuación, inspeccione el `MyProductTeaserImpl.java` en `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   El [patrón de delegación para modelos Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permite `MyProductTeaserImpl` para referencia `ProductTeaser` modelo a través de `sling:resourceSuperType` propiedad:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   For the methods that you do not want to override or change, you can return the value that the `ProductTeaser` devuelve. Por ejemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   This method minimizes the amount of Java™ code that an implementation must write.

1. AEM CIF Uno de los puntos de extensión adicionales que proporcionan los componentes principales de la es el `AbstractProductRetriever` que proporciona acceso a atributos de producto específicos. Inspect el `initModel()` método:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to initialize the productRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   El `@PostConstruct` Esta anotación garantiza que se llame a este método cuando se inicialice el modelo Sling.

   Observe que el producto GraphQL consulta ya se ha ampliado utilizando el método para recuperar el `extendProductQueryWith` atributo adicional `created_at` . Este atributo se utiliza posteriormente como parte del `isShowBadge()` método.

1. Actualice el consulta de GraphQL para incluir el atributo en el `eco_friendly` consulta parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Agregar al `extendProductQueryWith` método es una forma eficaz de garantizar que los atributos adicionales del producto estén disponibles para el resto del modelo. También minimiza el número de consultas ejecutadas.

   En el código anterior, el se utiliza para recuperar el`addCustomSimpleField` `eco_friendly` atributo. This attribute illustrates how you can query for any custom attributes that are part of the Adobe Commerce schema.

   >[!NOTE]
   >
   > El `createdAt()` método se ha implementado como parte de la [interfaz](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) del producto. Se han implementado la mayoría de los atributos de esquema encontrados con frecuencia, por lo que solo debe utilizarse `addCustomSimpleField` para atributos verdaderamente personalizados.

1. añadir un registrador para poder depurar el código Java™:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Siguiente, implementar el `isEcoFriendly()` método:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   En el método anterior, se `productRetriever` usa para recuperar el producto y el método para obtener el `getAsInteger()` valor del `eco_friendly` atributo. Según las consultas de GraphQL que ejecutó anteriormente, sabe que el valor esperado cuando el `eco_friendly` atributo se establece en &quot;Sí&#x200B;**&quot;** es en realidad un número entero de **1**.

   Ahora que se ha actualizado el modelo de Sling, el marcado Componente debe actualizarse para mostrar realmente un indicador de **Eco Friendly** basado en el modelo Sling.

## Personalización del marcado del teaser del producto {#customize-markup-product-teaser}

Una extensión común de los componentes de AEM es modificar el marcado que genera el componente. This editing is done by overriding the [HTL script](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) that the component uses to render its markup. El lenguaje de plantilla de HTML AEM (HTL) es un lenguaje de plantilla ligero que los componentes de la plantilla utilizan para representar dinámicamente el marcado basado en contenido creado, lo que permite reutilizar los componentes. El teaser de productos, por ejemplo, se puede reutilizar una y otra vez para mostrar diferentes productos.

En este caso, desea renderizar un titular sobre el teaser para indicar que el producto es &quot;Respetuoso con el medio ambiente&quot; basado en un atributo personalizado. El patrón de diseño para [personalizar el marcado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) AEM AEM CIF Cada componente es estándar para todos los componentes principales, no solo para los componentes principales de la.

>[!NOTE]
>
> If you customize a component using the CIF product and category pickers, like this Product Teaser or the CIF page component, make sure you include the required `cif.shell.picker` clientlib para los cuadros de diálogo de componentes. Consulte [CIF Uso del selector de productos y categorías de la](use-cif-pickers.md) para obtener más información.

1. En el IDE, desplácese y amplíe la módulo y expanda la `ui.apps` carpeta jerarquía a: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspeccione el `.content.xml` archivo.

   ![Teaser del producto ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   La definición Componente anterior es para el Componente de teaser del producto del proyecto. Observe la propiedad `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este Propiedad es un ejemplo de creación de un [componente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components) Proxy. En lugar de copiar y pegar los scripts HTL del teaser del producto desde los AEM componentes principales de CIF, puede usar el `sling:resourceSuperType` para heredar todos los funcionalidad.

1. Abra el archivo `productteaser.html`. Este archivo es una copia del archivo del teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) del `productteaser.html` [producto CIF.

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Observe que el modelo Sling para `MyProductTeaser` se utiliza y se asigna al `product` variable.

1. Modifique `productteaser.html` para poder llamar al `isEcoFriendly` método implementado en el ejercicio anterior:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Cuando se llama a un método de modelo Sling en HTL, la parte and `is` del método se elimina y la `get` primera letra se escribe en minúscula. Así `isShowBadge()` se convierte y se convierte `.showBadge` `.ecoFriendly`.`isEcoFriendly` En función del valor booleano devuelto por `.isEcoFriendly()` determina si el `<span>Eco Friendly</span>` valor se muestra.

   Puede encontrar más información y `data-sly-test` otras [instrucciones de bloqueo HTL aquí](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. Guardar los cambios y implementar las actualizaciones a AEM utilizando sus habilidades de Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Abra una nueva ventana del explorador y navegue hasta AEM y la **consola** OSGi > **Estado >****modelos** de Sling: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Search y `MyProductTeaserImpl` debería ver una línea gustar lo siguiente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Esta línea indica que el modelo de Sling está correctamente implementado y asignado al componente correcto.

1. Actualizar a la Página Venia **Home en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha añadido el teaser del** producto.

   ![Se muestra un mensaje ecológico](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Si el producto tiene el atributo establecido en Sí&#x200B;**, debería ver el `eco_friendly` texto &quot;Ecológico&quot; en** la Página. Pruebe a otros productos para ver el cambio de comportamiento.

1. Siguiente abra el AEM `error.log` para ver las instrucciones de registro agregadas. El `error.log` está en `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Search los registros de AEM para ver las instrucciones de registro agregadas en el modelo Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > También puede ver algunos seguimientos de pila si el producto utilizado en el teaser no tiene el `eco_friendly` atributo como parte de su conjunto de atributos.

## añadir estilos para el distintivo ecológico {#add-styles}

En este punto, la lógica de cuándo mostrar la **insignia ecológica** está funcionando, sin embargo, el texto sin formato podría usar algunos estilos. Siguiente agregar un icono y estilos al `ui.frontend` módulo para completar el implementación.

1. Descargue el [archivo eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) . Este archivo se utiliza como distintivo **ecológico** .
1. Vuelva al IDE y vaya al `ui.frontend` carpeta.
1. Añada el `eco_friendly.svg` archivo a la `ui.frontend/src/main/resources/images` carpeta:

   ![Se agregó un SVG ecológico](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra el archivo `productteaser.scss` en `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. añadir las siguientes reglas de Sass dentro de la `.productteaser` clase:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > [Consulte Estilos de los componentes](./style-cif-component.md) principales de CIF para obtener más detalles sobre los flujos de trabajo front-end.

1. Guardar los cambios y implementar las actualizaciones a AEM utilizando sus habilidades de Maven, desde un terminal de línea de comandos:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Actualice a la **Página principal de Venia** en [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) donde se ha agregado el teaser de productos.

   ![Implementación final de distintivo ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Felicitaciones {#congratulations}

AEM CIF Ha personalizado su primer componente de la. Descargue la [archivos de solución finalizados aquí](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafío de bonificación {#bonus-challenge}

Revise la funcionalidad de **Nuevo** que ya se ha implementado en el teaser de productos. Intente añadir una casilla de verificación adicional para que los autores controlen cuándo se **Respetuoso con el medio ambiente** debe mostrarse el distintivo. Update the component dialog box at `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuevo desafío de implementación de distintivos](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionales {#additional-resources}

- [Tipo de archivo de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)
- [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalización de los componentes principales del CIF de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/customize-cif-components.html)
- [Personalización de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=es)
- [Introducción a AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)
- [Uso del selector de productos y categoría CIF](use-cif-pickers.md)
