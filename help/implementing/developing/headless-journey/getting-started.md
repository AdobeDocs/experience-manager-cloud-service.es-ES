---
title: Introducción a AEM Headless como Cloud Service
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, obtenga información sobre AEM requisitos previos sin encabezado.
hide: true
hidefromtoc: true
index: false
exl-id: a39877d9-f5a1-48f0-a021-cc9849bd8ecb
source-git-commit: 83ed6295d2b29581025f5410236f2618ceb59012
workflow-type: tm+mt
source-wordcount: '3087'
ht-degree: 0%

---

# Introducción a AEM sin encabezado como Cloud Service {#getting-started}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) obtenga información sobre lo que se necesita para comenzar su propio proyecto con AEM sin encabezado.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido AEM sin encabezado, [Learn About CMS Headless Development](learn-about.md) ha aprendido la teoría básica de lo que es un CMS sin cabeza y ahora debería:

* Comprender los conceptos básicos y la terminología de la entrega de contenido sin encabezado
* Comprender por qué y cuándo se requiere un proceso sin encabezado
* Conocer en un nivel superior cómo se utilizan los conceptos sin encabezado y cómo se interrelacionan

Este artículo se basa en estos fundamentos para que entienda cómo puede utilizar AEM para implementar una solución sin encabezado.

## Objetivo {#objective}

Este documento le ayuda a comprender AEM sin encabezado en el contexto de su propio proyecto. Después de leer, debe:

* Comprender los conceptos básicos de AEM funciones sin encabezado.
* Conozca los requisitos previos para utilizar AEM funciones sin encabezado.
* Tenga en cuenta AEM niveles de integración sin objetivos.
* Puede definir el proyecto en términos de ámbito.

## Conceptos básicos de AEM {#aem-basics}

Para poder definir el proyecto sin encabezado dentro de AEM, es importante comprender algunos conceptos básicos de AEM.

### Instancia de autor {#author}

En su forma más sencilla, AEM consta de una instancia de autor y una [instancia de publicación](#publish) que trabajan juntas para crear, administrar y publicar el contenido.

El contenido comienza en la instancia de autor. Aquí es donde los autores de contenido crean su contenido. El entorno de creación ofrece varias herramientas para que los autores creen, organicen y reutilicen su contenido.

### Instancia de publicación {#publish}

Una vez creado el contenido en la instancia de autor, debe publicarse para que esté disponible para otros servicios que lo consuman. Una instancia de publicación contiene todo el contenido que se ha publicado.

### Replicación {#replication}

La replicación es el acto de transferir contenido de la instancia de autor a la instancia de publicación. Esto se hace automáticamente AEM cuando un autor u otro usuario con los derechos adecuados publica contenido.

### Resumen básico de AEM {#aem-basics-summary}

En su nivel más sencillo, la creación de experiencias digitales en AEM requiere los siguientes pasos:

1. Los autores de contenido crearán su contenido sin encabezado en la instancia de autor.
1. Cuando este contenido está listo, se replica en la instancia de publicación.
1. Luego se puede llamar a las API para recuperar este contenido.

AEM sin encabezado se basa en esta base técnica al ofrecer poderosas herramientas para administrar el contenido sin encabezado que se [describe en la siguiente sección.](#aem-headless-basics)

## Conceptos básicos AEM sin encabezado {#aem-headless-basics}

Las capacidades sin objetivos de AEM se basan en algunas funciones clave. Estas se explicarán en detalle en las partes posteriores del recorrido. Ahora sólo es importante conocer los conceptos básicos de lo que hacen y cómo se llaman.

### Modelos de fragmento de contenido {#content-fragment-models}

Los modelos de fragmento de contenido definen la estructura de los datos y el contenido que creará y administrará en AEM. Sirven como un tipo de andamiaje para el contenido. Al elegir crear contenido, los autores seleccionarán entre los modelos de fragmento de contenido que defina, que los guiarán en la creación de contenido.

### Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido le permiten diseñar, crear, depurar y publicar contenido independiente de las páginas. Permiten preparar contenido listo para usar en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

### API de GraphQL y REST {#apis}

Para modificar el contenido sin problemas, AEM ofrece dos API sólidas.

* La API de GraphQL permite crear solicitudes para acceder a los fragmentos de contenido y enviarlos.
* La API de REST de recursos permite crear y modificar fragmentos de contenido (y otros recursos).

Aprenderá a utilizar estas API en una parte posterior del recorrido sin AEM encabezado. O consulte la sección [recursos adicionales](#additional-resources) a continuación para obtener documentación adicional.

## Niveles de integración sin encabezado {#integration-levels}

AEM admite todos los modelos sin encabezado y los modelos tradicionales de pila completa o de cabeza de un CMS. Sin embargo, AEM ofrece no solo estas dos opciones exclusivas, sino también la capacidad de soportar modelos híbridos que combinan las ventajas de ambos, ofreciendo una flexibilidad única para su proyecto sin objetivos.

Con el fin de garantizar su comprensión de los conceptos sin objetivos, este Recorrido para desarrolladores AEM sin objetivos se centra en el modelo sin objetivos para ponerle en marcha lo antes posible sin necesidad de utilizar código en AEM.

Sin embargo, hay que tener en cuenta las posibilidades híbridas adicionales que se abren una vez que entienda AEM características sin periféricos. Presentamos estos casos a continuación para su conciencia. Al final del recorrido, se le introducirá en estos conceptos con más detalle en caso de que se requiera dicha flexibilidad para su proyecto.

### Ya tiene un consumo externo de contenido sin encabezado, como una aplicación de página única (SPA). {#already-have-a-spa}

Supongamos que su requisito básico es, como mínimo, entregar contenido de AEM a un servicio externo existente.

#### Nivel 1: Integración de fragmentos de contenido: modelo tradicional sin encabezado {#level-1}

Este nivel de integración es el modelo tradicional sin encabezado y permite a los autores de contenido crear contenido en AEM y ofrecerlo sin preocuparse por cualquier número de servicios externos mediante GraphQL o editarlos desde servicios externos mediante la API de Assets. No se requiere código en AEM.

En este modelo, AEM solo se utiliza para crear y servir el contenido mediante el uso de fragmentos de contenido AEM. El procesamiento y la interacción con el contenido se delegan en la aplicación externa consumidora, a menudo en una aplicación de una sola página (SPA).

#### Nivel 2: Incrustar el SPA en AEM - Modelo híbrido {#level-2}

Este nivel de integración se basa en el primer nivel, pero también permite que la aplicación externa (SPA) se incruste en AEM para que los autores de contenido puedan ver el contenido en el contexto de la aplicación externa dentro de AEM. La aplicación también puede admitir una edición limitada de la aplicación externa dentro de AEM.

Este nivel tiene la ventaja de permitir que los autores de contenido creen contenido de forma flexible de AEM de forma progresiva, con su contenido presentado en contexto con una SPA externa integrada, a la vez que siguen entregando el contenido sin problemas.

#### Nivel 3: Incrustar y activar completamente SPA en AEM - Modelo híbrido {#level-3}

Este nivel de integración se basa en el nivel dos al permitir que la mayoría del contenido de la SPA externa se pueda editar dentro de AEM.

### Todavía no tiene un consumidor externo del contenido sin encabezado, como una aplicación de una sola página (SPA). {#do-not-have-a-spa}

Si su objetivo es crear un nuevo SPA que consuma contenido sin encabezado desde AEM, puede utilizar funciones como Fragmentos de contenido para administrar el contenido sin encabezado y también generar un SPA con AEM marco de Editor SPA.

Con el Editor de SPA, el SPA no solo consume contenido de AEM, sino que también es totalmente editable dentro de AEM por los autores de contenido, lo que le ofrece la flexibilidad de envío sin periféricos y de edición en contexto dentro de AEM.

## Requisitos y requisitos previos {#requirements-prerequisites}

Hay varios requisitos antes de comenzar su proyecto de AEM sin encabezado.

### Conocimiento {#knowledge}

* GraphQL
* Experiencia de desarrollo crear SPA con marcos de React o Angular
* Capacidades básicas AEM crear fragmentos de contenido y utilizar el editor

### Herramientas {#tools}

* Acceso a espacio aislado para probar la implementación de su proyecto
* Instancia de desarrollo local para modelado y prueba de datos
* SPA externa existente u otro consumidor de su contenido AEM sin encabezado

## Definición del proyecto {#defining-your-project}

Para que cualquier proyecto tenga éxito, es importante definir claramente no sólo los requisitos del proyecto, sino también las funciones y responsabilidades.

### Ámbito {#scope}

Es muy importante tener un ámbito claramente definido para el proyecto. El ámbito informa los criterios de aceptación y le permite establecer una definición de hecho.

La primera pregunta que debe hacerse es &quot;¿Qué estoy tratando de lograr con AEM sin cabeza?&quot; La respuesta debe ser, en general, que tiene o tendrá en el futuro una aplicación de experiencia que ha creado con sus propias herramientas de desarrollo, no junto con AEM. Esta aplicación de experiencia puede ser una aplicación móvil, un sitio web o cualquier otra aplicación de experiencia de cara al cliente del usuario final. El objetivo de utilizar AEM sin encabezado es alimentar su aplicación de experiencia con contenido creado, almacenado y administrado en AEM con API de última generación que llamarían a AEM sin encabezado para recuperar contenido o incluso contenido completamente CRUD directamente desde su aplicación de experiencia. Si esto no es lo que está buscando hacer, probablemente desee [volver a la documentación de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) y encontrar la sección que mejor se adapte a lo que desea lograr.

### Funciones y responsabilidades {#roles-responsibilities}

Las funciones de cualquier proyecto individual variarán, pero las importantes que se deben tener en cuenta en el contenido de AEM desarrollo sin objetivos son:

* [Administrador](#administrator)
* [Autor de contenido](#content-author)
* [Modelador de contenido](#content-modeler)
* [Desarrollador](#developer)

#### Administrador {#administrator}

El administrador es responsable de la configuración y configuración base de su sistema. Por ejemplo, el administrador configurará su organización dentro del sistema de administración de usuarios de Adobe, denominado Sistema Identity Management (IMS). El administrador será el primer usuario de la organización en recibir una invitación por correo electrónico de Adobe una vez que su organización haya sido creada por el Adobe dentro de IMS. El administrador podrá iniciar sesión en IMS y agregar usuarios de otras personas.

Una vez que el administrador haya configurado los usuarios, se les otorgarán los permisos para acceder a todos los recursos de AEM para realizar su trabajo como contribuyentes a la entrega de la aplicación de experiencia mediante AEM sin encabezado.

El administrador debe ser el usuario que configure AEM y prepare el entorno de tiempo de ejecución para permitir a [autores de contenido](#content-author) crear y actualizar contenido y a [desarrolladores](#developer) utilizar API que recuperen o modifiquen contenido para sus aplicaciones de experiencia.

#### Autor de contenido {#content-author}

Los autores de contenido crean y administran el contenido que AEM entrega sin encabezado. Los autores de contenido utilizan funciones AEM, como los fragmentos de contenido y la consola Recursos, para administrar su contenido.

Los autores de contenido deben tener en cuenta las siguientes prácticas recomendadas.

#### Plan de localización {#localization}

Planifique la traducción y localización al principio del proyecto. Considere &quot;Internationalization Project Manager&quot; como una persona independiente cuya responsabilidad es definir qué contenido debe traducirse y qué no, y qué contenido traducido pueden modificar los productores de contenido regionales o locales.

Cree un plan sobre la localización de contenido que necesitará.

* ¿Solo necesita idiomas diferentes o también un idioma para adoptar los detalles regionales?
* ¿Necesita contenido multimedia enriquecido como imágenes o vídeos para que sea diferente en diferentes configuraciones regionales?

Obtenga información clara sobre el flujo de trabajo de actualización de contenido. ¿Cuál es el proceso de aprobación que el sistema necesita admitir? ¿Se pueden aprovechar AEM flujos de trabajo para automatizar este proceso?

Tenga en cuenta que la [jerarquía de contenido](#content-hierarchy) se puede aprovechar para facilitar la localización.

Consulte la sección [recursos adicionales](#additional-resources) para obtener documentación adicional sobre AEM flujos de trabajo y herramientas de localización.

##### Aprovechar la jerarquía de contenido {#content-hierarchy}

La jerarquía de carpetas puede abordar dos preocupaciones principales con respecto a la administración de contenido:

* [Localización](#localization) : AEM administra la localización del contenido manteniendo copias del contenido en carpetas específicas de la configuración regional.
* Organización: las carpetas se utilizan para definir la jerarquía de contenido necesaria para satisfacer las necesidades de localización, así como para administrar lógicamente los fragmentos de contenido.

AEM permite una estructura de contenido muy flexible y una jerarquía puede ser arbitrariamente grande. Sin embargo, es importante darse cuenta de que cualquier cambio en la estructura de carpetas puede tener consecuencias no deseadas para las consultas existentes que [dependen de la ruta de contenido.](#developer) Por lo tanto, una jerarquía bien definida y claramente establecida por adelantado, puede resultar extremadamente útil para los autores de contenido.

Las carpetas también se pueden restringir para permitir solo ciertos tipos de contenido (según los modelos de fragmento de contenido). Por lo general, se recomienda especificar siempre explícitamente qué modelos se permiten para todas las carpetas de la jerarquía. Especificación del contenido permitido para una carpeta determinada:

* Evita que los autores de contenido creen contenido que no pertenece a la carpeta.
* Optimiza el proceso de creación de contenido filtrando los tipos de contenido permitidos en la carpeta durante la creación para mostrar solo tipos de contenido válidos.

Al crear una estructura de contenido adecuada, resulta más fácil coordinar la creación de contenido sin encabezado en todos los canales para maximizar la reutilización de contenido. El aprovechamiento del contenido en varios canales mejorará considerablemente la eficacia de la producción de contenido y la administración de cambios.

##### Establecer convenciones de nombres correctos {#naming-conventions}

Los nombres de los fragmentos de contenido deben ser descriptivos para los autores de contenido. AEM gestiona de forma transparente la omisión o el truncamiento de los nombres que usan los ID en el nivel del repositorio. Por lo tanto, los nombres lógicos proporcionados por los autores de contenido siempre deben ser legibles y representar el contenido.

* Nombre incorrecto: `cta_btn_1`
* Nombre correcto: `Call To Action Button`

Consulte la sección [recursos adicionales](#additional-resources) para obtener documentación adicional sobre AEM convenciones de nomenclatura de páginas.

##### No amplíe el anidado de contenido {#content-nesting}

[Los ](#content-fragments) fragmentos de contenido se utilizan en AEM para crear contenido sin encabezado. AEM admite hasta diez niveles de anidación de contenido para fragmentos de contenido. Sin embargo, es importante tener en cuenta que AEM tendrá que resolver de forma iterativa cada referencia definida en el fragmento de contenido principal y, a continuación, comprobar si hay alguna referencia secundaria en todos los elementos del mismo nivel. Estas operaciones pueden sumarse rápidamente y convertirse en un problema de rendimiento.

Como regla general, las referencias de fragmento de contenido no deben anidarse más allá de cinco niveles.

#### Modelador de contenido {#content-modeler}

Los modeladores de contenido analizan los requisitos de los datos que deben entregarse sin problemas y definen la estructura de estos datos. Estas estructuras se denominan [Modelos de fragmento de contenido](#content-fragment-models) en AEM. Los modelos de fragmento de contenido se utilizan como base para los fragmentos de contenido que crean los autores de contenido.

Un enfoque útil a la hora de definir modelos de fragmento de contenido es crear modelos que se asignen a los componentes UX de las aplicaciones que consuman el contenido.

Dado que los autores de contenido interactúan con los modelos de forma continua a medida que crean contenido nuevo, alinear los modelos con el usuario les ayuda a visualizar la experiencia digital resultante. Siguiendo con esta alineación, puede asignar iconos a los modelos de fragmento de contenido que representan el elemento UX para que los autores puedan seleccionar de forma intuitiva el modelo correcto en función de las indicaciones visuales.

#### Desarrollador {#developer}

Los desarrolladores son responsables de unir el contenido que se crea sin problemas en AEM al consumidor de ese contenido, que a menudo puede ser una aplicación de una sola página (SPA), una aplicación web progresiva (PWA), una tienda web u otro servicio externo a AEM.

GraphQL sirve de &quot;pegamento&quot; entre AEM y los consumidores de contenido sin encabezado. GraphQL es el idioma que consulta AEM el contenido necesario.

Los desarrolladores deben tener en cuenta algunas recomendaciones básicas al planificar sus consultas:

* Las consultas no deben depender de una ruta fija (`ByPath`) para recuperar los fragmentos de contenido.
   * [Los autores de contenido tienen control total sobre la ](#content-hierarchy) jerarquía de fragmentos de contenido y podrían realizar cambios para romper dicha consulta.
   * Las consultas deben optar por referencias del modelo de fragmento de contenido con parámetros de consulta dinámicos para filtrar los resultados y generar la carga útil deseada.
* Para obtener el mejor rendimiento de las consultas, utilice siempre consultas persistentes en AEM. Estos se discuten más adelante en el recorrido.
* GraphQL está diseñado para ser declarativo siguiendo el lema &quot;Pide exactamente lo que necesitas, y consigue exactamente eso&quot;. Esto significa que, al crear consultas de GraphQL, evite siempre las consultas de tipo `select *` que pueda crear en una base de datos relacional.

Para una [implementación típica sin encabezado que utiliza AEM,](#level-1) el desarrollador no necesita tener conocimientos de codificación de AEM.

### Requisitos de rendimiento {#performance-requirements}

Para que cualquier proyecto sea un éxito, el rendimiento debe tenerse en cuenta antes de crear cualquier contenido.

Debe comprender las expectativas de los usuarios/visitantes y diseñar para ellos. Establezca objetivos de nivel de servicio (SLO) y mida para comprender si cumple con las expectativas del usuario.

#### Patrones de tráfico {#traffic-patterns}

Para comprender los patrones de tráfico y tráfico, comience por reunir lo que sabe del pasado y luego proyectar el crecimiento esperado en los próximos años. Algunas de las variables más importantes a tener en cuenta:

* ¿Cuántas llamadas a la API por hora/día/mes espera y hay potencial para picos y temporalidad?
* ¿Cuántos autores de contenido diferentes hay?
* ¿Cuántos autores de contenido espera que trabajen simultáneamente?
* ¿Cuál es la frecuencia de las actualizaciones de contenido?
* ¿Cuántos modelos de contenido se necesitan?
* ¿Cuántas instancias de modelos se necesitarán?

#### Frecuencia de actualización {#update-frequency}

Con mucha frecuencia, las secciones de experiencias diferentes tienen distintas frecuencias de actualizaciones de contenido. Comprender esto es importante para poder ajustar las configuraciones de CDN y caché. Esto también es importante para los [Modeladores de contenido](#content-modeler), ya que diseñan modelos para representar su contenido. Tenga en cuenta lo siguiente:

* ¿Deben caducar algunos tipos de contenido después de un período determinado?
* ¿Hay elementos específicos del usuario que no se pueden almacenar en caché?

## Siguientes {#what-is-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Comprender los conceptos básicos de AEM funciones sin encabezado.
* Conozca los requisitos previos para utilizar AEM funciones sin encabezado.
* Tenga en cuenta AEM niveles de integración sin objetivos.
* Puede definir el proyecto en términos de ámbito.

Debe continuar con el recorrido sin AEM al revisar el documento [Ruta a la primera experiencia con AEM sin encabezado](path-to-first-experience.md), donde aprenderá a configurar las herramientas necesarias y a empezar a pensar en modelar los datos en AEM.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de desarrollo sin encabezado revisando el documento [Ruta a la primera experiencia usando AEM sin encabezado,](path-to-first-experience.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no es necesario que continúen en el recorrido sin encabezado.

* [Introducción a la arquitectura de Adobe Experience Manager como Cloud Service](/help/core-concepts/architecture.md) : Comprender AEM como estructura de Cloud Service
* [AEM Tutorials sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) : utilice estos tutoriales prácticos para explorar cómo utilizar las distintas opciones para enviar contenido a puntos de conexión sin encabezado con AEM y elija lo que es adecuado para usted.
* [Administración de contenido sin objetivos mediante las API de GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) : siga este curso para obtener información general sobre la API de GraphQL implementada en AEM. Se requiere autenticación mediante Adobe ID.
* [AEM Guías WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) : este proyecto de GitHub incluye aplicaciones de ejemplo que destacan las API de GraphQL AEM.
* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md) : documentación técnica para el entorno de creación de AEM que incluye detalles sobre la configuración de creación y publicación
* [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) : Documentación técnica para la publicación de contenido en AEM
* [Convenciones de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md) : documentación técnica de las restricciones de nomenclatura de páginas en AEM
* [Multi Site Manager y traducción](/help/sites-cloud/administering/msm-and-translation.md) : documentación técnica sobre AEM potentes funciones de traducción
* [Flujos de trabajo AEM](/help/sites-cloud/authoring/workflows/overview.md) : Documentación técnica sobre cómo automatizar flujos de trabajo en AEM
* [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : documentación técnica para fragmentos de contenido.
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) : documentación técnica para modelos de fragmento de contenido.
* [Documentación técnica de GraphQL](https://graphql.org) : definición de GraphQL (vínculo externo)
* [API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) : documentación técnica que explica cómo crear solicitudes para acceder y enviar fragmentos de contenido
* [API de REST de recursos](/help/assets/content-fragments/assets-api-content-fragments.md) : documentación técnica que explica cómo crear y modificar fragmentos de contenido (y otros recursos)
* [Consultas persistentes](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) : documentación técnica sobre consultas persistentes en AEM
* [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) : un análisis completo de los niveles de integración sin objetivos disponibles en AEM
