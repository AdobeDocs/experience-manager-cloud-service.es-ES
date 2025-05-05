---
title: Requisitos previos para la herramienta de transferencia de contenido
description: Familiarícese con los requisitos previos de la herramienta de transferencia de contenido
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
feature: Migration
role: Admin
source-git-commit: d8730109f5cd7dab44f535b1de008ae09811f221
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 13%

---


# Requisitos previos para la herramienta de transferencia de contenido {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>abstract="Revise las consideraciones importantes para usar la herramienta de transferencia de contenido, incluidas las versiones de Java™ y AEM, los tipos de almacén de datos admitidos, las consideraciones de grupos de usuarios y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=es" text="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=es#best-practices" text="Prácticas recomendadas y directrices"

La siguiente tabla resume los requisitos previos para utilizar la herramienta de transferencia de contenido.

Revise todas las consideraciones enumeradas a continuación:

| Consideraciones | Qué se admite actualmente |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versión de AEM | AEM La herramienta de transferencia de contenido solo se puede ejecutar en la versión 6.3 o superior de la versión de. |
| Tamaño del almacén de segmentos | Actualmente se admite un repositorio existente que tenga menos de 750 millones de nodos JCR y hasta 500 GB (tamaño compactado en línea) en *Author* y 50 GB en *Publish*. Cree un vale de soporte con el Servicio de atención al cliente de Adobe para que pueda analizar las opciones de tamaño de almacén de segmentos por encima de estos límites. |
| Tamaño total del repositorio de contenido <br>*(almacén de segmentos + almacén de datos)* | La herramienta de transferencia de contenido está diseñada para transferir contenido de hasta 20 terabytes para el tipo de almacén de datos de archivo. Actualmente no se admite nada superior a 20 terabytes. Cree un ticket de asistencia con el Servicio de atención al cliente de Adobe para poder analizar las opciones de contenido superior a 20 terabytes. <br>Para acelerar significativamente el proceso de transferencia de contenido en repositorios grandes, se puede usar un paso [previo a la copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=es#setting-up-pre-copy-step) opcional. Este proceso se aplica a los tipos de almacén de datos de File Data Store, Amazon S3 y Azure Data Store. Para Amazon S3 y Azure Data Store, se admiten tamaños de repositorio superiores a 20 terabytes. |
| Tamaño total del índice de Lucene | Se admite un tamaño máximo de índice de Lucene de 25 GB, excluyendo `/oak:index/lucene` y `/oak:index/damAssetLucene`. Cree un vale de soporte con el Servicio de atención al cliente de Adobe para poder analizar las opciones de tamaño de índice por encima de este límite. |
| Contenido en rutas inmutables | La herramienta de transferencia de contenido no se puede usar para migrar contenido en rutas inmutables. Para transferir contenido de `/etc`, puede seleccionar ciertas rutas de acceso de `/etc`, pero solo para admitir [AEM Forms en AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=es#paths-of-various-aem-forms-specific-assets). Para todos los demás casos de uso, consulte [Reestructuración común de repositorios](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html?lang=es) para obtener más información sobre la reestructuración de repositorios. |
| Valor de propiedad del nodo en MongoDB | Los valores de propiedad del nodo almacenados en MongoDB no pueden superar los 16 MB. Esta regla la aplica MongoDB. Las ingestas fallan si hay valores de propiedad superiores a este límite. Antes de ejecutar una extracción, ejecute este script [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar). Revise todos los valores de propiedades de gran tamaño y valide si son necesarios. Los que superen los 16 MB deben convertirse a valores binarios. |

## Siguientes pasos {#whats-next}

Una vez que haya revisado los requisitos previos y haya determinado si puede usar la herramienta de transferencia de contenido en su proyecto de migración, consulte [Directrices y prácticas recomendadas para usar la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=es).
