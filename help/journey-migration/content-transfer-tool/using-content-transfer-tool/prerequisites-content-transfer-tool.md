---
title: Requisitos previos para la herramienta de transferencia de contenido
description: Requisitos previos para la herramienta de transferencia de contenido
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 11%

---

# Requisitos previos para la herramienta de transferencia de contenido {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>abstract="Revise consideraciones importantes para utilizar la herramienta de transferencia de contenido, incluidas las versiones de Java y AEM, los tipos de almacén de datos admitidos, las consideraciones de grupos de usuarios y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=es#pre-reqs" text="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#best-practices" text="Prácticas recomendadas y directrices"

En la tabla siguiente se resumen los requisitos previos para utilizar la herramienta de transferencia de contenido.

Revise todas las consideraciones enumeradas a continuación:

| Consideraciones | ¿Qué es compatible actualmente? |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Versión de AEM | La herramienta de transferencia de contenido solo se puede ejecutar en AEM versión 6.3 o posterior. |
| Tamaño del almacén de segmentos | Un repositorio existente que tiene menos de 55 millones de nodos JCR y hasta 250 GB (tamaño compactado en línea) en *Autor* y 50 GB en *Publicación* son compatibles actualmente. Cree un ticket de asistencia técnica con el Servicio de atención al cliente de Adobe para analizar las opciones de tamaño del almacén de segmentos por encima de estos límites. |
| Tamaño total del repositorio de contenido <br>*(almacén de segmentos + almacén de datos)* | La herramienta de transferencia de contenido está diseñada para transferir contenido de hasta 20 TB para el tipo de almacén de datos de archivos del almacén de datos. Actualmente no se admite cualquier valor superior a 20 TB. Cree un ticket de asistencia con el Servicio de atención al cliente de Adobe para analizar las opciones de contenido de más de 20 TB. <br>Para acelerar significativamente el proceso de transferencia de contenido para repositorios grandes, una [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=es#setting-up-pre-copy-step) se puede utilizar. Esto se aplica a los tipos de almacén de datos de archivos, Amazon S3 y Azure Data Store de almacén de datos. Para Amazon S3 y Azure Data Store, se admiten los tamaños de repositorio buenos a más de 20 TB. |
| Tamaño total del índice Lucene | Tamaño total del índice Lucene de 25 GB como máximo, excluido `/oak:index/lucene` y `/oak:index/damAssetLucene` es compatible actualmente. Cree un ticket de asistencia técnica con el Servicio de atención al cliente de Adobe para analizar las opciones de tamaño de índice por encima de este límite. |
| Longitud del nombre del nodo | La longitud de un nombre de nodo debe ser de 150 bytes o menos cuando la ruta principal del nodo es >= (igual o mayor que) 350 bytes. Estos nombres de nodo deben abreviarse para que tengan un valor &lt;= 150 bytes para que el almacén de nodos del documento los admita en AEM as a Cloud Service. Las entradas fallarán si no se corrigen estos nombres de nodo largos. |
| Contenido en rutas inmutables | La herramienta de transferencia de contenido no se puede usar para migrar contenido a rutas inmutables. Para transferir contenido de `/etc` only `/etc` se permite seleccionar rutas, pero solo para admitir [AEM Forms a AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). Para todos los demás casos de uso, consulte [Reestructuración común de repositorios](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html#restructuring) para obtener más información sobre la reestructuración de repositorios. |
| Valor de propiedad de nodo en MongoDB | Los valores de propiedad de nodo almacenados en MongoDB no pueden superar los 16 MB. Esto es aplicado por MongoDB. Las entradas fallarán si hay valores de propiedad superiores a este límite. Antes de ejecutar una extracción, ejecute esto [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) secuencia de comandos. Revise todos los valores de propiedad grandes y valide si son necesarios. Los que superen los 16 MB deberán convertirse a valores binarios. |

## Siguientes pasos {#whats-next}

Una vez que haya revisado los requisitos previos y haya determinado si puede utilizar la herramienta de transferencia de contenido en su proyecto de migración, consulte [Directrices y prácticas recomendadas para el uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html).
