---
title: Conversor de índices
description: AEM Obtenga información sobre cómo migrar sus definiciones de índice para prepararse para el paso a la as a Cloud Service de la.
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---

# Conversor de índices {#index-converter}

AEM Index Converter es una utilidad desarrollada para migrar las definiciones de índice de un cliente con el fin de prepararlo para el paso a las definiciones de índice as a Cloud Service.

## Introducción {#introduction}

AEM AEM El Conversor de índices permite a los desarrolladores de migrar las definiciones de índice de Oak personalizadas existentes a definiciones de índice de Oak personalizadas compatibles con el as a Cloud Service.

>[!NOTE]
>Solo se transforma el conversor de índices *lucene* Escriba Definiciones de índice de Oak personalizadas que estén presentes en `/apps` o `/oak:index`. No se transforma *lucene* índices de tipo creados para `nt:base`.

Existen dos formas de crear definiciones de índice de Oak personalizadas:

* `under /apps` (mediante cualquier paquete de contenido personalizado)
* directamente debajo de `/oak:index` ruta

If [Asegurar el índice de Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) AEM se ha utilizado, Asegúrese de que las definiciones no sean compatibles con los as a Cloud Service de la. AEM Como tal, primero deben convertirse a Definiciones de índice de Oak y luego migrarse a Definiciones de índice de Oak personalizadas que sean compatibles con las definiciones de índice de Oak as a Cloud Service, según las directrices siguientes:

* Si la propiedad omitir se establece en `true`, ignorar u omitir la definición de
* Actualice el `jcr:primaryType` hasta `oak:QueryIndexDefinition`
* Elimine cualquier propiedad que deba ignorarse como se menciona en las configuraciones OSGi
* Quitar subárbol `/facets/jcr:content` desde la definición de Asegúrese

## Uso del convertidor de índices {#using-index-converter}

* A través de CLI de Adobe I/O : Adobe recomienda utilizar el Conversor de índices a través de `aio-cli-plugin-aem-cloud-service-migration` AEM (complemento de refactorización de código as a Cloud Service para la CLI de Adobe I/O).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente : El convertidor de índices también puede ejecutarse como utilidad independiente.

  Consulte **[Recurso de Git: aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** para aprender a utilizar esta herramienta.
