---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.06.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.06.0 de
feature: Release Information
source-git-commit: 88227693b7dfc3cbd30751718dc85e55ee67bb96
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.06.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración de la versión 2022.06.0 de as a Cloud Service.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v2.0.20 es el 8 de junio de 2023.

### Novedades {#what-is-new-ctt}

* Con esta versión se ha integrado una nueva herramienta de migración, el transformador de contenido (CT), con la herramienta de transferencia de contenido (CTT). El transformador de contenido puede detectar y corregir automáticamente los problemas relacionados con el contenido notificados por el [Analizador de prácticas recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) AEM antes de migrar el contenido de su implementación actual de la (On-Premise o Managed Services AEM) a la as a Cloud Service de la.
Los beneficios que proporciona el transformador de contenido son:
   * Seguridad contra fallos: el transformador de contenido crea un paquete cada vez que realiza alguna modificación en el repositorio para solucionar problemas. Si es necesario, puede volver al estado anterior instalando el paquete.
   * Fácil de usar: el transformador de contenido se ha integrado con la herramienta de transferencia de contenido y viene con una interfaz de usuario sencilla e intuitiva.
   * Ahorra tiempo: cuando tiene un gran número de problemas de contenido que se incluyen en una categoría de patrón, puede resolverlos todos con solo un par de clics con el transformador de contenido, lo que reduce significativamente el tiempo y la complejidad de la migración.
