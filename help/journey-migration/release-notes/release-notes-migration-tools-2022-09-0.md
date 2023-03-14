---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.9.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.9.0 de
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.9.0 de {#release-notes}

AEM Esta página describe las notas de la versión para las herramientas de migración de as a Cloud Service 2022.9.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.34 es el 12 de septiembre de 2022.

### Novedades {#what-is-new-bpa}

* Ahora, BPA puede detectar e informar sobre si el cliente ha agregado una configuración de registrador personalizada. AEM El as a Cloud Service no admite archivos de registro personalizados. Todos los archivos de registro deben canalizarse a `error.log`
* BPA ahora puede informar sobre los diferentes tipos MIME binarios presentes en el repositorio del cliente y los recuentos asociados a ellos.

### Correcciones de errores {#bug-fixes-bpa}

* La interfaz de usuario de BPA tenía problemas de procesamiento al mostrar un gran número de conclusiones en un solo patrón. Esto se ha corregido.
* El BPA informaba incorrectamente de algunos hallazgos como cambios no compatibles con una gravedad crítica. Esto se ha corregido.
