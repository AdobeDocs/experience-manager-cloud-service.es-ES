---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.4.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.4.0 de
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 5%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.4.0 de {#release-notes}

AEM Esta página describe las notas de la versión para las herramientas de migración de as a Cloud Service 2022.4.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.28 es el 22 de abril de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de API de Asset Manager no admitidas. AEM Hay cuatro API que ya no son compatibles con el as a Cloud Service de la. Los clientes deben asegurarse de que ya no utilizan estas API y de que deben utilizar el nuevo método de carga de recursos.

* Capacidad para detectar el uso de plantillas de fragmentos de contenido. AEM Las plantillas de fragmento de contenido ya no son compatibles con la creación de nuevos fragmentos de contenido en las plantillas de fragmento de contenido en as a Cloud Service. Los clientes deberán crear modelos de fragmento de contenido para reemplazar las plantillas de fragmento de contenido.

* Capacidad para detectar recursos con más de 100 descendientes bajo el nodo de metadatos del recurso en el repositorio. Se recomienda quitar los nodos de metadatos que no sean necesarios para mejorar el rendimiento al cargar carpetas que cuenten con estos recursos.

* Capacidad para detectar y crear informes sobre el tipo de almacén de datos utilizado.

* AEM Patrón actualizado para el portal de formularios de.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de conclusiones para componentes principales en lugar de informar solo sobre componentes de clientes. Esto se ha corregido.
