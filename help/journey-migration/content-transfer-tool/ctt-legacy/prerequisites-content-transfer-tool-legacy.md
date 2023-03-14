---
title: Requisitos previos para la herramienta de transferencia de contenido (heredada)
description: Requisitos previos para la herramienta de transferencia de contenido
hide: true
hidefromtoc: true
exl-id: 6b2878cb-6882-452b-8cab-e590316633f6
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 2%

---

# Requisitos previos para la herramienta de transferencia de contenido (heredada) {#prerequisites}

La siguiente tabla resume los requisitos previos para utilizar la herramienta de transferencia de contenido.

Revise todas las consideraciones enumeradas a continuación:

| Consideraciones | Qué se admite actualmente |
|--- |--- |
| Versión de AEM | AEM La herramienta de transferencia de contenido solo se puede ejecutar en la versión 6.3 o superior de la versión de. |
| Tamaño del almacén de segmentos | Repositorio existente que tiene menos de 55 millones de nodos JCR y hasta 83 GB (tamaño compactado en línea) en *Autor* y 31 GB en *Publish* son compatibles actualmente. Cree un vale de soporte con el Servicio de atención al cliente de Adobe para discutir las opciones de tamaño de almacén de segmentos por encima de estos límites. |
| Tamaño total del repositorio de contenido <br>*(almacén de segmentos + almacén de datos)* | La herramienta de transferencia de contenido está diseñada para transferir contenido de hasta 20 TB para el tipo de almacén de datos de archivo. Actualmente no se admite nada superior a 20 TB. Cree un ticket de asistencia con el Servicio de atención al cliente de Adobe para discutir las opciones de contenido superior a 20 TB. <br>Para acelerar de forma significativa el proceso de transferencia de contenido para repositorios grandes, una [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step) Este paso se puede utilizar. Esto se aplica a los tipos de almacén de datos de File Data Store, Amazon S3 y Azure Data Store. Para Amazon S3 y Azure Data Store, se admiten tamaños de repositorio buenos a 20 TB. |
| Tamaño total del índice de Lucene | Actualmente, se admite un tamaño máximo de índice de Lucene de 25 GB. Cree un vale de soporte con el Servicio de atención al cliente de Adobe para discutir las opciones de tamaño de índice por encima de este límite. |
| Longitud del nombre del nodo | La longitud del nombre de un nodo debe ser de 150 bytes o menos. AEM Los nombres de nodo superiores a 150 bytes deben abreviarse para que sean &lt;= 150 bytes a fin de que sea compatible con el almacén de nodos de documento en as a Cloud Service de la. Las ingestas fallarán si estos nombres de nodo largos no están fijos. |
| Contenido en rutas inmutables | La herramienta de transferencia de contenido no se puede usar para migrar contenido en rutas inmutables. Para transferir contenido desde `/etc` solo ciertos `/etc` se permite seleccionar las rutas, pero solo para admitir [as a Cloud Service de AEM Forms a AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Para todos los demás casos de uso, consulte [Reestructuración común de repositorios](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) para obtener más información sobre la reestructuración de repositorios. |
| Valor de propiedad del nodo en MongoDB | Los valores de propiedad del nodo almacenados en MongoDB no pueden superar los 16 MB. Esto lo aplica MongoDB. Las ingestas fallarán si hay valores de propiedad superiores a este límite. Antes de ejecutar una extracción, ejecute esto [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) script. Revise todos los valores de propiedades de gran tamaño y valide si son necesarios. Los que superen los 16 MB deberán convertirse a valores binarios. |

## Siguientes pasos {#whats-next}

Una vez que haya revisado los requisitos previos y haya determinado si puede utilizar la herramienta de transferencia de contenido en su proyecto de migración, consulte [Directrices y prácticas recomendadas para utilizar la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en).
