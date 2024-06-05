---
title: Desarrollo de SPA para AEM
description: SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una aplicación para el desarrollo de la. AEM SPA SPA AEM También se ofrece una visión general de la arquitectura de los en relación con los aspectos que se deben tener en cuenta a la hora de implementar una implementación de una implementación de un entorno de desarrollo en la que se.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 8%

---

# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder generar sitios usando marcos de SPA y los autores quieren editar contenido dentro de AEM para un sitio generado usando dichos marcos.

SPA AEM AEM SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar un para y ofrece una visión general de la arquitectura de los recursos de la aplicación en relación con la implementación de los programas de desarrollo de software en el entorno de la.

## SPA AEM Principios de desarrollo de la {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA Si, como desarrollador front-end, sigue estas prácticas recomendadas generales y algunos principios específicos de la interfaz de usuario de, el desarrollador de la interfaz de usuario de le ofrece una experiencia práctica con la que puede trabajar en el desarrollo de soluciones específicas de la interfaz de usuario de la interfaz de usuario de, la interfaz de usuario de. [AEM y sus capacidades de creación de contenido](introduction.md#content-editing-experience-with-spa).

* **[Portabilidad](#portability)** - Al igual que con cualquier otro componente, los componentes deben estar diseñados para ser lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing)**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

SPA AEM Si tiene en cuenta estos principios a medida que desarrolle su, se vuelve lo más flexible y lo más seguro posible en el futuro, al tiempo que se habilitan todas las funcionalidades de creación de contenido compatibles.

AEM Si no necesita admitir características de creación de la, considere una opción diferente [SPA modelo de diseño de](#spa-design-models).

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

SPA El resultado debe ser construido con componentes altamente portátiles y reutilizables.

### AEM Estructura del sitio de {#aem-drives-site-structure}

SPA El desarrollador front-end debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de que se utilizan para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. [AEM Sin embargo, siempre es propietario de la estructura del sitio de,](editor-overview.md).

Este control significa que el desarrollador front-end puede agregar contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar una llamada de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

SPA La solo debe depender de la renderización dinámica del contenido. AEM Esta expectativa es la predeterminada en la que la recupera y procesa todos los elementos secundarios de la estructura de contenido.

AEM Cualquier renderización explícita que apunte a contenido específico se considera una renderización estática y, aunque se admite, es compatible con las funciones de creación de contenido de la. También va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. AEM En el [SPA la ruta siempre debe pertenecer a la dirección](routing.md) AEM y lo escucha, y recupera contenido basado en él.

Cualquier enrutamiento estático funciona con la variable [principio de portabilidad](#portability) AEM y limita al autor al no ser compatible con las funciones de creación de contenido de la aplicación de la creación de contenido de la. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, debe pedirle al desarrollador front-end que lo haga.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## SPA Modelos de diseño {#spa-design-models}

Si la variable [SPA AEM Principios de desarrollo de la](#spa-development-principles-for-aem) SPA AEM son seguidos, entonces su funciona con todas las funciones de creación de contenido de soporte que se admiten.

Sin embargo, puede haber casos en los que esta funcionalidad no sea completamente necesaria. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

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
   <td><p>AEM Los autores de contenido no pueden utilizar la experiencia de creación de contenido de.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El desarrollador front-end utiliza el marco de trabajo del SDK del Editor de, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>AEM Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de la.</p> <p>El código corre el riesgo de no ser portátil o reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA AEM El proyecto utiliza completamente el SDK del Editor de, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a los.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>AEM El autor del contenido puede editar la aplicación mediante la experiencia de creación de contenido de la.<br /> </p> <p>SPA La plantilla es compatible con el editor de plantillas de.</p> </td>
   <td><p>AEM El desarrollador no controla la estructura de la aplicación ni la parte de contenido delegada a la que se ha delegado la aplicación en el usuario.</p> <p>AEM El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con la ayuda de la herramienta de creación de segmentos de contenido de la aplicación de la aplicación de tipo de.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Aunque todos los modelos son compatibles con los modelos de, solo mediante la implementación de la tercera (y siguiendo las recomendaciones de). [SPA Principios de desarrollo de](#spa-development-principles-for-aem)SPA AEM ) son los autores de contenido capaces de interactuar con el contenido de la aplicación, así como de editarlo, en el contenido de la aplicación de contenido de la aplicación de la aplicación de la aplicación de la.

## SPA AEM Migración de recursos existentes a la {#migrating-existing-spas-to-aem}

SPA Por lo general, si el usuario sigue el procedimiento de [SPA AEM Principios de desarrollo de la](#spa-development-principles-for-aem)SPA AEM AEM SPA , la funciona en el modo de trabajo y se puede editar con el Editor de de trabajo.

SPA AEM Siga estos pasos para que pueda preparar sus existentes para trabajar con los recursos de la aplicación de forma más rápida y sencilla

1. **Haga que los componentes JS sean modulares.** : haga que sean capaces de procesarse en cualquier orden, posición y tamaño.
1. **Utilice los contenedores que proporciona el SDK para colocar los componentes en la pantalla.** AEM : proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. **AEM Cree un componente de para cada componente JS.** AEM : los componentes de la definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

SPA AEM La tarea principal al involucrar a un desarrollador front-end para crear una para la creación de segmentos es acordar sobre los componentes y sus modelos JSON.

SPA AEM A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una para la creación de segmentos de cliente de tipo

1. **Acordar componentes y su modelo JSON**

   AEM SPA Los desarrolladores de front-end y de back-end deben acordar qué componentes son necesarios y qué modelo, de modo que haya una coincidencia individualizada entre los componentes de la interfaz de usuario y los componentes de back-end de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario.

   AEM La mayoría de los componentes todavía son necesarios para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En Componentes de React, acceda al modelo mediante`this.props.cqModel`**

   SPA Una vez acordados los componentes y que el modelo JSON esté listo, el desarrollador front-end es libre de desarrollar el modelo de JSON y puede acceder a él simplemente a través de la interfaz de usuario de JSON. El desarrollador de JSON puede desarrollar el modelo de JSON de una manera sencilla y sencilla. `this.props.cqModel`.

1. **Implementar el del componente `render()` método**

   El desarrollador front-end implementa las `render()` y pueden utilizar los campos de la variable. `cqModel` propiedad. Este método genera los fragmentos DOM y HTML que se insertan en la página. Este método es también la forma estándar de crear una aplicación en React.

1. **AEM Asigne el componente al tipo de recurso de mediante`MapTo()`**

   La asignación almacena clases de componentes y la utiliza internamente el proporcionado `Container` para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Este mapa sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   El `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina el del componente `EditConfig` como parámetro a`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Ampliar el proporcionado `Container` clase para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use el HTML 5 `History` API.**

   Si la variable `ModelRouter` está habilitado, llamando a la función `pushState` y `replaceState` funciones déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   El `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada que sea específico para el Adobe AEM o la.

* AEM Todo lo que se encuentra dentro del componente JavaScript no es independiente de la aplicación de la aplicación de la aplicación de.
* AEM AEM Sin embargo, lo que es específico de la es que el componente JS debe asignarse a un componente de la aplicación de ayuda de MapTo.

![AEM Enfoque agnóstico de la](assets/aem-agnostic.png)

El `MapTo` Helper es el &quot;pegamento&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML al HTML SPA que procesa el componente JS, de modo que el Editor de datos sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` SPA AEM y crear una lista de componentes para la creación de informes de manera general, consulte la guía de introducción para obtener información sobre el marco de trabajo seleccionado.

* [SPA AEM Introducción a la administración de la en React](getting-started-react.md)
* [SPA AEM Introducción a la administración de la en Angular](getting-started-angular.md)

## AEM SPA Arquitectura de la y la {#aem-architecture-and-spas}

AEM SPA La arquitectura general de los entornos de desarrollo, creación y publicación, entre otros, no cambia al utilizar la. SPA Sin embargo, es útil comprender cómo encaja el desarrollo de la en esta arquitectura.

![AEM SPA arquitectura de la y la](assets/aem-architecture.png)

* **Entorno de compilación**

  SPA En este entorno es donde se extrae el origen de la aplicación y el componente de la aplicación de la.

   * SPA El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de.
   * AEM Maven se encarga de tomar esa biblioteca e implementarla el complemento de compilación de Maven junto con el componente al autor de la.

* **AEM Autor de**

  AEM SPA El contenido se crea en el autor de la, incluido el autor de la creación

  SPA SPA Cuando se edita una con el Editor de en el entorno de creación:

   1. SPA El HTML externo se lo solicita el.
   1. Se carga el CSS.
   1. SPA Se carga el JavaScript de la aplicación de.
   1. SPA Cuando se ejecuta la aplicación de la, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluido el `cq-data` atributos.
   1. El `cq-data` los atributos permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **AEM Publicación de**

  SPA Donde se publican el contenido creado y las bibliotecas compiladas, incluidos los artefactos de aplicación de la aplicación de la aplicación, las bibliotecas de cliente y los componentes, para uso público.

* **Dispatcher/CDN**

  AEM Dispatcher sirve como la capa de almacenamiento en caché de los recursos para los visitantes del sitio.
   * AEM Las solicitudes se procesan de forma similar a como se encuentran en el autor de la. Sin embargo, no se solicita la información de la página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>AEM Dentro de, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM SPA solo aloja los artefactos compilados de la aplicación de la.

## Siguientes pasos {#next-steps}

* [SPA AEM Introducción a la administración de la en React](getting-started-react.md) SPA SPA AEM muestra cómo se crea una básica para trabajar con el Editor de en el uso de React para el uso de la aplicación de react.
* [SPA AEM Introducción a la administración de la en el uso de Angular](getting-started-angular.md) SPA SPA AEM muestra cómo se crea una básica para trabajar con el Editor de en el uso de Angular.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [SPA Proyecto de WKND](wknd-tutorial.md) SPA AEM es un tutorial paso a paso sobre la implementación de un proyecto de simple en el sector de la.
* [SPA Asignación de modelos dinámicos a componentes para la creación de](model-to-component-mapping.md) SPA AEM explica el modelo dinámico para la asignación de componentes y cómo funciona dentro de la asignación de componentes de la interfaz de usuario de la aplicación de datos en la.
* [SPA Modelo de](blueprint.md) SPA AEM SPA AEM ofrece una explicación detallada de cómo funciona el SDK de la para la creación de informes en caso de que desee implementar la implementación de un módulo que no sea React o Angular, en caso de que desee implementar la implementación de un entorno de trabajo que no sea el de la plataforma de trabajo de. O, simplemente, desea una comprensión más profunda.
