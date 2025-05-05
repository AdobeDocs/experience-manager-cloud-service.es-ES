---
title: Integrar AEM Assets con aplicaciones descendentes
description: Integrar AEM Assets con aplicaciones descendentes
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 33%

---

# Integrar AEM Assets con aplicaciones descendentes {#integrate-dynamic-media-open-apis}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>La guía de Dynamic Media con funciones de OpenAPI ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía en PDF de Dynamic Media con funciones OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Todos los [recursos aprobados](/help/assets/approve-assets.md) disponibles en el repositorio de recursos de Experience Manager están disponibles para su envío a aplicaciones de flujo descendente.

Puede integrar su propia interfaz de usuario personalizada con el repositorio de Experience Manager Assets mediante las API de búsqueda y envío o utilizar el selector de recursos de Micro-Front-end de Adobe.

![Integración con el repositorio de AEM Assets](assets/asset-selector-integration.png)

Las API permiten buscar los recursos aprobados desde el repositorio de AEM Assets y, a continuación, enviar los recursos a aplicaciones de flujo descendente mediante una URL de entrega. Para obtener más información, consulte las API [Search](/help/assets/search-assets-api.md) y [Delivery](/help/assets/deliver-assets-apis.md).

El Selector de recursos de Micro-FrontEnd de Adobe proporciona una interfaz de usuario que se integra fácilmente con el repositorio [!DNL Experience Manager Assets as a Cloud Service], de modo que puede examinar o buscar recursos digitales aprobados disponibles en el repositorio y utilizarlos en la experiencia de creación de aplicaciones. Para obtener más información, consulte [Selector de recursos de Micro-Frontend](/help/assets/overview-asset-selector.md).

>[!MORELIKETHIS]
>
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Personalización del selector de recursos](/help/assets/asset-selector-customization.md)
