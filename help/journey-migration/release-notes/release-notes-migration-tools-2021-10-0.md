---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.10.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.11.0 de
feature: Release Information
exl-id: 6b1caa63-dcb0-4c48-ab2c-fd72617abf13
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 14%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.10.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración de as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=es).

## Cloud Acceleration Manager {#cam-release}

### Fecha de lanzamiento {#release-date-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 25 de octubre de 2021.

### Novedades {#what-is-new-cam}

Cloud Acceleration Manager ahora permite a los usuarios ver informes de BPA históricos en un informe de líneas de tendencias. Con este informe, los usuarios pueden ver el progreso que están realizando en una representación gráfica fácil de consumir. Consulte [Uso de Ver línea de tendencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) para obtener más información.

### Fecha de lanzamiento {#release-date-october-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 4 de octubre de 2021.

### Novedades {#what-is-new-cam-oct}

Cloud Acceleration Manager ahora permite a los usuarios ver los informes de BPA en una vista previa imprimible, lo que permite hacer una impresión simple o una impresión en el PDF para compartir fácilmente. Consulte los pasos 6 y 7 en [Tarjeta de análisis de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.6.0 es el 4 de octubre de 2021.

### Novedades {#what-is-new-ctt-oct}

* Se ha mejorado la herramienta de asignación de usuarios con una experiencia de usuario simplificada que incluye las siguientes funciones. Para obtener más información, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en).
   * Probar la conexión a la API de administración de usuarios antes de ejecutar la asignación de usuarios
   * Omitir correctamente los errores y continuar con la actividad de asignación de usuarios
   * La asignación de usuarios ya no falla si **Token de acceso** caduca pasadas 24 horas. La asignación de usuarios se puede volver a ejecutar desde la última vez que se detuvo.

* Para aumentar la solidez de la herramienta de transferencia de contenido, este se puede ingerir en una instancia de autor o de publicación a la vez. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es) para obtener más información.

* Cuando se incluyen versiones, la ruta `/var/audit` para migrar eventos de auditoría.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa-latest}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.20 es el 5 de octubre de 2021.

### Novedades {#what-is-new-bpa-oct}

* Capacidad para detectar e informar sobre la longitud del nombre del nodo.

* Capacidad para detectar y crear informes sobre el tamaño total del índice.

* Capacidad para detectar e informar sobre recursos que no tienen su representación original.
