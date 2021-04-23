---
title: Cómo modelar el contenido
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a modelar el contenido para AEM envío sin encabezado mediante el modelado de datos con modelos de fragmentos de contenido y fragmentos de contenido.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 5fd190b50f52a3182365a31e1539c5864f42afb4
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 2%

---


# Cómo modelar el contenido {#model-your-content}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado](#overview.md), puede aprender a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales.

## La historia hasta ahora {#story-so-far}

Al principio [Obtenga información sobre el desarrollo sin encabezado de CMS](learn-about.md) abarcaba el envío de contenido sin encabezado y por qué debería usarse. A continuación, [Introducción a AEM sin encabezado como Cloud Service](getting-started.md) describió AEM sin encabezado en el contexto de su propio proyecto

En el documento anterior del recorrido sin AEM encabezado, [Ruta a la primera experiencia con AEM sin encabezado](/help/implementing/developing/headless-journey/path-to-first-experience.md), se han aprendido los pasos necesarios para implementar el primer proyecto. Después de leerlo, debe:

* Comprender las consideraciones de planificación importantes para diseñar el contenido
* Comprender los pasos para implementar sin encabezado según los requisitos de nivel de integración.
* Configure las herramientas y configuraciones de AEM necesarias.
* Conozca las prácticas recomendadas para que su recorrido sin objetivos sea fluido, mantenga la eficiencia de la generación de contenido y asegúrese de que el contenido se entregue rápidamente.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio AEM proyecto sin objetivos.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Aprenda a modelar la estructura de contenido y luego a comprender esa estructura utilizando AEM modelos de fragmentos de contenido y fragmentos de contenido:
   * Introduzca conceptos y terminología relacionados con el [modelado de datos](#data-modeling).
   * Aprenda [por qué se necesita el modelado de datos para el envío de contenido sin encabezado](#data-modeling-for-aem-headless).
   * Aprenda [a realizar esta estructura utilizando AEM modelos de fragmento de contenido](#create-structure-content-fragment-models) (y cree contenido con [fragmentos de contenido](#use-content-to-author-content)).
   * Aprenda [a modelar su contenido](#getting-started-examples); principios con muestras básicas.

>[!NOTE]
>
>El modelado de datos es un campo muy grande, ya que se utiliza al desarrollar bases de datos relacionales. Hay muchos libros, y fuentes de información en línea, disponibles.
>
>Solo se tendrán en cuenta los aspectos que son de interés al modelar datos para su uso con AEM sin encabezado.

## Modelado de datos {#data-modeling}

*Es un gran mundo malo allá afuera*.

Tal vez, quizás no, pero ciertamente es un mundo ***complicado*** y el modelado de datos se utiliza para definir una representación simplificada de una subsección muy (muy) pequeña, utilizando la información específica que se necesita para un determinado propósito.

Por ejemplo:

Hay muchas escuelas, pero todas tienen varias cosas en común:

* Una ubicación
* Un profesor jefe
* Muchos profesores
* Muchos miembros del personal no docente
* Muchos alumnos
* Muchos ex profesores
* Muchos ex alumnos
* Muchas aulas
* Muchos (muchos) libros
* Muchos (muchos) equipos
* Muchas actividades extracurriculares
* y así sucesivamente....

Incluso en un ejemplo tan pequeño la lista puede parecer interminable. Pero si simplemente desea que la aplicación realice una tarea sencilla, debe limitar la información a lo esencial.

Por ejemplo, la publicidad de eventos especiales para todas las escuelas de la zona:

* Nombre del colegio
* Ubicación del colegio
* Profesor jefe
* Tipo de evento
* Fecha del evento
* Profesor organizando el evento

### Conceptos {#concepts}

Lo que desea describir se denomina **Entities**, básicamente las &quot;cosas&quot; sobre las que queremos almacenar información.

La información que queremos almacenar sobre ellos son los **Atributos** (propiedades), como Nombre y Cualificaciones para los profesores.

Luego hay varias **Relaciones** entre las entidades. Por ejemplo, normalmente una escuela tiene un solo profesor jefe y muchos maestros (y normalmente el profesor jefe también es profesor).

El proceso de análisis y definición de esta información, junto con las relaciones entre ellos, se denomina **Modelado de datos**.

### Datos básicos {#basics}

A menudo, es necesario empezar por elaborar un **Esquema conceptual** que describa las entidades y sus relaciones. Normalmente es de alto nivel (conceptual).

Una vez estable, puede traducir los modelos a un **Esquema lógico** que describa las entidades, junto con los atributos y las relaciones. En este nivel, debe examinar detenidamente las definiciones para eliminar la duplicación y optimizar el diseño.

>[!NOTE]
>
>A veces, estos dos pasos se combinan, a menudo según la complejidad del escenario.

Por ejemplo, ¿necesita entidades independientes para `Head Teacher` y `Teacher` o simplemente un atributo adicional en el modelo `Teacher`?

### Garantizar la integridad de los datos {#data-integrity}

La integridad de los datos es necesaria para garantizar la precisión y coherencia del contenido durante todo su ciclo de vida. Esto incluye garantizar que los autores de contenido puedan comprender fácilmente qué almacenar, por lo que lo siguiente es vital:

* una estructura clara
* una estructura lo más concisa posible (sin sacrificar la precisión)
* validación de campos individuales
* cuando proceda, restringir el contenido de campos específicos a lo que sea significativo

### Eliminación de la redundancia de datos {#data-redundancy}

La redundancia de datos se produce cuando la misma información se almacena dos veces dentro de la estructura de contenido. Esto debe evitarse, ya que puede provocar confusión al crear el contenido y errores al consultar; sin mencionar el uso indebido del espacio de almacenamiento.

### Optimización y rendimiento {#optimization-and-performance}

Al optimizar su estructura, puede mejorar el rendimiento, tanto para la creación de contenido como para las consultas.

Todo es un acto de equilibrio, pero la creación de una estructura demasiado compleja o con demasiados niveles puede:

* Sea confuso para los autores que generan el contenido.

* Afecta gravemente al rendimiento si la consulta tiene que acceder a varios fragmentos de contenido anidados (referenciados) para recuperar el contenido requerido.

## Modelado de datos para AEM sin encabezado {#data-modeling-for-aem-headless}

El Modelado de datos es un conjunto de técnicas establecidas, que a menudo se utilizan cuando se desarrollan bases de datos de relaciones, así que ¿qué significa para AEM sin encabezado?

### ¿Por qué? {#why}

Para garantizar que su aplicación pueda solicitar y recibir de forma consistente y eficiente el contenido necesario de AEM, este contenido debe estar estructurado.

Esto significa que la aplicación conoce de antemano la forma de respuesta y, por lo tanto, cómo procesarla. Esto es mucho más fácil que recibir contenido de forma libre, que debe analizarse para determinar qué contiene y, por lo tanto, cómo puede utilizarse.

### Introducción a How? {#how}

AEM utiliza los fragmentos de contenido para proporcionar las estructuras necesarias para la entrega sin encabezado de su contenido a sus aplicaciones.

La estructura del modelo de datos es:

* realizado mediante la definición del modelo de fragmento de contenido,
* se utiliza como base de los fragmentos de contenido utilizados para la generación de contenido.

>[!NOTE]
>
>Los modelos de fragmento de contenido también se utilizan como base de los esquemas AEM de GraphQL, que se utilizan para recuperar contenido; más información al respecto en una sesión posterior.

Las solicitudes de contenido se realizan mediante la API de AEM GraphQL, una implementación personalizada de la API estándar de GraphQL. La API de AEM GraphQL permite realizar consultas (complejas) en los fragmentos de contenido, cada una de las cuales depende de un tipo de modelo específico.

Las aplicaciones pueden utilizar el contenido devuelto.

## Creación de la estructura con modelos de fragmento de contenido {#create-structure-content-fragment-models}

Los modelos de fragmento de contenido proporcionan varios mecanismos que le permiten definir la estructura del contenido.

Un modelo de fragmento de contenido describe una entidad.

>[!NOTE]
>Debe habilitar la funcionalidad Fragmento de contenido en el navegador de configuración para poder crear nuevos modelos.

>[!TIP]
>
>Se debe asignar un nombre al modelo para que el autor del contenido sepa qué modelo seleccionar al crear un fragmento de contenido.

Dentro de un modelo:

1. **Los** tipos de datos permiten definir los atributos individuales.
Por ejemplo, defina el campo que contiene el nombre de un profesor como **Text** y sus años de servicio como **Number**.
1. Los tipos de datos **Content Reference** y **Fragment Reference** permiten crear relaciones con otro contenido dentro de AEM.
1. El tipo de datos **Referencia de fragmento** le permite obtener varios niveles de estructura anidando los fragmentos de contenido (según el tipo de modelo). Esto es vital para el modelado de datos.

Por ejemplo:
![Modelado de contenido con fragmentos de contenido](assets/headless-modeling-01.png "Modelado de contenido con fragmentos de contenido")

### Tipos de datos {#data-types}

AEM proporciona los siguientes tipos de datos para modelar el contenido:

* Texto de línea única
* Texto multilínea
* Número
* Booleano
* Fecha y hora
* Enumeración
* Etiquetas
* Referencia de contenido
* Referencia al fragmento
* Objeto JSON

### Referencias y contenido anidado {#references-nested-content}

Dos tipos de datos proporcionan referencias al contenido fuera de un fragmento específico:

* **Content**
ReferenceEsta opción proporciona una sencilla referencia a otro contenido de cualquier tipo.
Por ejemplo, puede hacer referencia a una imagen en una ubicación específica.

* **Referencia de**
fragmentoEsta opción proporciona referencias a otros fragmentos de contenido.
Este tipo de referencia se utiliza para crear contenido anidado y presenta las relaciones necesarias para modelar el contenido.
El tipo de datos se puede configurar para que los autores de fragmentos puedan:
   * Edite directamente el fragmento al que se hace referencia.
   * Cree un nuevo fragmento de contenido basado en el modelo apropiado

## Uso del modelo para crear contenido con fragmentos de contenido {#use-content-to-author-content}

Los fragmentos de contenido siempre se basan en un modelo de fragmento de contenido. El modelo proporciona la estructura, el fragmento alberga el contenido.

### Selección del modelo apropiado {#select-model}

El primer paso para crear el contenido es crear un fragmento de contenido. Se basa en un modelo de fragmento de contenido específico que se selecciona como primer paso del proceso de creación.

### Creación y edición de contenido estructurado {#create-edit-structured-content}

Una vez creado el fragmento, puede abrirlo en el Editor de fragmentos de contenido. Aquí puede hacer lo siguiente:

* Edite el contenido en modo normal o de pantalla completa.
* Dé formato al contenido como Texto completo, Texto sin formato o Marcado.
* Cree y administre Variaciones de su contenido.
* Asociar contenido.
* Edite los metadatos.
* Mostrar la estructura de árbol.
* Obtenga una vista previa de la representación JSON.

## Introducción a algunos ejemplos {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

Para obtener una estructura básica como ejemplo, consulte La estructura del fragmento de contenido de ejemplo.

## Siguientes {#whats-next}

Ahora que ha aprendido a modelar su estructura y a crear contenido en función de eso, el siguiente paso es [Aprenda a utilizar las consultas de GraphQL para acceder y recuperar el contenido de los fragmentos de contenido](access-your-content.md). Esto presentará y analizará GraphQL, y luego verá algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

## Recursos adicionales {#additional-resources}

* [Uso de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) : la página de inicio para fragmentos de contenido
   * [Fragmentos de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md) : habilite la funcionalidad Fragmento de contenido en el navegador de configuración
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) : creación y edición de modelos de fragmento de contenido
   * [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) : creación de fragmentos de contenido; esta página le llevará a otras secciones detalladas
* [Esquemas de AEM GraphQL](/help/implementing/developing/headless-journey/access-your-content.md) : cómo GraphQL lleva a cabo los modelos
* [La estructura de fragmento de contenido de ejemplo](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
