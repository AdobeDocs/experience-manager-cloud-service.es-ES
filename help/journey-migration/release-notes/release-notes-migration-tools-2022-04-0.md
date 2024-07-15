---
title: Notas de la versión para las herramientas de migración en la versión 2022.4.0 de AEM as a Cloud Service
description: Notas de la versión para las herramientas de migración en la versión 2022.4.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# Notas de la versión para las herramientas de migración en la versión 2022.4.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2022.4.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.28 es el 22 de abril de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de API de Asset Manager no admitidas. Hay cuatro API que ya no son compatibles con AEM as a Cloud Service. Los clientes deben asegurarse de que ya no utilizan estas API y de que deben utilizar el nuevo método de carga de recursos.

* Capacidad para detectar el uso de plantillas de fragmentos de contenido. Las plantillas de fragmentos de contenido ya no son compatibles con la creación de nuevos fragmentos de contenido en AEM as a Cloud Service. Los clientes deben crear modelos de fragmento de contenido para reemplazar las plantillas de fragmento de contenido.

* Capacidad para detectar recursos con más de 100 descendientes bajo el nodo de metadatos del recurso en el repositorio. Se recomienda quitar los nodos de metadatos que no sean necesarios para mejorar el rendimiento al cargar carpetas que cuenten con estos recursos.

* Capacidad para detectar y crear informes sobre el tipo de almacén de datos utilizado.

* AEM Patrón actualizado para el portal de formularios de.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de conclusiones para componentes principales en lugar de informar solo sobre componentes de clientes. Esto se ha corregido.
