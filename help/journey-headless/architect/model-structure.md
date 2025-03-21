---
title: Obtenga información acerca de la creación de modelos de fragmento de contenido en AEM
description: Obtenga información sobre los conceptos y la mecánica del contenido de modelado para su CMS sin periféricos usando modelos de fragmentos de contenido.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 6306ad88b889197aff377dc0a72ea232cd76ff9c
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 76%

---

# Obtenga información acerca de la creación de modelos de fragmento de contenido en AEM {#architect-headless-content-fragment-models}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido de autor de contenido sin encabezado de AEM](overview.md), los [Conceptos básicos de modelado de contenido para usuarios sin encabezado con AEM](basics.md) abarcaban los conceptos básicos y la terminología relevantes para la creación sin encabezado.

Este artículo se basa en estos principios para que pueda comprender cómo crear sus propios modelos de fragmentos de contenido para su proyecto sin encabezado de AEM.

## Objetivo {#objective}

* **Audiencia**: principiante
* **Objetivo**: obtener conceptos y mecanismos de modelado de contenido para su CMS sin encabezado utilizando los modelos de fragmentos de contenido.

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools > General > Configuration Browser. You can either select to configure the global entry, or create a configuration. For example:

![Define configuration](/help/sites-cloud/administering/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## Creación de modelos de fragmento de contenido {#creating-content-fragment-models}

A continuación, se pueden crear los modelos de fragmentos de contenido y definir la estructura.

1. En la Consola de fragmento de contenido, seleccione el panel para Modelos de fragmento de contenido.

1. Vaya a la carpeta adecuada para su configuración o subconfiguración.

1. Use **Crear** para abrir el cuadro de diálogo **Nuevo modelo de fragmento de contenido**.

   ![Título y descripción](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. Completar los detalles

1. Use **Crear** para guardar el modelo vacío o **Crear y abrir**.

<!--
Then the Content Fragments Models can be created and the structure defined. This can be done under **Tools** > **General** > **Content Fragment Models**. 

![Content Fragment Models in Tools](assets/cfm-tools.png)

After selecting this you navigate to the location for your model and select **Create**. Here you can enter various key details.

The option **Enable model** is activated by default. This means that your model is available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![Create Content Fragment Model](/help/sites-cloud/administering/content-fragments/assets/cfm-models-02.png)

Confirm with **Create** and you can then **Open** your model to start defining the structure.
-->

## Definición de los modelos de fragmento de contenido {#defining-content-fragment-models}

Cuando abra un nuevo modelo por primera vez, verá un gran espacio en blanco a la izquierda y una larga lista de **Tipos de datos** a la derecha:

![Modelo vacío](/help/sites-cloud/administering/content-fragments/assets/cfm-models-03.png)

Entonces, ¿qué se debe hacer?

Puede arrastrar instancias de los **Tipos de datos** en el espacio de la izquierda: ya estará definiendo su modelo.

 ![Definición de campos](/help/sites-cloud/administering/content-fragments/assets/cfm-models-04.png)

Una vez que haya agregado un tipo de datos, se le pedirá que defina las **Propiedades** para ese campo. Estas propiedades dependen del tipo que se utilice. Por ejemplo:

![Propiedades de datos](/help/sites-cloud/administering/content-fragments/assets/cfm-models-05.png)

Se pueden agregar tantos campos como se necesite. Por ejemplo:

![Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/assets/cfm-models-07.png)

### Sus autores de contenido {#your-content-authors}

Sus autores de contenido no ven los tipos de datos ni las propiedades reales que utilizó para crear los modelos. Esto significa que es posible que tenga que proporcionar ayuda e información sobre cómo completar campos específicos. Para obtener información básica, puede utilizar la etiqueta de campo y el valor predeterminado, pero puede que sea necesario tener en cuenta casos más complejos como la documentación específica del proyecto.

>[!NOTE]
>
>Consulte Recursos adicionales: Modelos de fragmento de contenido.

## Administración de los modelos de fragmento de contenido {#managing-content-fragment-models}

<!-- needs more details -->

La administración de modelos de fragmento de contenido implica lo siguiente:

* Habilitarlos (o deshabilitarlos): esto hace que estén disponibles para los autores al crear fragmentos de contenido.
* Eliminar: la eliminación siempre es necesaria, pero debe tener en cuenta la eliminación de un modelo que ya se utiliza para fragmentos de contenido; en particular, fragmentos que ya se han publicado.

## Publicación {#publishing}

<!-- needs more details -->

Los modelos de fragmento de contenido deben publicarse cuando se publican fragmentos de contenido dependientes, o antes de hacerlo.

>[!NOTE]
>
>Si un autor intenta publicar un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indica y el modelo se publica con el fragmento.

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

      * [Activación o desactivación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [Permitir modelos de fragmento de contenido en la carpeta Recursos](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [Eliminación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [Publicación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [Cancelación de la publicación de un modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [Modelos de fragmento de contenido bloqueados](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* Guías de introducción

   * [Creación de Modelos de fragmento de contenido: configuración sin encabezado](/help/headless/setup/create-content-model.md)
