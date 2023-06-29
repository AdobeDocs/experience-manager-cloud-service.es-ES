---
title: Herramienta de Dispatcher Converter de AEM
description: Herramienta de Dispatcher Converter de AEM
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 24%

---

# Dispatcher Converter de AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Dispatcher Converter de AEM"
>abstract="Dispatcher Converter de Adobe Experience Manager AEM AEM convierte las configuraciones existentes en Dispatcher de forma a configuraciones en Dispatcher de forma as a Cloud Service."

Dispatcher Converter de Adobe Experience Manager AEM AEM convierte las configuraciones existentes en Dispatcher de forma a configuraciones en Dispatcher de forma as a Cloud Service.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché, equilibrio de carga o ambos de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. AEM Por lo tanto, puede aumentar la seguridad de la instancia de mediante Dispatcher con un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para obtener información sobre cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

AEM Obtenga información sobre cómo estructurar las configuraciones as a Cloud Service de Apache y Dispatcher, y cómo validarlas y ejecutarlas localmente antes de implementarlas en entornos en la nube.

Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

AEM AEM Dispatcher Converter proporciona la capacidad de refactorizar las configuraciones locales existentes o las configuraciones de Dispatcher de Adobe Managed Services a una configuración de Dispatcher compatible as a Cloud Service.

## Uso de Dispatcher Converter de AEM {#using-dispatcher-converter}

* A través de Adobe Developer CLI : Adobe AEM recomienda utilizar el convertidor de Dispatcher de forma mediante `aio-cli-plugin-aem-cloud-service-migration` AEM (complemento de refactorización de código as a Cloud Service para la CLI de Adobe Developer).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que pueda aprender a instalar y utilizar el complemento.

* AEM Como utilidad independiente : La herramienta Dispatcher Converter de Dispatcher también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso de Git: Dispatcher Converter de AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para que pueda obtener más información sobre el uso y la solución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla con NodeJS. Adobe recomienda tener instalado NodeJS 10.0+.
