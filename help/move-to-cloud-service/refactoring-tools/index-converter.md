---
title: Convertidor de índices
description: Convertidor de índices
translation-type: tm+mt
source-git-commit: adfc453729b88a9cc457783806eb7b4d69150b21
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Convertidor de índices {#index-converter}

Index Converter es una utilidad desarrollada para migrar la definición de índice de un cliente como preparación para el cambio a AEM como Cloud Service.

## Introducción {#introduction}

Index Converter permite a los desarrolladores de AEM migrar las definiciones de índices Oak personalizados existentes a AEM como definiciones de índices Oak personalizados compatibles con el Cloud Service.

>[!NOTE]
>El Convertidor de índices solo transforma las definiciones de índice de roble personalizado de tipo *lucene* que están presentes en `/apps` o `/oak:index`. No transforma los índices de tipo *lucene* que se crean para `nt:base`.

Existen dos formas de crear definiciones de índice Oak personalizadas:

* `under /apps` (a través de cualquier paquete de contenido personalizado)
* directamente en `/oak:index` ruta

>[!NOTE]
>Consulte [Asegurarse de que el índice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) aprenda a definir y crear definiciones Oak

## Uso del Convertidor de índices {#using-index-converter}

>[!NOTE]
>Aunque se recomienda utilizar la herramienta Index Converter mediante [complemento CLI de AIO para la migración de fuentes](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration), también se puede ejecutar de forma independiente.

Consulte **[Recurso de Git: aem-cs-source-Migration-index-converter](https://git.corp.adobe.com/vavarshn/aem-cloud-service-source-migration/blob/master/packages/index-converter/README.md)** para aprender a instalar y utilizar el complemento.

