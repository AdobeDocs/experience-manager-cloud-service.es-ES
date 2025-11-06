---
title: Notas de la versión 2025.11.06 del editor universal
description: Estas son las notas de la versión 2025.11.06 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5c762da645ee26164d39af3936fc6b3fcbd43f0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 50%

---


# Notas de la versión 2025.11.06 del editor universal {#release-notes}

Estas son las notas de la versión del 6 de noviembre de 2025 de Universal Editor.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Funciones de adopción anticipada {#early-adopter}

Si le interesa probar estas nuevas funciones y compartir sus comentarios, envíe un correo electrónico a su Adobe Customer Success Manager desde la dirección de correo electrónico asociada a su Adobe ID.

### Nuevo RTE {#new-rte}

El nuevo RTE de ProseMirror, que cuenta con un selector de páginas en el cuadro de diálogo de vínculos, ya está disponible en el panel derecho. [Este RTE cuenta con opciones de configuración flexibles.](/help/implementing/universal-editor/configure-rte.md)

## Otras mejoras {#other-improvements}

* `og:title` campos de metadatos ahora se pueden eliminar correctamente.
* Se ha corregido un problema de navegación cuando un usuario edita la barra de ubicación en el editor del explorador de modo que los cambios se reflejen correctamente y el editor o la aplicación ahora naveguen a la URL solicitada.
* Se corrigió la resolución del modelo de campo y el editor utiliza el modelo del componente, si lo hay.
* El componentId ahora se incluye en la acción /add.
* Se ha corregido la posibilidad de eliminar algunas propiedades de metadatos que anteriormente no se podían eliminar.
* La captura sin procesar ahora se realiza de forma condicional para xwalk cuando no la establece el complemento de AEM.
* Se ha corregido la administración de MSM de fragmentos de contenido con RTE.
* Ahora se admite el resaltado de imágenes en una imagen.

