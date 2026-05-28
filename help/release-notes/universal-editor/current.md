---
title: Notas de la versión de Universal Editor 2026.05.28
description: Estas son las notas de la versión de la versión 2026.05.28 de Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 90bc340948b55150166d5a09b65c41425e5dbd01
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 14%

---


# Notas de la versión de Universal Editor 2026.05.28 {#release-notes}

Estas son las notas de la versión del editor universal del 28 de mayo de 2026.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novedades {#what-is-new}

* Se ha agregado un nuevo botón a la barra de herramientas [ para obtener acceso a las propiedades de página de AEM.](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)
   * Esto lleva la funcionalidad de la anterior `aem-page-properties` [extensión](/help/implementing/universal-editor/extending.md) de forma nativa al editor universal.
   * El botón solo se muestra cuando la página remota tiene una [conexión con el protocolo ](/help/implementing/universal-editor/component-definition.md#plugins) `aem` o `xwalk` y se puede resolver una ruta de acceso de página única desde el archivo editable actual.

## Otras mejoras {#other-improvements}

* El color de fondo predeterminado del lienzo de edición ahora es blanco (#FFFFFF) cuando la aplicación no establece ningún color de fondo propio.
* Se corrigió un problema en el cual la copia y pegado entre páginas no funcionaba.
