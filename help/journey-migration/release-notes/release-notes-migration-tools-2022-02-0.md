---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.2.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.2.0 de
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 55%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.2.0 de {#release-notes}

AEM Esta página describe las notas de la versión para las herramientas de migración de as a Cloud Service 2022.2.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.24 es el 1 de febrero de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar y crear informes sobre la cantidad de recursos con y sin etiquetas inteligentes.
* Capacidad para detectar y crear informes sobre la versión de componente principal utilizada.
* Capacidad para detectar y crear informes sobre el tipo de nivel de origen (autor o publicación) en el que se ejecutó BPA.

### Correcciones de errores {#bug-fixes-bpa}

* La lógica de tamaño de BPA se hizo más rápida y eficiente.
* En algunos casos, el BPA no incrementó el recuento analizado cuando se ejecutó. Esto se ha corregido.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.8.6 es el 3 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Validación de contenido: los usuarios pueden determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se ha introducido correctamente en la instancia de destino. Para utilizar esta función, actívela en la `System Console` AEM del entorno de origen de la. Consulte [Validación de transferencias de contenido: introducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html#getting-started) para obtener más información.

### Correcciones de errores {#bug-fixes-ctt}

* Algunos usuarios no estaban asignados porque la asignación de usuarios distinguía entre mayúsculas y minúsculas. Esto se ha corregido. La asignación de usuarios ya no distingue entre mayúsculas y minúsculas.
