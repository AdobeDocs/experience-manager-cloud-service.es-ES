---
title: Diseño interactivo
description: Con un diseño interactivo, las mismas experiencias se pueden mostrar de forma eficaz en varios dispositivos en varias orientaciones
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Diseño interactivo {#responsive-design}

Diseñe sus experiencias para que se adapten a la ventanilla del cliente en la que se muestran. Con un diseño interactivo, las mismas páginas se pueden mostrar de forma eficaz en varios dispositivos en ambas orientaciones. La siguiente imagen muestra algunas maneras en que una página puede responder a los cambios en el tamaño de la ventanilla móvil:

* Diseño: Utilice diseños de una sola columna para ventanillas más pequeñas y diseños de varias columnas para ventanillas más grandes.
* Tamaño del texto: Utilice un tamaño de texto mayor (cuando corresponda, como encabezados) en ventanillas más grandes.
* Contenido: Incluya solo el contenido más importante cuando se muestre en dispositivos más pequeños.
* Navegación: Se proporcionan herramientas específicas del dispositivo para acceder a otras páginas.
* Imágenes: Proporcionar representaciones de imagen adecuadas para la ventanilla del cliente según las dimensiones de la ventana.

![Ejemplos de diseño interactivo](assets/responsive-example.png)

Desarrolle aplicaciones de Adobe Experience Manager (AEM) que generen HTML5 que se adapte a varios tamaños de ventana y orientaciones. Por ejemplo, los siguientes intervalos de anchura de las ventanillas móviles se corresponden con varios tipos de dispositivos y orientaciones

* Anchura máxima de 480 píxeles (teléfono, vertical)
* Anchura máxima de 767 píxeles (teléfono, horizontal)
* Anchura entre 768 píxeles y 979 píxeles (tableta, vertical)
* Anchura entre 980 píxeles y 1199 píxeles (tableta, horizontal)
* Ancho de 1200 px o bueno (escritorio)

Consulte los siguientes temas para obtener información sobre la implementación del comportamiento de diseño interactivo:

* [Consultas de medios](#using-media-queries)
* [Cubiertas fluidas](#developing-a-fluid-grid)
* [Imágenes adaptables](#using-adaptive-images)

A medida que diseñe, use la variable **Emulador** para obtener una vista previa de las páginas con distintos tamaños de pantalla.

## Antes de desarrollar {#before-you-develop}

Antes de desarrollar la aplicación de AEM que admite las páginas web, se deben tomar varias decisiones de diseño. Por ejemplo, debe tener la siguiente información:

* Los dispositivos a los que está dirigiendo
* Los tamaños de las ventanillas de destino
* Los diseños de página para cada uno de los tamaños de la ventanilla objetivo

### Estructura de la aplicación {#application-structure}

La estructura de aplicación AEM típica admite todas las implementaciones de diseño adaptables:

* Los componentes de página residen debajo `/apps/<application_name>/components`
* Las plantillas residen debajo de `/apps/<application_name>/templates`

## Uso de consultas de medios {#using-media-queries}

Las consultas de medios permiten el uso selectivo de estilos CSS para el procesamiento de páginas. AEM herramientas y funciones de desarrollo le permiten implementar de forma eficaz y eficiente las consultas de medios en sus aplicaciones.

El grupo W3C proporciona la variable [Consultas multimedia](https://www.w3.org/TR/css3-mediaqueries/) recomendación que describe esta función de CSS3 y la sintaxis.

### Creación del archivo CSS {#creating-the-css-file}

En el archivo CSS, defina las consultas de medios en función de las propiedades de los dispositivos a los que esté dirigiendo. La siguiente estrategia de implementación es efectiva para administrar estilos para cada consulta de medios:

* Utilice un [Carpeta Biblioteca de cliente](clientlibs.md) para definir el CSS que se monta cuando se procesa la página.
* Defina cada consulta de medios y los estilos asociados en archivos CSS independientes. Es útil utilizar nombres de archivo que representen las características del dispositivo de la consulta de medios.
* Defina estilos comunes a todos los dispositivos en un archivo CSS independiente.
* En el archivo css.txt de la carpeta Biblioteca de cliente, ordene los archivos CSS de lista como se requiere en el archivo CSS ensamblado.

La variable [Tutorial de WKND](develop-wknd-tutorial.md) utiliza esta estrategia para definir estilos en el diseño del sitio. El archivo CSS utilizado por WKND se encuentra en `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
