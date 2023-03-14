---
title: Desarrollo de SPA para AEM
description: SPA AEM AEM SPA SPA AEM Este artículo presenta preguntas importantes que hay que tener en cuenta al contratar a un desarrollador front-end para que desarrolle una para la implementación, así como ofrece una visión general de la arquitectura de con respecto a las cuestiones que hay que tener en cuenta a la hora de implementar un desarrollador en la implementación de un desarrollador en la plataforma de desarrollo de la plataforma de la.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 13%

---

# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder generar sitios usando marcos de SPA y los autores quieren editar contenido dentro de AEM para un sitio generado usando dichos marcos.

SPA AEM AEM SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una aplicación para la y ofrece una visión general de la arquitectura de las soluciones de con respecto a la implementación de las soluciones de en la implementación de la aplicación de un desarrollador de front-end en el entorno de la.

## SPA AEM Principios de desarrollo de la {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA Si, como desarrollador front-end, sigue estas prácticas recomendadas generales, así como algunos principios específicos de la interfaz de usuario de la aplicación, el usuario de la aplicación estará operativo con la aplicación de los principios de la aplicación de la configuración de usuario de la aplicación de usuario de la plataforma de usuario de la interfaz de usuario de la plataforma de usuario, el usuario de la plataforma de usuario de la plataforma de usuario de [AEM y sus capacidades de creación de contenido](introduction.md#content-editing-experience-with-spa).

* **[Portabilidad](#portability)**: al igual que con cualquier componente, los componentes de deben estar creados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing)**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

SPA AEM Si tiene en cuenta estos principios a medida que desarrolle su, será lo más flexible y tendrá la mayor garantía de futuro posible, al tiempo que se habilitan todas las funcionalidades de creación de contenido compatibles.

AEM Si no necesita admitir características de creación de la, es posible que tenga que considerar una opción diferente [SPA modelo de diseño de](#spa-design-models).

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

SPA El resultado debe ser construido con componentes altamente portátiles y reutilizables.

### AEM Estructura del sitio de {#aem-drives-site-structure}

SPA El desarrollador front-end debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de la aplicación que se utilizan para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. [AEM Sin embargo, en todo momento, la estructura del sitio es propiedad de los usuarios.](editor-overview.md)

Esto significa que el desarrollador front-end puede añadir contenido del cliente antes o después del punto de entrada de los componentes y también puede realizar llamadas de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo se anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

SPA La solo debe depender de la renderización dinámica del contenido. AEM Esta es la expectativa predeterminada en la que la recupera y procesa todos los elementos secundarios de la estructura de contenido.

AEM Cualquier renderización explícita que apunte a contenido específico se considera una renderización estática y, aunque se admite, no es compatible con las funciones de creación de contenido. Esto también va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. AEM En el [SPA la ruta siempre debe pertenecer a la dirección](routing.md) AEM y lo escucha, y recupera contenido basado en él.

Cualquier enrutamiento estático funciona con la variable [principio de portabilidad](#portability) AEM y limita al autor al no ser compatible con las funciones de creación de contenido de la aplicación de la creación de contenido de la. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, tendría que pedirle al desarrollador front-end que lo haga.

## Tipo de archivo del proyecto AEM. {#aem-project-archetype}

Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## SPA Modelos de diseño {#spa-design-models}

Si la variable [SPA AEM Principios de desarrollo de la](#spa-development-principles-for-aem) SPA AEM son seguidos, entonces sus funcionarán con todas las funciones de creación de contenido de admitidas.

Sin embargo, puede haber casos en los que esto no sea del todo necesario. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como CMS sin encabezado sin usar el <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA Marco del SDK del editor de.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>AEM Los creadores de contenido no pueden aprovechar la experiencia de creación de contenido de.</p> <p>El código no es ni portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El desarrollador front-end utiliza el marco de trabajo del SDK del Editor de, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>AEM Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de la.</p> <p>El código corre el riesgo de no ser ni portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA AEM El proyecto aprovecha completamente el SDK del Editor de, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a los usuarios de la aplicación de forma que puedan acceder a la interfaz de usuario de la aplicación en un solo paso.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>AEM El autor del contenido puede editar la aplicación mediante la experiencia de creación de contenido de la.<br /> </p> <p>SPA La plantilla es compatible con el editor de plantillas de.</p> </td>
   <td><p>AEM El desarrollador no controla la estructura de la aplicación ni la parte de contenido delegada a la que se ha delegado la aplicación en el usuario.</p> <p>AEM El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con la ayuda de la herramienta de creación de segmentos de contenido de la aplicación de la aplicación de tipo de.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Aunque todos los modelos son compatibles con los modelos de, solo mediante la implementación de la tercera (y, por lo tanto, siguiendo el recomendado) [SPA AEM Principios de desarrollo de la en](#spa-development-principles-for-aem)SPA AEM ), los autores de contenido podrán interactuar con el contenido de la página de contenido y editarlo en la forma en la que están acostumbrados a la creación de la página de contenido de la página de la página de la página de inicio de la página de la página de inicio de la página de inicio de la página de inicio.

## SPA AEM Migración de recursos existentes a la {#migrating-existing-spas-to-aem}

SPA Por lo general, si el usuario sigue el procedimiento de [SPA AEM Principios de desarrollo de la](#spa-development-principles-for-aem)SPA AEM AEM SPA , el funcionará en el modo de trabajo y se podrá editar con el Editor de la de trabajo de la aplicación de.

SPA AEM Siga estos pasos para preparar sus existentes para trabajar con ellos.

1. **Haga que los componentes JS sean modulares.** - Hacerlos capaces de ser procesados en cualquier orden, posición y tamaño.
1. **Utilice los contenedores que proporciona nuestro SDK para colocar los componentes en la pantalla.** AEM : proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. **AEM Cree un componente de para cada componente JS.** AEM : los componentes de la definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

SPA AEM La tarea principal al involucrar a un desarrollador front-end para crear una para la creación de segmentos es acordar sobre los componentes y sus modelos JSON.

SPA AEM A continuación se describen los pasos que un desarrollador front-end debe seguir al desarrollar un para la creación de segmentos de cliente con un tipo de interfaz de usuario

1. **Acordar componentes y su modelo JSON**

   AEM SPA Los desarrolladores de front-end y de back-end deben ponerse de acuerdo sobre qué componentes son necesarios y un modelo, de modo que haya una coincidencia individualizada entre los componentes de la interfaz de usuario y los componentes de back-end de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario.

   AEM La mayoría de los componentes todavía son necesarios para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En Componentes de React, acceda al modelo mediante`this.props.cqModel`**

   SPA Una vez acordados los componentes y que el modelo JSON esté listo, el desarrollador front-end es libre de desarrollar el modelo de JSON y puede acceder a él simplemente a través de la interfaz de usuario de JSON. El desarrollador de JSON puede desarrollar el modelo de JSON de una manera sencilla y sencilla. `this.props.cqModel`.

1. **Implementación del componente `render()` método**

   El desarrollador front-end implementa las `render()` y pueden utilizar los campos de la variable. `cqModel` propiedad. Esto genera el DOM y los fragmentos de HTML que se insertarán en la página. Esta es la forma estándar de crear una aplicación en React.

1. **AEM Asigne el componente al tipo de recurso de mediante`MapTo()`**

   La asignación almacena clases de componentes y la utiliza internamente el proporcionado `Container` para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Esto sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   El `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el del componente `EditConfig` como parámetro a`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Ampliar el proporcionado `Container` clase para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use el HTML 5 `History` API.**

   Si la variable `ModelRouter` está habilitado, llamando a la función `pushState` y `replaceState` funciones almacenarán en déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   El `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada que sea específico para el Adobe AEM o la.

* AEM Todo lo que se encuentra dentro del componente JavaScript no es independiente de la aplicación de la aplicación de la aplicación de.
* AEM AEM Sin embargo, lo que sí es específico de la es que el componente JS debe asignarse a un componente de la aplicación de seguridad de la aplicación de ayuda de MapTo.

![AEM Enfoque agnóstico de la](assets/aem-agnostic.png)

El `MapTo` Helper es el &quot;pegamento&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML al HTML SPA que procesa el componente JS, de modo que el Editor de datos sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` SPA AEM y crear una lista de componentes para la creación de informes de manera general, consulte la guía de introducción para obtener información sobre el marco de trabajo seleccionado.

* [Introducción a SPA en AEM usando React](getting-started-react.md)
* [Introducción a SPA en AEM usando Angular](getting-started-angular.md)

## AEM SPA Arquitectura de la y la {#aem-architecture-and-spas}

AEM SPA La arquitectura general de los entornos de desarrollo, creación y publicación, entre otros, no cambia al utilizar la. SPA Sin embargo, es útil comprender cómo encaja el desarrollo de la en esta arquitectura.

![AEM SPA arquitectura de la y la](assets/aem-architecture.png)

* **Entorno de compilación**

   SPA Aquí es donde se desprotege el origen del origen de la aplicación y del origen del componente de la aplicación de.

   * SPA El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de.
   * Esa biblioteca la tomará Maven y la implementará el complemento de compilación de Maven junto con el componente al autor de AEM.

* **AEM Author**

   AEM SPA El contenido se crea en el autor de la, incluido el autor de la creación

   SPA SPA Cuando se edita una con el Editor de en el entorno de creación:

   1. SPA El HTML externo se lo solicita el.
   1. Se carga el CSS.
   1. SPA Se carga el JavaScript de la aplicación de la.
   1. SPA Cuando se ejecuta la aplicación de la, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluido el `cq-data` atributos.
   1. Esta `cq-data` Los atributos de permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **AEM Publish**

   SPA Aquí es donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de aplicación, clientlibs y componentes, se publican para uso público.

* **Dispatcher/CDN**

   AEM Dispatcher sirve como la capa de almacenamiento en caché de los datos para los visitantes del sitio.
   * Las solicitudes se procesan de forma similar a como se encuentran en el Autor de AEM, pero no hay ninguna solicitud de información de página, ya que solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>AEM Dentro de no hay necesidad de ejecutar mecanismos de compilación de Javascript o de ejecutar el propio Javascript. AEM SPA solo aloja los artefactos compilados de la aplicación de la.

## Pasos siguientes {#next-steps}

* [Introducción a SPA en AEM usando React](getting-started-react.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA de AEM usando React.
* [Introducción a SPA en AEM usando Angular](getting-started-angular.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA en AEM usando Angular.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [SPA Proyecto de WKND](wknd-tutorial.md) SPA AEM es un tutorial paso a paso sobre la implementación de un proyecto de simple en el sector de la.
* [SPA Asignación de modelos dinámicos a componentes para la creación de](model-to-component-mapping.md) SPA AEM explica el modelo dinámico para la asignación de componentes y cómo funciona dentro de la asignación de componentes de la interfaz de usuario de la aplicación de datos en la.
* [SPA Modelo de](blueprint.md) SPA AEM SPA AEM ofrece una explicación detallada de cómo funciona el SDK de la para la creación de informes en caso de que desee implementar un esquema de trabajo de forma más sencilla que no sea React o Angular, o simplemente desee tener una comprensión más profunda de la aplicación.
