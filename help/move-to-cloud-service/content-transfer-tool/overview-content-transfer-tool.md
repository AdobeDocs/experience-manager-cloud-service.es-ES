---
title: Información general sobre la herramienta de transferencia de contenido
description: Información general sobre la herramienta de transferencia de contenido
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 69%

---


# Información general {#overview-content-transfer-tool}

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para mover contenido existente de una instancia de AEM de origen (on-premise o AMS) a la instancia de destinatario de AEM de Cloud Service.

Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente.

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**: hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada *conjunto de migración*. El conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte el Proceso de [Extracción en Transferencia](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) de contenido para obtener más detalles.

2. **Ingesta**: la ingesta hace referencia a la ingesta de contenido del conjunto *de migración* en la instancia de Cloud Service del destinatario.

   Consulte el Proceso de [Ingesta en Transferencia](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) de contenido para obtener más detalles.

El conjunto *de migraciones* tiene los siguientes atributos:

* Se puede crear y mantener un máximo de cuatro conjuntos de migración a la vez durante la actividad de transferencia de contenido.
* Cada conjunto de migración debe tener un nombre exclusivo.
* Si un conjunto de migración ha estado inactivo durante más de 30 días, se elimina automáticamente.
* Cada vez que se crea un conjunto de migraciones, se asocia a un entorno específico. Solo puede realizar la ingesta en una instancia de autor o publicación del mismo entorno.

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
> Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

En la fase de extracción, para ***completar*** un conjunto de migración existente, se debe desactivar la opción de *sobrescritura*. Consulte la Extracción [](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) Superior para obtener más detalles.

En la fase de ingesta, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado*. Consulte la Ingesta [](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) Superior para obtener más detalles.


## Directrices y prácticas recomendadas {#best-practices}

Siga esta sección para conocer las directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido:

* Es aconsejable ejecutar [Revision Cleanup](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html) y comprobaciones [de coherencia del almacén de](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) datos en el repositorio de **origen** para identificar posibles problemas y reducir el tamaño del repositorio.

* Si la configuración de la red de Envío de contenido de AEM Cloud Author (CDN) está configurada para tener una lista blanca de direcciones IP, debe asegurarse de que las direcciones IP de entorno de origen también se añadan a la lista de permitidas para que el entorno de origen y el entorno de AEM Cloud puedan comunicarse entre sí.

* En la fase de ingesta se recomienda ejecutarla mediante el modo de *borrado* activado, en el que el repositorio existente (autor o publicación) en el entorno de Cloud Service de AEM de destinatario se eliminará por completo y, a continuación, se actualizará con los datos del conjunto de migración. Este modo es mucho más rápido que el modo sin borrado, donde el conjunto de migración se aplica sobre el contenido  existente.

* Una vez completada la actividad de transferencia de contenido, se requiere la estructura de proyecto correcta en el entorno de Cloud Service para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

* Antes de ejecutar la herramienta de transferencia de contenido, debe asegurarse de que hay suficiente espacio en disco en el `crx-quickstart` subdirectorio de la instancia de AEM de origen. Esto se debe a que la herramienta de transferencia de contenido crea una copia local del repositorio que se carga posteriormente en el conjunto de migración.
La fórmula general para calcular el espacio en disco necesario es la siguiente:
   `data store size + node store size * 1.5`

   * *tamaño* del almacén de datos: la herramienta de transferencia de contenido utiliza 64 GB, incluso si el almacén de datos real es más grande.
   * *tamaño*del almacén de nodos: el tamaño del directorio del almacén de segmentos o el tamaño de la base de datos MongoDB.
Por lo tanto, para un tamaño de almacén de segmentos de 20 GB, el espacio libre requerido en disco sería de 94 GB.