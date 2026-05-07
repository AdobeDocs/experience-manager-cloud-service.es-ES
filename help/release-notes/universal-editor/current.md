---
title: Notas de la versión de Universal Editor 2026.05.07
description: Estas son las notas de la versión de la versión 2026.05.07 de Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 4f66cd6048d7a78bea33c0f9c21017983b9032d5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 12%

---


# Notas de la versión de Universal Editor 2026.05.07 {#release-notes}

Estas son las notas de la versión del editor universal del 7 de mayo de 2026.

>[!TIP]
>
>Si desea probar las **próximas** funciones del editor universal antes de su lanzamiento, consulte las [notas de la versión del editor universal.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, consulte [esta página.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novedades {#what-is-new}

* Ahora puede [arrastrar y soltar componentes en el editor para moverlos.](/help/sites-cloud/authoring/universal-editor/authoring.md#drag-and-drop-move)
* Se ha introducido un trabajo de servicio para reducir la latencia entre la interfaz de usuario del editor universal y los sistemas back-end.
* Todos los adaptadores para fragmentos de contenido (AEM 6.5, OpenAPI y GraphQL) ahora incluyen los filtros para el selector de recursos para garantizar la coherencia y que los usuarios solo puedan seleccionar los recursos permitidos.
* Ahora se proporciona la intención `content:patch`.
* Para ayudar con la accesibilidad, se han definido el flujo de creación y los puntos de referencia.

## Otras mejoras próximas {#other-improvements}

* Se eliminaron aserciones de tipo innecesarias en `assignImageDimensionFields`.
* Y se corrigió un problema en el cual la administración del lado del servidor de la operación `add` iteraba el valor de cadena, tratándolo como un objeto en lugar de como un parche.
