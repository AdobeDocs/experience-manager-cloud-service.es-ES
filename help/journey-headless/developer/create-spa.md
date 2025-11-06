---
title: 'Opcional: creación de aplicaciones de una sola página (SPA) con Adobe Experience Manager (AEM)'
description: En esta continuación opcional del Recorrido para desarrolladores de AEM sin encabezado, aprenderá cómo AEM combina la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con el marco de trabajo del editor SPA de AEM.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 100%

---

# Creación de aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional del [ Recorrido para desarrolladores de AEM sin encabezado](overview.md), aprenda cómo AEM puede combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa. También aprenderá a crear plantillas editables utilizando el marco de trabajo del editor de SPA de AEM e integrar las funcionalidades externas, lo que le permitirá editar las funciones editables que necesite. 

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [Recorrido para desarrolladores de AEM sin encabezado](overview.md) y comprender los conceptos básicos de la entrega de contenido sin encabezado en AEM, incluido lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.

Hasta ahora, ha puesto en marcha su primer proyecto sin encabezado de AEM o tiene los conocimientos necesarios para hacerlo. Enhorabuena.

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que recuerde que en la [Introducción](getting-started.md#integration-levels) hemos examinado brevemente cómo AEM no solo admite entregas sin encabezado y modelos de pila completos tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin encabezado, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

Este artículo se basa en sus conocimientos de AEM sin encabezado para explorar en profundidad cómo puede crear sus propias aplicaciones de una sola página (SPA) que se pueden editar en AEM. De este modo puede crear contenido y enviarlo sin encabezado a una SPA, pero dicha SPA sigue siendo editable en AEM.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco de trabajo del editor de SPA de AEM. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender la función básica del editor de SPA.
* Conocer los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar las SPA externas en AEM.
* Comprender cómo se puede implementar o no el procesamiento en el lado del servidor.

## Condiciones y requisitos previos {#requirements-prerequisites}

Antes de empezar a trabajar con las SPA en AEM hay varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.
* Asegúrese de revisar el documento [Con encabezado y sin encabezado en AEM](/help/implementing/developing/headful-headless.md) para comprender los distintos niveles de integración de SPA posibles.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente (opcional, según el modelo de integración elegido).
* Tipo de archivo del proyecto AEM.

## ¿Qué es una SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas AJAX para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una carga de una sola página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esta funcionalidad reduce la necesidad de actualizaciones de la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido de AEM.

## ¿Por qué una SPA? {#why-spa}

Una experiencia se convierte en una experiencia atractiva, al ser más rápida, fluida y más parecida a una aplicación nativa. No solo es bueno para el visitante de la página web, sino también para los especialistas en marketing y los desarrolladores debido a la naturaleza de cómo funcionan las SPA.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona las SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. Si como desarrollador front-end sigue estas prácticas recomendadas generales y algunos principios específicos de AEM, su SPA se vuelve funcional con AEM y su funcionalidad de creación de contenido.

* **Portabilidad**: al igual que con cualquier componente, los componentes de SPA deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **AEM impulsa la estructura del sitio**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **Procesamiento dinámico**: todo el procesamiento debe ser dinámico.
* **Enrutamiento dinámico**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona las SPA, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## El editor de SPA de AEM {#aem-spa-editor}

Los sitios creados con marcos de SPA comunes, como React y Angular, cargan su contenido mediante JSON dinámicos. No proporcionan la estructura de HTML necesaria para que el editor de la página de AEM pueda colocar los controles de edición.

Para permitir la edición de las SPA dentro de AEM, se necesita una asignación entre la salida JSON de las SPA y el modelo de contenido en el repositorio AEM para que pueda guardar los cambios en el contenido.

El soporte de las SPA en AEM introduce una capa delgada de JavaScript que interactúa con el código JavaScript de la aplicación cuando se carga en el Editor de página con el que se pueden enviar eventos. La ubicación de los controles de edición se puede activar para permitir la edición en contexto. Esta función se basa en el concepto de punto final de API de Servicios de contenido porque el contenido de las SPA debe cargarse mediante Servicios de contenido.

Para obtener una descripción completa del editor de SPA de AEM, consulte el apartado [recursos adicionales](#additional-resources) para obtener los vínculos a documentación más detallada.

## Adaptación de las SPA existentes {#existing-spas}

Si tiene una SPA existente, AEM permite integrarlo en AEM para que sea visible para los autores de contenido en el editor de AEM. Esta capacidad puede resultar muy útil para ver el contenido que crean mediante los fragmentos de contenido en el contexto de la aplicación final en la que se consume.

Además, con tan solo unos pequeños cambios, puede habilitar una determinada capacidad de edición en la SPA externa dentro del editor de AEM.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer que una SPA externa se pueda editar en AEM, consulte la sección [recursos adicionales](#additional-resources) para obtener vínculos a documentación más detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propia SPA para AEM, revise los siguientes documentos:

* [Tutorial WKND de SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Introducción a React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Introducción a Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Si necesita adaptar una SPA existente para utilizarla en AEM, revise los documentos siguientes:

* [El componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Consulte los [recursos adicionales](#additional-resources) para profundizar en los temas de las SPA en AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Con encabezado y sin encabezado en AEM](/help/implementing/developing/headful-headless.md): una descripción de los diferentes modelos de entrega disponibles en AEM.
* [Introducción y tutorial de SPA](/help/implementing/developing/hybrid/introduction.md): una buena introducción a las SPA en AEM.
* [Desarrollo de las SPA para AEM](/help/implementing/developing/hybrid/developing.md): directrices sobre cómo desarrollar las SPA para AEM
* [Información general del editor de SPA](/help/implementing/developing/hybrid/editor-overview.md): detalles del funcionamiento del editor de SPA.
* [Documentos de referencia de SPA](/help/implementing/developing/hybrid/reference-materials.md): referencias de la API de JavaScript y vínculos a los proyectos de GitHub de SPA en AEM de código abierto
* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments): cómo crear fragmentos de contenido
* [Arquetipo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es): plantilla de Maven que crea un proyecto mínimo, basado en las prácticas recomendadas de Adobe Experience Manager (AEM) como punto de partida para su sitio web
