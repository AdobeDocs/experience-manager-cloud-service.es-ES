---
title: Descubra los conceptos básicos del modelado de contenido
description: Conozca los aspectos básicos del modelado de contenido para su CMS sin encabezado mediante fragmentos de contenido.
index: true
hide: false
hidefromtoc: false
source-git-commit: 6605349c698325d432479fac0253a6fd53d7f175
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 4%

---


# Descubra los conceptos básicos del modelado de contenido para usuarios sin encabezado con AEM {#content-modeling-headless-basics}

## La historia hasta ahora {#story-so-far}

Al principio del [AEM Recorrido de arquitectos de contenido sin encabezado](overview.md) [Introduction](introduction.md) abarcaba los conceptos básicos y la terminología relevantes para el modelado de contenido para que no tenga encabezado.

Este artículo se basa en estos elementos para que pueda comprender cómo modelar el contenido para su proyecto sin objetivos AEM.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Introduzca los conceptos de Modelado de contenido para CMS sin encabezado.

## Modelado de contenido con modelos de fragmento de contenido {#architect-content-fragment-models}

El modelado de contenido (datos) es un conjunto de técnicas establecidas, que a menudo se utilizan cuando se desarrollan bases de datos de relaciones, por lo que ¿qué significa el modelado de contenido para AEM sin encabezado?

### ¿Por qué? {#why}

Para garantizar que su aplicación pueda solicitar y recibir de forma consistente y eficiente el contenido necesario de AEM, este contenido debe estar estructurado.

Esto significa que la aplicación conoce de antemano la forma de respuesta y, por lo tanto, cómo procesarla. Esto es mucho más fácil que recibir contenido de forma libre, que debe analizarse para determinar qué contiene y, por lo tanto, cómo puede utilizarse.

### Introducción a How? {#how}

AEM utiliza los fragmentos de contenido para proporcionar las estructuras necesarias para la entrega sin encabezado de su contenido a sus aplicaciones.

La estructura del modelo de contenido es:

* realizado mediante la definición del modelo de fragmento de contenido,
* se utiliza como base de los fragmentos de contenido utilizados para la generación de contenido.

>[!NOTE]
>
>Los modelos de fragmento de contenido también se utilizan como base de los esquemas AEM de GraphQL, que se utilizan para recuperar el contenido. Más información sobre el Recorrido para desarrolladores.

Las solicitudes de contenido se realizan mediante la API de AEM GraphQL, una implementación personalizada de la API estándar de GraphQL. La API de AEM GraphQL permite a las aplicaciones realizar consultas (complejas) en los fragmentos de contenido, cada una de las cuales depende de un tipo de modelo específico.

Las aplicaciones pueden utilizar el contenido devuelto.

## Creación de la estructura con modelos de fragmento de contenido {#create-structure-content-fragment-models}

Los modelos de fragmento de contenido proporcionan varios mecanismos que le permiten definir la estructura del contenido.

Un modelo de fragmento de contenido describe una entidad.

>[!NOTE]
>La funcionalidad de fragmento de contenido debe estar habilitada en el navegador de configuración para poder crear nuevos modelos.

>[!TIP]
>
>Se debe asignar un nombre al modelo para que el autor del contenido sepa qué modelo seleccionar al crear un fragmento de contenido.

Dentro de un modelo:

1. **Los** tipos de datos permiten definir los atributos individuales.
Por ejemplo, defina el campo que contiene el nombre de un profesor como **Text** y sus años de servicio como **Number**.
1. Los tipos de datos **Content Reference** y **Fragment Reference** permiten crear relaciones con otro contenido dentro de AEM.
1. El tipo de datos **Referencia de fragmento** le permite obtener varios niveles de estructura anidando los fragmentos de contenido (según el tipo de modelo). Esto es vital para el modelado de contenido.

Por ejemplo:

![Modelado de contenido con ](assets/headless-modeling-01.png "fragmentos de contenidoModelado de contenido con fragmentos de contenido")

## Tipos de datos {#data-types}

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

>[!NOTE]
>
>Encontrará más información en Modelos de fragmento de contenido: Tipos de datos.

## Referencias y contenido anidado {#references-nested-content}

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

>[!NOTE]
>
>También puede crear referencias ad hoc utilizando vínculos dentro de bloques de texto.

## Niveles de estructura (fragmentos anidados) {#levels-of-structure-nested-fragments}

Para el modelado de contenido, el tipo de datos **Referencia de fragmento** permite crear varios niveles de estructura y relaciones.

Con esta referencia puede *conectar* varios modelos de fragmento de contenido para representar las interrelaciones. Esto permite que la aplicación sin periféricos siga las conexiones y acceda al contenido según sea necesario.

>[!NOTE]
>
>Debe usarse con precaución y la práctica recomendada puede definirse como *anidar en la medida necesaria, pero tan poco como sea posible*.

Las referencias de fragmento hacen precisamente eso: le permiten hacer referencia a otro fragmento.

Por ejemplo, puede tener los siguientes modelos de fragmento de contenido definidos:

* Ciudad
* Empresa
* Person
* Premios

Parece bastante sencillo, pero por supuesto una compañía tiene un CEO y empleados....y todas son personas, cada una definida como una persona.

Y una persona puede tener un premio (o tal vez dos).

* Mi empresa - Empresa
   * CEO - Persona
   * Empleado(s) - Persona
      * Premio personal - Premio

Y eso es sólo para empezar. Según la complejidad, un Premio podría ser específico de la empresa o una empresa podría tener su oficina principal en una ciudad específica.

Representar estas interrelaciones se puede lograr con Referencias de fragmento, tal como usted (el arquitecto) entiende, el autor del contenido y las aplicaciones sin encabezado.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos básicos, el siguiente paso es [Obtenga información sobre la creación de modelos de fragmento de contenido en AEM](model-structure.md). Esto introducirá y discutirá las distintas referencias disponibles, y cómo crear niveles de estructura con las Referencias de fragmento - una parte clave del modelado para que no tenga objetivos.

## Recursos adicionales {#additional-resources}

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)

   * [Modelos de fragmento de contenido: tipos de datos](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) : esta página se basa principalmente en la consola  **** Sitios, pero muchas de las funciones (la mayoría) también son relevantes para la creación de  **fragmentos de** contenido en la consola  **** Recursos.

* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
