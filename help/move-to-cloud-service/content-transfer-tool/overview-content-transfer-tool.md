---
title: Información general sobre la herramienta de transferencia de contenido
description: Información general sobre la herramienta de transferencia de contenido
translation-type: tm+mt
source-git-commit: f2a6b67e3673bf6dfeb63d445074f6d1e05971cf
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Información general {#overview-content-transfer-tool}

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para mover contenido existente de una instancia de AEM de origen (in situ o AMS) a la instancia de destinatario AEM Cloud Service.

Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente.

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**:  Extracción hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada conjunto *de* migración. Un conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte Proceso de [Extracción en Transferencia](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) de contenido para obtener más detalles.

2. **Ingesta**: La ingestión hace referencia a la ingesta de contenido del conjunto *de* migración en la instancia de servicio de destinatario Cloud.

   Consulte Proceso de [ingestión en Transferencia](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) de contenido para obtener más detalles.

Un conjunto *de migraciones* tiene los atributos siguientes:

* Se puede crear y mantener un máximo de cuatro conjuntos de migración a la vez durante la actividad de transferencia de contenido.
* Cada conjunto de migración debe tener un nombre único.
* Si un conjunto de migración ha estado inactivo durante más de 30 días, se eliminará automáticamente.
* Cada vez que se crea un conjunto de migraciones, se asocia a un entorno específico. Solo puede realizar la ingesta en una instancia de autor o publicación del mismo entorno.

La herramienta de transferencia de contenido tiene una función que admite la adición de contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
> Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse al servicio de nube.

En la fase de extracción, para ***completar*** un conjunto de migración existente, se debe desactivar la opción de *sobrescritura* . Consulte la Extracción [](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) Superior para obtener más detalles.

En la fase de ingestión, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado* . Consulte [Introducción](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) para obtener más información.


## Directrices y prácticas recomendadas {#best-practices}

Siga la sección siguiente para conocer las directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido:

* Es aconsejable ejecutar pruebas de compactación, consistencia del almacén de datos en los repositorios antes de mandar para detectar posibles problemas y también reducir la basura presente en el repositorio.

* Si la configuración de la red de Envío de contenido de AEM Cloud Author (CDN) está configurada para tener una lista blanca de direcciones IP, debe asegurarse de que las direcciones IP de entorno de origen también se añadan a la lista blanca para que el entorno de origen y el entorno de AEM Cloud puedan comunicarse entre sí.

* En la fase de ingestión, se recomienda ejecutar la ingesta mediante el modo de *borrado* activado, en el que el repositorio existente (autor o publicación) en el entorno de servicio de nube de AEM de destinatario se eliminará por completo y, a continuación, se actualizará con los datos del conjunto de migración. Este modo es mucho más rápido que el modo sin barrido, donde el conjunto de migración se aplica sobre el contenido actual.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de servicios de nube para garantizar que el contenido se procese correctamente en el entorno de servicios de nube.
