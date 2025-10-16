---
title: Obtenga información sobre el uso de referencias en fragmentos de contenido
description: Obtenga información sobre el uso de referencias en fragmentos de contenido para los contenidos, otros fragmentos y archivos (medios). Introduzca la necesidad y la mecánica de los fragmentos anidados para la creación de CMS sin encabezado.
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 18c997a5644288e870c109a8d745b196349b923d
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 100%

---

# Obtenga información sobre el uso de referencias en fragmentos de contenido {#author-headless-references}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido del autor de contenido de AEM sin encabezado](overview.md), en la [introducción](introduction.md) se han abordado los conceptos básicos y la terminología relevante para la creación sin encabezado.

Ha aprendido los conceptos básicos de la creación de CMS sin encabezado, con una introducción a la creación con AEMaaCS y, en particular, la creación de fragmentos de contenido.

Este artículo se basa en estos conceptos para que pueda comprender cómo utilizar las referencias para crear su propio contenido para su proyecto de AEM sin encabezado.

## Objetivo {#objective}

* **Público**: avanzado
* **Objetivo**: introducir el uso de referencias para la creación de CMS sin encabezado. Qué tipos de referencias están disponibles y cuáles son sus propósitos:

   * Referencias de contenidos
   * Referencias de recursos/medios
   * Referencias a fragmentos
   * Referencias improvisadas desde dentro de un bloque de texto

## Qué son las referencias {#what-are-references}

Las referencias son simplemente un mecanismo para conectar los recursos, ya sea otro contenido, recursos (como en las imágenes) u otros fragmentos. Aunque son muy similares, existen algunas diferencias.

Algunas referencias tienen tipos de datos específicos (por ejemplo, Referencias de contenidos y Referencias a fragmentos), mientras que otras se agregan simplemente como una referencia dentro de un bloque de texto (referencias de recursos y referencias improvisadas).

![Fragmentos de contenido: referencias](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

## Referencias de contenido {#content-references}

Las referencias de contenido hacen precisamente eso: permiten hacer referencia a cualquier otro contenido. Se abre un explorador que permite seleccionar el elemento de contenido.

Existen dos tipos:

* **Referencia de contenido**
   * especifica la ruta del recurso al que se hace referencia
* **Referencia de contenido (UUID)**
   * En el editor, las referencia especifica la ruta al recurso al que se hace referencia; internamente, la referencia se mantiene como ID único universal (UUID) que hace referencia al recurso

## Referencias de recursos/medios {#assets-media-references}

Se puede hacer referencia a los recursos (por ejemplo, imágenes o medios) dentro de un bloque de texto utilizando la opción **Insertar recurso**. Se abre un explorador que permite seleccionar el recurso.

![Fragmentos de contenido: insertar recurso](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Referencias a fragmentos {#fragment-references}

Una vez más, las referencias a fragmentos hacen precisamente eso: permiten hacer referencia a otro fragmento. Hay que explicar un poco más por qué esto es importante.

Por ejemplo, puede que tenga definidos los siguientes modelos de fragmento de contenido:

* Ciudad
* Compañía
* Persona
* Premios

Parece bastante sencillo, pero una Compañía tiene un director ejecutivo (CEO) y empleados…y todas ellas se definen como una persona.

Una persona puede obtener un premio (o tal vez dos).

* Mi compañía: compañía
   * CEO: persona
   * Empleado(s): persona
      * Premio(s) personal(es): premio

Y esto es solo para empezar. Según la complejidad, un premio podría ser específico de una compañía, o una compañía podría tener su oficina principal en una ciudad específica.

La representación de estas interrelaciones se puede lograr con Referencias a fragmentos, tal como las entienden el usuario (el autor) y las aplicaciones sin encabezado.

Como autor, no es responsable de definir estas relaciones (lo hace el arquitecto de contenido al crear el modelo de fragmento de contenido), pero necesita saber cómo reconocer y editar las referencias.

Hay dos tipos:

* **Referencia al fragmento**
   * especifica la ruta del recurso al que se hace referencia
* **Referencia de fragmento (UUID)**
   * En el editor, las referencia especifica la ruta al recurso al que se hace referencia; internamente, la referencia se mantiene como ID único universal (UUID) que hace referencia al recurso

### Creación de fragmentos anidados {#author-nested-fragment}

La creación de referencias a fragmentos es bastante sencilla (aunque normalmente el campo no se etiqueta como **Referencia a fragmento**). Puede escribir la referencia directamente o seleccionar el icono de carpeta para abrir el explorador (lo más probable) que le permita desplazarse y seleccionar el fragmento que necesita.

![Fragmentos de contenido: referencias](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La definición del modelo de los fragmentos de contenido controla lo siguiente:

* si se puede seleccionar que se agreguen varias referencias,
* y los tipos de modelo de Fragmentos de contenido que puede seleccionar. El modelo de fragmento de contenido define los modelos de fragmento permitidos para la referencia, por lo que AEM presenta solo fragmentos basados en esos modelos.

### Navegación por los fragmentos anidados {#navigate-nested-fragment}

Al usar la pestaña **Árbol de estructura** del Editor de fragmentos de contenido podrá desplazarse por los fragmentos a los que hace referencia el fragmento y, a continuación, por las referencias que puedan contener. Al seleccionar una referencia, se abre ese fragmento para editarlo.

![Árbol de estructura de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-structure-tree.png)

## Referencias Ad hoc {#adhoc-references}

Las referencias improvisadas se pueden agregar como un vínculo simple dentro de un bloque de texto.

![Fragmentos de contenido: referencias Ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Siguientes pasos {#whats-next}

Ahora que ha aprendido acerca de referencias y estructuras en los fragmentos de contenido, el siguiente paso es [Descubrir más información sobre metadatos y etiquetado](metadata-tagging.md). Esto presentará y explicará cómo puede definir los metadatos y las etiquetas para sus fragmentos de contenido.

## Recursos adicionales {#additional-resources}

* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Administración de los fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md)

      * [Aplicación de la configuración a la carpeta Recursos](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

      * [Creación de un fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [Creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md)

   * [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Modelos de fragmento de contenido: tipos de datos](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [Modelos de fragmento de contenido: propiedades](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

* Guías de introducción
   * [Creación de la carpeta Recursos: configuración sin encabezado](/help/headless/setup/create-assets-folder.md)

* Recorrido para arquitectos de contenido sin encabezado de AEM

* Recorrido de traducción de AEM sin encabezado
