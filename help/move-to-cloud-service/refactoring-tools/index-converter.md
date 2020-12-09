---
title: Convertidor de índices
description: Convertidor de índices
translation-type: tm+mt
source-git-commit: 3fe19282f9e96d503f4e8be05553c6f48a6f19b6
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Convertidor de índices {#index-converter}

Index Converter es una herramienta desarrollada para migrar las definiciones de índice de un cliente como preparación para el cambio a AEM como Cloud Service.

## Introducción {#introduction}

El Convertidor de índices permite a los desarrolladores de AEM migrar las definiciones de índices Oak personalizados existentes a AEM como definiciones de índices Oak personalizados compatibles con el Cloud Service.

>[!NOTE]
>El Convertidor de índices solo transforma las definiciones de índice de roble personalizado de tipo *lucene* que están presentes en `/apps` o `/oak:index`. No transforma los índices de tipo *lucene* que se crean para `nt:base`.

Existen dos formas de crear definiciones de índice Oak personalizadas:

* `under /apps` (a través de cualquier paquete de contenido personalizado)
* directamente en `/oak:index` ruta

Si [Asegúrese de utilizar el índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html), tenga en cuenta que Asegurarse de que las definiciones no sean compatibles con AEM como Cloud Service y, por lo tanto, primero deben convertirse a definiciones de índices Oak y luego deben migrarse a definiciones de índices Oak personalizadas compatibles con AEM como Cloud Service, según las directrices siguientes:

* Si la propiedad ignore está establecida en `true`, omita o omita la definición de aseguramiento
* Actualice `jcr:primaryType` a `oak:QueryIndexDefinition`
* Elimine las propiedades que se deben ignorar, como se indica en las configuraciones de OSGi
* Quitar subárbol `/facets/jcr:content` de la definición de aseguramiento

## Uso del Convertidor de índices {#using-index-converter}

* Mediante Adobe I/O CLI: Se recomienda utilizar Index Converter mediante `aio-cli-plugin-aem-cloud-service-migration` (AEM como un complemento de refactorización de código de Cloud Service para Adobe I/O CLI).

   Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente: Index Converter también se puede ejecutar como una utilidad independiente.

   Consulte **[Recurso de Git: aem-cs-source-Migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para aprender a utilizar esta herramienta.



