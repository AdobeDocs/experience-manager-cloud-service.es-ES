---
title: Notas de la versión 2054.01.16 del editor universal
description: Estas son las notas de la versión 2025.01.16 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 19%

---


# Notas de la versión 2025.01.16 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 16 de enero de 2025.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Desuso de la biblioteca CORS &lt; 3.0.0**: para garantizar la compatibilidad futura y mejorar la seguridad, el editor universal ahora admite exclusivamente la versión 3.0.0 o superior de
  `@Adobe Express/universal-editor-cors` biblioteca.
   * La biblioteca ahora se entrega únicamente a través de [`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js)
   * Aparece una notificación de obsolescencia para los usuarios al abrir una página que utiliza versiones anteriores de la biblioteca CORS, pidiéndoles que se actualicen.
* **Punto de extensión para la página de aterrizaje** - [Se ha introducido un nuevo punto de extensión](/help/implementing/universal-editor/customizing.md#extending) para que las extensiones aparezcan en el carril lateral de la página de aterrizaje del Editor universal.
   * Ahora los desarrolladores pueden especificar si las extensiones son aplicables al editor, a la página de aterrizaje o a ambos, lo que ofrece una mayor personalización y facilidad de uso.

## Otras mejoras {#other-improvements}

* **Se corrigieron direcciones URL no válidas en elementos recientes de la página de aterrizaje**. Se resolvió un problema por el que se dañaban las direcciones URL mostradas en la lista &quot;Recientes&quot; de la página de aterrizaje del Editor universal.
* **Sincronización de temas en Unified Shell**: el editor universal ahora sincroniza dinámicamente el tema con la configuración de Unified Shell del sistema y ajusta automáticamente entre los modos claro y oscuro.
   * Esto garantiza un aspecto visual coherente en todos los microfront, incluidos los selectores de fragmentos y recursos.
