---
title: Información general sobre la herramienta de transferencia de contenido (heredada)
description: Información general sobre la herramienta de transferencia de contenido
hide: true
hidefromtoc: true
exl-id: dd031580-e9d7-461e-8689-9bc3dbb2121b
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 70%

---

# Información general de la herramienta de transferencia de contenido (heredada) {#overview-content-transfer-tool}

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para mover contenido existente de una instancia de AEM de origen (on-premise o AMS) a la instancia de destinatario de AEM de Cloud Service.

Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente.

## Fases en la herramienta de transferencia de contenido {#phases-content-transfer-tool}

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**: hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada *conjunto de migración*. El conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte el Proceso de [Extracción en Transferencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=es) de contenido para obtener más detalles.

   >[!NOTE]
   >Ejecute la herramienta de asignación de usuarios como parte de la fase de extracción. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) para obtener más información.

1. **Ingesta**: hace referencia a la ingesta de contenido del *conjunto de migración* en la instancia de Cloud Service del destinatario.

   Para obtener más detalles, consulte [Proceso de ingesta en la transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html).

## Atributos de un conjunto de migración {#attributes-migration-set}

El conjunto de migración tiene los siguientes atributos:

* Se puede crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido.
* Cada conjunto de migración debe tener un nombre exclusivo.
* Si un conjunto de migración está inactivo durante más de 30 días, se elimina automáticamente.
* Cada vez que se crea un conjunto de migraciones, se asocia a un entorno específico. Solo puede realizar la ingesta en una instancia de autor o publicación del mismo entorno.


La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

En la fase de extracción, a ***recargar*** un conjunto de migración existente, la variable *sobrescribir* La opción debe estar desactivada. Consulte la [Extracción Superior](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process) para obtener más detalles.

En la fase de ingesta, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado*. Consulte la [Ingesta Superior](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process) para obtener más detalles.

## Siguientes pasos {#whats-next}

AEM Después de conocer la herramienta de transferencia de contenido y su descripción general, esta herramienta se puede utilizar para mover el contenido existente de una instancia de origen de la transferencia (local o AMS) a la instancia de AEM Cloud Service de destino. Revisar [Requisitos previos para la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
