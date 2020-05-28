---
title: Personalización detectada
description: Personalización detectada
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 3%

---


# Personalización detectada {#cust-pattern}

Esta página describe el código de patrón de Personalización detectado.

## Fondo {#background}

Este código de patrón se utiliza para identificar las personalizaciones realizadas en la instancia de AEM. Como la personalización de AEM es común, este patrón no necesariamente indica que haya un problema. Identifica un registro de personalizaciones para poder evaluarlas con respecto a su impacto en los planes de actualización.

Las personalizaciones detectadas incluyen:

* Código del cliente (paquetes) y configuraciones
* Paquetes de terceros
* Integraciones con servicios de terceros
* Índices de roble no estándar

## Datos del patrón {#pattern-data}

En la representación JSON del patrón se incluyen los siguientes objetos:

* **item.message**: hace referencia al mensaje del patrón.
* **item.context**: hace referencia a información adicional sobre la información general:
   * *type*: customization.detect.
   * *data*: Un objeto JSON que contiene los datos que describen la personalización

### Posibles consecuencias y riesgos {#possible-implications}

No aplicable.

### Posibles soluciones  {#possible-solutions}

No aplicable.
