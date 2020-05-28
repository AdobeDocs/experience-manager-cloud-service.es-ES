---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter convierte las configuraciones existentes de AMS Dispatcher a AEM como una configuración de Cloud Service Dispatcher.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es la herramienta de almacenamiento en caché o de equilibrio de carga de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. Por lo tanto, puede aumentar la seguridad de su instancia de AEM mediante Dispatcher y un servidor web de clase empresarial.

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

Consulte Información general [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) Dispatcher para conocer cómo realiza el despachante el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

Debe aprender a estructurar AEM como una configuración de Apache y Dispatcher de servicio de nube, así como a validarla y ejecutarla localmente antes de implementarla en entornos de nube.

Consulte [Dispatcher en la nube](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) para obtener más información.

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter es una utilidad para convertir configuraciones existentes de AMS Dispatcher a AEM como configuraciones de Cloud Service Dispatcher. Esta utilidad es para instancias de AMS.

El convertidor implementado es **AEMDispatcherConfigConverter** que sigue las directrices de transformación.

Consulte [Conversión de un AMS a una configuración](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) de Adobe Experience Manager como distribuidor de servicios en la nube para convertir un AMS a una configuración de Adobe Experience Manager como distribuidor de servicios en la nube.

## Uso de AEM Dispatcher Converter {#using-dispatcher-converter}

En la sección siguiente se describen los recursos y la información necesarios para utilizar la herramienta AEM Dispatcher Converter.

Consulte Recurso **[Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**para conocer el uso, las limitaciones y la resolución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla con Python 3.7.3. Se recomienda tener instalado Python 3.5 o superior.

## Restricciones          {#limitations}

AEM Dispatcher Converter funciona suponiendo que la estructura de la carpeta de configuración del despachante proporcionada es similar a la descrita en la configuración del despachante de Cloud Manager.


