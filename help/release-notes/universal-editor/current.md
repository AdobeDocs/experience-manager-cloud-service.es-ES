---
title: Notas de la versión de Universal Editor 2024.09.3
description: Estas son las notas de la versión de la versión 2024.09.3 del Editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b70acef8dc259fff3041617abe0a89f7eb73dfab
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# Notas de la versión de Universal Editor 2024.09.3 {#release-notes}

Estas son las notas de la versión del editor universal del 3 de septiembre de 2024.

>[!TIP]
>
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novedades de la aplicación {#what-is-new}

* AEM **`rootPath`ya está disponible para el selector de contenido**: ahora se puede proporcionar al selector de contenido un `rootPath` para presentar al usuario una selección de contenido de destino al usar los tipos de campo [Contenido,](/help/implementing/universal-editor/field-types.md#aem-content) [Fragmento de contenido,](/help/implementing/universal-editor/field-types.md#content-fragment) y [Fragmento de experiencia](/help/implementing/universal-editor/field-types.md#experience-fragment).
   * Por lo tanto, la selección de contenido se limita al contenido en la ruta especificada y a cualquier subdirectorio.

## Programa de adopción anticipada para el soporte de 6.5 {#early-adoption}

AEM El editor universal ya está disponible para casos de uso sin encabezado al utilizar la versión 6.5 de la aplicación como parte de un programa de adopción anticipada.

Si está interesado en probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a su representante de Adobe desde la dirección de correo electrónico asociada a su Adobe ID.

## Correcciones de errores {#bug-fixes}

* **Arrastrar y soltar en contenedores múltiples**: [Mover componentes entre contenedores diferentes mediante arrastrar y soltar](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) ahora respeta [los filtros de componentes](/help/implementing/universal-editor/customizing.md#filtering-components) tanto en el origen como en el destino.
