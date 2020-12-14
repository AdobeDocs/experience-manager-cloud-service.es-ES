---
title: Diseño adaptable
description: Con el diseño interactivo, las mismas experiencias se pueden mostrar eficazmente en varios dispositivos en varias orientaciones
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Diseño interactivo {#responsive-design}

Diseñe las experiencias para que se adapten a la ventanilla del cliente en la que se muestran. Con el diseño interactivo, las mismas páginas se pueden mostrar eficazmente en varios dispositivos en ambas orientaciones. La siguiente imagen muestra algunas formas en que una página puede responder a los cambios en el tamaño de la ventanilla:

* Diseño: Utilice diseños de una sola columna para ventanillas móviles más pequeñas y diseños de varias columnas para ventanillas móviles más grandes.
* Tamaño del texto: Utilice un tamaño de texto mayor (cuando sea necesario, como encabezados) en ventanillas móviles más grandes.
* Contenido: Incluya solo el contenido más importante cuando se muestre en dispositivos más pequeños.
* Navegación: Las herramientas específicas del dispositivo se proporcionan para acceder a otras páginas.
* Imágenes: Representaciones de imágenes adecuadas para la ventanilla del cliente según las dimensiones de la ventana.

![Ejemplos de diseño interactivo](assets/responsive-example.png)

Desarrolle aplicaciones de Adobe Experience Manager (AEM) que generen HTML5 que se adapte a varios tamaños de ventana y orientaciones. Por ejemplo, los siguientes rangos de anchuras de ventanilla se corresponden con varios tipos de dispositivos y orientaciones

* Ancho máximo de 480 píxeles (teléfono, vertical)
* Ancho máximo de 767 píxeles (teléfono, horizontal)
* Anchura entre 768 píxeles y 979 píxeles (tableta, vertical)
* Anchura entre 980 y 1199 píxeles (tableta, horizontal)
* Ancho de 1200 px o bueno (escritorio)

Consulte los siguientes temas para obtener información sobre la implementación del comportamiento de diseño interactivo:

* [Consultas de medios](#using-media-queries)
* [Cuadrículas fluidas](#developing-a-fluid-grid)
* [Imágenes adaptables](#using-adaptive-images)

A medida que diseña, utilice la barra de herramientas **Emulador** para previsualización de las páginas para distintos tamaños de pantalla.

## Antes de desarrollar {#before-you-develop}

Antes de desarrollar la aplicación de AEM que admite las páginas web, se deben tomar varias decisiones de diseño. Por ejemplo, necesita tener la siguiente información:

* Los dispositivos que va a segmentar
* Tamaños de la ventanilla de destinatario
* Los diseños de página para cada uno de los tamaños de ventanilla de destino

### Estructura de la aplicación {#application-structure}

La estructura típica de la aplicación AEM admite todas las implementaciones de diseño adaptables:

* Los componentes de página residen debajo de `/apps/<application_name>/components`
* Las plantillas residen debajo de `/apps/<application_name>/templates`

## Uso de Consultas de medios {#using-media-queries}

Las consultas de medios permiten el uso selectivo de estilos CSS para la representación de páginas. AEM herramientas y funciones de desarrollo le permiten implementar de forma eficaz y eficiente consultas de medios en sus aplicaciones.

El grupo W3C proporciona la recomendación [Consultas de medios](https://www.w3.org/TR/css3-mediaqueries/) que describe esta función de CSS3 y la sintaxis.

### Creación del archivo CSS {#creating-the-css-file}

En el archivo CSS, defina consultas de medios en función de las propiedades de los dispositivos que vaya a utilizar. La siguiente estrategia de implementación es eficaz para administrar estilos en cada consulta de medios:

* Utilice una [carpeta Biblioteca de clientes](clientlibs.md) para definir la CSS que se ensamblará cuando se procese la página.
* Defina cada consulta de medios y los estilos asociados en archivos CSS independientes. Es útil utilizar nombres de archivo que representen las características del dispositivo de la consulta de medios.
* Defina estilos comunes a todos los dispositivos en un archivo CSS independiente.
* En el archivo css.txt de la carpeta Biblioteca de clientes, ordene los archivos CSS de lista como se requiere en el archivo CSS ensamblado.

El [tutorial de WKND](develop-wknd-tutorial.md) utiliza esta estrategia para definir estilos en el diseño del sitio. El archivo CSS utilizado por WKND se encuentra en `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
