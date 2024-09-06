---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Integre el selector de recursos con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User
source-git-commit: fb1350c91468f9c448e34b66dc938fa3b5a3e9a9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 47%

---


# Integración del Selector de recursos mediante Vanilla JS {#integration-using-vanilla-js}

Puede integrar cualquier aplicación de [!DNL Adobe] o que no sea de Adobe con el repositorio [!DNL Experience Manager Assets] y seleccionar recursos desde la aplicación. Consulte [Integración del selector de recursos con varias aplicaciones](#integrate-asset-selector.md).

La integración se realiza importando el paquete Selector de recursos y conectándose a los Assets as a Cloud Service mediante la biblioteca JavaScript de Vanilla. Edite un `index.html` o cualquier archivo apropiado dentro de su aplicación para:

* Definición de los detalles de autenticación
* Acceso al repositorio Assets as a Cloud Service
* Configurar las propiedades de visualización del Selector de recursos

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* Está integrando una aplicación de [!DNL Adobe] en [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=es).
* Ya ha generado un token de IMS para la autenticación.

## Integración del Selector de recursos con varias aplicaciones {#asset-selector-integration-with-apps}

Puede integrar el Selector de recursos con varias aplicaciones, como:

* [Integrar el Selector de recursos con una aplicación  [!DNL Adobe] ](#integrate-asset-selector.md)
* [Integración del Selector de recursos con una aplicación que no sea de Adobe](#integrate-asset-selector-non-adobe.md)
* [Integración de Dynamic Media con funciones de OpenAPI](#integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Personalización del selector de recursos](/help/assets/asset-selector-customization.md)
>* [Propiedades del selector de recursos](/help/assets/asset-selector-properties.md)
>* [API abiertas de medios dinámicos del Selector de recursos integrado](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)

