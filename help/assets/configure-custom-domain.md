---
title: Configuración de un dominio personalizado para el nivel de entrega
description: Obtenga información sobre cómo configurar un dominio personalizado para el nivel de entrega en Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 80a32672ec018274b0410abfa14fdd761fdb5aba
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---


# Configuración de un dominio personalizado para el nivel de entrega{#configure-custom-domain}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

>[!NOTE]
>
>Los clientes con licencias de Dynamic Media Prime o Dynamic Media Ultimate deben utilizar la configuración de dominio personalizado de autoservicio disponible en Cloud Manager.Consulte [Documentación de Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md#configure-custom-domain-in-delivery-tier) para obtener más información.
>
>Los clientes que utilicen configuraciones de Dynamic Media antiguas en las que Dynamic Media con OpenAPI está habilitado manualmente, deben seguir esta documentación. Para estas configuraciones, la asignación de dominio personalizado se completa mediante una solicitud de asistencia de Adobe.

## Prepárese para empezar

Asegúrese de cumplir los siguientes requisitos antes de iniciar el proceso de configuración:

* Acceso a Cloud Manager
* Dynamic Media ya está habilitado con OpenAPI en su entorno a través de un ticket de asistencia
* Certificado SSL de tipo EV u OV para el dominio utilizado en el nivel de entrega. Consulte [Introducción a los certificados SSL](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates) para obtener más información

## Configuración de dominios personalizados en el nivel de envío mediante Cloud Manager

Ejecute los siguientes pasos en Cloud Manager:

1. [Agregar un certificado SSL administrado por el cliente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)

2. [Añadir un nombre de dominio personalizado](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)

Después de completar los pasos anteriores, genere un ticket de asistencia de Adobe para la asignación de dominios personalizados. Adobe realiza la asignación de dominios como parte del proceso de asistencia.

**Consulte también**

* [Traducir recursos](/help/assets/translate-assets.md)
* [API HTTP de recursos](/help/assets/mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](/help/assets/file-format-support.md)
* [Buscar recursos](/help/assets/search-assets.md)
* [Recursos de red](/help/assets/use-assets-across-connected-assets-instances.md)
* [Informes de recurso](/help/assets/asset-reports.md)
* [Esquemas de metadatos](/help/assets/metadata-schemas.md)
* [Descarga de recursos](/help/assets/download-assets-from-aem.md)
* [Administración de metadatos](/help/assets/manage-metadata.md)
* [Administración de plantillas de Dynamic Media](/help/assets/dynamic-media/manage-dynamic-media-templates.md)
* [Administrar informes](/help/assets/manage-reports-assets-view.md)
* [Facetas de búsqueda](/help/assets/search-facets.md)
* [Administrar colecciones](/help/assets/manage-collections.md)
* [Importación masiva de metadatos](/help/assets/metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

