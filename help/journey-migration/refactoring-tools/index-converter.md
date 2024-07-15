---
title: Conversor de índices
description: Obtenga información sobre cómo migrar sus definiciones de índice para prepararse para el paso a AEM as a Cloud Service.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Conversor de índices {#index-converter}

Index Converter es una utilidad desarrollada para migrar las definiciones de índice de un cliente como preparación para el paso a AEM as a Cloud Service.

## Introducción {#introduction}

AEM El Conversor de índices permite a los desarrolladores de migrar las definiciones de índice de Oak personalizadas existentes a definiciones de índice de Oak personalizadas compatibles con AEM as a Cloud Service.

>[!NOTE]
>El conversor de índices solo transforma las definiciones de índice de Oak personalizadas de tipo *lucene* que están presentes en `/apps` o `/oak:index`. No transforma los índices de tipo *lucene* creados para `nt:base`.

Existen dos formas de crear definiciones de índice de Oak personalizadas:

* `under /apps` (a través de cualquier paquete de contenido personalizado)
* directamente bajo la ruta de acceso `/oak:index`

Si se usó [Asegúrese de que el índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html), asegúrese de que las definiciones no sean compatibles con AEM as a Cloud Service. Como tal, primero deben convertirse a Definiciones de índice de Oak y luego migrarse a Definiciones de índice de Oak personalizadas compatibles con AEM as a Cloud Service, según las directrices siguientes:

* Si la propiedad omitir está establecida en `true`, ignorar u omitir la definición
* Actualizar `jcr:primaryType` a `oak:QueryIndexDefinition`
* Elimine cualquier propiedad que deba ignorarse como se menciona en las configuraciones OSGi
* Quitar subárbol `/facets/jcr:content` de la definición de secure

## Uso del convertidor de índices {#using-index-converter}

* A través de CLI de Adobe I/O: Adobe recomienda utilizar el Conversor de índices a través de `aio-cli-plugin-aem-cloud-service-migration` (complemento de refactorización de código AEM as a Cloud Service para la CLI de Adobe I/O).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para obtener información sobre cómo instalar y utilizar el complemento.

* Como utilidad independiente : El convertidor de índices también puede ejecutarse como utilidad independiente.

  Consulte **[Recurso de Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para obtener información sobre cómo utilizar esta herramienta.
