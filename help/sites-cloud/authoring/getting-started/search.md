---
title: Búsqueda
description: Encuentre su contenido más rápidamente con una búsqueda completa
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 83%

---

# Búsqueda   {#search-feature}

El entorno de autor AEM ofrece varios mecanismos para buscar contenido, en función del tipo de recurso.

## Conceptos básicos de búsqueda {#search-basics}

La función de búsqueda está disponible en la barra de herramientas superior:

![Icono de búsqueda](/help/sites-cloud/authoring/assets/search-icon.png)

Con el carril de búsqueda puede:

* Busque una palabra clave, una ruta o una etiqueta específicas.
* Filtre según criterios específicos de recurso, como fechas de modificación, estados de página, tamaño de archivo, etc.
* Defina y utilice una [búsqueda guardada](#saved-searches) según los criterios anteriores

>[!NOTE]
>
>También se puede iniciar una búsqueda con la tecla de función `/` (barra diagonal) cuando el carril de búsqueda esté visible.

## Buscar y filtrar {#search-and-filter}

Para buscar y filtrar sus recursos: 

1. Abra **Buscar** (con la lupa de la barra de herramientas) y escriba el término de búsqueda. Se ofrecen sugerencias que se pueden seleccionar:

   ![Término de búsqueda](/help/sites-cloud/authoring/assets/search-term.png)

   De forma predeterminada, los resultados de la búsqueda están limitados a su ubicación actual (es decir, la consola y el tipo de recurso relacionado): 

   ![Ubicación de la búsqueda](/help/sites-cloud/authoring/assets/search-term-location.png)

1. Si es necesario, puede quitar el filtro de ubicación (seleccione **X** en el filtro que desea eliminar) para buscar en todas las consolas/tipos de recursos.
1. Los resultados se muestran agrupados según la consola y el tipo de recurso relacionado.

   Puede seleccionar un recurso específico (para realizar más acciones), o explorar en profundidad seleccionando el tipo de recurso necesario; por ejemplo, **Ver todos los sitios**:

   ![Resultados de la búsqueda](/help/sites-cloud/authoring/assets/search-results.png)

1. Si desea explorar más en profundidad, seleccione el símbolo de carril (parte superior izquierda) para abrir el panel lateral **Filtros y opciones**.

   ![Botón carril](/help/sites-cloud/authoring/assets/rail-button.png)

   Según el tipo de recurso, la búsqueda mostrará una selección predefinida de criterios de búsqueda o de filtro.

   El panel lateral permite seleccionar:

   * Búsquedas guardadas
   * Directorio de búsqueda
   * Etiquetas
   * Criterios de búsqueda; por ejemplo, fechas de modificación, estado de Publish o estado de Live Copy.

   >[!NOTE]
   >
   >Los criterios de búsqueda pueden variar:
   >
   >* Según el tipo de recurso que haya seleccionado; por ejemplo, los criterios de Assets y Comunidades son comprensiblemente especializados.
   >* Su instancia, al igual que los formularios de búsqueda, se puede personalizar (según la ubicación en AEM).

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![Panel lateral de búsqueda](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. También se pueden agregar términos de búsqueda adicionales.

1. Cierre **Buscar** con la **X** (parte superior derecha).

>[!NOTE]
>
>Los criterios de búsqueda se mantienen al seleccionar un elemento en los resultados de la búsqueda.
>
>Cuando se selecciona un elemento en la página de resultados de la búsqueda, al volver a la página de búsqueda después de usar el botón Atrás del explorador, los criterios de búsqueda se mantienen. 

## Búsquedas guardadas {#saved-searches}

Además de buscar aplicando una amplia gama de criterios, también puede guardar una configuración de búsqueda determinada para recuperarla y utilizarla en otro momento:

1. Defina los criterios de búsqueda y seleccione **Guardar**.

   ![Guardar una búsqueda](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. Asigne un nombre y luego utilice **Guardar** para confirmar la acción:

   ![Guardar una búsqueda con un nombre](/help/sites-cloud/authoring/assets/search-save-name.png)

1. La próxima vez que acceda al panel de búsqueda, la búsqueda guardada estará disponible en el selector:

   ![Búsquedas guardadas](/help/sites-cloud/authoring/assets/saved-searches.png)

1. Una vez guardada, puede hacer lo siguiente:

   * Use **x** (con el nombre de la búsqueda guardada) para iniciar una nueva consulta (la búsqueda guardada en sí no se eliminará).
   * Use la opción **Editar búsqueda guardada**, cambie las condiciones de búsqueda y luego utilice **Guardar** nuevamente.

Las búsquedas guardadas se pueden modificar seleccionando la búsqueda guardada y haciendo clic en **Editar búsqueda guardada** en la parte inferior del panel de búsqueda.

![Modificar una búsqueda guardada](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
