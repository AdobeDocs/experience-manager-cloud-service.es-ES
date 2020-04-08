---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.4.0
description: Notas de la versión de Experience Manager para 2020.4.0
translation-type: tm+mt
source-git-commit: 57df03fe198564a6c02e54e19ef059e46064d163

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

La fecha de lanzamiento de [!DNL Experience Manager] como servicio de nube 2020.4.0 es el 9 de abril de 2020.

## What&#39;s New in Assets {#assets}

Obtenga información sobre las nuevas funciones, mejoras y correcciones de errores de [!DNL Experience Manager Assets] y [!DNL Dynamic Media] en la versión actual.

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) admite los casos de uso de distribución de recursos para Experience Manager Assets. [!DNL Brand Portal] ayuda a las organizaciones a satisfacer sus necesidades de marketing mediante la distribución segura de recursos de productos y marcas aprobados a agencias externas, socios, equipos internos y distribuidores para su descarga.
   * [!DNL Brand Portal] la configuración se completa mediante [!DNL Adobe I/O] la consola.
   * El abastecimiento de recursos en [!DNL Brand Portal] no es compatible con [!DNLEExperience Manager] como servicio de nube.

* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) v2.0 funciona [!DNL Experience Manager] como un servicio de nube. [!DNL Adobe Asset Link] facilita la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido mediante la conexión [!DNL Experience Manager Assets] con las aplicaciones de [!DNL Creative Cloud] escritorio [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] a través del panel en la aplicación [!DNL Asset Link] .
   * [!DNL Experience Manager] está preconfigurado para [!DNL Adobe Asset Link], lo que resulta en una configuración [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) sencilla y una implementación más rápida para los profesionales creativos.
   * [!DNL Asset Link] ahora es compatible con un conmutador [de entorno de](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) Experience Manager que permite a los usuarios creativos conectarse fácilmente a un [!DNL Experience Manager] entorno diferente. Un ejemplo en el que esta funcionalidad es útil es para diseñadores de agencias que trabajan con varios clientes mediante diferentes [!DNL Experience Manager Assets] implementaciones.

* Los usuarios pueden configurar flujos de trabajo [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) postprocesamiento para el inicio automático en la interfaz de usuario [!UICONTROL Propiedades] de la carpeta para jerarquías de carpetas específicas.
   * La interfaz de usuario [!UICONTROL Propiedades] de la carpeta se simplifica, con la nueva ficha Procesamiento [!UICONTROL de] recursos que contiene el perfil de metadatos, el perfil de procesamiento y la nueva configuración del flujo de trabajo de inicio automático.
   * El cuadro de diálogo de reprocesamiento de recursos permite seleccionar un perfil de procesamiento específico y decidir volver a procesarlo en subcarpetas.
   * [!DNL Dynamic Media]:: Se ha Añadido la configuración de publicación selectiva para que los recursos se publiquen automáticamente solo para previsualización segura. Además, los recursos se pueden publicar explícitamente en Experience Manager sin necesidad de publicarlos en DMS7 para envío de dominio público.

* Se abordan las siguientes cuestiones:
   * Correcciones de problemas de procesamiento de recursos.
   * Correcciones en [!DNL Dynamic Media] la configuración y publicación de recursos en el servicio de [!DNL Dynamic Media] envío.

>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurar el portal de marca](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurar Experience Manager para que funcione con Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Crear un flujo de trabajo en Experience Manager mediante los microservicios de recursos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)

