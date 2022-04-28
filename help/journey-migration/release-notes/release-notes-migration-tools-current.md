---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.4.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.4.0
feature: Release Information
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 5%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.4.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.4.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.28 es el 22 de abril de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de API de Asset Manager no admitidas. Hay cuatro API que ya no son compatibles con AEM as a Cloud Service. Los clientes deben asegurarse de que ya no utilizan estas API y de que deben utilizar el nuevo método de carga de recursos.

* Capacidad para detectar el uso de plantillas de fragmento de contenido. Las plantillas de fragmento de contenido ya no son compatibles con la creación de nuevos fragmentos de contenido en AEM as a Cloud Service. Los clientes deberán crear modelos de fragmento de contenido para reemplazar las plantillas de fragmento de contenido.

* Capacidad para detectar activos con más de 100 descendientes bajo el nodo de metadatos del recurso en el repositorio. Se recomienda eliminar los nodos de metadatos que no son necesarios para mejorar el rendimiento al cargar carpetas que consistan en estos recursos.

* Capacidad para detectar e informar sobre el tipo de almacén de datos utilizado.

* Patrón actualizado para AEM portal de formularios.

### Correcciones de errores {#bug-fixes-bpa}

* El BPA presentaba informes sobre los resultados de los componentes principales en lugar de informar únicamente sobre los componentes del cliente. Esto se ha corregido.