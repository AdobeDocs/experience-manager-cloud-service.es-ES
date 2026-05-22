---
title: Herramienta de Dispatcher Converter de AEM
description: Aprenda a convertir las configuraciones existentes en AEM Dispatcher a configuraciones en AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 30%

---

# Dispatcher Converter de AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Dispatcher Converter de AEM"
>abstract="El conversor de Adobe Experience Manager Dispatcher convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher."

El conversor de Adobe Experience Manager Dispatcher convierte las configuraciones existentes de AEM Dispatcher en configuraciones de AEM as a Cloud Service Dispatcher.

## Introducción a Dispatcher {#introduction-dispatcher}

Dispatcher es la herramienta de almacenamiento en caché, equilibrio de carga o ambos de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. Por lo tanto, puede aumentar la seguridad de su instancia de AEM mediante Dispatcher con un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para conocer cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

Obtenga información sobre cómo estructurar las configuraciones de AEM as a Cloud Service Apache y Dispatcher, y cómo validarlas y ejecutarlas localmente antes de implementarlas en entornos en la nube.

Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

AEM Dispatcher Converter permite refactorizar las configuraciones locales o de Adobe Managed Services Dispatcher existentes a una configuración de Dispatcher compatible con AEM as a Cloud Service.

## Uso del conversor AEM Dispatcher {#using-dispatcher-converter}

* A través de Adobe Developer CLI : Adobe recomienda utilizar AEM Dispatcher Converter mediante `aio-cli-plugin-aem-cloud-service-migration` (complemento de refactorización de código AEM as a Cloud Service para Adobe Developer CLI).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para obtener información sobre cómo instalar y utilizar el complemento.

* Como utilidad independiente : La herramienta Dispatcher Converter de AEM también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso Git: Conversor Dispatcher de AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para obtener información sobre el uso y la solución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla con NodeJS. Adobe recomienda tener instalado NodeJS 10.0 o posterior.
