---
title: Herramienta de Dispatcher Converter de AEM
description: AEM Aprenda a convertir las configuraciones existentes en Dispatcher de la manera más rápida a configuraciones en Dispatcher de AEM as a Cloud Service.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
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

Dispatcher es la herramienta de almacenamiento en caché, equilibrio de carga o ambos de Adobe Experience Manager. El uso de Dispatcher de AEM también le permitirá proteger el servidor AEM de ataques. AEM Por lo tanto, puede aumentar la seguridad de la instancia de la mediante Dispatcher con un servidor web de clase empresarial.

>[!NOTE]
>Generalmente, Dispatcher se utiliza para copiar en la caché las respuestas de las **instancias publicadas en AEM**, para aumentar así la capacidad de respuesta y seguridad de su sitio web público.

Consulte [Información general de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para conocer cómo Dispatcher realiza el almacenamiento en caché, devuelve documentos y realiza el equilibrio de carga.

### Configuración y prueba de Apache y Dispatcher {#dispatcher-configurations-cloud}

Obtenga información sobre cómo estructurar las configuraciones de AEM as a Cloud Service Apache y Dispatcher, y cómo validarlas y ejecutarlas localmente antes de implementarlas en entornos en la nube.

Consulte [Dispatcher en la nube](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para obtener más información.

## Dispatcher Converter de AEM {#aem-dispatcher-converter}

AEM El convertidor de Dispatcher proporciona la capacidad de refactorizar las configuraciones locales o de Adobe existentes de Managed Services Dispatcher a una configuración de Dispatcher compatible con AEM as a Cloud Service.

## AEM Uso de Dispatcher Converter {#using-dispatcher-converter}

* A través de Adobe Developer CLI : El Adobe AEM recomienda utilizar el conversor Dispatcher de a través de `aio-cli-plugin-aem-cloud-service-migration` (complemento de refactorización de código AEM as a Cloud Service para la CLI de Adobe Developer).

  Consulte **[Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para obtener información sobre cómo instalar y utilizar el complemento.

* AEM Como utilidad independiente : La herramienta Conversor de Dispatcher de la aplicación también se puede ejecutar como utilidad independiente.

  Consulte **[Recurso Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para obtener información sobre el uso y la solución de problemas de esta herramienta.

>[!IMPORTANT]
>AEM Dispatcher Converter se desarrolla mediante NodeJS. Adobe recomienda tener instalado NodeJS 10.0+.
