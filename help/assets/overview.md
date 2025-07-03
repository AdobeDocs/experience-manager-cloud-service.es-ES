---
title: Administración de activos digitales (DAM) de Adobe mediante AEM
description: Obtenga información sobre cómo utilizar y administrar la administración de activos digitales (DAM) de Adobe mediante Experience Manager Assets as a Cloud Service.
contentOwner: AK
feature: Asset Management
role: User, Leader, Architect
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: ht
source-wordcount: '927'
ht-degree: 100%

---


# Introducción a Assets as a [!DNL Cloud Service] para la administración de activos digitales en AEM {#assets-cloud-service-introduction}

<!-- Need review information from gklebus -->

Adobe Experience Manager Assets as a [!DNL Cloud Service] ofrece una solución PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y medios dinámicos con rapidez e impacto, sino que también utilicen funcionalidades inteligentes de próxima generación, como IA y aprendizaje automático, desde un sistema que siempre esté actualizado, disponible y aprendiendo.

La ingesta simultánea de muchos recursos o recursos complejos es una tarea intensiva en recursos para una instancia de Autor de Experience Manager. La instancia principal consume considerables recursos de CPU, memoria e I/O cuando se agregan, procesan o incluso migran recursos. Estos problemas de rendimiento afectan a la experiencia de creación y exploración de los usuarios finales.

Las empresas necesitan soporte para una amplia variedad de formatos de archivo y resoluciones de contenido para casos de uso multilingüe, entre dispositivos y geográficos. Los requisitos de procesamiento y almacenamiento de recursos exigen recursos y funcionalidades que pueden sobrecargar una solución tradicional. A veces, las limitaciones técnicas del procesamiento de recursos no producen los resultados deseados y en otros momentos el coste del almacenamiento es un impedimento para los márgenes de ganancia.

Para empezar, comprenda los [beneficios de una oferta nativa de la nube](#solution-benefits) para la administración de activos digitales. Eche un vistazo a los [cambios notables en Experience Manager as a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md) que también afectan a Experience Manager Assets como continuación a los [cambios notables en Recursos](/help/assets/assets-cloud-changes.md).

Siga leyendo para conocer [detalles sobre las nuevas funcionalidades de Recursos](#whats-new-assets) y [sus problemas conocidos](/help/release-notes/maintenance/latest.md). Consulte una lista de [funcionalidades obsoletas o eliminadas](/help/release-notes/deprecated-removed-features.md) para saber qué se quita en esta versión. Por último, comprenda los términos de Experience Manager con la ayuda de este [glosario](/help/overview/terminology.md).

## Beneficios de la solución {#solution-benefits}

Los siguientes son los beneficios clave de Assets as a [!DNL Cloud Service] para la administración de activos digitales. Para obtener más información, consulte [la información general de Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md).

* **Servicios de nube modernos para el procesamiento de recursos**: los nuevos microservicios de recursos son un servicio de procesamiento de recursos basado en la nube, escalable, fiable y sin complicaciones.
* **Muy escalable**: escalabilidad flexible en todos los tipos de implementaciones. Recursos prácticamente ilimitados, disponibles bajo demanda, según sea necesario. Ahorra el coste del exceso de diseño en comparación con un sistema tradicional.
* **Último software**: siempre vigente y actualizado. Todos los usuarios cuentan únicamente con el último software con todos los parches, funciones, seguridad y correcciones de errores disponibles. Los desarrolladores y los integradores trabajan con el último conjunto de API sin problemas de compatibilidad con varias versiones.
* **Siempre en línea**: sin tiempo de inactividad (0dt) gracias a la instancia implementada en un clúster con copias de seguridad y redundancia. Las actualizaciones también son 0dt.
* **Monitorización constante**: la monitorización del sistema es automatizada y las comprobaciones y los activadores integrados ayudan a mantener el rendimiento, la disponibilidad y la resistencia general.
* **Implementaciones sin complicaciones**: las operaciones de Experience Manager en la nube están completamente automatizadas y no requieren intervención manual. Para implementaciones automatizadas, el componente Cloud Manager (CM) automatiza la versión de imágenes de Docker implementables que contienen su código personalizado.

## Experiencias basadas en los grupos de usuarios disponibles para la administración de activos digitales {#persona-based-experiences}

Adobe ofrece una solución sólida de administración de activos digitales (DAM) para que usted pueda sacar el máximo partido sus recursos digitales. Adobe Experience Manager Assets tiene dos experiencias independientes que utilizan el mismo repositorio de Cloud Services:

* **Vista de administrador**: la interfaz de usuario as a Cloud Service de Assets existente. Utilice la Vista de administrador para todas las funciones avanzadas de administración de activos digitales, entre ellas integraciones, flujos de trabajo, automatización de contenido, publicación y mucho más.

* **Vista de recursos**: la experiencia de administración de recursos ligera de Adobe para almacenar, administrar, descubrir y utilizar recursos digitales. Interfaz de usuario optimizada que contiene funciones esenciales de administración de activos digitales. Diseñada para los usuarios de DAM ligeros con un enfoque en la carga, administración de metadatos, búsqueda, descarga y uso compartido.

Los usuarios con acceso a la vista del administrador también pueden acceder a la vista Recursos. La interfaz de usuario simplificada de Assets Essentials facilita la administración, la detección y la distribución de sus recursos digitales. Un amplio conjunto de usuarios de diferentes funciones, incluidos los equipos creativos, de marketing y de línea de negocios, pueden colaborar en los activos y acceder a los activos correctos y aprobados cuando y donde los necesiten. Muchos usuarios ocasionales de DAM prefieren la vista Recursos porque solo contiene un subconjunto de funciones. La experiencia está dirigida a creativos, consumidores de recursos de solo lectura y usuarios de DAM de menor peso.

Los bibliotecarios, desarrolladores y superusuarios de DAM pueden seguir utilizando la vista de administrador o cambiar entre las interfaces de usuario, según sea necesario. Puede seleccionar la experiencia que mejor se adapte a su función.

![add-tags](assets/newui-overview.svg)

Para obtener información sobre cómo acceder a la vista Recursos y algunas de las simplificaciones que ofrece a través de la vista Administración, consulte [Introducción a la vista de recursos](/help/assets/assets-view-introduction.md).

## Integración con la creación basada en documentos para Edge Delivery Services {#integrate-doc-authoring-edge-and-assets}

Con Edge Delivery, puede crear entornos de desarrollo rápidos en los que los autores actualizan y publican contenido rápidamente y en los que inician nuevos sitios rápidamente.

Integre AEM Assets con la creación basada en documentos para Edge Delivery Services para permitir que los autores de sitios web utilicen las imágenes disponibles en repositorios de AEM Assets durante la creación de documentos en Microsoft Word o Google Docs. Para obtener más información, consulte [Integración de AEM Assets con la creación basada en documentos](/help/edge/using.md#integrate-assets-edge).

## Integración con Adobe Journey Optimizer {#integration-with-ajo}

[Adobe Journey Optimizer](https://business.adobe.com/es/products/journey-optimizer/adobe-journey-optimizer.html) simplifica la administración de recorrido para que los clientes proporcionen campañas omnicanal con decisiones y perspectivas inteligentes. Al diseñar mensajes con Journey Optimizer, puede acceder al repositorio de Assets as a Cloud Service directamente desde la interfaz de Journey Optimizer. Los usuarios obtienen acceso a los recursos mediante la interfaz de usuario de Experience Manager Assets. Para obtener más información, consulte [Creación y administración de recursos con Experience Manager Assets](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/assets-images/assets.html?lang=es).

## Nuevas funcionalidades de Recursos {#whats-new-assets}

Las nuevas y significativas funcionalidades son las siguientes:

* [Microservicios de recursos](/help/assets/asset-microservices-overview.md)
* [Métodos de carga de recursos](/help/assets/add-assets.md)

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
