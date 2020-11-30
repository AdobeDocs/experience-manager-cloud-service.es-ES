---
title: Edición de lanzamientos
description: 'Después de crear el lanzamiento para la página (o el conjunto de páginas), se puede editar el contenido de la copia de inicio de las páginas. '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 93%

---


# Edición de lanzamientos {#editing-launches}

## Editar páginas de lanzamiento {#editing-launch-pages}

Cuando se crea un lanzamiento de una página (o conjunto de páginas), se puede editar el contenido de la copia de lanzamiento de la página.

1. Acceda a [Lanzamiento desde las referencias (consola de sitios)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Ir a página** para abrir la página para editarla.

### Editar páginas de lanzamiento sujetas a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Si el lanzamiento se basa en una Live Copy, deberá hacer lo siguiente: <!--If your launch is based upon a [live copy](/help/sites-administering/msm.md) then you will:-->

* Consulte Bloqueo de símbolos (pequeños candados) al editar un componente (contenido y/o propiedades).
* See the **Live Copy** tab in **Page Properties**

Se utiliza una Live Copy para sincronizar contenido *desde* la rama de origen *a* la rama de lanzamiento (para mantener el lanzamiento actualizado con los cambios realizados en la fuente).

Puede realizar cambios, del mismo modo que puede editar una Live Copy estándar; por ejemplo:

* Al hacer clic en un candado cerrado interrumpirá la sincronización y podrá utilizar nuevas actualizaciones de contenido en el lanzamiento. Una vez que se desbloquea (icono del candado abierto), los cambios no se sobrescriben con ningún cambio que se realice en la misma ubicación de la rama de origen.
* **Suspender** (y **reanudar**) la herencia de una página específica.

Consulte Cambiar el contenido de una Live Copy para obtener más información. <!--See [Changing Live Copy Content](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) for further information.-->

## Comparar una página de lanzamiento con su página de origen {#comparing-a-launch-page-to-its-source-page}

Para rastrear los cambios realizados, puede ver el lanzamiento en **Referencias** y comparar la página de lanzamiento con la página de origen:

1. En la consola **Sitios**, [vaya a la página de origen del lanzamiento y selecciónela](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra el panel **[Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** y seleccione **Lanzamientos**.
1. Seleccione un lanzamiento específico y la opción **Comparar con el origen**:

   ![Comparación entre inicio y origen](/help/sites-cloud/authoring/assets/launches-compare.png)

1. Las dos páginas (lanzamiento y origen) se abrirán en paralelo.

   Para obtener información completa sobre el uso de esta característica, consulte la [diferencia de la página](/help/sites-cloud/authoring/features/page-diff.md).

## Cambiar las páginas de origen utilizadas {#changing-the-source-pages-used}

Puede añadir en cualquier momento las páginas en el rango de páginas de origen para el lanzamiento, o eliminarlas: 

1. Acceda y seleccione el lanzamiento de:
   * The [Launches console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleccione **Editar**.
   * [Referencias (consola Sitios)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles:
      * Seleccione **Editar lanzamiento**. 
      * Las páginas de origen se mostrarán.
1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.

>[!NOTE]
>
>Para añadir páginas a un lanzamiento, deben estar bajo una raíz de idioma común; es decir, dentro de un solo sitio.

## Editar una configuración de lanzamiento {#editing-a-launch-configuration}

Las propiedades del lanzamiento se pueden editar en cualquier momento:

1. Acceda y seleccione el lanzamiento de:
   * La [consola Lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleccione **Propiedades**.
   * [Referencias (consola Sitios)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles:
      * Seleccione **Editar propiedades**. 
      * Se mostrarán los detalles.
1. Realice los cambios necesarios y confirme haciendo clic en **Guardar**.
   * Consulte [Lanzamientos: orden de eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obtener información sobre la finalidad y la interacción de los campos **Fecha de inicio** y **Producción lista**.

## Detección del estado de lanzamiento de una página {#discovering-the-launch-status-of-a-page}

Se muestra el estado cuando se selecciona un lanzamiento específico en la ficha de referencias (consulte [Lanzamientos en las referencias (consola Sitios)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Descubrimiento del estado de inicio](/help/sites-cloud/authoring/assets/launches-status.png)
