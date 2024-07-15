---
title: Notas de la versión de las herramientas de migración en la versión 2023.10.0 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2022.10.0 de AEM as a Cloud Service
feature: Release Information
exl-id: e5250b5b-a56c-4bf0-8510-2334a12e36b6
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 4%

---

# Notas de la versión de las herramientas de migración en la versión 2023.10.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2023.10.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v3.0.4 es el 6 de octubre de 2023.

### Novedades {#what-is-new-ctt}

* AEM Se han realizado cambios en el proceso de ingesta de contenido: ya no es necesario enviar un ticket de servicio de atención al cliente/asistencia para deshabilitar las actualizaciones de la versión de la en el entorno de destino. Este proceso está ahora automatizado. AEM Para obtener más información, consulte [Actualizaciones e ingestas de versiones](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#aem-version-updates-and-ingestions)
* La concurrencia dinámica se utilizará durante el paso [previo a la copia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) tanto en las fases de extracción como de ingesta, lo que reducirá significativamente el tiempo de migración del contenido.
