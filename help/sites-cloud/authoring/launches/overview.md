---
title: Lanzamientos para páginas
description: Aprenda a utilizar Lanzamientos para páginas en Adobe Experience Manager as a Cloud Service. Los lanzamientos permiten desarrollar contenido de forma eficaz para una versión futura sin perder de vista las páginas actuales.
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 4c75904958f7faf91173cb8a37d5be5b3048cfae
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 74%

---

# Lanzamientos para páginas {#launches-for-pages}

En Adobe Experience Manager (AEM) as a Cloud Service, los lanzamientos le permiten desarrollar contenido de forma eficaz para una versión futura.

Se crea un *Launch* para permitirle realizar cambios con el fin de prepararse para una publicación futura y, al mismo tiempo, mantener el contenido actual. Para las páginas de AEM, esto significa que está editando dos versiones al mismo tiempo: páginas que se publican actualmente y una versión de esas páginas, que se publicarán a la vez en el futuro. Una vez que llegue ese momento, puede reemplazar las páginas originales y publicar las nuevas versiones.

<!--
>[!NOTE]
>
>Launches are also available for Content Fragments. The basic concepts are the same, but there are differences in how to manage them in AEM. 
>
>For full details see [Launches for Content Fragments](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).
-->

Usted crea un *Lanzamiento* y, después de editar y actualizar sus páginas de *Lanzamiento*, las *Promociona* de nuevo a *Source*. A continuación, puede activar estas páginas de *Source* (nivel superior). La promoción duplica el contenido del lanzamiento en las páginas de origen y se puede realizar de forma manual o automática (según los campos establecidos a la hora de crear y editar el lanzamiento).

Por ejemplo, las páginas de productos de temporada de su tienda en línea se actualizan trimestralmente para que los productos destacados se correspondan con la temporada actual. Para preparar la próxima actualización trimestral, se puede crear un lanzamiento de las páginas web correspondientes. Durante el trimestre, se acumulan los cambios siguientes en la copia de lanzamiento:

* Cambios en las páginas de origen que se producen como resultado de tareas normales de mantenimiento. Estos cambios se duplican automáticamente en las páginas de lanzamiento.
* Ediciones que se realizan en las páginas de lanzamiento directamente en preparación para el trimestre siguiente.

También puede hacer lo siguiente:

* Navegue por el contenido en la rama de lanzamiento; agregue o elimine páginas según sea necesario.
* Previsualice el aspecto que tendrá el contenido publicado en una fecha específica en el futuro.

Cuando llegue el trimestre siguiente, las páginas de lanzamiento se promocionan de forma que se puedan publicar las páginas de origen (que contienen el contenido actualizado). Puede promocionar todas las páginas o solamente aquellas que se han modificado. 

También se puede realizar lo siguiente:

* Se han creado lanzamientos para varias ramas de raíz. Aunque puede crear el lanzamiento para todo el sitio (y realizar los cambios allí), esto puede resultar poco práctico, ya que se debe copiar todo el sitio. Cuando hay cientos o incluso miles de páginas implicadas, los requisitos del sistema y el rendimiento se ven afectados por la acción de copiar y, posteriormente, por las comparaciones necesarias para las tareas de promoción.
* Cree lanzamientos anidados (un lanzamiento dentro de otro lanzamiento). Esto permite crear un lanzamiento a partir de uno existente, de modo que los autores puedan aprovechar los cambios ya realizados, en lugar de tener que realizar los mismos cambios varias veces para cada lanzamiento.

En esta sección se describe cómo crear, editar y promocionar (y, si fuera necesario [eliminar](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) páginas de lanzamiento desde la consola Sitios o la [consola Lanzamientos](#the-launches-console):

* [Creación de lanzamientos](/help/sites-cloud/authoring/launches/creating.md)
* [Edición de lanzamientos](/help/sites-cloud/authoring/launches/editing.md)
* [Administración de páginas en Lanzamientos](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Uso de la deformación de tiempo para previsualizar el contenido en función de los lanzamientos](/help/sites-cloud/authoring/launches/preview.md)
* [Promoción de lanzamientos](/help/sites-cloud/authoring/launches/promoting.md)

## Lanzamientos: orden de eventos {#launches-the-order-of-events}

Los lanzamientos permiten desarrollar contenido con eficacia para una versión futura de una o más páginas web activadas.

Los lanzamientos permiten realizar lo siguiente:

* Cree una copia de las páginas de origen:
   * La copia es su lanzamiento.
   * Las páginas de origen de nivel superior se denominan **Producción**.
      * Las páginas de origen puedan obtenerse de varias ramas (separadas).

  ![Orden de operación de los lanzamientos](/help/sites-cloud/authoring/assets/launches-order.png)

* Edite la configuración de lanzamiento:
   * Adición o eliminación de páginas o ramas en el lanzamiento.
   * Editar propiedades de lanzamiento; como **Título**, **Fecha de lanzamiento** e indicador **Listo para la producción**.
* Es posible promocionar y publicar el contenido de forma manual o automática:
   * Manualmente:
      * Promocione de nuevo el contenido del lanzamiento en el **Destino** (páginas de origen) cuando esté listo para su publicación.
      * Publique el contenido de las páginas de origen (tras volver a promocionarlo).
      * Promocione todas las páginas o solo las páginas modificadas.
   * Automáticamente. Esto implica lo siguiente:
      * El campo **Fecha**(**Live**) **de lanzamiento**: esto se puede establecer al crear o editar un lanzamiento. 
      * El indicador **Producción lista**: esto solo se puede establecer al editar un lanzamiento.
      * Si se establece el indicador **Preparado para la producción**, el lanzamiento se promocionará automáticamente a las páginas de producción en la **fecha** de **Lanzamiento**(**Activo**). Después de la promoción, las páginas de producción se publican automáticamente.\
        Si no se ha establecido ninguna fecha, el indicador no tiene ningún efecto.
* Actualice las páginas de origen y de lanzamiento en paralelo:
   * Los cambios que se realicen en las páginas de origen se implementan automáticamente en la copia de lanzamiento (si está configurada con herencia; es decir, como Live Copy). 
   * Los cambios en la copia de lanzamiento se pueden realizar sin interrumpir las actualizaciones automáticas o las páginas de origen. 

  ![Acciones en paralelo](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Crear un lanzamiento anidado](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch): un lanzamiento dentro de un lanzamiento:
   * El origen es un lanzamiento existente.
   * Puede [promocionar un lanzamiento anidado](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) a cualquier destino; puede ser un lanzamiento principal o las páginas de origen de nivel superior (producción).

  ![Un lanzamiento anidado](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >Al eliminar un lanzamiento, se quitarán el lanzamiento en sí y todos los lanzamientos anidados descendentes.

>[!NOTE]
>
>La creación y edición de lanzamientos requieren derechos de acceso a `/content/launches`, como con el grupo predeterminado `content-authors`.
>
>Si experimenta algún problema, póngase en contacto con el administrador del sistema. 

## Lanzamientos en referencias (consola Sites) {#launches-in-references-sites-console}

1. En la consola **Sites**, vaya al origen de los lanzamientos.
1. Abra el carril **Referencias** y seleccione la página de origen.
1. Seleccione **Lanzamientos**, y se mostrarán los lanzamientos existentes, así como el acceso a la **consola Lanzamientos**:

   ![Referencias de lanzamientos en la consola Sites](/help/sites-cloud/authoring/assets/launches-references.png)

1. Seleccione el lanzamiento adecuado y se mostrará la lista de acciones posibles:

   ![Acciones que se deben realizar en lanzamientos desde la consola Sitios](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## La consola Lanzamientos {#the-launches-console}

>[!NOTE]
>
>Esta consola solo es para Lanzamientos para páginas.
>
>Para administrar los fragmentos de contenido, consulte [Inicios para fragmentos de contenido](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).

La consola Lanzamientos proporciona una descripción general de los lanzamientos y le permite actuar sobre los enumerados.

![Consola de lanzamiento: administrar contenido](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

Se puede acceder a la consola desde: 

* La consola **Herramientas**: **Herramientas**, **General**, **Lanzamientos**.

* La **consola Lanzamientos** se encuentra en la parte inferior de la sección **Lanzamientos** del carril **Referencias** al navegar por el contenido de origen en la consola Sitios.

  ![Consola Lanzamientos en Referencias de lanzamientos en la consola Sitios](/help/sites-cloud/authoring/assets/launches-references.png)

* El botón **Lanzamientos** se encuentra en la parte superior derecha al navegar por el contenido de lanzamiento en la consola Sitios:

  ![Opción Lanzamientos en la consola Sitios](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
