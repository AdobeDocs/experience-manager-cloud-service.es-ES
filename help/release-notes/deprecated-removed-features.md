---
title: Funciones obsoletas y eliminadas
description: Notas de la versión específicas de funciones obsoletas y eliminadas de Adobe Experience Manager como servicio de nube.
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Deprecated and removed features {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades del producto para reinventar o reemplazar con el tiempo las funciones antiguas con alternativas más modernas a fin de mejorar el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores. Además, como Adobe Experience Manager como servicio de nube proporciona un modelo de implementación nativo de la nube, ciertas funciones y características fueron reemplazadas por homólogos nativos de la nube.

Para comunicar la eliminación o el reemplazo inminente de las capacidades de AEM, se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Las funciones obsoletas siguen estando disponibles, pero no se mejoran aún más.
1. Las funciones anunciadas como obsoletas se eliminan en la siguiente versión principal, como muy pronto. Se anuncia la fecha límite real para la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Deprecated features {#deprecated-features}

Esta sección enumera las funciones y funciones que se han marcado como obsoletas en Experience Manager como servicio de nube. Normalmente, las funciones que se planea eliminar en una versión futura se establecen en primer lugar como obsoletas, con una alternativa proporcionada.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Función | Reemplazo |
| ------------ | ------------------ | ----------- |
| Recursos | La ingesta y el procesamiento de recursos ya no utilizan el flujo de trabajo `DAM Asset Update` | La ingestión de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos ahora. |
| Recursos | Carga de recursos directamente en AEM. Consulte API de carga de recursos [obsoletas](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [La carga](/help/assets/add-assets.md) binaria directa se utiliza en Experience Manager como un servicio de nube. Para obtener más información técnica, consulte API de carga [directa](/help/assets/developer-reference-material-apis.md#overview-binary-upload). |
| Recursos | [No se admiten determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) de flujo de trabajo en el `DAM Asset Update` flujo de trabajo, incluida la llamada a herramientas de línea de comandos como ImageMagick | [Los microservicios](/help/assets/asset-microservices-overview.md) de recursos sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice flujos de trabajo [](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)posteriores al procesamiento. |

## Removed features {#removed-features}

En esta sección se enumeran las funciones y capacidades que se han eliminado de AEM con Experience Manager como servicio de nube.

| Área | Función | Reemplazo |
| ------------ | ------------------ | ----------- |
| IU | Aunque algunos cuadros de diálogo de la IU clásica permanecen por el momento en algunas funciones seleccionadas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de servicio de nube, el acceso a la IU clásica en general se ha eliminado en la interfaz de usuario del producto de AEM. | IU estándar |
| Dynamic Media | Las integraciones anteriores con [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) y el modo [híbrido de medios](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) dinámicos no están disponibles en AEM como servicio de nube. | Utilice los medios [dinámicos](/help/assets/dynamic-media/dynamic-media.md) proporcionados con Experience Manager como un servicio de nube. |
| Sitios | Director de portal y componente de portlet | Estas funciones quedaron obsoletas en AEM 6.4 y ahora se han eliminado de AEM. |
| Sitios | Importador de diseños | Esta capacidad se ha eliminado porque no se puede acceder a las secciones inmutables del repositorio de AEM durante la ejecución. |
| Recursos | [El uso compartido de AEM Assets con el servicio principal de Marketing Cloud Assets y los servicios](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) de Creative Cloud no está disponible. | Para la integración con Creative Cloud, utilice [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). |
