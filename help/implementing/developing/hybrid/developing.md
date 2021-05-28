---
title: Desarrollo de SPA para AEM
description: Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador de front-end para que desarrolle un SPA para AEM, así como una visión general de la arquitectura de AEM con respecto a SPA tener en cuenta al implementar un SPA desarrollado en AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 0%

---

# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con dichos marcos.

Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador de front-end para que desarrolle un SPA para AEM y ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

## Principios de desarrollo de SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador del front-end observa las prácticas recomendadas estándar al crear un SPA. Si como desarrollador de front-end sigue estas prácticas recomendadas generales, así como algunos principios específicos de AEM, su SPA funcionará con [AEM y sus capacidades de creación de contenido](introduction.md#content-editing-experience-with-spa).

* **[Portabilidad](#portability)** : Al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. El SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM estructura del sitio](#aem-drives-site-structure)** : el desarrollador de front-end crea componentes y posee su estructura interna, pero depende de la AEM para definir la estructura de contenido del sitio.
* **[Renderización dinámica](#dynamic-rendering)** : todas las renderizaciones deben ser dinámicas.
* **[Enrutamiento dinámico](#dynamic-routing)** : El SPA es responsable del enrutamiento y AEM lo escucha y obtiene en función de él. Cualquier enrutamiento también debe ser dinámico.

Si tiene en cuenta estos principios al desarrollar su SPA, será lo más flexible y la prueba más futura posible, al mismo tiempo que habilita todas las funciones de creación AEM compatibles.

Si no necesita admitir AEM funciones de creación, puede que tenga que considerar un [SPA modelo de diseño](#spa-design-models) diferente.

### Portabilidad {#portability}

Al igual que cuando se desarrolla cualquier componente, los componentes deben diseñarse de manera que se maximice su portabilidad. Cualquier patrón que funcione en contra de la portabilidad o reutilización de los componentes debe evitarse para garantizar la compatibilidad, flexibilidad y mantenimiento en el futuro.

El SPA resultante debe crearse con componentes altamente portátiles y reutilizables.

### AEM estructura del sitio {#aem-drives-site-structure}

El desarrollador principal debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de SPA que se utilizan para crear la aplicación. El desarrollador de front-end tiene control total de la estructura interna de los componentes. [Sin embargo, AEM en todo momento posee la estructura del sitio.](editor-overview.md)

Esto significa que el desarrollador del front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador de front-end no tiene control absoluto sobre cómo se anidan los componentes, por ejemplo.

### Renderización dinámica {#dynamic-rendering}

El SPA solo debe depender de la representación dinámica del contenido. Esta es la expectativa predeterminada en la que AEM recupera y procesa todos los elementos secundarios de la estructura de contenido.

Cualquier renderización explícita que señale a contenido específico se considera una renderización estática y aunque compatible, no será compatible con AEM funciones de creación de contenido. Esto también va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con la renderización, todo el enrutamiento también debe ser dinámico. En AEM, [el SPA siempre debe ser propietario del enrutamiento](routing.md) y AEM lo escucha y busca contenido basado en él.

Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](#portability) y limita al autor al no ser compatible con las funciones de creación de contenido de AEM. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador del front-end que lo hiciera.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos con React o Angular y aprovecha el SDK de SPA.

## Modelos de diseño de SPA {#spa-design-models}

Si se siguen los [principios de desarrollo de SPA en AEM](#spa-development-principles-for-aem) , el SPA funcionará con todas las funciones AEM creación de contenido admitidas.

Sin embargo, puede haber casos en que esto no sea completamente necesario. La siguiente tabla ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como un CMS sin encabezado sin utilizar el <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA marco del SDK del Editor.</a></td>
   <td>El desarrollador del front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden aprovechar AEM experiencia de creación de contenido.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador del front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador de front-end utiliza el marco del SDK del Editor de SPA, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control sobre la aplicación habilitando la creación solo en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de AEM experiencia de creación de contenido.</p> <p>El código corre el riesgo de no ser portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador del front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto aprovecha completamente el SDK del Editor de SPA y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega en AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación mediante AEM experiencia de creación de contenido.<br /> </p> <p>El SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegada a AEM.</p> <p>El desarrollador aún puede reservar áreas de la aplicación para el contenido que no está pensado para su creación mediante AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos se admiten en AEM, solo implementando el tercero (y siguiendo así los [SPA principios de desarrollo recomendados en AEM](#spa-development-principles-for-aem)) los autores de contenido podrán interactuar con el contenido del SPA y editarlo en AEM a medida que estén acostumbrados.

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Por lo general, si la SPA sigue los [SPA Principios de desarrollo para AEM](#spa-development-principles-for-aem), la SPA funcionará en AEM y se podrá editar con el AEM Editor de SPA.

Siga estos pasos para preparar su SPA existente para trabajar con AEM.

1. **Haga que los componentes de JS sean modulares.** - Hacerlos capaces de procesarse en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por nuestro SDK para colocar sus componentes en la pantalla .** - AEM proporciona un componente de sistema de páginas y párrafos para que lo utilice.
1. **Cree un componente AEM para cada componente JS.** : Los componentes de AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La tarea principal de contratar a un desarrollador de front-end para crear un SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador de front-end al desarrollar un SPA para AEM.

1. **Aceptar componentes y su modelo JSON**

   Los desarrolladores de front-end y los desarrolladores de AEM de back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo, de modo que exista una coincidencia individual entre los componentes de SPA y los componentes del back-end.

   AEM componentes siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y exportar el modelo de componentes.

1. **En Componentes de React, acceda al modelo a través de`this.props.cqModel`**

   Una vez que los componentes están acordados y el modelo JSON está en su lugar, el desarrollador front-end puede desarrollar el SPA y simplemente acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el  `render()` método del componente**

   El desarrollador de front-end implementa el método `render()` tal como lo consideran adecuado y puede utilizar los campos de la propiedad `cqModel` . Esto genera los fragmentos DOM y HTML que se insertan en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso AEM mediante`MapTo()`**

   La asignación almacena clases de componentes y la utiliza internamente el componente proporcionado `Container` para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de reacción.

   Los `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el parámetro del componente  `EditConfig` como`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe nombrar el componente mientras no se haya procesado aún o no haya contenido para procesar.

1. **Ampliar la  `Container` clase proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a componentes internos funcione según lo esperado.

1. **Implemente una solución de enrutamiento que utilice la  `History` API de HTML5.**

   Cuando `ModelRouter` está habilitado, la llamada a las funciones `pushState` y `replaceState` envía una solicitud a `PageModelManager` para recuperar un fragmento que falta en el modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias personales.

   El `ModelRouter` se puede deshabilitar o configurar para ignorar una lista de expresiones regulares.

## AEM-agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada específico para el Adobe o el AEM.

* Todo lo que se encuentra dentro del componente JavaScript no es AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente de MapTo.

![AEM Enfoque agnóstico](assets/aem-agnostic.png)

El asistente `MapTo` es el &quot;pegamento&quot; que permite que los componentes del back-end y del front-end se comparen entre sí:

* Indica al contenedor de JS (o sistema de párrafos JS) qué componente JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Añade un atributo de datos HTML al HTML que procesa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` y la creación de SPA para AEM en general, consulte la guía de introducción para el marco seleccionado.

* [Introducción a SPA en AEM con React](getting-started-react.md)
* [Introducción a SPA en AEM Uso de Angular](getting-started-angular.md)

## Arquitectura AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo SPA desarrollo encaja en esta arquitectura.

![arquitectura AEM y SPA](assets/aem-architecture.png)

* **Entorno de compilación**

   Aquí es donde se extrae el origen de la aplicación SPA y el origen de componentes.

   * El generador clientlib de NPM crea una biblioteca de cliente del proyecto SPA.
   * Maven la tomará y la implementará el complemento de compilación de Maven junto con el componente en AEM Author.

* **AEM Author**

   El contenido se crea en el autor AEM, incluido el SPA de creación.

   Cuando se edita una SPA con el Editor de SPA en el entorno de creación:

   1. El SPA solicita el HTML externo.
   1. Se carga el CSS.
   1. Se carga el JavaScript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación SPA, se solicita el JSON, lo que permite que la aplicación cree el DOM de la página, incluidos los atributos `cq-data`.
   1. Estos atributos `cq-data` permiten al editor cargar información de página adicional para que sepa qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de SPA aplicación, clientlibs y componentes, se publican para el consumo público.

* **Dispatcher/CDN**

   Dispatcher sirve como capa de AEM de almacenamiento en caché para los visitantes del sitio.
   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author; sin embargo, no hay solicitud de la información de la página, ya que el editor solo lo necesita.
   * Javascript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>Dentro de AEM no hay necesidad de ejecutar mecanismos de compilación de Javascript ni de ejecutar el propio Javascript. AEM solo aloja los artefactos compilados desde la aplicación SPA.

## Pasos siguientes {#next-steps}

* [Introducción a SPA en AEM con ](getting-started-react.md) Reactancia muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con React.
* [Introducción a SPA en AEM con ](getting-started-angular.md) Angularis muestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM con Angular.
* [SPA ](editor-overview.md) Información general del editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [WKND SPA ](wknd-tutorial.md) Project es un tutorial paso a paso que implementa un proyecto de SPA simple en AEM.
* [Asignación de modelos dinámicos a componentes para ](model-to-component-mapping.md) SPAs explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de SPA en AEM.
* [SPA ](blueprint.md) Blueprintoofrece una explicación detallada sobre cómo funciona el SDK de SPA para AEM en caso de que desee implementar SPA en AEM para un marco que no sea React o Angular, o simplemente desee un entendimiento más profundo.
