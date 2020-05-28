---
title: Información general de AEM System
description: Información general de AEM System
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%

---


# Información general de AEM System {#aem-system}

En esta página se describe Información general del sistema de Adobe Experience Manager (AEM).

## Fondo {#background}

Este patrón se utiliza para identificar la información general que proporciona una visión general del sistema AEM. La información puede incluir elementos como:

Versión de AEM Productos de AEM utilizados (sitios, recursos, formularios, etc.) Recuentos de nodos (páginas, recursos, etc.)

## Datos del patrón {#pattern-data}

En la representación JSON del patrón se incluyen los siguientes objetos:

* **item.message**: hace referencia al mensaje del patrón.
* **item.context**: hace referencia a información adicional sobre la información general:
   * *type*: El tipo de datos de contexto, ya sea &quot;aem.version&quot;, &quot;aem.product&quot; o &quot;node.count&quot;.
   * *data*: Un objeto JSON que contiene los datos correspondientes al tipo: &quot;version&quot; (cadena), &quot;product&quot; (cadena) o &quot;count&quot; (entero).

### Posibles consecuencias y riesgos {#possible-implications}

No aplicable.

### Posibles soluciones  {#possible-solutions}

No aplicable.
