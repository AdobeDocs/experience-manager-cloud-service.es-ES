---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2021.10.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.10.0
feature: Release Information
exl-id: null
source-git-commit: 0058cfda65ec8f59dbe3ea1bbcc43c08c5e5fe3e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 6%

---


# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2021.10.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Cloud Acceleration Manager {#cam-release}

### Fecha de la versión {#release-date-cam}

La fecha de versión de Cloud Acceleration Manager es el 25 de octubre de 2021.

### Novedades {#what-is-new-cam}

Cloud Acceleration Manager ahora permite a los usuarios ver informes históricos de BPA en un informe de línea de tendencia. Con este informe, los usuarios pueden ver el progreso que están haciendo en una representación gráfica fácil de usar. Consulte [Uso de Ver línea de tendencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) para obtener más información.

### Fecha de la versión {#release-date-october-cam}

La fecha de versión de Cloud Acceleration Manager es el 4 de octubre de 2021.

### Novedades {#what-is-new-cam-oct}

Cloud Acceleration Manager ahora proporciona a los usuarios la capacidad de ver los informes de BPA en una vista previa imprimible, lo que permite imprimir o imprimir de forma sencilla a un PDF para facilitar el uso compartido. Consulte los pasos 6 y 7 de [Uso de la tarjeta de análisis de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).


## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.6.0 es el 4 de octubre de 2021.

### Novedades {#what-is-new-ctt-oct}

* Herramienta de asignación de usuarios mejorada con una experiencia de usuario simplificada, que incluye las siguientes funciones que se enumeran a continuación. Para obtener más información, consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * Probar la conexión a la API de administración de usuarios antes de ejecutar la asignación de usuarios
   * Omita correctamente los errores y continúe con la actividad de Asignación de usuarios
   * La asignación de usuarios ya no falla si **Token de acceso** caduca a las 24 horas. La asignación de usuarios se puede volver a ejecutar desde donde se detuvo por última vez.

* Para aumentar la solidez de la herramienta de transferencia de contenido, el contenido se puede ingerir a instancias de Autor o de Publicación a la vez. Consulte [Introducción a la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) para obtener más información.

* Cuando se incluyen versiones, la ruta `/var/audit` se incluye automáticamente para migrar eventos de auditoría.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa-latest}

La fecha de versión de Best Practices Analyzer v2.1.20 es el 5 de octubre de 2021.

### Novedades {#what-is-new-bpa-oct}

* Capacidad para detectar y crear informes sobre la longitud del nombre del nodo.

* Capacidad para detectar el tamaño total del índice e informar al respecto.

* Capacidad para detectar y crear informes sobre los recursos que no tienen su representación original.