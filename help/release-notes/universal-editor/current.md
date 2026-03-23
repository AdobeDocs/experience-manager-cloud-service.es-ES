---
title: Notas de la versión 2026.03.19 del editor universal
description: Estas son las notas de la versión 2026.03.19 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 048e86fe7930173bb33de9252607e2910520b575
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 34%

---


# Notas de la versión 2026.03.19 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 19 de marzo de 2026.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* Los elementos de las propiedades ahora se contraen al volver a [la pantalla principal.](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [El selector de recursos](/help/implementing/universal-editor/configure-assets-selector.md) ahora admite [definiciones de filtros.](/help/implementing/universal-editor/filtering.md)
* Si no hay acciones disponibles para el elemento seleccionado, [el menú contextual](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu) muestra ahora un mensaje que lo indica.

## Otras mejoras {#other-improvements}

* Si hay una definición de modelo, filtro o componente, se recuperará al cambiar de una aplicación a otra en el editor.
* La eliminación de una imagen ya no deja etiquetas de imagen vacías al utilizar DA como back end.
* Las clases en bloques ahora se gestionan correctamente al utilizar DA como back end.
* Open API ahora guarda los recursos remotos correctamente como objetos.

## Cambio radical {#breaking-change}

* Todas las extensiones deben actualizarse a `@adobe/uix-guest` >= `1.1.7` para mejorar la estabilidad.
