---
title: Administración de proyectos
description: Proyectos le permite organizar su proyecto al agrupar los recursos en una entidad a la que se puede acceder y se puede administrar en la consola Proyectos
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 100%

---

# Administración de proyectos {#managing-projects}

Proyectos le permite agrupar los recursos en una entidad para organizar el proyecto.

En la consola **Proyectos**, puede acceder a los proyectos y realizar acciones con ellos:

![La consola Proyectos](/help/sites-cloud/authoring/assets/projects-console.png)

En Proyectos, puede crear un proyecto, asociar recursos al proyecto y, además, eliminar un proyecto o vínculos a recursos. Es posible que desee abrir un mosaico para ver su contenido, así como para añadir elementos a un mosaico. En este tema se describen estos procedimientos.

## Creación de un proyecto {#creating-a-project}

En la versión básica, AEM proporciona estas plantillas para elegir al crear un proyecto:

* Proyecto simple
* Proyecto multimedia
* Proyecto de traducción

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

El procedimiento para crear un proyecto es el mismo de un proyecto a otro. La diferencia entre los tipos de proyectos incluye las [funciones de usuario](/help/sites-cloud/authoring/projects/overview.md) y los [flujos de trabajo](/help/sites-cloud/authoring/projects/workflows.md) disponibles. Para crear un nuevo proyecto:

1. En **Proyectos**, pulse o haga clic en **Crear** y abrirá el asistente **Crear proyecto**:
1. Seleccione una plantilla y haga clic en **Siguiente**.

   ![Creación de un proyecto](/help/sites-cloud/authoring/assets/projects-create.png)

1. Defina el **Título** y la **Descripción** y añada una imagen en **miniatura** si es necesario. También puede añadir o eliminar a usuarios y al grupo al que pertenecen. Además, puede hacer clic en **Avanzadas** para añadir un nombre utilizado en la dirección URL.

   ![Adición de detalles del proyecto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque o haga clic en **Crear**. La confirmación le preguntará si desea abrir el proyecto nuevo o regresar a la consola.

### Asociación de recursos al proyecto {#associating-resources-with-your-project}

Dado que los proyectos le permiten agrupar los recursos en una entidad, puede asociar recursos al proyecto. Estos recursos se denominan **Mosaicos**. Los tipos de recursos que puede añadir se describen en [Mosaicos de proyecto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Para asociar recursos al proyecto:

1. Abra el proyecto en la consola **Proyectos**.
1. Toque o haga clic en **Añadir mosaico** y seleccione el mosaico que desea vincular al proyecto. Puede seleccionar varios tipos de mosaicos.

   ![Adición de un mosaico a un proyecto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >Los mosaicos de proyecto que se pueden asociar a un proyecto se describen detalladamente en [Mosaicos de proyecto.](/help/sites-cloud/authoring/projects/overview.md#project-tiles)

1. Toque o haga clic en **Crear**. El recurso está vinculado al proyecto y, a partir de ahora, podrá acceder a él desde el proyecto.

### Eliminación de un proyecto o un vínculo a un recurso {#deleting-a-project-or-resource-link}

Para eliminar un proyecto desde la consola o un recurso vinculado desde el proyecto se utiliza el mismo método: 

1. Vaya a la ubicación adecuada:

   * Para eliminar un proyecto vaya al nivel superior de la consola **Proyectos**.
   * Para eliminar un vínculo a un recurso de un proyecto, abra el proyecto en la consola **Proyectos**.

1. Para introducir el modo de selección, haga clic en **Seleccionar** y seleccione el proyecto o el vínculo a un recurso.
1. Toque o haga clic en **Eliminar**.

1. Debe confirmar la eliminación en un cuadro de diálogo. Si se confirma, se elimina el proyecto o el vínculo a un recurso. Toque o haga clic en **Anular selección** para salir del modo de selección.

>[!NOTE]
>
>Al crear el proyecto y agregar usuarios a las distintas funciones, los grupos asociados con el proyecto se crean automáticamente para administrar los permisos asociados. Por ejemplo, un proyecto llamado Myproject tendría tres grupos: **Propietarios de Myproject**, **Editores de Myproject**, **Observadores de Myproject**. Sin embargo, si se elimina el proyecto, esos grupos no se eliminarán automáticamente. Un administrador debe eliminar manualmente los grupos en **Herramientas** > **Seguridad** > **Grupos**.

### Adición de elementos a un mosaico {#adding-items-to-a-tile}

En algunos mosaicos, puede que desee añadir más de un elemento. Por ejemplo, puede tener más de un flujo de trabajo que se ejecuta al mismo tiempo o más de una experiencia.

Para añadir elementos a un mosaico:

1. En **Proyectos**, vaya al proyecto y haga clic o pulse en las comillas angulares hacia abajo en el mosaico al que desee agregar un elemento.

   ![Adición de un elemento a un mosaico](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Añada un elemento al mosaico como lo haría al crear un mosaico nuevo. Los mosaicos de proyecto se describen [aquí](/help/sites-cloud/authoring/projects/overview.md#project-tiles). En este ejemplo, se ha añadido otro flujo de trabajo.

### Apertura de un mosaico {#opening-a-tile}

Puede que desee ver qué elementos se incluyen en un mosaico actual, o modificar o eliminar elementos del mosaico.

Para abrir un mosaico para que pueda ver o modificar elementos:

1. En la consola Proyectos, toque o haga clic en los puntos suspensivos (…). en la parte inferior de la tarjeta.

   ![Apertura de un mosaico](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM enumera los elementos de ese mosaico. Puede introducir el modo de selección para modificar o eliminar los elementos.

   ![Mosaico abierto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Visualización de estadísticas del proyecto {#viewing-project-statistics}

Puede ver las estadísticas del proyecto en la consola **Proyectos**.

### Visualización de una línea de tiempo del proyecto {#viewing-a-project-timeline}

La línea de tiempo del proyecto proporciona información sobre cuándo se utilizaron por última vez los recursos del proyecto. Para ver la cronología del proyecto, pulse o haga clic en **Cronología** y, a continuación, introduzca el modo de selección y seleccione el proyecto. Los recursos se muestran en el panel izquierdo. Pulse o haga clic en **Cronología** para volver a la consola **Proyectos**.

![Cronología del proyecto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Visualización de proyectos activos/inactivos {#viewing-active-inactive-projects}

Para alternar entre los proyectos activos e inactivos, en la consola **Proyectos**, haga clic en **Alternar proyectos activos**. Si el icono tiene una marca de verificación junto a él, muestra los proyectos activos.

![Botón Alternar proyectos activos](/help/sites-cloud/authoring/assets/projects-active.png)

Si el icono tiene una x junto a él, muestra los proyectos inactivos.

![Botón Alternar proyectos inactivos](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Hacer que los proyectos sean activos o inactivos {#making-projects-inactive-or-active}

Es posible que desee hacer que un proyecto sea inactivo si lo ha completado, pero desea mantener la información del proyecto.

Para hacer que un proyecto sea inactivo (o activo):

1. En la consola **Proyectos**, abra el proyecto y, a continuación, busque el mosaico **Información del proyecto**.

   >[!NOTE]
   >Es posible que deba añadir este mosaico si aún no está en el proyecto. Consulte [Añadir mosaicos](#adding-items-to-a-tile).

1. Pulse o haga clic en **Editar**.
1. Cambie el selector de **Activo** a **Inactivo** (o viceversa).

   ![Activación de un proyecto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque o haga clic en **Hecho** para guardar los cambios.
