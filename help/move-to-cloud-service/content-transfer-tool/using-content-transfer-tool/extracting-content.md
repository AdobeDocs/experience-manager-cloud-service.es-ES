---
title: Extracción de contenido del origen en la herramienta de transferencia de contenido
description: Extracción de contenido del origen en la herramienta de transferencia de contenido
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 48%

---


# Extracción de contenido del origen en la herramienta de transferencia de contenido {#extracting-content}

## Proceso de Extracción en la herramienta de transferencia de contenido {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extracción de contenido"
>abstract="Extracción hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada conjunto de migración. El conjunto de migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extracción superior"

Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:
>[!NOTE]
>Si se utiliza Amazon S3 o Azure Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de extracción. Para ello, debe configurar un archivo `azcopy.config` antes de ejecutar la extracción. Consulte [Gestión de repositorios de contenido grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obtener más información.

1. Seleccione un conjunto de migraciones de la página *Información general* y haga clic en **Extracción** para empezar la extracción. Aparece el cuadro de diálogo **Migration Set extraction** y haga clic en **Extract** para iniciar la fase de extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción.


1. El campo **EXTRACTION** ahora muestra el estado **RUNNING** para indicar que la extracción está en curso.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   Una vez finalizada la extracción, el estado del conjunto de migración se actualiza a **FINALIZADO** y aparece un icono de nube *verde lisa* debajo del campo **INFORMACIÓN** .

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >La interfaz de usuario tiene una función de recarga automática que vuelve a cargar la página de información general cada 30 segundos.
   >Cuando se inicia la fase de extracción, el bloqueo de escritura se crea y se libera después de *60 segundos*. Por lo tanto, si se detiene una extracción, hay que esperar un minuto para que se libere el bloqueo antes de volver a iniciarla.

## Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.
>Además, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior. Complete los siguientes pasos:

1. Vaya a la página *Información general* y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior. Aparece el cuadro de diálogo **extracción de conjunto de migración** .

   >[!IMPORTANT]
   >
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >
   >![image](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a extraer contenido del origen en la herramienta de transferencia de contenido, ya estará listo para aprender el proceso de ingesta en la herramienta de transferencia de contenido. Consulte [Ingesta de contenido en Target en la herramienta de transferencia de contenido](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obtener información sobre cómo introducir el conjunto de migración de la herramienta de transferencia de contenido.
