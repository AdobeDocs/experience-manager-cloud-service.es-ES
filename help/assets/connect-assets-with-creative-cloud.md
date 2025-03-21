---
title: Conectar AEM Assets a Creative Cloud
description: Obtenga información sobre cómo configurar y conectar AEM Assets a Creative Cloud. Conéctese a una asignación de derechos de Creative Cloud que esté aprovisionada para una organización IMS diferente para utilizar fácilmente las últimas integraciones de Creative Cloud en AEM Assets, incluidas Express y Creative Cloud Libraries.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 70%

---

# Conectar AEM Assets a Creative Cloud  {#cross-org-entitlements}

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

Experience Manager Assets tiene la capacidad de conectarse a una asignación de derechos de Creative Cloud que se proporciona a una organización IMS diferente para utilizar fácilmente las últimas integraciones de Creative Cloud en AEM Assets, incluidas Express y Creative Cloud Libraries.

Si los productos de Creative Cloud y AEM Assets se suministran a organizaciones IMS independientes, puede conectarse a una organización de Creative Cloud diferente para poder ejecutar flujos de trabajo integrados entre las dos soluciones.

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
