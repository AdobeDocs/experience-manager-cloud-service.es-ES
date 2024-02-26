---
title: Panel lateral de la consola Sites
description: AEM Aprenda a utilizar el panel lateral de la consola Sitios de la para comprender mejor el contenido y navegar por él.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 23%

---


# Panel lateral de la consola Sites {#side-panel}

AEM Aprenda a utilizar el panel lateral en la **Sites** para comprender mejor su contenido y navegar por él.

## Orientación {#orientation}

El panel lateral se cierra de forma predeterminada al entrar en el **Sites** consola. De este modo, la pantalla está dedicada completamente a su contenido.

Haga clic o pulse en **Panel lateral** en el menú **Sites** barra de herramientas de la consola para activar el panel lateral y elegir la vista del contenido.

* [Solo contenido](#content-only)
* [Árbol de contenido](#content-tree)
* [Escala de cronología](#timeline)
* [Referencias](#references)
* [Sitio](#site)
* [Filter](#filter)
* [Análisis de configuración](#setup-analytics)

![Vistas del panel lateral de la consola Sitios](assets/sites-console-side-panel-views.png)

La vista actual seleccionada se indica con una marca de verificación azul en la lista desplegable y el icono del panel lateral de la barra de herramientas se actualiza con el nombre de la vista seleccionada.

## Solo contenido {#content-only}

Esta vista del panel lateral está desactivándola efectivamente, es decir, solo muestra el contenido del sitio.

>[!TIP]
>
>Use el acento grave o acento grave `´` método abreviado de teclado para cambiar a la vista solo contenido del panel lateral.

## Árbol de contenido {#content-tree}

Esta vista del panel lateral muestra el contenido en una jerarquía de árbol. El árbol de contenido se puede utilizar para navegar rápidamente por la jerarquía del sitio dentro del panel lateral y ver mucha información sobre las páginas de la carpeta actual.

![La vista de árbol de contenido del panel lateral](assets/console-side-panel-content-tree.png)

Un corchete que señala hacia la derecha junto a un elemento del árbol indica un nodo que se puede expandir para mostrar sus elementos secundarios. Pulse o haga clic en las comillas angulares para mostrar los elementos secundarios.

La consola muestra el contenido del elemento seleccionado actualmente en el árbol de contenido.

Con el panel lateral del árbol de contenido junto con una vista de lista o una vista de tarjetas, puede ver fácilmente la estructura jerárquica del proyecto y navegar fácilmente por la estructura de contenido con el panel lateral del árbol de contenido y ver información detallada de la página en la vista de lista.

>[!TIP]
>
>* Utilice el `Alt+1` método abreviado de teclado para cambiar a la vista de árbol de contenido del panel lateral.
>* Una vez seleccionada una entrada en la vista de jerarquía, las teclas de flecha sirven para desplazarse rápidamente por la jerarquía.
>* Consulte los [métodos abreviados del teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para obtener más información.

## Escala de cronología {#timeline}

La cronología puede utilizarse para ver eventos que hayan afectado al recurso seleccionado. También puede utilizarlo para iniciar ciertos eventos, como flujos de trabajo o versiones.

![Detalles de la cronología](/help/sites-cloud/authoring/assets/timeline-detail.png)

El **Cronología** el panel lateral permite ver varios eventos relacionados con un elemento seleccionado seleccionable como tipos desde una lista desplegable:

* Comentarios
* [Anotaciones](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Actividades](/help/sites-cloud/authoring/personalization/activities.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)
* [Versiones](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md)
   * Tenga en cuenta que no se mostrará ninguna información sobre los flujos de trabajo transitorios, ya que no se guarda ninguna información del historial para ellos.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Mostrar todos

Además, puede agregar o ver comentarios sobre el elemento seleccionado mediante el **Comentario** Cuadro que se muestra al final de la lista de eventos. Escribir un comentario seguido de `Return` registrará el comentario. Se muestra cuando se selecciona **Comentarios** o **Mostrar todo**.

En el **Sites** consola también puede acceder a funciones adicionales mediante el botón de puntos suspensivos situado junto a la **Comentario** field.

* [Guardar una versión](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Iniciar un flujo de trabajo](/help/sites-cloud/authoring/workflows/applying.md)

![Campo de comentarios de la consola Sites](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Utilice el `Alt+2` método abreviado de teclado para cambiar a la vista de línea de tiempo del panel lateral.
>* Consulte los [métodos abreviados del teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para obtener más información.

## Referencias {#references}

El **Referencias** La vista muestra una lista de tipos de referencias hacia o desde el recurso seleccionado en la consola.

![Detalles de referencias](assets/console-side-panel-references-detail.png)

Seleccione el tipo de referencia adecuado para obtener más información. En determinadas situaciones, hay disponibles acciones adicionales al seleccionar una referencia específica, como las siguientes:

* **Vínculos entrantes**, proporciona una lista de páginas que hacen referencia a la página, así como acceso directo a **Editar** Seleccione una de esas páginas cuando seleccione un vínculo específico.
   * Esto solo puede mostrar vínculos estáticos, no vínculos generados dinámicamente como del componente Lista.
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md), que proporciona acceso a lanzamientos relacionados.
* [Live Copies](/help/sites-cloud/administering/msm/overview.md) muestra las rutas de todas las Live Copies que se basan en el recurso seleccionado.
* [Modelo](/help/sites-cloud/administering/msm/best-practices.md), proporciona detalles y diversas acciones
* [Copias de idiomas](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), proporciona detalles y diversas acciones

## Sitio {#site}

El **Sitio** la vista del panel lateral muestra detalles de sitios [creado con una plantilla del sitio.](/help/sites-cloud/administering/site-creation/create-site.md)

![Panel del sitio](assets/console-side-panel-site-paenl.png)

Ver el documento [Uso del panel del sitio para administrar el tema del sitio](/help/sites-cloud/administering/site-creation/site-rail.md) para obtener más información sobre cómo puede utilizar el panel para administrar el [tema del sitio.](/help/sites-cloud/administering/site-creation/site-themes.md).

Si todavía no ha configurado la canalización front-end para habilitar la creación de sitios basados en temas, el panel lateral ofrecerá esa opción.

![Opción para habilitar la canalización front-end en el panel lateral](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>Puede encontrar una descripción completa del proceso de crear un sitio a partir de una plantilla y personalizar su tema en el [Recorrido de creación rápida de sitios.](/help/journey-sites/quick-site/overview.md)

## Filter {#filter}

El **Filtrar** El panel es similar al de [función de búsqueda](/help/sites-cloud/authoring/search.md) con los filtros de ubicación adecuados ya establecidos, lo que le permite filtrar aún más el contenido que desea ver.

![Ejemplo de filtro](assets/console-side-panel-filter.png)

A diferencia de otras vistas del panel lateral, para cambiar a otra vista, toque o haga clic en `X` en el campo de búsqueda.

## Análisis de configuración {#setup-analytics}

Esta vista le permite configurar rápidamente Adobe Analytics para un sitio seleccionado.

![Análisis de configuración](assets/sites-console-side-panel-setup-analytics.png)
