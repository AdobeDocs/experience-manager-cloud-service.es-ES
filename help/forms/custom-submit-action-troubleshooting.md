---
title: Solución de problemas con el error 502 en la acción de envío personalizada para Forms adaptable
description: Obtenga información sobre cómo identificar y resolver 502 páginas de error que se producen al utilizar acciones de envío personalizadas en Forms adaptable (componentes principales). Esta guía explica causas comunes, como las excepciones no controladas, y proporciona pasos de resolución.
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---


# Solución de problemas: Página de error 502 en la acción de envío personalizada

Al trabajar con Forms adaptable (componentes principales), puede encontrar una página de error **502 en HTML** después de enviar un formulario que usa una acción de envío personalizada.

## Problema

**Error:** Se muestra una página de error 502 en HTML cuando falla un servicio de acción de envío personalizado.

**Motivo:** Esto sucede si la acción de envío personalizada genera un error no controlado, por ejemplo, un puntero nulo, una respuesta de API no válida o un error de tiempo de ejecución.

## Resolución

Para evitar la página de error 502, ajuste la lógica de envío con bloques try-catch para gestionar correctamente los errores.

Para ver los pasos detallados, consulte [Crear una acción de envío personalizada para Forms adaptable (componentes principales)](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md).
