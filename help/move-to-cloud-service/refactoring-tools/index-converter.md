---
title: Convertidor de índices
description: Convertidor de índices
translation-type: tm+mt
source-git-commit: 21bd9392d913369a5e8e0ebd9badbbe30fd4bba3
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Convertidor de índices {#index-converter}

Index Converter es una utilidad desarrollada para migrar la definición de índice de un cliente como preparación para el cambio a AEM como Cloud Service.

## Introducción {#introduction}

Index Converter permite a los desarrolladores de AEM migrar las definiciones de índices Oak personalizados existentes a AEM como definiciones de índices Oak personalizados compatibles con el Cloud Service.

>[!NOTE]
>El Convertidor de índices solo transforma *lucene* las definiciones de índice de roble personalizado presentes en `/apps` o `/oak:index`. No transforma los índices de tipo *lucene* que se crean para `nt:base`.

## Uso del Convertidor de índices {#using-index-converter}

Consulte **[Recurso de Git: aem-cs-source-Migration-index-converter](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

