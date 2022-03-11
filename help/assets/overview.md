---
title: Introducción a Assets as a [!DNL Cloud Service]
description: Novedades de Assets as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management
role: User,Leader,Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Introducción a Assets como [!DNL Cloud Service] {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] ofrece una solución de PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y Dynamic Media con rapidez e impacto, sino que también utilicen funciones inteligentes de próxima generación, como AI/ML, desde un sistema que siempre está actualizado, siempre disponible y siempre aprendiendo.

La ingesta simultánea de muchos recursos o recursos complejos es una tarea intensiva en recursos para una instancia de Autor de Experience Manager. La instancia principal consume considerables recursos de CPU, memoria y E/S cuando se agregan, procesan o incluso migran recursos. Estos problemas de rendimiento afectan a la experiencia de creación y exploración de los usuarios finales.

Las empresas necesitan soporte para una amplia variedad de formatos de archivo y resoluciones de contenido para casos de uso multilingüe, entre dispositivos y geografía. Los requisitos de procesamiento y almacenamiento de recursos exigen recursos y capacidades que pueden sobrecargar una solución tradicional. A veces, las limitaciones técnicas del procesamiento de activos no producen los resultados deseados y en otros momentos el costo del almacenamiento es un impedimento para los márgenes de ganancia.

Para empezar, comprenda la [ventajas de una oferta nativa de la nube](#solution-benefits). Eche un vistazo a lo notable [cambios en Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) que también afectan al seguimiento de Experience Manager Assets de la [cambios en Assets](/help/assets/assets-cloud-changes.md).

Siga leyendo para conocer la [detalles de las nuevas funciones de Assets](#whats-new-assets) y [problemas conocidos](/help/release-notes/known-issues.md). Consulte una lista de [funcionalidad obsoleta o eliminada](/help/release-notes/deprecated-removed-features.md) para saber qué se ha eliminado en esta versión y ver esto [lista de funciones futuras](/help/release-notes/known-issues.md#upcoming-assets-capabilities) para saber lo que vendrá en breve. Por último, comprenda los términos del Experience Manager con la ayuda de esta [glosario](/help/overview/terminology.md).

## Ventajas de la solución {#solution-benefits}

Las siguientes son las ventajas clave de Assets as a [!DNL Cloud Service]. Para obtener más información, consulte [descripción general de Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Servicios de nube modernos para el procesamiento de recursos**: Los nuevos microservicios de recursos son un servicio de procesamiento de recursos basado en la nube, escalable, fiable y sin complicaciones.
* **Muy escalable**: Escalabilidad elástica en todos los tipos de implementaciones. Recursos prácticamente ilimitados disponibles bajo demanda, según sea necesario. Ahorra el costo del diseño excesivo en comparación con un sistema tradicional.
* **Último software**: Siempre actualizado y siempre actualizado. Todos los usuarios solo tienen el último software con todos los parches, funciones, seguridad y correcciones de errores disponibles. Los desarrolladores y los integradores trabajan con el último conjunto de API sin problemas de compatibilidad con varias versiones.
* **Siempre en línea**: Sin downtime (0dt), gracias a la instancia implementada en un cluster con backups y redundancia. Las actualizaciones también son 0dt.
* **Supervisión constante**: La supervisión del sistema es automatizada y las comprobaciones y déclencheur integrados ayudan a mantener el rendimiento, la disponibilidad y la solidez general.
* **Implementaciones sin complicaciones**: Los Experience Manager de las operaciones de Cloud están completamente automatizados y no requieren intervención manual. Para implementaciones automatizadas, el componente Cloud Manager (CM) automatiza la compilación de imágenes de Docker implementables que contienen su código personalizado.

## Nuevas funciones de Assets {#whats-new-assets}

Las nuevas y significativas capacidades son:

* [Microservicios de recursos](/help/assets/asset-microservices-overview.md)
* [Métodos de carga de recursos](/help/assets/add-assets.md)
