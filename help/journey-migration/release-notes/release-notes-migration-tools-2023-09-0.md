---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.09.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.09.0 de
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 4%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.09.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración en la versión as a Cloud Service 2023.09.0 de la versión de.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v3.0.0 es el 7 de septiembre de 2023.

### Novedades {#what-is-new-ctt}

La herramienta de transferencia de contenido se ha mejorado para proporcionar las siguientes ventajas:

* Se ha reducido el tiempo de transferencia al migrar un subconjunto de un repositorio de contenido mediante AzCopy para copiar solo los ID de blob necesarios en lugar de copiar todos los ID de blob.
* Reposiciones de contenido diferencial más rápidas con la actualización de Oak.
* Se ha mejorado la solidez al separar el proceso de indexación del proceso de ingesta de contenido. Si se produce un error en la indexación, no es necesario volver a introducir el contenido. Solo la indexación se reinicia automáticamente, lo que ahorra un tiempo y esfuerzo significativos.
