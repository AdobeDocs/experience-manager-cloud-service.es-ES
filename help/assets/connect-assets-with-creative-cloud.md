---
title: Conectar AEM Assets a Creative Cloud
description: Obtenga información sobre cómo configurar y conectar AEM Assets a Creative Cloud. Conéctese a una asignación de derechos de Creative Cloud que esté aprovisionada para una organización IMS diferente para utilizar fácilmente las últimas integraciones de Creative Cloud en AEM Assets, incluidas Express y Creative Cloud Libraries.
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 80a32672ec018274b0410abfa14fdd761fdb5aba
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 74%

---

# Conectar AEM Assets a Creative Cloud  {#cross-org-entitlements}

Experience Manager Assets tiene la capacidad de conectarse a una asignación de derechos de Creative Cloud que se proporciona a una organización IMS diferente para utilizar fácilmente las últimas integraciones de Creative Cloud en AEM Assets, incluidas Express y Creative Cloud Libraries.

Si los productos de Creative Cloud y AEM Assets se suministran a organizaciones IMS independientes, puede conectarse a una organización de Creative Cloud diferente para poder ejecutar flujos de trabajo integrados entre las dos soluciones.

>[!IMPORTANT]
>
>La integración de Creative Cloud Libraries con Assets View se eliminará el 1 de mayo de 2026.

## Requisitos previos {#prerequisites}

* Derechos de administrador en Experience Manager Assets

* Derecho activo al Creative Cloud para el mismo ID de usuario utilizado en Creative Cloud y Experience Manager. Los derechos sobre los ID personales y federados con la misma dirección de correo electrónico se manejan como ID de usuario diferentes.

## Conexión a una nueva organización de Creative Cloud {#connect-to-creative-cloud-org}

Para conectarse a una nueva organización de Creative Cloud, ejecute los siguientes pasos:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Creative Cloud]**.

1. Seleccione la nueva organización de Creative Cloud mediante la lista desplegable **[!UICONTROL Seleccione el nuevo ID de organización de Creative Cloud]**. La lista muestra todas las organizaciones a las que tiene acceso. Seleccione la organización con derechos de Creative Cloud activos.

1. Haga clic en **[!UICONTROL Cambiar organizaciones]** para cambiar a la nueva organización.

   ![Derechos entre organizaciones](assets/cross-org-entitlements.png)

## Restricciones {#limitations}

* Puede conectar AEM Assets a una organización de Creative Cloud a la vez. No se admite la conexión a varias organizaciones de Creative Cloud a la vez.

* La organización de Creative Cloud a la que se conecta en AEM Assets se aplica a todos los usuarios de su organización.

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

