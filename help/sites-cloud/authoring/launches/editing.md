---
title: Edición de lanzamientos
description: Después de crear un lanzamiento para la página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 87%

---

# Edición de lanzamientos {#editing-launches}

## Edición de páginas de lanzamiento {#editing-launch-pages}

Cuando se ha creado un lanzamiento para una página (o conjunto de páginas), puede editar el contenido en la copia de lanzamiento de las páginas.

1. Acceda a [Lanzamiento desde las referencias (consola Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Ir a la página** para abrir la página y editarla.

Al editar la página, puede ver una indicación en la barra de herramientas superior, junto con el **Salir** y **Navegar** opciones:

![Salir y navegar por el lanzamiento desde el editor de páginas](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>No se le permite mover una página dentro de un lanzamiento. Si se intenta esta acción, se generará un mensaje de advertencia:
>
>* Advertencia: Esta página es el origen de un lanzamiento. No se permite mover la página.

### Editar páginas de lanzamiento sujetas a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Si el lanzamiento se basa en una [Live Copy](/help/sites-cloud/administering/msm/overview.md), deberá hacer lo siguiente:

* Consulte los símbolos de bloqueo (en forma de pequeños candados) cuando edite un componente (contenido o propiedades).
* Consulte la pestaña **Live Copy** en **Propiedades de página**

Se utiliza una Live Copy para sincronizar contenido *desde* la rama de origen *a* la rama de lanzamiento (para mantener el lanzamiento actualizado con los cambios realizados en la fuente).

Puede realizar cambios de la misma manera que puede editar una Live Copy estándar; por ejemplo:

* Al hacer clic en un candado cerrado, se interrumpirá esta sincronización y se le permitirá realizar nuevas actualizaciones del contenido en el lanzamiento. Una vez desbloqueados (candado abierto), los cambios no se sobrescribirán con ningún cambio realizado en la misma ubicación dentro de la rama de origen.
* **Suspender** (y **reanudar**) la herencia de una página específica.

Consulte [Cambio del contenido de Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) para obtener más información.

## Comparación de una página de lanzamiento con su página de origen {#comparing-a-launch-page-to-its-source-page}

Para rastrear los cambios realizados, puede ver el lanzamiento en **Referencias** y comparar la página de lanzamiento con la página de origen:

1. En la consola **Sitios**, [vaya a la página de origen del lanzamiento y seleccione uno](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra el panel **[Referencias](/help/sites-cloud/authoring/basic-handling.md#references)** y seleccione **Lanzamientos**.
1. Seleccione el lanzamiento específico y luego **Comparar con el origen**:

   ![Comparación entre el lanzamiento y el origen](/help/sites-cloud/authoring/assets/launches-compare.png)

1. Las dos páginas (inicio y origen) se abrirán una junto a la otra.

   Para obtener información completa sobre el uso de esta funcionalidad, consulte [Diferencias de página](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Cambio de las páginas de origen utilizadas {#changing-the-source-pages-used}

Puede añadir en cualquier momento las páginas en el rango de páginas de origen para el lanzamiento, o eliminarlas: 

1. Acceda y seleccione el lanzamiento de:
   * La [consola Lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleccione **Editar**.
   * [Referencias (consola Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles:
      * Seleccione **Editar lanzamiento**. 
      * Se muestran las páginas de origen.
1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

>[!NOTE]
>
>Para añadir páginas a un lanzamiento, deben estar debajo de una raíz de idioma común; es decir, dentro de un solo sitio.

## Edición de una configuración de lanzamiento {#editing-a-launch-configuration}

Las propiedades del lanzamiento se pueden editar en cualquier momento:

1. Acceda y seleccione el lanzamiento de:
   * la [consola Lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleccione **Propiedades**.
   * [Referencias (consola Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles:
      * Seleccione **Editar propiedades**. 
      * Se muestran los detalles.
1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.
   * Consulte [Lanzamientos: el orden de los eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obtener información sobre el propósito y la interacción de los campos **Fecha de lanzamiento** y **Listo para producción**.

## Descubrimiento del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

El estado se muestra al seleccionar un lanzamiento específico en la pestaña Referencias (consulte [Lanzamientos en referencias (consola Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Descubrimiento del estado de lanzamiento](/help/sites-cloud/authoring/assets/launches-status.png)
