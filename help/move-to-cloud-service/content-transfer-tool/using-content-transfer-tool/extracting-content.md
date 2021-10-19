---
title: Extracción de contenido del origen
description: Extracción de contenido del origen
source-git-commit: f549a7d9e1a5732d75489bc327a8cb67876a4483
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 36%

---


# Extracción de contenido del origen {#extracting-content}

## Proceso de Extracción en la herramienta de transferencia de contenido {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extracción de contenido"
>abstract="Extracción hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada conjunto de migración. El conjunto de migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extracción superior"


Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Si se utiliza Amazon S3 o Azure Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de extracción. Para ello, deberá configurar un `azcopy.config` antes de ejecutar la extracción. Consulte [Gestión de repositorios de contenido grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obtener más información.

>[!IMPORTANT]
>Debe ejecutar la herramienta de asignación de usuarios antes de extraer contenido del origen. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) para obtener más información.

1. Seleccionar un conjunto de migraciones de **Transferencia de contenido** asistente y haga clic en **Extraer** para iniciar la extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-01.png)

1. La variable **Extracción de conjunto de migración** aparece el cuadro de diálogo y haga clic en **Extraer** para iniciar la fase de extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción.

   >[!IMPORTANT]
   >Si la Asignación de usuarios no se ha ejecutado en este conjunto de migración antes de extraer contenido del origen, verá una advertencia mostrando que el paso Asignación de usuarios está pendiente, como se muestra en la figura siguiente. Haga clic en **Asignar usuarios** para ejecutar la herramienta Asignación de usuarios.
   >![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. La variable **Extracción** ahora muestra la variable **EJECUCIÓN** para indicar que la extracción está en curso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-03.png)

   Una vez finalizada la extracción, el estado del conjunto de migración se actualiza a **FINALIZADO** y aparece un icono de nube *verde lisa* debajo del campo **INFORMACIÓN** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >La interfaz de usuario tiene una función de recarga automática que vuelve a cargar el **Transferencia de contenido** cada 30 segundos.
   >Cuando se inicia la fase de extracción, el bloqueo de escritura se crea y se libera después de *60 segundos*. Por lo tanto, si se detiene una extracción, hay que esperar un minuto para que se libere el bloqueo antes de volver a iniciarla.

## Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.
>Además, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior.

Complete los siguientes pasos:

1. Vaya a la **Transferencia de contenido** y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-05.png)

1. La variable **Extracción de conjunto de migración** se abre. Haga clic en **Extraer**.

   >[!IMPORTANT]
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-06.png)


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a extraer contenido del origen en la herramienta de transferencia de contenido, ya estará listo para aprender el proceso de ingesta en la herramienta de transferencia de contenido. Consulte [Ingesta de contenido en Target](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para aprender a ingerir el conjunto de migraciones desde la herramienta de transferencia de contenido.
