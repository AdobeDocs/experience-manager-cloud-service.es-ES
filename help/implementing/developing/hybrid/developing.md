---
title: Desarrollo de SPA para AEM
description: Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una SPA para AEM. También ofrece una descripción general de la arquitectura de AEM en relación con las SPA que se deben tener en cuenta al implementar una SPA desarrollada en AEM.
exl-id: f6c6f31a-69ad-48f6-b995-e6d0930074df
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 8%

---


# Desarrollo de SPA para AEM {#developing-spas-for-aem}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder generar sitios usando marcos de SPA y los autores quieren editar contenido dentro de AEM para un sitio generado usando dichos marcos.

Este artículo presenta preguntas importantes que se deben tener en cuenta al contratar a un desarrollador front-end para desarrollar una SPA para AEM y ofrece una visión general de la arquitectura de AEM en relación con la implementación de SPA en AEM.

{{ue-over-spa}}

## Principios de desarrollo de SPA para AEM {#spa-development-principles-for-aem}

El desarrollo de aplicaciones de una sola página en AEM supone que el desarrollador front-end sigue las prácticas recomendadas estándar al crear una SPA. Si como desarrollador front-end sigue estas prácticas recomendadas generales y algunos principios específicos de AEM, su SPA funciona con [AEM y sus capacidades de creación de contenido](introduction.md#content-editing-experience-with-spa).

* **[Portabilidad](#portability)**: al igual que con cualquier componente, los componentes deben crearse para que sean lo más portátiles posible. La SPA debe crearse con componentes transferibles y reutilizables.
* **[AEM impulsa la estructura del sitio](#aem-drives-site-structure)**: el desarrollador front-end crea componentes y posee su estructura interna, pero depende de AEM para definir la estructura de contenido del sitio.
* **[Procesamiento dinámico](#dynamic-rendering)**: todo el procesamiento debe ser dinámico.
* **[Enrutamiento dinámico](#dynamic-routing)**: la SPA es responsable del enrutamiento, y AEM la atiende y recupera en función de esta. Cualquier enrutamiento también debe ser dinámico.

Si tiene en cuenta estos principios al desarrollar la SPA, esta se vuelve lo más flexible y segura posible de cara al futuro, al tiempo que se habilitan todas las funcionalidades de creación de AEM admitidas.

Si no necesita admitir características de creación de AEM, considere un [modelo de diseño de SPA](#spa-design-models) diferente.

### Portabilidad {#portability}

Al igual que al desarrollar cualquier componente, los componentes deben diseñarse de tal manera que maximice su portabilidad. Debe evitarse cualquier patrón que vaya en contra de la portabilidad o reutilización de los componentes para garantizar la compatibilidad, flexibilidad y capacidad de mantenimiento en el futuro.

El SPA resultante debe crearse con componentes altamente portátiles y reutilizables.

### Estructura del sitio de unidades AEM {#aem-drives-site-structure}

El desarrollador front-end debe considerarse responsable de crear una biblioteca de componentes de SPA utilizados para crear la aplicación. El desarrollador front-end tiene un control total de la estructura interna de los componentes. [Sin embargo, AEM siempre posee la estructura del sitio](editor-overview.md).

Este control significa que el desarrollador front-end puede agregar contenido de cliente antes o después del punto de entrada de los componentes y también puede realizar una llamada de terceros dentro del componente. Sin embargo, el desarrollador front-end no tiene control total sobre cómo anidan los componentes, por ejemplo.

### Procesamiento dinámico {#dynamic-rendering}

La SPA solo debe depender de la renderización dinámica del contenido. Esta expectativa es la predeterminada en la que AEM recupera y procesa todos los elementos secundarios de la estructura de contenido.

Cualquier representación explícita que apunte a contenido específico se considera una representación estática y, aunque se admite, es compatible con las funciones de creación de contenido de AEM. También va en contra del principio de [portabilidad](#portability).

### Enrutamiento dinámico {#dynamic-routing}

Al igual que con el procesamiento, todo el enrutamiento también debe ser dinámico. En AEM, [la SPA siempre debe ser propietaria del enrutamiento](routing.md), y AEM lo escucha y recupera contenido basado en él.

Cualquier enrutamiento estático funciona en contra del [principio de portabilidad](#portability) y limita al autor al no ser compatible con las características de creación de contenido de AEM. Por ejemplo, con el enrutamiento estático, si el autor de contenido desea cambiar una ruta o cambiar una página, debe pedirle al desarrollador front-end que lo haga.

## Arquetipo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Modelos de diseño SPA {#spa-design-models}

Si se siguen los [principios del desarrollo de SPA en AEM](#spa-development-principles-for-aem), su SPA funcionará con todas las funciones de creación de contenido de AEM admitidas.

Sin embargo, puede haber casos en los que esta funcionalidad no sea completamente necesaria. En la tabla siguiente se ofrece una descripción general de los distintos modelos de diseño, sus ventajas y sus desventajas.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de diseño<br /> </strong></th>
   <th><strong>Ventajas</strong></th>
   <th><strong>Desventajas</strong></th>
  </tr>
  <tr>
   <td>AEM se usa como CMS sin encabezado sin usar el marco de trabajo <a href="/help/implementing/developing/hybrid/reference-materials.md">SPA Editor SDK.</a></td>
   <td>El desarrollador front-end tiene control total sobre la aplicación.</td>
   <td><p>Los autores de contenido no pueden utilizar la experiencia de creación de contenido de AEM.</p> <p>El código no es portátil ni reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El desarrollador front-end utiliza el marco de trabajo de SDK del Editor SPA, pero solo abre algunas áreas al autor del contenido.</td>
   <td>El desarrollador mantiene el control de la aplicación y solo permite la creación en áreas restringidas de la aplicación.</td>
   <td><p>Los autores de contenido están restringidos a un conjunto limitado de experiencias de creación de contenido de AEM.</p> <p>El código corre el riesgo de no ser portátil o reutilizable si contiene referencias estáticas o enrutamiento.</p> <p>No permite el uso del editor de plantillas, por lo que el desarrollador front-end debe mantener plantillas editables a través de JCR.</p> </td>
  </tr>
  <tr>
   <td>El proyecto utiliza completamente la SDK del Editor de SPA, y los componentes de front-end se desarrollan como una biblioteca y la estructura de contenido de la aplicación se delega a AEM.</td>
   <td><p>La aplicación es reutilizable y portátil.</p> <p>El autor del contenido puede editar la aplicación con la experiencia de creación de contenido de AEM.<br /> </p> <p>La SPA es compatible con el editor de plantillas.</p> </td>
   <td><p>El desarrollador no controla la estructura de la aplicación ni la parte del contenido delegado a AEM.</p> <p>El desarrollador puede seguir reservando áreas de la aplicación para el contenido que no vaya a crearse con AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Aunque todos los modelos son compatibles con AEM, solo implementando el tercero (y siguiendo los [principios de desarrollo de SPA](#spa-development-principles-for-aem) recomendados) los autores de contenido pueden interactuar con el contenido de SPA en AEM y editarlo.

## Migración de SPA existentes a AEM {#migrating-existing-spas-to-aem}

Por lo general, si su SPA sigue los [Principios de desarrollo de SPA para AEM](#spa-development-principles-for-aem), su SPA funciona en AEM y se puede editar con el Editor de SPA de AEM.

Siga estos pasos para poder preparar su SPA existente para trabajar con AEM.

1. **Haga que sus componentes JS sean modulares.**: haga que se puedan procesar en cualquier orden, posición y tamaño.
1. **Use los contenedores proporcionados por SDK para colocar los componentes en la pantalla.**: AEM proporciona un componente del sistema de páginas y párrafos para que lo utilice.
1. **Cree un componente de AEM para cada componente JS.**: los componentes de AEM definen el cuadro de diálogo y la salida JSON.

## Instrucciones para desarrolladores de front-end {#instructions-for-front-end-developers}

La tarea principal al involucrar a un desarrollador front-end para crear una SPA para AEM es acordar los componentes y sus modelos JSON.

A continuación se describen los pasos que debe seguir un desarrollador front-end al desarrollar una SPA para AEM.

1. **Aceptar componentes y su modelo JSON**

   Los desarrolladores de front-end y de back-end de AEM deben acordar qué componentes son necesarios y un modelo, de modo que haya una coincidencia individualizada entre los componentes de SPA y los componentes de back-end.

   Los componentes de AEM siguen siendo necesarios principalmente para proporcionar cuadros de diálogo de edición y para exportar el modelo de componente.

1. **En los componentes de React, acceda al modelo a través de`this.props.cqModel`**

   Una vez acordados los componentes y configurado el modelo JSON, el desarrollador front-end puede desarrollar la SPA y simplemente acceder al modelo JSON a través de `this.props.cqModel`.

1. **Implementar el método `render()` del componente**

   El desarrollador front-end implementa el método `render()` como crea conveniente y puede utilizar los campos de la propiedad `cqModel`. Este método genera los fragmentos DOM y HTML que se insertan en la página. Este método es también la forma estándar de crear una aplicación en React.

1. **Asigne el componente al tipo de recurso de AEM mediante`MapTo()`**

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

## AEM-Agnostic {#aem-agnostic}

Estos bloques de código ilustran cómo los componentes de React y Angular no necesitan nada específico de Adobe o AEM.

* Todo lo que se encuentra dentro del componente JavaScript no depende de AEM.
* Sin embargo, lo que es específico de AEM es que el componente JS debe asignarse a un componente AEM con el asistente de MapTo.

![Enfoque no basado en AEM](assets/aem-agnostic.png)

El asistente de `MapTo` es el &quot;pegado&quot; que permite hacer coincidir los componentes del back-end y del front-end:

* Indica al contenedor de JS (o sistema de párrafos de JS) qué componente de JS es responsable de procesar cada uno de los componentes presentes en el JSON.
* Agrega un atributo de datos de HTML a HTML que procesa el componente JS, de modo que el Editor de SPA sepa qué cuadro de diálogo mostrar al autor al editar el componente.

Para obtener más información sobre el uso de `MapTo` y la creación de SPA para AEM en general, consulte la guía de introducción para el marco de trabajo elegido.

* [Introducción a SPA en AEM con React](getting-started-react.md)
* [Introducción a SPA en AEM con Angular](getting-started-angular.md)

## Arquitectura de AEM y SPA {#aem-architecture-and-spas}

La arquitectura general de AEM, incluidos los entornos de desarrollo, creación y publicación, no cambia al utilizar SPA. Sin embargo, es útil comprender cómo encaja el desarrollo de SPA en esta arquitectura.

![Arquitectura de AEM y SPA](assets/aem-architecture.png)

* **Entorno de compilación**

  En este entorno es donde se extrae el origen de la aplicación SPA y del componente.

   * El generador clientlib de NPM crea una biblioteca de cliente a partir del proyecto de SPA.
   * Esa biblioteca la toma Maven y la implementa el complemento de compilación de Maven junto con el componente al autor de AEM.

* **Autor de AEM**

  El contenido se crea en el autor de AEM, incluidas las SPA de creación.

  Cuando se edita una SPA con el Editor de SPA en el entorno de creación:

   1. La SPA solicita la HTML externa.
   1. Se carga el CSS.
   1. Se carga la JavaScript de la aplicación SPA.
   1. Cuando se ejecuta la aplicación SPA, se solicita el JSON, lo que permite a la aplicación crear el DOM de la página, incluidos los atributos `cq-data`.
   1. Los atributos `cq-data` permiten al editor cargar información de página adicional para saber qué configuraciones de edición están disponibles para los componentes.

* **Publicación de AEM**

  Donde el contenido creado y las bibliotecas compiladas, incluidos los artefactos de la aplicación SPA, las bibliotecas de cliente y los componentes, se publican para el consumo público.

* **Dispatcher / CDN**

  Dispatcher sirve como capa de almacenamiento en caché de AEM para los visitantes del sitio.
   * Las solicitudes se procesan de forma similar a como se encuentran en AEM Author. Sin embargo, no se solicita la información de la página porque solo la necesita el editor.
   * JavaScript, CSS, JSON y HTML se almacenan en caché, lo que optimiza la página para una entrega rápida.

>[!NOTE]
>
>Dentro de AEM, no es necesario ejecutar los mecanismos de compilación de JavaScript ni ejecutar el propio JavaScript. AEM solo aloja los artefactos compilados de la aplicación SPA.

## Siguientes pasos {#next-steps}

* [Introducción a SPA en AEM con React](getting-started-react.md) muestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM con React.
* [Introducción a SPA en AEM con Angular](getting-started-angular.md) muestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM con Angular.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [Proyecto de SPA de WKND](wknd-tutorial.md) es un tutorial paso a paso para implementar un proyecto de SPA simple en AEM.
* [Asignación de modelos dinámicos a componentes para SPA](model-to-component-mapping.md) explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de SPA en AEM.
* [Modelo SPA](blueprint.md) proporciona una explicación detallada del funcionamiento de SPA SDK para AEM en caso de que desee implementar SPA en AEM para un módulo que no sea React o Angular. O, simplemente, desea una comprensión más profunda.
