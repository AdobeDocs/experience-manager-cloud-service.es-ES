---
title: Creación de experiencias de producto
description: Aprenda a crear experiencias de producto.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 4%

---

# Creación de experiencias de producto {#building-experiences}

Obtenga información sobre cómo administrar las experiencias de producto.

## La historia hasta ahora {#story-so-far}

AEM En el documento anterior del recorrido de Contenido y Comercio de la, [Administrar experiencias del catálogo de productos clasificados](staged-catalog.md), ha aprendido a administrar las experiencias del catálogo de productos clasificados.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo crear contenido y experiencias de productos.

## Administración de experiencias de producto {#management}

AEM La administración de experiencias de producto es la disciplina para decorar datos de productos (que son propiedad de una solución PIM o comercial) con contenido de marketing en el área de la administración de la experiencia del producto (PIM, por sus siglas en inglés) y la administración de experiencias del producto (PIM, por sus siglas en inglés). Estos datos de productos enriquecidos con contenido se pueden utilizar en varios canales para crear una experiencia de compra envolvente.

AEM En la documentación de, puede crear varios tipos de contenido y vincularlos al catálogo de productos. El contenido asociado se puede descubrir y utilizar fácilmente, lo que conlleva una alta productividad.

### Assets {#assets}

En un nivel superior, hay dos tipos de activos relacionados con los productos: producto y marketing. Los recursos del producto generalmente los administran los comerciantes y se centran en mostrar el producto (principalmente delante de un fondo neutro). Los recursos se administran en la solución de comercio o en AEM Assets (con una integración de recursos a la solución de comercio/pim).

Los activos de marketing están relacionados con la promoción y el uso del producto, que normalmente pertenece al marketing. Algunos ejemplos son la visualización de varios productos (&quot;comprar el aspecto&quot;), en un contexto específico (&quot;colección de otoño al aire libre&quot;) o pdf explicativos. AEM CIF proporciona una manera fácil de vincular cualquier recurso con cualquier objeto del catálogo de productos.

Abra las propiedades del recurso y cambie a **Comercio** pestaña. Esta pestaña le permite administrar la asociación con los productos. La tabla debajo del selector proporciona información adicional para los objetos vinculados (solo visible con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina de productos. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![recursos pem](assets/pem-assets.png)

### Fragmentos de experiencias {#experience-fragments}

Los fragmentos de experiencias son una buena manera de crear contenido de producto reutilizable o individual a escala. La asociación funciona de forma similar a un recurso. Abra las propiedades y cambie a **Comercio** pestaña. Esta pestaña le permite administrar la asociación con productos y categorías. Las tablas debajo de los selectores proporcionan información adicional para los objetos vinculados (solo visibles con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina de productos. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![pem xf](assets/pem-xf.png)

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido son el mejor tipo de contenido para cualquier contenido estructurado. Esto se puede utilizar para aumentar los datos de productos externos con datos de marketing adicionales o para crear contenido sin encabezado. La asociación de un fragmento de contenido con un objeto de catálogo de productos se produce mediante los tipos de referencia de producto o categoría en el Editor del modelo de fragmentos de contenido. Basta con arrastrar y soltar el tipo de referencia correcto en el modelo y configurar el campo. Estos tipos admiten la selección única o múltiple.

![modelo pem cf](assets/pem-cf-model.png)

Si crea un nuevo fragmento de contenido basado en este modelo, estos tipos de referencia le proporcionan una manera sencilla de seleccionar el objeto correcto mediante el selector correspondiente.

![pem cf](assets/pem-cf.png)

### Product Cockpit {#product-cockpit}

Hemos introducido la cabina del producto (o consola) en uno de los módulos anteriores. AEM La cabina es una forma sencilla no solo de navegar por el catálogo de productos, sino también de ver todo el contenido asociado en un solo lugar, sin tener que volver a ver el contenido de los productos en un solo lugar. Vaya a la consola del producto y abra las propiedades de un producto que tenga contenido asociado. Cambie a la pestaña correspondiente para ver el contenido asociado.

![cabina pem](assets/pem-cockpit.png)

Al hacer clic en el icono de acción, se abre ese fragmento de contenido en una nueva pestaña del explorador.

## Enriquecimiento de páginas de productos y categorías individuales {#enrich}

En los módulos anteriores ha aprendido a trabajar con varias plantillas de catálogo de productos. Las plantillas múltiples son una buena manera de crear diferentes plantillas, pero no son necesarias en muchos casos. En muchos casos, se puede utilizar la misma plantilla en combinación con marcadores de posición para contenido individual. CIF admite marcadores de posición para fragmentos de contenido y fragmentos de experiencias.

Empecemos con el marcador de posición del fragmento de experiencia. AEM Abra una plantilla de producto en el editor de. Arrastre y suelte el **Fragmento de experiencia de Commerce** en la plantilla y, a continuación, abra el cuadro de diálogo de configuración.

![marcador de posición pem](assets/pem-placeholder.png)

Abra el cuadro de diálogo del componente e introduzca un nombre para este marcador de posición. El nombre del marcador de posición es obligatorio y le permite agregar tantos marcadores de posición como necesite.

![cuadro de diálogo pem XF](assets/pem-dialog-xf.png)

Abra el fragmento de experiencia que ha asociado a un producto en el paso anterior. Abra las propiedades y cambie a la pestaña comercio. Introduzca el mismo nombre de marcador de posición en **Ubicación del marcador de posición del catálogo**.

![pem xf](assets/pem-xf.png)

Ahora arrastre y suelte el **Fragmento de contenido de Commerce** en la plantilla y abra el cuadro de diálogo de configuración.

![cuadro de diálogo pem CF](assets/pem-dialog-cf.png)

Este cuadro de diálogo reutiliza el cuadro de diálogo Fragmento de contenido del componente principal. Encontrará más información en recursos adicionales. La única diferencia es la **Elemento de vínculo** que configura el campo de identificador (SKU de producto o UID de categoría) en el modelo de fragmento de contenido.

Vista previa ahora de una página de producto que tenga asociados un fragmento de contenido o un fragmento de experiencia. AEM Cuando procesa una página, realizará una búsqueda de cada marcador de posición en función del tipo (Contenido o Fragmento de experiencia), el identificador y el nombre del marcador de posición de los Fragmentos de experiencias. AEM Utiliza un solucionador de URL para obtener el identificador (SKU de productos, UID de categorías). Si se devuelve una experiencia o un fragmento de contenido, se procesará en la ubicación del marcador de posición; de lo contrario, se ignorará el marcador de posición.

![resultado de pem](assets/pem-result.png)

## Hacer que el contenido se pueda comprar {#making-shoppable}

AEM También es posible hacer que una página de la lista de compras habitual de la página de la barra de herramientas se pueda comprar añadiendo componentes de comercio. AEM Cree una nueva página de contenido en el editor y abra la página vacía en el editor.

![página vacía de pem](assets/pem-page-empty.png)

En primer lugar, arrastre y suelte un componente de detalles del producto en la página. A continuación, cambie a la barra lateral Recursos, cambie a productos y seleccione un producto. Arrastre y suelte ese producto en el componente de producto. Esto mostrará un componente de producto normal en una página de contenido.

![página de producto de pem](assets/pem-page-product.png)

Si ha creado contenido asociado para ese producto, cambie en la barra lateral de Recursos a **Contenido de comercio asociado**. AEM Esta pestaña le muestra todo el contenido de la que estaba asociado a este producto. Esto le permite ahora embellecer rápidamente las páginas con cualquier contenido asociado.

![página enriquecida pem](assets/pem-page-enriched.png)

## ¿Fin del recorrido? {#end-of-journey}

¡Enhorabuena! AEM ¡Ha completado el recorrido para desarrolladores de contenido y comercio de! Ahora debería hacer lo siguiente:

* AEM descubra cómo puede asociar cualquier contenido de la a objetos del catálogo de productos
* utilice marcadores de posición para enriquecer individualmente las páginas de productos y categorías
* Obtenga información sobre cómo hacer que el contenido se pueda comprar y utilice la pestaña de contenido asociada

AEM Ya está listo para administrar las experiencias de producto mediante Contenido y comercio de. AEM Sin embargo, Contenido y comercio de la tienen muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la sección [Recursos adicionales](#additional-resources) para obtener más información acerca de las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Creación de experiencias comerciales](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
