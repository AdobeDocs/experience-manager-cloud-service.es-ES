---
title: Desarrollo de SPA para AEM
description: Este artículo presenta importantes cuestiones que deben tenerse en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM, así como también ofrece una visión general de la arquitectura de AEM con respecto a SPA que debe tener en cuenta al implementar un SPA desarrollado en AEM.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '2078'
ht-degree: 0%

---


# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

Este artículo presenta importantes cuestiones que deben tenerse en cuenta al contratar a un desarrollador front-end para que desarrolle un SPA para AEM y ofrece una visión general de la arquitectura de AEM con respecto a la implementación de SPA en AEM.

## Principios de desarrollo SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end observa las optimizaciones estándar al crear un SPA. Si, como desarrollador front-end, sigue estas optimizaciones generales, así como algunos principios específicos de AEM, su SPA funcionará con [AEM y sus capacidades](introduction.md#content-editing-experience-with-spa)de creación de contenido.

* **[Portabilidad](#portability)** : Al igual que con cualquier componente, los componentes se deben crear para que sean lo más portátiles posible. El SPA debe construirse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura](#aem-drives-site-structure)** del sitio: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento](#dynamic-rendering)** dinámico: todo el procesamiento debe ser dinámico.
* **[Enrutamiento](#dynamic-routing)** dinámico: El SPA es responsable del enrutamiento y AEM lo escucha y obtiene basándose en él. Cualquier enrutamiento también debería ser dinámico.

Si tiene en cuenta estos principios a medida que desarrolla su SPA, será lo más flexible y la prueba más futura posible, al tiempo que se habilitará toda la funcionalidad AEM creación admitida.

Si no necesita admitir funciones de creación de AEM, puede que tenga que considerar un modelo [de diseño de](#spa-design-models)SPA diferente.

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de manera que se maximice su portabilidad. Cualquier patrón que funcione en contra de la portabilidad o reutilización de los componentes debe evitarse para garantizar la compatibilidad, la flexibilidad y la sostenibilidad a partir de ahora.

El SPA resultante debe construirse con componentes muy portátiles y reutilizables.

### AEM impulsa la estructura del sitio {#aem-drives-site-structure}

El desarrollador de front-end debe considerarse responsable de crear una biblioteca de componentes de SPA que se utilizan para crear la aplicación. El desarrollador front-end tiene control total de la estructura interna de los componentes. [Sin embargo, AEM en todo momento posee la estructura del sitio.](editor-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador de front-end no tiene el control absoluto de cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

El SPA solo debe basarse en la representación dinámica del contenido. Es la expectativa predeterminada en la que AEM captura y procesa todos los elementos secundarios de la estructura de contenido.

Cualquier representación explícita que apunte a contenido específico se considera representación estática y aunque se admite, no será compatible con las funciones de creación de contenido de AEM. Esto también va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que en el procesamiento, todo el enrutamiento también debe ser dinámico. En AEM, [el SPA siempre debe ser propietario del enrutamiento](routing.md) y AEM lo escucha y captura contenido basado en él.

Cualquier enrutamiento estático va en contra del [principio de portabilidad](#portability) y limita al autor al no ser compatible con las funciones de creación de contenido de AEM. Por ejemplo, con un enrutamiento estático, si el autor del contenido desea cambiar una ruta o una página, deberá pedir al desarrollador del front-end que lo haga.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html)de proyecto, que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

## Modelos de diseño SPA {#spa-design-models}

Si se siguen los [principios de desarrollo de SPA en AEM](#spa-development-principles-for-aem) , su SPA funcionará con todas las funciones de creación de contenido AEM admitidas.

Sin embargo, puede haber casos en los que esto no es totalmente necesario. La siguiente tabla ofrece una visión general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como un CMS sin encabezado sin utilizar el marco del SDK del Editor de <a href="/help/implementing/developing/spa/reference-materials.md">SPA.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden aprovechar AEM experiencia de creación de contenido.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador front-end utiliza el marco del SDK del Editor de SPA, pero solo abre algunas áreas para el autor del contenido.</td>
   <td>El desarrollador mantiene el control sobre la aplicación al habilitar únicamente la creación en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido AEM.</p> <p>El código no puede ser portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables mediante el JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto aprovecha completamente el SDK SPA Editor y los componentes principales se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega en AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación con AEM experiencia de creación de contenido.<br /> </p> <p>El SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegada a AEM.</p> <p>El desarrollador aún puede reservar áreas de la aplicación para el contenido que no está pensado para ser creado con AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos se admiten en AEM, sólo implementando el tercero (y siguiendo así los principios de desarrollo [SPA recomendados en AEM](#spa-development-principles-for-aem)) los autores de contenido podrán interactuar con el contenido del SPA y editarlo en AEM a medida que estén acostumbrados.

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Generalmente, si su SPA sigue los Principios de desarrollo [SPA para AEM](#spa-development-principles-for-aem), su SPA trabajará en AEM y será editable mediante el Editor de SPA.

Siga estos pasos para preparar el SPA existente para trabajar con AEM.

1. **Haga que los componentes de JS sean modulares.** - Hacerlos capaces de procesarse en cualquier orden, posición y tamaño.
1. **Utilice los contenedores proporcionados por nuestro SDK para colocar sus componentes en la pantalla.** - AEM proporciona un componente de sistema de páginas y párrafos para que lo utilice.
1. **Cree un componente de AEM para cada componente de JS.** - Los componentes AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La principal tarea de contratar a un desarrollador front-end para crear un SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar un SPA para AEM.

1. **Aceptar los componentes y su modelo JSON**

   Los desarrolladores de front-end y los desarrolladores de AEM de back-end deben acordar qué componentes son necesarios y qué modelo, de modo que exista una coincidencia individual entre los componentes de SPA y los componentes de back-end.

   AEM componentes siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y para exportar el modelo de componentes.

1. **En componentes React, acceda al modelo mediante`this.props.cqModel`**

   Una vez que se han acordado los componentes y se ha implantado el modelo JSON, el desarrollador front-end puede desarrollar el SPA y simplemente acceder al modelo JSON mediante `this.props.cqModel`.

1. **Implementar el método `render()` del componente**

   El desarrollador front-end implementa el `render()` método según lo que considere necesario y puede utilizar los campos de la `cqModel` propiedad. Esto genera los fragmentos DOM y HTML que se insertarán en la página. Esta es la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso AEM mediante`MapTo()`**

   La asignación almacena clases de componente y el componente proporcionado la utiliza internamente para recuperar y crear instancias dinámicas de componentes en función del tipo de recurso determinado. `Container`

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end, de modo que el editor sabe a qué componentes de reacción corresponden.

   Los `Page` y `ResponsiveGrid` son buenos ejemplos de clases que extienden la base `Container`.

1. **Defina el parámetro del componente `EditConfig` como`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe nombrar el componente mientras no se procese o no tenga contenido para procesar.

1. **Extender la `Container` clase proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo previsto.

1. **Implemente una solución de enrutamiento que utilice la API de HTML5 `History` .**

   Cuando `ModelRouter` está activado, la llamada a las funciones `pushState` y `replaceState` activará una solicitud al `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual del modelo `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo de Sling. No admite el uso de direcciones URL personales o alias.

   El `ModelRouter` se puede deshabilitar o configurar para ignorar una lista de expresiones regulares.

## AEM-agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada específico para el Adobe o el AEM.

* Todo lo que se encuentra dentro del componente JavaScript no es AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente MapTo.

![AEM Enfoque agnóstico](assets/aem-agnostic.png)

El `MapTo` ayudante es el &quot;pegamento&quot; que permite que los componentes del back-end y del front-end se comparen entre sí:

* Indica al contenedor JS (o sistema de párrafos JS) qué componente JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos HTML al HTML que representa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso `MapTo` y la creación de SPA para AEM en general, consulte la Guía de introducción de la estructura seleccionada.

* [Introducción a SPA en AEM con React](getting-started-react.md)
* [Introducción a SPA en AEM con Angular](getting-started-angular.md)

## Arquitectura AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo SPA desarrollo encaja en esta arquitectura.

![Arquitectura AEM y SPA](assets/aem-architecture.png)

* **Generar Entorno**

   Aquí es donde se extrae el origen de la aplicación SPA y el origen del componente.

   * El generador clientlib de NPM crea una biblioteca de cliente del proyecto SPA.
   * Maven se encargará de la utilización de esa biblioteca y la implementará el complemento Maven Build junto con el componente en AEM Author.

* **AEM Author**

   El contenido se crea en el autor AEM, incluido el SPA de creación.

   Cuando se edita un SPA con el Editor de SPA en el entorno de creación:

   1. El SPA solicita el HTML externo.
   1. Se carga la CSS.
   1. Se carga el Javascript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación de SPA, se solicita el JSON, lo que permite que la aplicación genere el DOM de la página, incluidos los `cq-data` atributos.
   1. Estos `cq-data` atributos permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos SPA artefactos de aplicación, clientlibs y componentes, se publican para consumo público.

* **Dispatcher/CDN**

   El despachante sirve como capa de almacenamiento en caché de AEM para visitantes al sitio.
   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author; sin embargo, no hay ninguna solicitud de la información de la página, ya que solo lo necesita el editor.
   * Javascript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para un envío rápido.

>[!NOTE]
>
>Dentro de AEM no hay necesidad de ejecutar los mecanismos de compilación de Javascript ni de ejecutar el propio Javascript. AEM solo aloja los artefactos compilados de la aplicación SPA.

## Próximos pasos {#next-steps}

* [Introducción a SPA en AEM con React](getting-started-react.md) muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con React.
* [Introducción a SPA en AEM con Angular](getting-started-angular.md) muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con Angular.
* [SPA información general](editor-overview.md) del Editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [WKND SPA Project](wknd-tutorial.md) es un tutorial paso a paso que implementa un sencillo proyecto SPA en AEM.
* [La asignación de modelo dinámico a componente para SPA](model-to-component-mapping.md) explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de SPA en AEM.
* [SPA modelo](blueprint.md) oferta un profundo análisis de cómo funciona el SDK de SPA para AEM en caso de que desee implementar SPA en AEM para un entorno que no sea React o Angular o simplemente quiera un entendimiento más profundo.
