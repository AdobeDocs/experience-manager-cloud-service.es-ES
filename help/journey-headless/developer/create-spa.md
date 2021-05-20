---
title: 'Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM'
description: En esta continuación opcional del Recorrido para desarrolladores sin encabezado de AEM, aprenderá cómo AEM combinar la entrega sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables con AEM marco de edición de SPA.
source-git-commit: ddd320ae703225584d4a2055d0f882d238d60987
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---


# Cómo crear aplicaciones de una sola página (SPA) con AEM {#create-spa}

En esta continuación opcional del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprenderá cómo AEM combinar el envío sin encabezado con las funciones tradicionales de CMS de pila completa y cómo puede crear SPA editables utilizando AEM marco de edición de SPA, así como integrar SPA externas, habilitando las funciones de edición según sea necesario.

## La historia hasta ahora {#story-so-far}

En este punto, debe haber completado todo el [AEM Recorrido para desarrolladores sin encabezado](overview.md) y comprender los conceptos básicos del envío sin encabezado en AEM, incluida la comprensión de:

* La diferencia entre la entrega de contenido sin encabezado y con encabezado.
* AEM características sin periféricos.
* Organizar y AEM proyecto sin encabezado.
* Cómo crear contenido sin encabezado en AEM.
* Cómo recuperar y actualizar contenido sin encabezado en AEM.
* Cómo poner en marcha un proyecto AEM sin encabezado.

Así que ahora ya sea que usted se ha puesto en marcha con su primer proyecto AEM sin cabeza o tiene todo el conocimiento necesario para hacerlo. Felicitaciones!

Entonces, ¿por qué está leyendo esta continuación adicional y opcional del recorrido? Es probable que recuerde que en [Getting Started](getting-started.md#integration-levels) analizamos brevemente cómo no solo AEM admite envíos sin periféricos y modelos de pila completa tradicionales, sino que también puede admitir modelos híbridos que combinan las ventajas de ambos. Aunque no es el modelo tradicional sin cabeza, estos modelos híbridos pueden ofrecer una flexibilidad sin precedentes a ciertos proyectos.

Este artículo se basa en su conocimiento de AEM sin encabezado al explorar en profundidad cómo puede crear sus propias aplicaciones de una sola página (SPA) que realmente se pueden editar en AEM. De este modo puede crear contenido y enviarlo sin problemas a un SPA, pero ese SPA sigue siendo editable en AEM.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se desarrollan las aplicaciones de una sola página mediante el marco AEM SPA Editor. Después de leer este documento, debe:

* Comprender la función básica del SPA Editor.
* Conozca los requisitos para crear una SPA totalmente editable para AEM.
* Comprender cómo se pueden integrar los SPA externos en AEM.
* Comprenda cómo se debe implementar o no la representación del lado del servidor.

## Requisitos y requisitos previos {#requirements-prerequisites}

Hay varios requisitos antes de comenzar a trabajar con SPA en AEM.

### Conocimiento {#knowledge}

* Experiencia de desarrollo crear SPA con marcos de React o Angular
* Capacidades básicas AEM crear fragmentos de contenido y utilizar el editor
* Asegúrese de revisar el documento [Headful and Headless en AEM](/help/implementing/developing/headful-headless.md) para comprender los distintos niveles de integración SPA posibles.

### Herramientas {#tools}

* Acceso a espacio aislado para probar la implementación de su proyecto
* Instancia de desarrollo local para modelado y prueba de datos
* SPA externa existente (opcional, según el modelo de integración elegido)
* Tipo de archivo del proyecto AEM

## ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El AEM SPA Editor permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

## ¿Por qué un SPA? {#why-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo SPA funciona.

Para obtener una descripción completa de los SPA y por qué los utilizaría, consulte la sección [recursos adicionales](#additional-resources) para ver vínculos a documentación más detallada.

## Cómo AEM gestiona SPA

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador del front-end observa las prácticas recomendadas estándar al crear un SPA. Si como desarrollador de front-end sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con AEM y sus funciones de creación de contenido.

* **Portabilidad** : Al igual que con cualquier componente, los componentes SPA deben crearse para que sean lo más portátiles posible. El SPA debe crearse con componentes transferibles y reutilizables.
* **AEM estructura del sitio** : el desarrollador de front-end crea componentes y posee su estructura interna, pero depende de la AEM para definir la estructura de contenido del sitio.
* **Renderización dinámica** : todas las renderizaciones deben ser dinámicas.
* **Enrutamiento dinámico** : El SPA es responsable del enrutamiento y AEM lo escucha y obtiene en función de él. Cualquier enrutamiento también debe ser dinámico.

Para obtener una descripción completa de cómo AEM gestiona SPA, consulte la sección [recursos adicionales](#additional-resources) para ver vínculos a documentación más detallada.

## El Editor de SPA de AEM {#aem-spa-editor}

Los sitios creados con marcos de SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de SPA dentro de AEM, se necesita una asignación entre la salida JSON del SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

SPA compatibilidad con en AEM introduce una capa de JS fina que interactúa con el código JS de SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y se puede activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de extremo de la API de servicios de contenido, ya que el contenido de la SPA debe cargarse a través de los servicios de contenido.

Para obtener una descripción completa del AEM SPA Editor, consulte la sección [recursos adicionales](#additional-resources) para ver vínculos a documentación más detallada.

## Adaptación de SPA existentes {#existing-spas}

Si tiene un SPA existente, AEM puede incrustarlo en AEM para que sea visible para los autores de contenido en el editor de AEM. Esto puede resultar muy útil para ver el contenido que están creando mediante fragmentos de contenido en el contexto de la aplicación final en la que se consumirá.

Además, con solo cambios pequeños, puede habilitar cierta capacidad de edición en el SPA externo dentro del editor de AEM.

El componente RemotePage permite procesar una SPA externa en AEM.

Para obtener una descripción completa de cómo hacer editable una SPA externa en AEM, consulte la sección [recursos adicionales](#additional-resources) para ver vínculos a más documentación detallada.

## Siguientes {#what-is-next}

Para comenzar a desarrollar su propio SPA para AEM, revise los siguientes documentos:

* [Tutorial de SPA WKND](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Introducción a React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Introducción a Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Si necesita adaptar un SPA existente para utilizarlo en AEM, revise los siguientes documentos:

* [El componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Edición de un SPA externo dentro de AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Consulte a continuación [recursos adicionales](#additional-resources) que pueden profundizar en SPA temas de AEM.

## Recursos adicionales {#additional-resources}

A continuación se muestran algunos recursos adicionales que profundizan en algunos conceptos mencionados en este documento.

* [Encabezado y sin encabezado en AEM](/help/implementing/developing/headful-headless.md) : una descripción de los diferentes modelos de envío disponibles en AEM
* [SPA Introducción y Tutorial.](/help/implementing/developing/hybrid/introduction.md) - Una buena introducción a la SPA en AEM
* [Desarrollo de SPA para AEM](/help/implementing/developing/hybrid/developing.md) : Directrices sobre cómo desarrollar SPA para AEM
* [Información general del Editor de SPA](/help/implementing/developing/hybrid/editor-overview.md) : Detalles del funcionamiento del Editor de SPA
* [Renderización del servidor](/help/implementing/developing/hybrid/ssr.md) : configuración del SSR para AEM SPA
* [SPA Documentos de referencia](/help/implementing/developing/hybrid/reference-materials.md) : referencias y vínculos de la API de JavaScript a los proyectos de código abierto AEM SPA GitHub
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : creación de fragmentos de contenido
* [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) : plantilla Maven que crea un proyecto mínimo de Adobe Experience Manager (AEM) basado en las prácticas recomendadas como punto de partida para el sitio web.
