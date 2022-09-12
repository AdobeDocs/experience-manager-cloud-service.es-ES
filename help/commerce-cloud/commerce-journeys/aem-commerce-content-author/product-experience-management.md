---
title: Creación de experiencias de producto
description: Aprenda a crear experiencias de producto.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 4%

---

# Creación de experiencias de producto {#building-experiences}

Obtenga información sobre cómo administrar experiencias de productos.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Contenido y Comercio AEM, [Administrar experiencias de catálogo de productos por etapas](staged-catalog.md), ha aprendido a administrar las experiencias de catálogo de productos organizadas.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo crear contenido y experiencias de producto.

## Administración de experiencia del producto {#management}

La administración de experiencia del producto es la disciplina para decorar los datos del producto (propiedad de una solución de comercio o PIM) con contenido de marketing en AEM. Estos datos de productos enriquecidos con contenido se pueden utilizar en varios canales para crear una experiencia de compra inmersiva.

En AEM, puede crear varios tipos de contenido y vincularlos al catálogo de productos. El contenido asociado se puede descubrir y utilizar fácilmente, lo que produce una alta productividad.

### Assets {#assets}

En un nivel superior, existen dos tipos de activos relacionados con los productos: producto y marketing. Los recursos de productos suelen ser administrados por comerciantes y se centran en mostrar el producto (principalmente frente a un fondo neutro). Los recursos se administran en la solución de comercio o en AEM Assets (con una integración de recursos en la solución de comercio/pim).

Los recursos de marketing están relacionados con la promoción y el uso del producto, que generalmente pertenece al marketing. Algunos ejemplos son la visualización de varios productos (&quot;comprar el aspecto&quot;), en un contexto específico (&quot;colección de visitas en el exterior&quot;) o los pdfs explicativos. CIF proporciona una manera fácil de vincular cualquier recurso AEM con el objeto de catálogo de productos.

Abra las propiedades del recurso y cambie a la **Comercio** pestaña . Esta pestaña le permite administrar la asociación con productos. La tabla debajo del selector proporciona información adicional para los objetos vinculados (solo visible con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina del producto. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![recursos pem](assets/pem-assets.png)

### Fragmentos de experiencias {#experience-fragments}

Los fragmentos de experiencias son una buena forma de crear contenido de productos reutilizable o individual a escala. La asociación funciona de forma similar a un recurso. Abra las propiedades y cambie a la **Comercio** pestaña . Esta pestaña le permite administrar la asociación con productos y categorías. Las tablas debajo de los selectores proporcionan información adicional para los objetos vinculados (solo visible con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina del producto. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![pem xf](assets/pem-xf.png)

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido son el mejor tipo de contenido para cualquier contenido estructurado. Esto se puede utilizar para aumentar los datos de productos externos con datos de marketing adicionales o para crear contenido de forma directa. La asociación de un fragmento de contenido con un objeto de catálogo de productos se produce mediante los tipos de referencia de producto o categoría del Editor del modelo de fragmento de contenido. Basta con arrastrar y soltar el tipo de referencia correcto en el modelo y configurar el campo. Estos tipos admiten selección única o múltiple.

![modelo pem cf](assets/pem-cf-model.png)

Si crea un nuevo fragmento de contenido basado en este modelo, estos tipos de referencia le permitirán seleccionar fácilmente el objeto correcto mediante el selector correspondiente.

![pem cf](assets/pem-cf.png)

### Product Cockpit {#product-cockpit}

Hemos introducido la cabina de producto (o consola) en uno de los módulos anteriores. La cabina es una manera fácil de examinar no solo el catálogo de productos, sino también de ver todo el contenido de AEM asociado en un solo lugar. Vaya a la consola del producto y abra las propiedades de un producto que tenga contenido asociado. Cambie a la pestaña correspondiente para ver el contenido asociado.

![cresta de pem](assets/pem-cockpit.png)

Al hacer clic en el icono de acción, se abrirá esa parte de contenido en una nueva pestaña del navegador.

## Enriquecimiento de páginas de productos y categorías individuales {#enrich}

En los módulos anteriores ha aprendido a trabajar con varias plantillas de catálogo de productos. Varias plantillas son una buena forma de crear diferentes plantillas, pero no son necesarias en muchos casos. En muchos casos, la misma plantilla se puede utilizar en combinación con marcadores de posición para contenido individual. CIF admite marcadores de posición para fragmentos de contenido y fragmentos de experiencias.

Empecemos con el marcador de posición Fragmento de experiencia . Abra una plantilla de producto en el editor de AEM. Arrastre y suelte la **Fragmento de experiencia comercial** en la plantilla y, a continuación, abra el cuadro de diálogo de configuración.

![pem placeholder](assets/pem-placeholder.png)

Abra el cuadro de diálogo del componente e introduzca un nombre para este marcador de posición. El nombre del marcador de posición es obligatorio y le permite agregar tantos marcadores de posición como necesite.

![diálogo pem XF](assets/pem-dialog-xf.png)

Abra el fragmento de experiencia que haya asociado a un producto en el paso anterior. Abra las propiedades y cambie a la pestaña comercio . Introduzca el mismo nombre de marcador de posición en **Ubicación del marcador de posición del catálogo**.

![pem xf](assets/pem-xf.png)

A continuación, arrastre y suelte el **Fragmento de contenido de comercio** en la plantilla y abra el cuadro de diálogo de configuración.

![cuadro de diálogo pem CF](assets/pem-dialog-cf.png)

Este cuadro de diálogo está reutilizando el cuadro de diálogo Fragmento de contenido de componente principal . Encontrará más información en recursos adicionales. La única diferencia es que **Elemento Vínculo** propiedad que configura el campo identificador (SKU de producto o UID de categoría) en el modelo de fragmento de contenido.

La vista previa ahora es una página de producto que tiene asociada un fragmento de contenido y/o un fragmento de experiencia. Cuando AEM procesa una página, realiza una búsqueda para cada marcador de posición en función del tipo (contenido o fragmento de experiencia), identificador y nombre de marcador de posición para fragmentos de experiencias. AEM utiliza una resolución de URL para obtener el identificador (SKU para productos, UID para categorías). Si se devuelve una experiencia o un fragmento de contenido, se procesa en la ubicación del marcador de posición; de lo contrario, se ignora el marcador de posición.

![resultado de pem](assets/pem-result.png)

## Hacer que el contenido sea comercializable {#making-shoppable}

También es posible crear una página de AEM normal de ventas añadiendo componentes de comercio. Cree una nueva página de contenido en AEM y abra la página vacía en el editor.

![pem empty page](assets/pem-page-empty.png)

En primer lugar, arrastre y suelte un componente de detalles del producto en la página. A continuación, cambie a la barra lateral de Assets, cambie a productos y seleccione un producto. Arrastre y suelte el producto en el componente del producto. Se mostrará un componente de producto normal en una página de contenido.

![página de producto de pem](assets/pem-page-product.png)

Si ha creado contenido asociado para ese producto, cambie en la barra lateral de Assets a **Contenido de comercio asociado**. Esta ficha muestra todo AEM contenido asociado a este producto. Esto le permite ahora incrustar rápidamente las páginas con cualquier contenido asociado.

![página enriquecida por pem](assets/pem-page-enriched.png)

## ¿Fin del recorrido? {#end-of-journey}

¡Felicitaciones! ¡Ha completado el recorrido para desarrolladores de contenido y comercio de AEM! Ahora debería hacer lo siguiente:

* comprender cómo se puede asociar cualquier contenido de AEM a los objetos del catálogo de productos
* utilice marcadores de posición para enriquecer individualmente las páginas de productos y categorías
* sepa cómo hacer que el contenido se pueda comprar y utilizar la pestaña de contenido asociada

Ya está listo para administrar experiencias de producto mediante AEM Contenido y comercio. Sin embargo, AEM Contenido y Comercio tienen muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la sección [Recursos adicionales](#additional-resources) para obtener más información acerca de las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Creación de experiencias comerciales](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
