---
title: Herramienta de Dispatcher Converter de AEM
description: Herramienta de Dispatcher Converter de AEM
translation-type: ht
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: ht
source-wordcount: '348'
ht-degree: 100%

---


# Dispatcher Converter de AEM {#introduction}

Dispatcher Converter de Adobe Experience Manager convierte las configuraciones existentes de AMS Dispatcher a configuraciones de AEM as a Cloud Service Dispatcher.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es la herramienta de almacenamiento en caché o de equilibrio de carga de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. Por lo tanto, puede aumentar la seguridad de su instancia de AEM mediante Dispatcher y un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://docs.adobe.com/content/help/es-ES/experience-manager-dispatcher/using/dispatcher.html) para conocer cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

Debe aprender a estructurar las configuraciones de Apache y Dispatcher de AEM as a Cloud Service, así como a validarla y ejecutarla localmente antes de implementarla en entornos en la nube.

Consulte [Dispatcher en la nube](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

Dispatcher Converter de AEM es una utilidad para convertir configuraciones existentes de AMS Dispatcher a configuraciones de AEM as a Cloud Service Dispatcher. Esta utilidad es para instancias de AMS.

El conversor implementado es **AEMDispatcherConfigConverter** que sigue las directrices de transformación.

Consulte [Conversión de AMS a una configuración de Dispatcher de Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) para convertir un AMS a una configuración de Dispatcher de Adobe Experience Manager as a Cloud Service.

## Uso de Dispatcher Converter de AEM {#using-dispatcher-converter}

En la sección siguiente se describen los recursos y la información necesarios para utilizar la herramienta Dispatcher Converter de AEM.

Consulte el documento **[Recursos de Git: Dispatcher Converter de AEM Cloud Service](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**para conocer sobre el uso, las limitaciones y la resolución de problemas de esta herramienta.

>[!IMPORTANT]
>Dispatcher Converter de AEM se desarrolla con Python 3.7.3. Se recomienda tener instalado Python 3.5 o superior.

## Restricciones     {#limitations}

Dispatcher Converter de AEM funciona bajo el supuesto de que la estructura de la carpeta de configuración de Dispatcher proporcionada es similar a la descrita en la configuración de Dispatcher de Cloud Manager.


