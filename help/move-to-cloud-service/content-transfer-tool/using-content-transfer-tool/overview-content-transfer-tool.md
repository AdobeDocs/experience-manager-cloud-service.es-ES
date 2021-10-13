---
title: Información general sobre la herramienta de transferencia de contenido
description: Información general sobre la herramienta de transferencia de contenido
exl-id: 4715937e-4c4c-4680-af15-016db4fe7db9
source-git-commit: 001c0003a19153edeb238938a8eae330396e67c5
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 61%

---

# Información general {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Información general"
>abstract="Content Transfer Tool es una herramienta desarrollada por Adobe que puede utilizarse para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de AEM Cloud Service de destino. Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Proceso de extracción"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Proceso de Ingesta"

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para mover contenido existente de una instancia de AEM de origen (on-premise o AMS) a la instancia de destinatario de AEM de Cloud Service.

Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente.

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**: hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada *conjunto de migración*. El conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte el Proceso de [Extracción en Transferencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html) de contenido para obtener más detalles.

>[!NOTE]
>
> Se recomienda ejecutar la herramienta de asignación de usuarios como parte de la fase de extracción. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) para obtener más información.

1. **Ingesta**: la ingesta hace referencia a la ingesta de contenido del conjunto *de migración* en la instancia de Cloud Service del destinatario.

   Consulte el Proceso de [Ingesta en Transferencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) de contenido para obtener más detalles.

El conjunto *de migraciones* tiene los siguientes atributos:

* Se puede crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido.
* Cada conjunto de migración debe tener un nombre exclusivo.
* Si un conjunto de migración ha estado inactivo durante más de 30 días, se elimina automáticamente.
* Cada vez que se crea un conjunto de migraciones, se asocia a un entorno específico. Solo puede realizar la ingesta en una instancia de autor o publicación del mismo entorno.


La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

En la fase de extracción, para ***completar*** un conjunto de migración existente, se debe desactivar la opción de *sobrescritura*. Consulte la Extracción [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process) Superior para obtener más detalles.

En la fase de ingesta, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado*. Consulte la Ingesta [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process) Superior para obtener más detalles.

## Siguientes pasos {#whats-next}

Una vez que conozca la herramienta de transferencia de contenido y su descripción general que describe esta herramienta se puede utilizar para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de AEM Cloud Service de destino, debe revisar [Requisitos previos para la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).

