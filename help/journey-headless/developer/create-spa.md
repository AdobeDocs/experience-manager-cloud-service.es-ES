---
title: 'SPA Opcional: cómo crear aplicaciones de una sola página () con Adobe Experience Manager AEM ()'
description: En esta continuación opcional del Recorrido para desarrolladores de AEM sin encabezado, aprenderá cómo AEM combina la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con el marco de trabajo del editor SPA de AEM.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 48%

---

# Creación de aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional de la [AEM Recorrido de desarrollador sin encabezado](overview.md)AEM , aprenderá a combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa. SPA AEM SPA SPA También aprenderá a crear plantillas editables utilizando el marco de trabajo de Editor de e integrar las funcionalidades externas de edición, lo que le permitirá crear las versiones editables que necesite con el editor de segmentos de trabajo de la plataforma de trabajo de la plataforma de trabajo de la.

## La historia hasta ahora {#story-so-far}

En este punto, debería haber completado todo el [Recorrido para desarrolladores de AEM sin encabezado](overview.md) y comprender los conceptos básicos de la entrega de contenido sin encabezado en AEM, incluido lo siguiente:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* Las características sin encabezado de AEM.
* Cómo organizar un proyecto sin encabezado en AEM.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto de AEM sin encabezado.

AEM Hasta ahora, se ha puesto en marcha su primer proyecto sin encabezado o ha tenido el conocimiento de que puede hacerlo. Enhorabuena.

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Lo recuerda en el [Primeros pasos](getting-started.md#integration-levels)AEM Además, se discutió cómo no solo admite la entrega sin encabezado y modelos tradicionales de pila completa, sino también modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin encabezado, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

AEM SPA AEM Este artículo se basa en su conocimiento de las aplicaciones sin encabezado de explorando en profundidad cómo puede crear sus propias aplicaciones de una sola página () que se pueden editar en los entornos de trabajo de la interfaz de usuario de la aplicación de la interfaz de usuario de. SPA SPA AEM De este modo, puede crear contenido y enviarlo sin encabezado a un, pero ese contenido sigue siendo editable en el caso de los.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco de trabajo del editor de SPA de AEM. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender la función básica del editor de SPA.
* Conocer los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar las SPA externas en AEM.
* Comprender cómo se puede implementar o no el procesamiento en el lado del servidor.

## Condiciones y requisitos previos {#requirements-prerequisites}

SPA AEM Antes de comenzar a trabajar con los recursos de la, deben cumplirse varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en desarrollo creando SPA con marcos de trabajo React o Angular.
* Conocimientos básicos de AEM para crear fragmentos de contenido y utilizar el editor.
* Asegúrese de revisar el documento [AEM Encabezado y sin encabezado en el](/help/implementing/developing/headful-headless.md) SPA para que pueda comprender los distintos niveles posibles de integración de la.

### Herramientas {#tools}

* Acceso a la zona protegida para probar la implementación de su proyecto.
* Instancia de desarrollo local para modelado y prueba de datos.
* SPA externa existente (opcional, según el modelo de integración elegido).
* Tipo de archivo del proyecto AEM.

## ¿Qué es una SPA? {#what-is-a-spa}

SPA Una aplicación de una sola página () se diferencia de una página convencional en que se procesa en el lado del cliente y se basa principalmente en JavaScript, y depende de llamadas de Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría, o todo, el contenido se recupera una vez en una sola carga de página con recursos adicionales cargados asincrónicamente según sea necesario, en función de la interacción del usuario con la página.

Esta funcionalidad reduce la necesidad de actualizar la página y presenta una experiencia al usuario que se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido de AEM.

## ¿Por qué una SPA? {#why-spa}

SPA Al ser más rápido, fluido y más parecido a una aplicación nativa, una experiencia se convierte en una experiencia atractiva. SPA Es bueno no solo para el visitante de la página web, sino también para los especialistas en marketing y los desarrolladores debido a la naturaleza de cómo funcionan los.

Para obtener una descripción completa de las SPA y por qué las utilizaría, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## Cómo AEM gestiona las SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA AEM Como desarrollador front-end, si sigue estas prácticas recomendadas generales y algunos principios específicos de la, su usuario se vuelve funcional con la creación de contenido y las capacidades de la aplicación para la creación de contenido de la misma.

* **Portabilidad**: al igual que con cualquier componente, los componentes de SPA deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **AEM Estructura del sitio de** AEM : el desarrollador front-end crea componentes y es propietario de su estructura interna, pero depende de la definición de la estructura de contenido del sitio en la que se basa para definir el contenido.
* **Procesamiento dinámico**: todo el procesamiento debe ser dinámico.
* **Enrutamiento dinámico**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona las SPA, consulte los [recursos adicionales](#additional-resources) para obtener vínculos a más documentación detallada.

## El editor de SPA de AEM {#aem-spa-editor}

SPA Los sitios creados con marcos de trabajo comunes, como React y Angular, cargan su contenido mediante JSON dinámicos. No proporcionan la estructura de HTML AEM necesaria para que el editor de páginas de la página de la pueda colocar los controles de edición.

SPA AEM SPA AEM Para habilitar la edición de la dentro de la misma, es necesaria una asignación entre la salida JSON del modelo de contenido y el modelo de contenido en el repositorio de para poder guardar los cambios en el contenido.

SPA AEM SPA La compatibilidad con la aplicación en la introduce una capa delgada de JavaScript que interactúa con el código JavaScript de la aplicación cuando se carga en el Editor de páginas con el que se pueden enviar eventos. La ubicación de los controles de edición se puede activar para permitir la edición en contexto. SPA Esta función se basa en el concepto de extremo de API de servicios de contenido porque el contenido de la debe cargarse mediante servicios de contenido.

Para obtener una descripción completa del editor de SPA de AEM, consulte el apartado [recursos adicionales](#additional-resources) para obtener los vínculos a documentación más detallada.

## Adaptación de las SPA existentes {#existing-spas}

SPA AEM AEM AEM Si tiene un recurso existente, es compatible con la incrustación en el editor de contenido, por lo que es visible para los autores de contenido en el editor de contenido. En el editor de contenido, el editor de contenido se puede insertar en el editor de contenido, en el que se muestra a los usuarios de manera que no se puede acceder a él Esta capacidad puede resultar útil para ver el contenido que están creando mediante fragmentos de contenido en el contexto de la aplicación final en la que se consume.

SPA AEM Además, con solo pequeños cambios, puede habilitar cierta capacidad de edición en el editor de externo en el propio editor de contenido.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer que una SPA externa se pueda editar en AEM, consulte la sección [recursos adicionales](#additional-resources) para obtener vínculos a documentación más detallada.

## Siguientes pasos {#what-is-next}

Para comenzar a desarrollar su propia SPA para AEM, revise los siguientes documentos:

* [Tutorial WKND de SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Introducción a React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Introducción a Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

SPA AEM Si debe adaptar un documento existente para utilizarlo en la, revise los siguientes documentos:

* [El componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Consulte los [recursos adicionales](#additional-resources) para profundizar en los temas de las SPA en AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Con encabezado y sin encabezado en AEM](/help/implementing/developing/headful-headless.md): una descripción de los diferentes modelos de entrega disponibles en AEM.
* [SPA Introducción y tutorial de](/help/implementing/developing/hybrid/introduction.md) SPA AEM - Una buena introducción a la.
* [Desarrollo de las SPA para AEM](/help/implementing/developing/hybrid/developing.md): directrices sobre cómo desarrollar las SPA para AEM
* [Información general del editor de SPA](/help/implementing/developing/hybrid/editor-overview.md): detalles del funcionamiento del editor de SPA.
* [Procesamiento del lado del servidor](/help/implementing/developing/hybrid/ssr.md) AEM SPA - Cómo configurar SSR para la de la
* [SPA Documentos de referencia](/help/implementing/developing/hybrid/reference-materials.md) AEM SPA - Referencias de la API de JavaScript y vínculos a proyectos de código abierto de GitHub de
* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md): cómo crear fragmentos de contenido
* [Arquetipo del proyecto de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es): plantilla de Maven que crea un proyecto mínimo, basado en las prácticas recomendadas de Adobe Experience Manager (AEM) como punto de partida para su sitio web
