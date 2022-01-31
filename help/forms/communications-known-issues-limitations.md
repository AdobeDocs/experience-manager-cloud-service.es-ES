---
title: 'Problemas conocidos '
description: Prácticas recomendadas de comunicaciones, problemas conocidos y limitaciones
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Preguntas más frecuentes, prácticas recomendadas, problemas conocidos y limitaciones {#best-practices-known-issues-and-limitations}

Antes de empezar a usar las API de comunicación, consulte las preguntas más frecuentes y revise los siguientes problemas y limitaciones conocidos:

## Problemas conocidos

- Puede utilizar un tipo de renderización específico (PDF, PRINT) solo una vez en la lista de opciones de impresión. Por ejemplo, no puede tener dos opciones de IMPRESIÓN cada una que especifique un tipo de renderizado PCL.

- Para una configuración por lotes, solo una instancia de combinación de valores de OutputType(PDF, PRINT) y RenderType(PostScript, PCL, IPL, ZPL, etc.) está permitido.

## Prácticas recomendadas  

- Adobe recomienda alojar los archivos de datos en el almacén de contenedores de blob en la región de la nube utilizada por AEM Cloud Service.

## Preguntas frecuentes {#faq}

**¿Puedo utilizar una carpeta vigilada u otros mecanismos de almacenamiento para almacenar entradas y salidas?**

En este momento, puede utilizar el almacenamiento de Microsoft Azure para guardar datos de entrada y documentos generados. El almacenamiento de Microsoft Azure ofrece varias opciones para [automatizar las operaciones de movimiento de datos](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**¿Se incluye una cuenta de almacenamiento de Microsoft Azure con licencia de Cloud Service de Experience Manager Forms?**

La cuenta de almacenamiento de Microsoft Azure es independiente de la licencia de Cloud Service de Experience Manager Forms.

**¿Las API de comunicación almacenan datos en los servidores Cloud Service de Experience Manager Forms?**

Los datos de entrada y salida solo se guardan en el almacenamiento de Microsoft Azure.

**¿Las API de comunicación solo están disponibles para el Cloud Service de Experience Manager Forms? ¿Puedo obtener una funcionalidad similar en el entorno local?**

Puede utilizar el servicio de salida de AEM Forms para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL y ZPL.

En comparación con el entorno local, el Cloud Service ofrece beneficios adicionales de escalado automático y rentabilidad.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**¿Puedo ejecutar varias operaciones por lotes simultáneamente?**
Sí, puede ejecutar varias operaciones por lotes de forma similar. Utilice siempre carpetas de origen y destino diferentes para cada operación a fin de evitar conflictos.
