---
title: Creación de experiencias de producto
description: Aprenda a crear contenido de producto que luego se pueda utilizar en varios canales para crear una experiencia de compra envolvente.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# Creación de experiencias de producto {#building-experiences}

Obtenga información sobre cómo administrar las experiencias de producto.

## La historia hasta ahora {#story-so-far}

En el documento anterior de Contenido de Adobe Experience Manager AEM () y recorrido de Commerce, [Administrar experiencias del catálogo de productos clasificados](staged-catalog.md), ha aprendido a administrar las experiencias del catálogo de productos clasificados.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo crear contenido y experiencias de productos.

## Administración de experiencias de producto {#management}

AEM La administración de experiencias de producto es la disciplina para decorar datos de productos (que son propiedad de una solución PIM o comercial) con contenido de marketing en el área de la administración de la experiencia del producto (PIM, por sus siglas en inglés) y la administración de experiencias del producto (PIM, por sus siglas en inglés). Estos datos de productos enriquecidos con contenido se pueden utilizar en varios canales para crear una experiencia de compra envolvente.

AEM En la documentación de, puede crear varios tipos de contenido y vincularlos al catálogo de productos. El contenido asociado se puede descubrir y utilizar fácilmente, lo que conlleva una alta productividad.

### Recursos {#assets}

En un nivel superior, hay dos tipos de activos relacionados con los productos: producto y marketing. Los comerciantes administran los recursos del producto y se centran en mostrar el producto (principalmente delante de un fondo neutro). Los recursos se administran en la solución de comercio o en AEM Assets (con una integración de Assets con la solución de comercio/pim).

Los activos de marketing están relacionados con la promoción y el uso del producto propiedad del marketing. Algunos ejemplos son la visualización de varios productos (&quot;comprar el aspecto&quot;), en un contexto específico (&quot;colección de otoño al aire libre&quot;) o pdf explicativos. CIF AEM proporciona una forma sencilla de vincular cualquier recurso de la con un objeto de catálogo de productos.

Abra las propiedades del recurso y cambie a la pestaña **Commerce**. Esta pestaña le permite administrar la asociación con los productos. La tabla debajo del selector proporciona información adicional para los objetos vinculados (solo visible con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina del producto. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![recursos pem](assets/pem-assets.png)

### Fragmentos de experiencias {#experience-fragments}

Los fragmentos de experiencias son una buena manera de crear contenido de producto reutilizable o individual a escala. La asociación funciona de manera similar a un recurso. Abra las propiedades y cambie a la ficha **Commerce**. Esta pestaña le permite administrar la asociación con productos y categorías. Las tablas debajo de los selectores proporcionan información adicional para los objetos vinculados (solo visibles con una selección). Haga clic en el icono de detalles para obtener una vista completa en la cabina del producto. Para asociar un nuevo objeto, haga clic en el icono del selector de productos (icono de carpeta), seleccione un objeto y cierre el selector.

![pem xf](assets/pem-xf.png)

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido son el mejor tipo de contenido para cualquier contenido estructurado. Esto se puede utilizar para aumentar los datos de productos externos con datos de marketing adicionales o para crear contenido sin encabezado. La asociación de un fragmento de contenido con un objeto de catálogo de productos se produce mediante los tipos de referencia de producto o categoría en el Editor del modelo de fragmentos de contenido. Basta con arrastrar y soltar el tipo de referencia correcto en el modelo y configurar el campo. Estos tipos admiten la selección única o múltiple.

![modelo pem cf](assets/pem-cf-model.png)

Si crea un fragmento de contenido basado en este modelo, estos tipos de referencia le proporcionan una manera sencilla de seleccionar el objeto correcto mediante el selector correspondiente.

![pem cf](assets/pem-cf.png)

### Product Cockpit {#product-cockpit}

Se le presentó a la cabina (o consola) de productos en uno de los módulos anteriores. AEM La cabina es una forma sencilla no solo de navegar por el catálogo de productos, sino también de ver todo el contenido asociado en un solo lugar, sin tener que volver a ver el contenido de los productos en un solo lugar. Vaya a la consola del producto y abra las propiedades de un producto que tenga contenido asociado. Cambie a la pestaña correspondiente para ver el contenido asociado.

![cabina pem](assets/pem-cockpit.png)

Al hacer clic en el icono de acción, se abre ese fragmento de contenido en una nueva pestaña del explorador.

## Enriquecimiento de páginas de productos y categorías individuales {#enrich}

En los módulos anteriores, ha aprendido a trabajar con varias plantillas de catálogo de productos. Las plantillas múltiples son una buena manera de crear diferentes plantillas, pero a menudo no son necesarias. A menudo, se puede utilizar la misma plantilla con marcadores de posición para contenido individual. CIF Compatibilidad con marcadores de posición para fragmentos de contenido y fragmentos de experiencias.

Empecemos con el marcador de posición del fragmento de experiencia. AEM Abra una plantilla de producto en el Editor de la. Arrastre y suelte el componente **Fragmento de experiencia de Commerce** en la plantilla y, a continuación, abra el cuadro de diálogo de configuración.

![marcador de posición pem](assets/pem-placeholder.png)

Abra el cuadro de diálogo del componente e introduzca un nombre para este marcador de posición. Se requiere un nombre de marcador de posición que le permita agregar tantos marcadores de posición como necesite.

![cuadro de diálogo de Pem XF](assets/pem-dialog-xf.png)

Abra el fragmento de experiencia que ha asociado a un producto en el paso anterior. Abra las propiedades y cambie a la pestaña comercio. Escriba el mismo nombre de marcador de posición en la **ubicación del marcador de posición del catálogo**.

![pem xf](assets/pem-xf.png)

Ahora arrastre y suelte el componente **Fragmento de contenido de Commerce** en la plantilla y abra el cuadro de diálogo de configuración.

![cuadro de diálogo de Pem CF](assets/pem-dialog-cf.png)

Este cuadro de diálogo vuelve a utilizar el cuadro de diálogo Fragmento de contenido del componente principal. Encontrará más información en recursos adicionales. La única diferencia es la propiedad **Link Element** que configura el campo de identificador (SKU de producto o UID de categoría) en el modelo de fragmento de contenido.

Vista previa ahora de una página de producto que tenga asociados un fragmento de contenido o un fragmento de experiencia. AEM Cuando procesa una página, realiza una búsqueda de cada marcador de posición en función del tipo (Contenido o Fragmento de experiencia), el identificador y el nombre del marcador de posición de los Fragmentos de experiencias. AEM Utiliza un solucionador de URL para obtener el identificador (SKU de productos, UID de categorías). Si se devuelve una experiencia o un fragmento de contenido, se procesará en la ubicación del marcador de posición; de lo contrario, se ignorará el marcador de posición.

![resultado pem](assets/pem-result.png)

## Hacer que el contenido se pueda comprar {#making-shoppable}

AEM También es posible hacer que una página de la lista de compras habitual de la página de la barra de herramientas se pueda comprar añadiendo componentes de comercio. AEM Cree una página de contenido en el editor y abra la página vacía en el editor.

![página vacía pem](assets/pem-page-empty.png)

En primer lugar, arrastre y suelte un componente de detalles del producto en la página. A continuación, cambie a la barra lateral de Assets, cambie a Productos y seleccione un producto. Arrastre y suelte ese producto en el componente de producto. Muestra un componente de producto normal en una página de contenido.

![página de producto pem](assets/pem-page-product.png)

Si ha creado contenido asociado para ese producto, cambie en la barra lateral de Assets a **Contenido asociado de Commerce**. AEM Esta pestaña le muestra todo el contenido de la que estaba asociado a este producto. Esto le permite ahora embellecer rápidamente las páginas con cualquier contenido asociado.

![página enriquecida pem](assets/pem-page-enriched.png)

## ¿Fin del recorrido? {#end-of-journey}

Felicitaciones. AEM ¡Ha completado el recorrido para desarrolladores de contenido y Commerce de! Ahora debería hacer lo siguiente:

* AEM descubra cómo puede asociar cualquier contenido de la a objetos del catálogo de productos
* utilice marcadores de posición para enriquecer individualmente las páginas de productos y categorías
* Obtenga información sobre cómo hacer que el contenido se pueda comprar y utilice la pestaña de contenido asociada

AEM Ya está listo para administrar las experiencias del producto mediante Contenido de la y Commerce. AEM Sin embargo, Contenido de la aplicación y Commerce tienen muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la sección [Recursos adicionales](#additional-resources), donde podrá obtener más información acerca de las características que vio en este recorrido.

## Recursos adicionales {#additional-resources}

* [Creación de experiencias de Commerce](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es)
