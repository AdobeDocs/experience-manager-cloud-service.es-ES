---
title: Herramienta de Dispatcher Converter de AEM
description: Herramienta de Dispatcher Converter de AEM
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 61%

---

# Dispatcher Converter de AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Dispatcher Converter de AEM"
>abstract="Dispatcher Converter de Adobe Experience Manager convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher."

Dispatcher Converter de Adobe Experience Manager convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es la herramienta de almacenamiento en caché o de equilibrio de carga de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. Por lo tanto, puede aumentar la seguridad de su instancia de AEM mediante Dispatcher y un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para conocer cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

Debe aprender a estructurar las configuraciones de Apache y Dispatcher de AEM as a Cloud Service, así como a validarla y ejecutarla localmente antes de implementarla en entornos en la nube.

Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=es) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

AEM Dispatcher Converter proporciona la capacidad de refactorizar las configuraciones existentes in situ o Adobe Managed Services Dispatcher para AEM configuración as a Cloud Service compatible con Dispatcher.

## Uso de Dispatcher Converter de AEM {#using-dispatcher-converter}

* A través de la CLI de Adobe I/O : Se recomienda utilizar el AEM Dispatcher Converter mediante `aio-cli-plugin-aem-cloud-service-migration` (AEM complemento de refactorización de código as a Cloud Service para la CLI de Adobe I/O).

   Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para aprender a instalar y utilizar el complemento.

* Como utilidad independiente: La herramienta AEM Dispatcher Converter también se puede ejecutar como una utilidad independiente.

   Consulte **[Recurso de Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para obtener más información sobre el uso y la resolución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla mediante NodeJS. Se recomienda tener instalado NodeJS 10.0+.
