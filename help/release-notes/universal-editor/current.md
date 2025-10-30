---
title: Notas de la versión 2025.10.30 del editor universal
description: Estas son las notas de la versión 2025.10.30 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: e3e571bef450ddc09eb30ab7d73b144ea521a87b
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 58%

---


# Notas de la versión 2025.10.30 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 30 de octubre de 2025.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* [El nuevo RTE](#new-rte) ahora puede insertar imágenes.
   * Esta característica está deshabilitada para OtB y debe habilitarse explícitamente mediante una definición de filtro [Filter.](/help/implementing/universal-editor/configure-rte.md#toolbar)

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas nuevas funciones y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, que cuenta con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho. [Este RTE cuenta con opciones de configuración flexibles.](/help/implementing/universal-editor/configure-rte.md)

## Otras mejoras {#other-improvements}

* Ahora se informa al evento de actualización si la acción se ha deshecho.
* La cadena `No results` ahora depende de la configuración regional del explorador en las etiquetas del Editor universal.
* Se ha corregido un salto de línea adicional en el botón de publicación del Editor universal.
* Se ha realizado la limpieza para aplicar parches a la API.
* El botón Seleccionar contenido ahora está visible en Safari.
* Se corrigió la compilación de RPM.
* Actualización de CORS para evitar volver a actualizar el texto editado después de guardarlo.
