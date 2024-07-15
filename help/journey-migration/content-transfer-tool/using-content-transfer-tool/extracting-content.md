---
title: Extracción de contenido del origen
description: Obtenga información sobre cómo extraer contenido de una instancia de Adobe Experience Manager AEM () de origen para transferirlo más tarde a una instancia de Cloud Service AEM de.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 19%

---

# Extracción de contenido del origen {#extracting-content}

## Proceso de extracción en herramienta de transferencia de contenido {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extracción de contenido"
>abstract="La extracción hace referencia a la obtención de contenido de la instancia de Adobe Experience Manager (AEM) de origen en un área temporal denominada conjunto de migración. El conjunto de migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es" text="Extracción superior"


Siga los pasos a continuación para extraer el conjunto de migración de la herramienta de transferencia de contenido:

>[!NOTE]
>Si se utiliza Amazon S3, el almacén de datos de Azure o el almacén de datos de archivos como tipo de almacén de datos, puede ejecutar el paso opcional previo a la copia para aumentar la velocidad de la fase de extracción. El paso previo a la copia es más eficaz para la primera extracción e ingesta completas. Consulte [Gestión de repositorios de contenido grandes](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para obtener más información.

1. Seleccione un conjunto de migración del asistente **Transferencia de contenido** y haga clic en **Extraer** para iniciar la extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Ahora se puede programar una ingesta para que se inicie automáticamente inmediatamente después de que una extracción se realice correctamente. Consulte [Ingesta de contenido en Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obtener más información.

   >[!IMPORTANT]
   >
   >Asegúrese de que la clave de extracción sea válida y no esté cerca de su caducidad. Si está cerca de su fecha de caducidad, puede renovar la clave de extracción seleccionando el conjunto de migración y haciendo clic en Propiedades. Haga clic en **Renovar**. Esto lo lleva a Cloud Acceleration Manager, donde puede hacer clic en **Copiar clave de extracción**. Cada vez que hace clic en **Copiar clave de extracción**, se genera una nueva clave de extracción que es válida durante 14 días desde el momento de la creación.
   >![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Esto abre el cuadro de diálogo Extracción. Haga clic en **Extraer** para iniciar la fase de extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >Opcionalmente, puede sobrescribir el contenedor de ensayo durante la fase de extracción. Si **Sobrescribir contenedor de almacenamiento provisional** está deshabilitado, puede acelerar las extracciones en migraciones posteriores en las que las rutas de contenido o la configuración de las versiones de inclusión no hayan cambiado. Sin embargo, si la configuración de las rutas de contenido o las versiones de inclusión ha cambiado, **Sobrescribir contenedor de almacenamiento provisional** debe estar habilitado.

1. El campo **Extracción** ahora muestra el estado **EN EJECUCIÓN** para indicar que la extracción está en curso.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Puede hacer clic en **Ver progreso** para obtener una vista granular de la extracción en curso.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   También puede monitorizar el progreso de la fase de extracción desde Cloud Acceleration Manager. Para ello, visite la página de transferencia de contenido y véala con más detalle haciendo clic en **...** > **Ver detalles**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Cuando finalice la extracción, revise las otras columnas como **Source** y **Rutas** para obtener detalles del conjunto de migración que ha rellenado. Haciendo clic en **...** > **Ver detalles** para ver los detalles, incluida la duración de cada paso de la extracción. Vea este cuadro de diálogo durante la extracción para poder ver cómo progresan los pasos.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extracción Superior {#top-up-extraction-process}

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse al Cloud Service. Si ha utilizado el paso de precopia para la primera extracción completa, puede omitir la precopia para las siguientes extracciones de recarga (si el tamaño del conjunto de migración superior es inferior a 200 GB). El motivo es que puede añadir tiempo a todo el proceso.
>Además, es esencial que la estructura de contenido del contenido existente no cambie desde el momento en que se realiza la extracción inicial hasta cuando se ejecuta la extracción superior. Las recargas no se pueden ejecutar en contenido cuya estructura se haya cambiado desde la extracción inicial. Asegúrese de restringir esto durante el proceso de migración.

Una vez completado el proceso de extracción, se puede transferir contenido delta mediante el método de extracción superior.

Complete los siguientes pasos:

1. Vaya al asistente **Transferencia de contenido** y seleccione el conjunto de migración para el que desea realizar la extracción superior. Haga clic en **Extracción** para iniciar la extracción superior.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. Aparece el cuadro de diálogo **extracción de conjunto de migración**. Haga clic en **Extraer**.

   >[!IMPORTANT]
   >Se debe desactivar la opción **Sobrescribir el contenedor de ensayo durante la extracción** .
   >![image](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## Siguientes pasos {#whats-next}

Después de haber aprendido a extraer contenido de Source en la herramienta de transferencia de contenido, ahora está listo para aprender el proceso de ingesta en la herramienta de transferencia de contenido. Consulte [Ingesta de contenido en Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md), donde podrá aprender a ingerir el conjunto de migración desde la herramienta de transferencia de contenido.
