---
title: Herramienta de Dispatcher Converter de AEM
description: AEM AEM Aprenda a convertir las configuraciones existentes en Dispatcher de forma que se conviertan en configuraciones en Dispatcher as a Cloud Service de la.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 28%

---

# Dispatcher Converter de AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Dispatcher Converter de AEM"
>abstract="El conversor de Adobe Experience Manager Dispatcher convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher."

El conversor de Adobe Experience Manager Dispatcher convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché, equilibrio de carga o ambos de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. AEM Por lo tanto, puede aumentar la seguridad de la instancia de mediante Dispatcher con un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para obtener información sobre cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

AEM Obtenga información sobre cómo estructurar las configuraciones as a Cloud Service de Apache y Dispatcher, y cómo validarlas y ejecutarlas localmente antes de implementarlas en entornos en la nube.

Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

AEM Dispatcher Converter proporciona la capacidad de refactorizar las configuraciones locales o de Adobe de Managed Services AEM Dispatcher existentes para establecer una configuración de Dispatcher compatible as a Cloud Service con la de Dispatcher.

## AEM Uso de Dispatcher Converter {#using-dispatcher-converter}

* A través de Adobe Developer CLI : Adobe AEM recomienda utilizar el convertidor de Dispatcher de forma mediante `aio-cli-plugin-aem-cloud-service-migration` AEM (complemento de refactorización de código as a Cloud Service para la CLI de Adobe Developer).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que pueda aprender a instalar y utilizar el complemento.

* AEM Como utilidad independiente : La herramienta Dispatcher Converter de Dispatcher también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso de Git: Dispatcher Converter de AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para que pueda obtener más información sobre el uso y la solución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla con NodeJS. Adobe recomienda tener instalado NodeJS 10.0+.
