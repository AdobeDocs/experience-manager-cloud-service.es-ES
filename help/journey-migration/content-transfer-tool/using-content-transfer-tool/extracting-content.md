---
title: Extracción de contenido del origen
description: Extracción de contenido del origen
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: b31fe77cd43362b6ad768e8a2b258c23ae84466c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 27%

---

# Extracción de contenido del origen {#extracting-content}

## Proceso de Extracción en la herramienta de transferencia de contenido {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extracción de contenido"
>abstract="Extracción hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada conjunto de migración. El conjunto de migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es" text="Extracción superior"


Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:

>[!NOTE]
>Si se usa Amazon S3, Azure Data Store o File Data Store como tipo de almacén de datos, puede ejecutar el paso de precopia opcional para acelerar significativamente la fase de extracción. El paso de precopia es más eficaz para la primera extracción e ingesta completa. Consulte [Gestión de repositorios de contenido grandes](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para obtener más información.

1. Seleccionar un conjunto de migraciones de **Transferencia de contenido** asistente y haga clic en **Extraer** para iniciar la extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >Asegúrese de que la clave de Extracción sea válida y no esté cerca de su caducidad. Si está cerca de su fecha de caducidad, puede renovar la clave de Extracción seleccionando el conjunto de migración y haciendo clic en Propiedades. Haga clic en **Renovar**. Esto le llevará al Cloud Acceleration Manager, donde puede hacer clic en **Copiar clave de extracción**. Cada vez que haga clic en **Copiar clave de extracción**, se genera una nueva clave de Extracción que es válida durante 14 días desde el momento de la creación.
   >![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Esto abrirá el cuadro de diálogo Extracción . Haga clic en **Extraer** para iniciar la fase de extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >Tiene la opción de sobrescribir el contenedor de ensayo durante la fase de extracción. If **Sobrescribir contenedor de ensayo** está desactivado, puede acelerar las extracciones para migraciones posteriores en las que las rutas de contenido o la configuración de versiones de inclusión no hayan cambiado. Sin embargo, si las rutas de contenido o la configuración de las versiones de inclusión han cambiado, **Sobrescribir contenedor de ensayo** debe estar habilitado.

1. La variable **Extracción** ahora muestra la variable **EJECUCIÓN** para indicar que la extracción está en curso.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Puede hacer clic en **Ver progreso** para obtener una vista granular de la extracción en curso.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   También puede supervisar el progreso de la fase de Extracción desde Cloud Acceleration Manager visitando la página de Transferencia de Contenido y verlo en más detalle haciendo clic en **...** y luego **Ver detalles**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Una vez completada la extracción, revise las demás columnas como **Fuente** y **Rutas** para obtener más información sobre el conjunto de migración que ha rellenado haciendo clic en **...** y luego **Ver detalles** para ver los detalles, incluida la duración de cada paso de la extracción. Vea este cuadro de diálogo durante la extracción para ver cómo progresan los pasos.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extracción superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service. Si ha utilizado el paso de precopia para la primera extracción completa, puede omitir la precopia para las siguientes extracciones adicionales (si el tamaño del conjunto de migración superior es inferior a 200 GB) porque puede añadir tiempo al proceso completo.
>Además, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se toma la extracción inicial hasta cuando se ejecuta la extracción superior. Las superposiciones no se pueden ejecutar en contenido cuya estructura haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior.

Complete los siguientes pasos:

1. Vaya a la **Transferencia de contenido** y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. La variable **Extracción de conjunto de migración** se abre. Haga clic en **Extraer**.

   >[!IMPORTANT]
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a extraer contenido del origen en la herramienta de transferencia de contenido, ya estará listo para aprender el proceso de ingesta en la herramienta de transferencia de contenido. Consulte [Ingesta de contenido en Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para aprender a ingerir el conjunto de migraciones desde la herramienta de transferencia de contenido.
