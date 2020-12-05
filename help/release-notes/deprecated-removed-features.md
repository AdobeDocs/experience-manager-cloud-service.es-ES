---
title: Funciones en desuso y eliminadas
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager as a Cloud Service.
translation-type: tm+mt
source-git-commit: e31ac0c2d28f60d7b98036c16f154a09da51d6bf
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 92%

---


# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores. Además, como Adobe Experience Manager as a Cloud Service proporciona un modelo de implementación nativo de la nube, ciertas funciones y características fueron reemplazadas por homólogos nativos de la nube.

Para comunicar la eliminación o el reemplazo inminente de las capacidades de AEM, se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Las funciones obsoletas siguen estando disponibles, pero no se siguen actualizando.
1. Las funciones anunciadas como obsoletas se eliminan en la siguiente versión principal, como pronto. Se anuncia la auténtica fecha límite para la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección enumera las funciones que se han marcado como obsoletas en Experience Manager as a Cloud Service. Normalmente, las funciones que se quieren eliminar en una versión futura se establecen en primer lugar como obsoletas, con una alternativa que las sustituye.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Capacidades | Función en desuso | Reemplazo |
| ------------ | ------------------ | ----------- |
| Assets | `DAM Asset Update` flujo de trabajo para procesar imágenes grabadas. | Ahora, el consumo de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos. |
| Recursos | Cargar recursos directamente en AEM. Consulte [API de carga de recursos en desuso](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilice la [carga binaria directa](/help/assets/add-assets.md). Para obtener más información técnica, consulte [API de carga directa](/help/assets/developer-reference-material-apis.md#upload-binary). |
| Recursos | No se admiten [determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) en el flujo de trabajo `DAM Asset Update`, incluida la llamada a herramientas de línea de comandos como ImageMagick.. | [Los microservicios de recursos](/help/assets/asset-microservices-overview.md) sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| Recursos | Fmpeg transcodificar vídeos. | Para la generación de miniaturas de FFmpeg, use los [microservicios de Asset](/help/assets/asset-microservices-overview.md). Para la transcodificación FFmpeg, utilice [Dynamic Media](/help/assets/manage-video-assets.md). |

## Funciones eliminadas {#removed-features}

En esta sección se enumeran las funciones que se han eliminado de AEM con Experience Manager as a Cloud Service.

| Área | Función | Reemplazo |
| ------------ | ------------------ | ----------- |
| IU | Aunque algunos cuadros de diálogo de la interfaz de usuario clásica permanecen por el momento en algunas funciones concretas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de Cloud Service, el acceso a la IU clásica en general se ha eliminado en la interfaz de usuario del producto de AEM. | IU estándar |
| Dynamic Media | Las integraciones anteriores con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) y [modo híbrido de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) no están disponibles en AEM como Cloud Service. | Utilice [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) proporcionados con Experience Manager as a Cloud Service. |
| Sites | Portal Director y componentes Portlet | Estas funciones quedaron obsoletas en AEM 6.4 y ahora se han eliminado de AEM. |
| Sitios | Importador de diseños | Esta capacidad se ha eliminado porque no se puede acceder a las secciones inmutables del repositorio de AEM durante la ejecución. |
| Recursos | [El uso compartido de AEM Assets con el servicio principal de Experience Cloud Assets y Creative Cloud Services](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) no está disponible. | Para la integración con Creative Cloud, utilice [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html). |
