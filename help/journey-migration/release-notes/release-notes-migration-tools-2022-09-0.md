---
title: Notas de la versión para las herramientas de migración en la versión 2022.9.0 de AEM as a Cloud Service
description: Notas de la versión para las herramientas de migración en la versión 2022.9.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---

# Notas de la versión para las herramientas de migración en la versión 2022.9.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2022.9.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.34 es el 12 de septiembre de 2022.

### Novedades {#what-is-new-bpa}

* Ahora, BPA puede detectar e informar sobre si el cliente ha agregado una configuración de registrador personalizada. AEM as a Cloud Service no admite archivos de registro personalizados. Es necesario canalizar todos los archivos de registro a `error.log`
* BPA ahora puede informar sobre los diferentes tipos MIME binarios presentes en el repositorio del cliente y los recuentos asociados a ellos.

### Correcciones de errores {#bug-fixes-bpa}

* La interfaz de usuario de BPA tenía problemas de procesamiento al mostrar un gran número de conclusiones en un solo patrón. Esto se ha corregido.
* El BPA informaba incorrectamente de algunos hallazgos como cambios no compatibles con una gravedad crítica. Esto se ha corregido.
