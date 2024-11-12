---
title: Notas de la versión 2024.11.12 del editor universal
description: Son las notas de la versión 2024.11.12 del editor universal.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 03ccad00e689052ada8cca976d6c385be01d3cc9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 12%

---


# Notas de la versión 2024.11.12 del editor universal {#release-notes}

Estas son las notas de la versión del editor universal del 12 de noviembre de 2024.

>[!TIP]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Novedades {#what-is-new}

* **Opción de reintento en el tiempo de espera de CORS:** Con la [versión 2024.09.26,](/help/release-notes/universal-editor/2024/2024-09-26.md) se introdujo un panel de error cuando el editor no pudo establecer una conexión con la página cargada, lo que evitó estados de carga interminables.
   * Con esta versión, el editor sigue reintentando automáticamente y, una vez establecida la conexión, se puede reanudar la edición.
   * Esto resulta especialmente útil en páginas que pueden tardar más de un minuto en inicializarse.
* **Mejoras de extensibilidad para desarrolladores:** El editor universal ahora admite la difusión de eventos en extensiones, lo que permite a los desarrolladores de extensiones suscribirse a [eventos.](/help/implementing/universal-editor/events.md)
   * Esto permite a los desarrolladores [reaccionar a los eventos del editor dentro de sus extensiones personalizadas.](/help/implementing/universal-editor/customizing.md#extending)
* **Selección persistente de componentes:** Los componentes seleccionados en el editor persistirán incluso después de actualizar el explorador.
   * Esto garantiza que los usuarios puedan seguir trabajando sin perder su contexto al volver a cargar la página.
* **Vínculos rápidos localizados:** La sección **Vínculos rápidos** de la pantalla de inicio ahora proporciona vínculos localizados a la documentación, lo que ayuda a los usuarios a acceder fácilmente a las guías relevantes en función de sus preferencias de idioma.
* **ID de solicitud para depuración avanzada:** Las notificaciones de error ahora incluyen **ID de solicitud** en la sección de detalles, que se correlaciona con `x-request-id header`.
   * Esto facilita a los equipos de ingeniería de Adobe el seguimiento y el diagnóstico de problemas al hacer coincidir esos errores con los registros internos.

## Otras mejoras {#other-improvements}

* **Etiquetas largas de árbol de contenido fijas:** Se ha resuelto un problema por el que las etiquetas largas del panel **Árbol de contenido** se cortaban
   * Esto garantiza que los controladores de arrastrar y soltar siempre estén visibles para la reordenación del contenido.
* **Etiquetas de propiedades largas fijas:** Se corrigió un error en el que las etiquetas de campos largos del panel **Propiedades** se superponían con la información de validación de campos
* **Desplazamiento horizontal en el panel Propiedades:** Se ha corregido un problema por el que los elementos anchos en el panel **Propiedades** provocaban un desplazamiento horizontal
* **Se ha corregido la barra de herramientas inactiva durante las notificaciones:** La barra de herramientas superior de **Adobe Experience Cloud** ahora funciona por completo cuando se muestran las notificaciones de [toast](https://spectrum.adobe.com/page/toast/).
* **Estabilidad mejorada:** Se agregaron límites de error para gestionar valores inesperados, lo que evita que toda la interfaz de usuario se bloquee cuando falla un solo procesador o validador, lo que mejora la solidez
