---
title: Notas de la versión de Universal Editor Preview
description: Estas son las notas de la versión de la vista previa del editor universal.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: f3ba70f276ab534e0becea47390fe58bf8a825d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Notas de la versión de Universal Editor Preview {#preview}

Estas son las notas de la versión de la **versión de vista previa** del editor universal. Estas características están disponibles actualmente en el **entorno de vista previa** del editor universal. Estas funciones están programadas para su lanzamiento general el 7 de mayo de 2026.

Estas notas de la versión de **preview** se proporcionan para que sepa qué cambios se avecinan en el editor universal y pueda probarlos al [cambiar a la versión de vista previa.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Para las **notas de la versión actuales** del editor universal, consulte el documento [Notas de la versión del editor universal.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>El contenido de la versión real y la fecha de lanzamiento están sujetos a cambios.

## Próximas funciones {#upcoming-features}

* Se ha introducido un trabajo de servicio para reducir la latencia entre la interfaz de usuario del editor universal y los sistemas back-end.
* Todos los adaptadores para fragmentos de contenido (AEM 6.5, OpenAPI y GraphQL) ahora incluyen los filtros para el selector de recursos para garantizar la coherencia y que los usuarios solo puedan seleccionar los recursos permitidos.
* Ahora se proporciona la intención `content:patch`.
* Para ayudar con la accesibilidad, se han definido el flujo de creación y los puntos de referencia.

## Otras mejoras próximas {#other-improvements}

* Se eliminaron aserciones de tipo innecesarias en `assignImageDimensionFields`.
* Y se corrigió un problema en el cual la administración del lado del servidor de la operación `add` iteraba el valor de cadena, tratándolo como un objeto en lugar de como un parche.
