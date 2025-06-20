---
title: Publicación de contenido con el editor de páginas
description: Descubra cómo el Editor de páginas publica contenido.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 44%

---


# Publicación de contenido con el Editor de sitios {#publishing}

Descubra cómo el Editor de páginas publica contenido.

## Publicar desde el editor de páginas {#publishing-from-the-page-editor}

Si está editando una página en el [editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), puede publicarla directamente desde el editor.

1. Seleccione el icono **Información de página** para abrir el menú y, a continuación, elija la opción **Publicar página**.

   ![Publicación de una página mediante las opciones de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. En función de si la página tiene referencias que es necesario publicar:

   * La página se publica directamente si no hay ninguna referencia por publicar.
   * Si la página tiene referencias que es necesario publicar, se enumeran en el asistente **Publicar**, donde puede:
      * Especifique cuál de los recursos, o etiquetas, etc., desea publicar junto con la página y, a continuación, utilice **Publicar** para completar el proceso.
      * Utilizar **Cancelar** para anular la acción.

   ![Publicación de referencias con la página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Si selecciona **Publicar**, se replicará la página en el entorno de publicación. En el editor de páginas se muestra un mensaje que confirma la acción de publicación.

   ![Mensaje de información de estado de publicación](/help/sites-cloud/authoring/assets/publishing-info.png)

   Al ver la misma página en la consola, se muestra el estado actualizado de publicación.

   ![Estado de publicación de la página en la vista de columna de la consola Sitios](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La publicación desde el editor de páginas es superficial; es decir, solo se publica la página o páginas seleccionadas y no las páginas secundarias.

>[!NOTE]
>
>No se pueden publicar las páginas a las que se tiene acceso mediante [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) en el editor. Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

## Cancelar la publicación desde el editor de páginas {#unpublishing}

Al editar una página con el Editor de páginas, si desea cancelar la publicación de esa página, seleccione **Cancelar la publicación de la página** en el menú **Información de la página**, de manera similar a como haría [publicar la página](#publishing-from-the-editor).

>[!NOTE]
>
>No se puede cancelar la publicación de las páginas a las que se accede mediante [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) en el editor. Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

## Publicar y cancelar la publicación desde la consola Sitios {#publishing-sites-console}

También puede publicar [desde la consola Sitios,](/help/sites-cloud/authoring/sites-console/publishing-pages.md), lo que puede resultar útil cuando desea publicar varias páginas de contenido o programar la publicación o cancelación de la publicación.
