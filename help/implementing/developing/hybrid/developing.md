---
title: Desarrollo de SPA para AEM
description: SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una aplicación para el desarrollo de la. AEM SPA SPA AEM También se ofrece una visión general de la arquitectura de los en relación con los aspectos que se deben tener en cuenta a la hora de implementar una implementación de una implementación de un entorno de desarrollo en la que se.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 8%

---

# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder generar sitios usando marcos de SPA y los autores quieren editar contenido dentro de AEM para un sitio generado usando dichos marcos.

SPA AEM AEM SPA AEM Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar un para y ofrece una visión general de la arquitectura de los recursos de la aplicación en relación con la implementación de los programas de desarrollo de software en el entorno de la.

{{ue-over-spa}}

## SPA AEM Principios de desarrollo de la {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. AEM SPA AEM Si, como desarrollador front-end, sigue estas prácticas recomendadas generales y algunos principios específicos de la aplicación, su funciona con [y sus capacidades de creación de contenido](introduction.md#content-editing-experience-with-spa).

* **[Portabilidad](#portability)**: al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing)**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

SPA AEM Si tiene en cuenta estos principios a medida que desarrolle su, se vuelve lo más flexible y lo más seguro posible en el futuro, al tiempo que se habilitan todas las funcionalidades de creación de contenido compatibles.

AEM SPA Si no necesita admitir características de creación de la creación de la, considere la posibilidad de utilizar un [modelo de diseño de la diferente](#spa-design-models).

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

SPA El resultado debe ser construido con componentes altamente portátiles y reutilizables.

### AEM Estructura del sitio de {#aem-drives-site-structure}

SPA El desarrollador front-end debe considerarse a sí mismo como responsable de crear una biblioteca de componentes de que se utilizan para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. AEM [Sin embargo, siempre es propietario de la estructura del sitio](editor-overview.md), por lo que siempre es propietario de la misma.

Este control significa que el desarrollador front-end puede agregar contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar una llamada de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

SPA La solo debe depender de la renderización dinámica del contenido. AEM Esta expectativa es la predeterminada en la que la recupera y procesa todos los elementos secundarios de la estructura de contenido.

AEM Cualquier representación explícita que apunte a contenido específico se considera una representación estática y, aunque se admite, es compatible con las funciones de creación de contenido de los que se dispone en el documento de trabajo, que son compatibles con las de la creación de contenido de la. También va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. AEM SPA AEM En, [la siempre debe ser propietaria del enrutamiento](routing.md) y, a la vez, la escucha y recupera el contenido basado en él, de manera que la escucha de manera correcta.

AEM Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](#portability) y limita al autor al no ser compatible con las características de creación de contenido de los programas de trabajo de los que se puede crear contenido. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, debe pedirle al desarrollador front-end que lo haga.

## Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## SPA Modelos de diseño {#spa-design-models}

SPA AEM SPA AEM Si se siguen los [principios de desarrollo de la en el ](#spa-development-principles-for-aem), entonces su funciona con todas las características de creación de contenido de la admitidas.

Sin embargo, puede haber casos en los que esta funcionalidad no sea completamente necesaria. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se utiliza como CMS SPA sin encabezado sin usar el marco de trabajo de <a href="/help/implementing/developing/hybrid/reference-materials.md">Editor SDK de.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>AEM Los autores de contenido no pueden utilizar la experiencia de creación de contenido de.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El desarrollador front-end utiliza el marco de trabajo de SDK del Editor de, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>AEM Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido que se pueden crear con un contenido de la.</p> <p>El código corre el riesgo de no ser portátil o reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>SPA El proyecto utiliza completamente el SDK AEM del Editor de, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a los.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>AEM El autor del contenido puede editar la aplicación usando la experiencia de creación de contenido que se está usando para la creación de contenido de la.<br /> </p> <p>SPA La plantilla es compatible con el editor de plantillas de.</p> </td>
   <td><p>AEM El desarrollador no controla la estructura de la aplicación ni la parte de contenido delegada a la que se ha delegado la aplicación en el usuario.</p> <p>AEM El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con la ayuda de la herramienta de creación de segmentos de contenido de la aplicación de la aplicación de tipo de.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM SPA SPA AEM Aunque todos los modelos son compatibles con los modelos, solo implementando el tercero (y siguiendo los [principios de desarrollo recomendados](#spa-development-principles-for-aem)) los autores de contenido pueden interactuar con el contenido de la y editarlo en el mismo.

## SPA AEM Migración de recursos existentes a la {#migrating-existing-spas-to-aem}

SPA SPA AEM SPA AEM AEM SPA Por lo general, si el sigue los [Principios de desarrollo de la](#spa-development-principles-for-aem), el funciona en la y es editable mediante el Editor de la.

SPA AEM Siga estos pasos para que pueda preparar sus existentes para trabajar con los recursos de la aplicación de forma más rápida y sencilla

1. **Haga que sus componentes JS sean modulares.**: haga que se puedan procesar en cualquier orden, posición y tamaño.
1. **Use los contenedores proporcionados por SDK para colocar los componentes en la pantalla.AEM**: proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. AEM **Cree un componente de para cada componente JS.AEM**: los componentes de la definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

SPA AEM La tarea principal al involucrar a un desarrollador front-end para crear una para la creación de segmentos es acordar sobre los componentes y sus modelos JSON.

SPA AEM A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una para la creación de segmentos de cliente de tipo

1. **Aceptar componentes y su modelo JSON**

   AEM SPA Los desarrolladores de front-end y de back-end deben acordar qué componentes son necesarios y qué modelo, de modo que haya una coincidencia individualizada entre los componentes de la interfaz de usuario y los componentes de back-end de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario.

   AEM La mayoría de los componentes todavía son necesarios para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En los componentes de React, acceda al modelo a través de`this.props.cqModel`**

   SPA Una vez acordados los componentes y configurado el modelo JSON, el desarrollador front-end es libre de desarrollar el modelo y puede acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el método `render()` del componente**

   El desarrollador front-end implementa el método `render()` como crea conveniente y puede utilizar los campos de la propiedad `cqModel`. Este método genera los fragmentos DOM y HTML que se insertan en la página. Este método es también la forma estándar de crear una aplicación en React.

1. AEM **Asigne el componente al tipo de recurso de a través de`MapTo()`**

   La asignación almacena clases de componentes y el componente `Container` proporcionado la utiliza internamente para recuperar y crear instancias de componentes de forma dinámica en función del tipo de recurso dado.

   Este mapa sirve como &quot;pegamento&quot; entre el front-end y el back-end para que el editor sepa a qué componentes corresponden los componentes de react.

   `Page` y `ResponsiveGrid` son buenos ejemplos de clases que amplían la base `Container`.

1. **Defina `EditConfig` del componente como parámetro para`MapTo()`**

   Este parámetro es necesario para indicar al editor cómo se debe asignar un nombre al componente, siempre que no se haya procesado aún o no tenga contenido para procesar.

1. **Extender la clase `Container` proporcionada para páginas y contenedores**

   Los sistemas de páginas y párrafos deben ampliar esta clase para que la delegación a los componentes internos funcione según lo esperado.

1. **Implementar una solución de enrutamiento que use la API HTML5 `History`.**

   Cuando `ModelRouter` está habilitado, al llamar a las funciones `pushState` y `replaceState` se déclencheur una solicitud a `PageModelManager` para recuperar un fragmento que falta del modelo.

   La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

   `ModelRouter` se puede deshabilitar o configurar para que ignore una lista de expresiones regulares.

## AEM agnóstico {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes React y Angular no necesitan nada que sea específico para el Adobe AEM o la.

* Todo lo que se encuentra dentro del componente JavaScript AEM no es compatible con el uso de la.
* AEM AEM Sin embargo, lo que es específico de la es que el componente JS debe asignarse a un componente de la aplicación de ayuda de MapTo.

AEM ![Enfoque agnóstico](assets/aem-agnostic.png)

El asistente de `MapTo` es el &quot;pegado&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML al HTML SPA que procesa el componente JS, de modo que el Editor de datos sepa qué cuadro de diálogo mostrar al autor al editar el componente.

SPA AEM Para obtener más información sobre el uso de `MapTo` y la generación de la para los usuarios en general, consulte la guía de introducción para el marco de trabajo elegido.

* [SPA AEM Introducción a la administración de la en React](getting-started-react.md)
* [SPA AEM Introducción a la administración de la en Angular](getting-started-angular.md)

## AEM SPA Arquitectura de la y la {#aem-architecture-and-spas}

AEM SPA La arquitectura general de los entornos de desarrollo, creación y publicación, entre otros, no cambia al utilizar la. SPA Sin embargo, es útil comprender cómo encaja el desarrollo de la en esta arquitectura.

AEM SPA ![arquitectura de la y el recurso de la cuenta de usuario ](assets/aem-architecture.png)

* **Entorno de compilación**

  SPA En este entorno es donde se extrae el origen de la aplicación y el componente de la aplicación de la.

   * SPA El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de.
   * AEM Maven se encarga de tomar esa biblioteca e implementarla el complemento de compilación de Maven junto con el componente al autor de la.

* AEM **Autor de**

  AEM SPA El contenido se crea en el autor de la, incluido el autor de la creación

  SPA SPA Cuando se edita una con el Editor de en el entorno de creación:

   1. SPA El HTML externo se lo solicita el.
   1. Se carga el CSS.
   1. Se carga la JavaScript SPA de la aplicación de la.
   1. SPA Cuando se ejecuta la aplicación de, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluidos los atributos `cq-data`.
   1. Los atributos `cq-data` permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* AEM **Publish**

  SPA Donde se publican el contenido creado y las bibliotecas compiladas, incluidos los artefactos de aplicación de la aplicación de la aplicación, las bibliotecas de cliente y los componentes, para uso público.

* **Dispatcher / CDN**

  Dispatcher AEM sirve como capa de almacenamiento en caché de los recursos para los visitantes del sitio.
   * AEM Las solicitudes se procesan de forma similar a como se encuentran en el autor de la. Sin embargo, no se solicita la información de la página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>AEM Dentro de, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM SPA solo aloja los artefactos compilados de la aplicación de la.

## Siguientes pasos {#next-steps}

* SPA AEM SPA SPA AEM [Introducción a la en el uso de React](getting-started-react.md) muestra cómo se crea un básico para trabajar con el Editor de la en el uso de React.
* SPA AEM [Introducción a la en el uso del Angular SPA SPA AEM de trabajo](getting-started-angular.md) muestra cómo se crea un básico para trabajar con el Editor de en el uso del Angular de trabajo de la.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* SPA SPA AEM El [Proyecto de WKND de](wknd-tutorial.md) es un tutorial paso a paso para implementar un proyecto de simple en el área de trabajo de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de.
* SPA SPA AEM [Asignación de modelos dinámicos a componentes para el modelo dinámico para el que se ha asignado el componente ](model-to-component-mapping.md) explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de la asignación de componentes de la de trabajo de la.
* SPA SPA [Modelo de](blueprint.md) ofrece una explicación detallada del funcionamiento de SDK AEM SPA AEM para la en caso de que desee implementar un modelo de trabajo en el que no sea React o Angular, en el caso de que desee implementar un modelo de trabajo en el que se pueda implementar un modelo de trabajo en el que se pueda implementar un modelo de trabajo que no sea el de React o el de. O, simplemente, desea una comprensión más profunda.
