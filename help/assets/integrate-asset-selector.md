---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Integre el selector de recursos con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 47%

---

# Integración del Selector de recursos mediante Vanilla JS {#integration-using-vanilla-js}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Puede integrar cualquier aplicación de [!DNL Adobe] o que no sea de Adobe con el repositorio [!DNL Experience Manager Assets] y seleccionar recursos desde la aplicación. Consulte [Integración del selector de recursos con varias aplicaciones](#asset-selector-integration-with-apps).

La integración se realiza importando el paquete Selector de recursos y conectándose a los Assets as a Cloud Service mediante la biblioteca JavaScript de Vanilla. Edite un `index.html` o cualquier archivo apropiado dentro de su aplicación para:

* Definición de los detalles de autenticación
* Acceso al repositorio Assets as a Cloud Service
* Configurar las propiedades de visualización del Selector de recursos

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* Está integrando una aplicación de [!DNL Adobe] en [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=es).
* Ya ha generado un token de IMS para la autenticación.

## Integración del Selector de recursos con varias aplicaciones {#asset-selector-integration-with-apps}

Puede integrar el Selector de recursos con varias aplicaciones, como:

* [Integrar el Selector de recursos con una aplicación  [!DNL Adobe] ](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integre el Selector de recursos con una aplicación que no sea de Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integración de Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
>* [Propiedades del selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integrar el Selector de recursos con Dynamic Media con capacidades OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
