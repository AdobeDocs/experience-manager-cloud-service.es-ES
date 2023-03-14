---
title: Diseño interactivo
description: Con un diseño interactivo, las mismas experiencias se pueden mostrar de forma eficaz en varios dispositivos y en varias orientaciones
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Diseño interactivo {#responsive-design}

Diseñe sus experiencias para que se adapten a la ventanilla del cliente en la que se muestran. Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos en ambas orientaciones. La siguiente imagen muestra algunas formas en que una página puede responder a los cambios en el tamaño de la ventanilla móvil:

* Diseño: utilice diseños de una sola columna para las ventanillas más pequeñas y diseños de varias columnas para las ventanillas más grandes.
* Tamaño de texto: utilice un tamaño de texto más grande (cuando corresponda, como encabezados) en las ventanillas móviles más grandes.
* Contenido: incluya solo el contenido más importante al mostrarlo en dispositivos más pequeños.
* Navegación: se proporcionan herramientas específicas del dispositivo para acceder a otras páginas.
* Imágenes: se muestran las representaciones de imágenes apropiadas para la ventanilla del cliente según las dimensiones de la ventana.

![Ejemplos de diseño interactivo](assets/responsive-example.png)

Desarrolle aplicaciones de Adobe Experience Manager AEM () que generen HTML5, que se adapta a múltiples tamaños y orientaciones de ventana. Por ejemplo, los siguientes intervalos de anchuras de ventanilla móvil se corresponden con varios tipos de dispositivos y orientaciones

* Anchura máxima de 480 píxeles (teléfono, vertical)
* Anchura máxima de 767 píxeles (teléfono, horizontal)
* Anchura entre 768 píxeles y 979 píxeles (tableta, vertical)
* Anchura entre 980 píxeles y 1199 píxeles (tableta, horizontal)
* Anchura de 1200 px o bueno (escritorio)

Consulte los siguientes temas para obtener información sobre la implementación del comportamiento de diseño interactivo:

* [Consultas de medios](#using-media-queries)
* [Rejillas fluidas](#developing-a-fluid-grid)
* [Imágenes adaptables](#using-adaptive-images)

A medida que diseñe, utilice el **Emulador** para obtener una vista previa de las páginas para varios tamaños de pantalla.

## Antes de desarrollar {#before-you-develop}

AEM Antes de desarrollar la aplicación que admite sus páginas web, se deben tomar varias decisiones de diseño. Por ejemplo, necesita tener la siguiente información:

* Los dispositivos a los que está dirigiendo
* Tamaños de las ventanillas móviles de destino
* Diseños de página para cada uno de los tamaños de ventanilla móvil de destino

### Estructura de aplicación {#application-structure}

AEM La estructura típica de la aplicación de la es compatible con todas las implementaciones de diseño adaptables:

* Los componentes de página se encuentran debajo `/apps/<application_name>/components`
* Las plantillas se encuentran debajo `/apps/<application_name>/templates`

## Uso de consultas de medios {#using-media-queries}

Las consultas de medios permiten el uso selectivo de estilos CSS para el procesamiento de páginas. AEM Las herramientas y características de desarrollo de la le permiten implementar de forma eficaz y eficiente las consultas de medios en sus aplicaciones.

El grupo W3C proporciona el [Consultas de medios](https://www.w3.org/TR/css3-mediaqueries/) recomendación que describe esta función de CSS3 y la sintaxis.

### Creación del archivo CSS {#creating-the-css-file}

En el archivo CSS, defina consultas de medios basadas en las propiedades de los dispositivos a los que está dirigiendo. La siguiente estrategia de implementación es eficaz para administrar estilos para cada consulta de medios:

* Utilice un [Carpeta de biblioteca de cliente](clientlibs.md) para definir el CSS que se monta cuando se procesa la página.
* Defina cada consulta de medios y los estilos asociados en archivos CSS independientes. Es útil utilizar nombres de archivo que representen las características del dispositivo de la consulta de medios.
* Defina estilos que sean comunes a todos los dispositivos en un archivo CSS independiente.
* En el archivo css.txt de la carpeta Biblioteca de cliente, ordene los archivos CSS de lista como se requiere en el archivo CSS ensamblado.

El [Tutorial de WKND](develop-wknd-tutorial.md) utiliza esta estrategia para definir estilos en el diseño del sitio. El archivo CSS utilizado por WKND se encuentra en `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
