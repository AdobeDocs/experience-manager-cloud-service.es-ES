---
title: Información general sobre la herramienta de transferencia de contenido
description: AEM Aprenda a utilizar la herramienta de transferencia de contenido para transferir contenido de una instancia de local a AEM as a Cloud Service
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
feature: Migration
role: Admin
source-git-commit: d9565e86c4b7e513cb1a95ecbe7a30c9586d9fb1
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 52%

---

# Información general {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Información general"
>abstract="La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe que se puede utilizar para iniciar la migración de contenido existente de una instancia de AEM de origen (On-Premise o AMS) a la instancia de AEM Cloud Service de destinatario. Esta herramienta también transfiere las entidades principales (usuarios o grupos) automáticamente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=es" text="Directrices y prácticas recomendadas"

La herramienta de transferencia de contenido es una herramienta desarrollada por Adobe AEM que se puede utilizar para iniciar la migración del contenido existente de una instancia de origen de la aplicación (On-Premise o AMS) a una instancia de AEM Cloud Service de destino.

Esta herramienta también transfiere entidades principales (usuarios o grupos) automáticamente.  Consulte [Asignación de usuarios y migración de entidades principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) para obtener más información.

La herramienta de transferencia de contenido integra el proceso de transferencia de contenido con Cloud Acceleration Manager. Esto otorga al usuario todos los beneficios que proporciona:

* Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo.
* Se ha mejorado la experiencia del usuario mediante mejores estados de carga, protecciones y administración de errores
* Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas.
* Los informes de validación y migración de principales están disponibles para la validación

## Fases en la herramienta de transferencia de contenido {#phases-content-transfer-tool}

Existen dos fases asociadas con la transferencia de contenido:

1. **Extracción**: hace referencia a la extracción de contenido de la instancia de AEM de origen en un área temporal denominada *conjunto de migración*. El conjunto *de* migración es un área de almacenamiento en la nube proporcionada por Adobe para almacenar temporalmente el contenido transferido entre la instancia de AEM de origen y la instancia de AEM de Cloud Service.

   Consulte [Proceso de extracción en transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obtener más información.

   >[!NOTE]
   >La asignación de usuarios ahora se ejecuta automáticamente como parte de la fase de extracción en el autor (pero se puede deshabilitar en el autor o habilitar en la publicación). Consulte [Asignación de usuarios y migración de entidades principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) para obtener más información.

1. **Ingesta**: hace referencia a la ingesta de contenido del *conjunto de migración* en la instancia de Cloud Service del destinatario.

   Para obtener más detalles, consulte [Proceso de ingesta en la transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

## Atributos de un conjunto de migración {#attributes-migration-set}

El conjunto de migración tiene los siguientes atributos:

* Con la nueva versión, puede crear un máximo de diez conjuntos de migración dentro de un proyecto creado en Cloud Acceleration Manager.
* Cada conjunto de migración debe tener un nombre exclusivo.

La herramienta de transferencia de contenido tiene una función que permite agregar contenido diferencial donde solo es posible transferir los cambios realizados desde la actividad de transferencia de contenido anterior.

>[!NOTE]
>Después de la transferencia de contenido inicial, se recomienda realizar frecuentes recargas de contenido diferencial para acortar el período de congelación de contenido para la transferencia de contenido diferencial final antes de lanzarse a Cloud Service.

En la fase de extracción, para ***completar*** un conjunto de migración existente, se debe desactivar la opción de *sobrescritura*. Consulte [Extracción Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) para obtener más información.

En la fase de ingesta, para aplicar el contenido delta sobre el contenido actual, se debe desactivar la opción de *borrado*. Consulte [Ingesta Superior](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) para obtener más información.

## Caducidad del conjunto de migración {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="Caducidad de un conjunto de migración"
>abstract="Obtenga información sobre la caducidad de un conjunto de migración."

Todos los conjuntos de migración caducarán finalmente después de un período prolongado de inactividad de aproximadamente 45 días. Una vez que los indicadores se muestren en la tarjeta de proyecto y en las filas de la tabla de trabajos de migración durante un período de tiempo, el conjunto de migración caducará y sus datos dejarán de estar disponibles. La hora de caducidad se puede ampliar fácilmente actuando en función del conjunto de migración de las siguientes formas:

* edición de su descripción
* obteniendo su clave de extracción
* realización de una extracción en él
* realizar una ingesta desde él

La caducidad de un conjunto de migración se puede supervisar en la fila Conjunto de migración. Un indicador visual útil de que un conjunto de migración se está acercando a su fecha de caducidad también agregó la tarjeta del proyecto.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## Siguientes pasos {#whats-next}

Una vez que haya obtenido información general sobre la herramienta de transferencia de contenido, en la que se indica que esta herramienta se puede utilizar para mover contenido existente de una instancia de AEM de origen (On-Premise o AMS) a la instancia de AEM Cloud Service del destinatario, debe revisar los [Requisitos previos para la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).
