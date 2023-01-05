---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.9.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.9.0
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.9.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.9.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.34 es el 12 de septiembre de 2022.

### Novedades {#what-is-new-bpa}

* BPA ahora puede detectar e informar si el cliente ha agregado una configuración de registrador personalizada. AEM as a Cloud Service no admite archivos de registro personalizados. Todos los archivos de registro deben canalizarse a `error.log`
* BPA ahora puede informar sobre los diferentes tipos de MIME binarios presentes en el repositorio del cliente y los recuentos asociados a ellos.

### Correcciones de errores {#bug-fixes-bpa}

* La interfaz de usuario de BPA tenía problemas de renderización al mostrar un gran número de conclusiones en un único patrón. Esto se ha corregido.
* BPA informaba incorrectamente de algunos hallazgos como cambios no compatibles con gravedad crítica. Esto se ha corregido.
