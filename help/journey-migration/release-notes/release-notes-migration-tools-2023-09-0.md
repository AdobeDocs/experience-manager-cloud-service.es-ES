---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.09.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.09.0 de
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
source-git-commit: c89ca7320d8f31d2545cadf98f39e577337b8918
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.09.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración en la versión as a Cloud Service 2022.09.0 de.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v3.0.0 es el 7 de septiembre de 2023.

### Novedades {#what-is-new-ctt}

La herramienta de transferencia de contenido se ha mejorado considerablemente para ofrecer las siguientes ventajas:
* Se ha reducido el tiempo de transferencia al migrar un subconjunto de un repositorio de contenido mediante AzCopy para copiar solo los ID de blob necesarios en lugar de copiar todos los ID de blob
* Reposiciones de contenido diferencial más rápidas con la actualización de Oak
* Se ha mejorado la solidez al separar el proceso de indexación del proceso de ingesta de contenido. En caso de error de indexación, no es necesario volver a ingerir el contenido. Solo la indexación se reiniciará automáticamente, lo que ahorrará un tiempo y esfuerzo significativos
