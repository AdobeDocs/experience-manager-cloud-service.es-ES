---
title: Conversor de índices
description: Conversor de índices
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# Conversor de índices {#index-converter}

Index Converter es una utilidad desarrollada para migrar las definiciones de índice de un cliente como preparación para el cambio a AEM as a Cloud Service.

## Introducción {#introduction}

El Conversor de índices permite a los desarrolladores de AEM migrar las definiciones de índices Oak personalizadas existentes a AEM definiciones de índices Oak personalizadas compatibles de forma as a Cloud Service.

>[!NOTE]
>El conversor de índices solo transforma *lucene* escriba las definiciones de índice personalizadas de Oak que están presentes en `/apps` o `/oak:index`. No se transforma *lucene* índices de tipo creados para `nt:base`.

Existen dos maneras de crear definiciones de índice Oak personalizadas:

* `under /apps` (a través de cualquier paquete de contenido personalizado)
* directamente en `/oak:index` ruta

If [Asegúrese del índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) Se ha utilizado, tenga en cuenta que asegúrese de que las definiciones no sean compatibles con AEM as a Cloud Service y, por lo tanto, primero deben convertirse a definiciones de índices de Oak y luego deben migrarse a definiciones de índices de Oak personalizadas compatibles con AEM as a Cloud Service según las siguientes directrices:

* Si la propiedad ignore está definida en `true`, ignorar u omitir la definición de Asegúrese
* Actualice el `jcr:primaryType` a `oak:QueryIndexDefinition`
* Elimine las propiedades que se deben ignorar, como se menciona en las configuraciones de OSGi
* Quitar subárbol `/facets/jcr:content` desde la definición de asegurado

## Uso del conversor de índices {#using-index-converter}

* A través de la CLI de Adobe I/O : Se recomienda utilizar el conversor de índices mediante `aio-cli-plugin-aem-cloud-service-migration` (AEM complemento de refactorización de código as a Cloud Service para la CLI de Adobe I/O).

   Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente: El conversor de índices también se puede ejecutar como una utilidad independiente.

   Consulte **[Recurso de Git: aem-cs-source-migration-index-conversion](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para aprender a utilizar esta herramienta.
