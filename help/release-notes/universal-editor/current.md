---
title: Notas de la versión 2024.12.02 del editor universal
description: Estas son las notas de la versión 2024.12.02 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 16%

---


# Notas de la versión 2024.12.02 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 2 de diciembre de 2024.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Navegación por teclado del árbol de contenido**: [El árbol de contenido,](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) disponible en el panel lateral, ahora es totalmente accesible mediante el teclado.
   * Los autores pueden navegar e interactuar con elementos de vista de árbol mediante controles de teclado estándar, siguiendo las [directrices WCAG 2.1](/help/sites-cloud/authoring/page-editor/accessible-content.md) para accesibilidad.
   * Esta mejora garantiza que todos los elementos interactivos del árbol se puedan utilizar con el teclado, lo que mejora la inclusividad de los usuarios que dependen de la navegación mediante el teclado.
* **Anulación de selección de elementos editables**: los autores ahora pueden anular la selección de elementos editables seleccionados anteriormente en la página.
   * Esto elimina las distracciones cuando los autores desean ver la página sin bordes de selección activos.
* **Selector de fragmentos**: en las instancias de AEM as a Cloud Service, las referencias a fragmentos ahora abren el selector de fragmentos como selector de contenido, lo que ofrece una funcionalidad mejorada, como obedecer a los modelos de fragmentos de contenido permitidos, buscar fragmentos de contenido y una experiencia general mejorada.
   * Esto se alinea con otras IU de Adobe y mejora la coherencia.
   * AEM [Para entornos de 6.5 de la,](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) el selector de contenido existente permanece en uso.
* **Descripción del contenedor**: [El componente contenedor](/help/implementing/universal-editor/field-types.md#container) utilizado en el panel [propiedades,](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail) para hacer referencia al contenido, ahora admite un atributo de descripción, mostrado sobre los campos de contenedor.
   * Esta adición mejora la claridad al proporcionar a los autores contexto sobre los campos agrupados que están editando.

## Otras mejoras {#other-improvements}

* **Sincronización de campos de texto enriquecido**: se mejoró la sincronización del contenido sin procesar y procesado en los campos de texto enriquecido en el panel de propiedades, y se solucionaron problemas en los proyectos de Edge Delivery Services en los que el contenido de texto enriquecido y la representación procesada pueden diferir.
* **Eventos de modo de edición**: el editor universal ahora emite de forma fiable eventos de modo de edición, incluso después de volver a cargar aplicaciones remotas.
