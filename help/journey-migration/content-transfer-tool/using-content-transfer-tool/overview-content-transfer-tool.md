---
title: Información general sobre la herramienta de transferencia de contenido
description: Información general sobre la herramienta de transferencia de contenido
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 8a55e011a93ce069f067192f58bd36399a39130b
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 44%

---

# Información general {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Información general"
>abstract="Content Transfer Tool es una herramienta desarrollada por Adobe que puede utilizarse para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de AEM Cloud Service de destino. Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="Directrices y prácticas recomendadas"

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para mover contenido existente de una instancia de AEM de origen (on-premise o AMS) a la instancia de destinatario de AEM de Cloud Service.

Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente.

Hay disponible una nueva versión de la herramienta de transferencia de contenido que integra el proceso de transferencia de contenido con Cloud Acceleration Manager. Se recomienda cambiar a esta nueva versión para aprovechar todas las ventajas que ofrece:

* Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo
* Experiencia del usuario mejorada mediante mejores estados de carga, protecciones y gestión de errores
* Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas

Para empezar a utilizar la nueva versión, deberá desinstalar las versiones anteriores de la herramienta de transferencia de contenido, ya que se ha producido un cambio importante en la arquitectura de la herramienta.

>[!NOTE]
>
> En situaciones en las que una migración ya esté en curso, puede seguir utilizando la versión anterior de CTT hasta que se complete la migración. Para obtener documentación relacionada con la versión anterior de CTT, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## Fases en la herramienta de transferencia de contenido {#phases-content-transfer-tool}

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**: hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada *conjunto de migración*. El conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte el Proceso de [Extracción en Transferencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html) de contenido para obtener más detalles.

   >[!NOTE]
   > Se recomienda ejecutar la herramienta de asignación de usuarios como parte de la fase de extracción. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) para obtener más información.

1. **Ingesta**: la ingesta hace referencia a la ingesta de contenido del conjunto *de migración* en la instancia de Cloud Service del destinatario.

   Consulte [Proceso de Ingesta en transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) para obtener más información.

## Atributos de un conjunto de migraciones {#attributes-migration-set}

El conjunto de migraciones tiene los siguientes atributos:

* Con la nueva versión, puede crear un máximo de cinco conjuntos de migración dentro de un proyecto creado en Cloud Acceleration Manager.
* Cada conjunto de migración debe tener un nombre exclusivo.

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

En la fase de extracción, para ***completar*** un conjunto de migración existente, se debe desactivar la opción de *sobrescritura*. Consulte la Extracción [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process) Superior para obtener más detalles.

En la fase de ingesta, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado*. Consulte la Ingesta [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process) Superior para obtener más detalles.

## Siguientes pasos {#whats-next}

Una vez que conozca la herramienta de transferencia de contenido y su descripción general que describe esta herramienta se puede utilizar para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de AEM Cloud Service de destino, debe revisar [Requisitos previos para la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
