---
title: Notas de la versión 2025.03.10 del editor universal
description: Estas son las notas de la versión 2025.03.10 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 23%

---


# Notas de la versión 2025.03.10 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 10 de marzo de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Mover componentes:** [Mover componentes entre contenedores](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) ahora observa el filtro de componentes del contenedor de destino.
   * Ya no es necesario tener la misma [definición de filtro](/help/implementing/universal-editor/filtering.md) para los contenedores de destino y destino a fin de mover el componente entre los contenedores.
* **Páginas bloqueadas:** el servicio de editor universal observa el estado de bloqueo de una página](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page) y solo escribe en páginas que no están bloqueadas o que el usuario las ha bloqueado.[

## Otras mejoras {#other-improvements}

* Se han realizado correcciones para corregir la validación para lienzo sin encabezado.

## Desaprobación {#deprecation}

* La biblioteca `universal-editor-cors` proporcionada a través de npm o `https://unviersal-editor-service.experiencecloud.live/corslib/*` ya no debe usarse.
   * Se debe usar una etiqueta de script que apunte a `https://universal-editor-service.adobe.io/cors.js` en su lugar.
   * Consulte la [Información general del editor universal para desarrolladores de AEM](/help/implementing/universal-editor/developer-overview.md) para obtener detalles sobre cómo instrumentar correctamente la página para usarla con el editor universal.
   * Los usuarios verán un mensaje de obsolescencia una vez al día si se utiliza el método incorrecto.
