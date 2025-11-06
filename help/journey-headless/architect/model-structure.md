---
title: Obtenga información acerca de la creación de modelos de fragmento de contenido en AEM
description: Obtenga información sobre los conceptos y la mecánica del contenido de modelado para su CMS sin periféricos usando modelos de fragmentos de contenido.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 83%

---

# Obtenga información acerca de la creación de modelos de fragmento de contenido en AEM {#architect-headless-content-fragment-models}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido de autor de contenido sin encabezado de AEM](overview.md), los [Conceptos básicos de modelado de contenido para usuarios sin encabezado con AEM](basics.md) abarcaban los conceptos básicos y la terminología relevantes para la creación sin encabezado.

Este artículo se basa en estos principios para que pueda comprender cómo crear sus propios modelos de fragmento de contenido para su proyecto sin encabezado de AEM.

## Objetivo {#objective}

* **Público**: principiante
* **Objetivo**: obtener conceptos y mecanismos de modelado de contenido para su CMS sin encabezado utilizando los modelos de fragmentos de contenido.

## Creación de modelos de fragmento de contenido {#creating-content-fragment-models}

A continuación, se pueden crear los modelos de fragmento de contenido y definir la estructura. 

1. En la Consola de fragmentos de contenido, seleccione el panel para Modelos de fragmento de contenido.

1. Vaya a la carpeta adecuada para su configuración o subconfiguración.

1. Use **Crear** para abrir el cuadro de diálogo **Nuevo modelo de fragmento de contenido**.

   ![Título y descripción](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. Complete los detalles

1. Use **Crear** para guardar el modelo vacío o **Crear y abrir**.

## Definición de los modelos de fragmento de contenido {#defining-content-fragment-models}

Cuando abra un nuevo modelo por primera vez, verá un espacio grande (bastante) en blanco en el medio, una larga lista de **Tipos de datos** a la izquierda y **Propiedades** (vacías al principio, como en el campo seleccionado) a la derecha:

![Modelo vacío](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-empty-model.png)

Entonces, ¿qué se debe hacer?

Puede realizar una de las acciones siguientes:

* Arrastre un tipo de datos desde el panel izquierdo a la ubicación requerida para un campo del panel central.
* Seleccione el icono + junto a un Tipo de datos para añadirlo a la parte inferior de la lista de campos.
* Seleccione Agregar en el panel central y, a continuación, el tipo de datos requerido en la lista desplegable resultante para agregar un campo al final de la lista.

Ya está definiendo el modelo.

Una vez que haya agregado un tipo de datos, se le pedirá que defina las **Propiedades** para ese campo. Estas propiedades dependen del tipo que se utilice. Por ejemplo:

![Propiedades de datos](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-field-properties.png)

### Sus autores de contenido {#your-content-authors}

Sus autores de contenido no ven los tipos de datos ni las propiedades reales que utilizó para crear los modelos. Esto significa que es posible que tenga que proporcionar ayuda e información sobre cómo completar campos específicos. Para obtener información básica, puede utilizar la etiqueta de campo y el valor predeterminado, pero puede que sea necesario tener en cuenta casos más complejos como la documentación específica del proyecto.

>[!NOTE]
>
>Consulte Recursos adicionales: Modelos de fragmento de contenido.

## Administración de los modelos de fragmento de contenido {#managing-content-fragment-models}

<!-- needs more details -->

La administración de modelos de fragmento de contenido implica lo siguiente:

* Habilitarlos (o deshabilitarlos): esto hace que estén disponibles para los autores al crear fragmentos de contenido.
* Eliminación: la eliminación siempre es necesaria, pero debe tener en cuenta la eliminación de un modelo que ya se esté utilizando para los fragmentos de contenido, en particular los fragmentos que ya se han publicado.

## Publicación {#publishing}

<!-- needs more details -->

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

>[!NOTE]
>
>Si un autor intenta publicar un fragmento de contenido para el que aún no se ha publicado el modelo, la lista de selección lo indica y el modelo se publica con el fragmento.

En cuanto se publica el modelo, aparece *bloqueado* en modo de SOLO LECTURA en el autor. Esto tiene como objetivo evitar cambios que pudieran provocar errores en los esquemas y consultas de GraphQL existentes, especialmente en el entorno de publicación. En la consola se indica como **Bloqueado**.

Cuando el modelo está **Bloqueado** (en modo de SOLO LECTURA), puede ver el contenido y la estructura de los modelos, pero no puede editarlos directamente; aunque puede administrar los modelos **Bloqueados** desde la consola o desde el editor de modelos.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido los conceptos básicos, el siguiente paso es comenzar a crear sus propios modelos de fragmento de contenido.

## Recursos adicionales {#additional-resources}

* [Conceptos de creación](/help/sites-cloud/authoring/author-publish.md)

* [Gestión básica](/help/sites-cloud/authoring/basic-handling.md): esta página se basa principalmente en la consola de **Sitios**, pero muchas de las funciones principales también son relevantes para desplazarse y realizar acciones en el apartado **Modelos de fragmento de contenido** en la consola **General**.

* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Definición del modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [Habilitación o deshabilitación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [Permitir modelos de fragmento de contenido en la carpeta Recursos](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [Eliminación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [Publicación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [Cancelación de la publicación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [Modelos de fragmento de contenido bloqueados](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* Guías de introducción

   * [Creación de Modelos de fragmento de contenido: configuración sin encabezado](/help/headless/setup/create-content-model.md)
