---
title: Funciones en desuso y eliminadas
description: Notas de la versión específicas de las funciones en desuso y eliminadas de [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: d55e2aec4718e752cfc0dfa610abf1a1d36a583f
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 34%

---

# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funciones obsoletas y eliminadas en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service tiene un modelo de implementación nativo de la nube. Algunas funciones y características han sido reemplazadas por homólogos nativos de la nube y esta pestaña muestra esas funciones."


Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores. También, como [!DNL Adobe Experience Manager] como [!DNL Cloud Service] proporciona un modelo de implementación nativo de la nube, ciertas funcionalidades y características fueron reemplazadas por homólogos nativos de la nube.

Comunicar la próxima eliminación/sustitución de [!DNL Experience Manager] , se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Las funciones obsoletas siguen estando disponibles, pero no se siguen mejorando.
1. Las funciones anunciadas como obsoletas se eliminan en la siguiente versión principal, como pronto. Se anuncia la auténtica fecha límite para la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección enumera las funciones y capacidades que se han marcado como obsoletas en [!DNL Experience Manager] como [!DNL Cloud Service]. Normalmente, las funciones que se eliminarán en una versión futura se establecen primero como obsoletas, y se proporciona una alternativa.

Se aconseja a los clientes que comprueben si utilizan la función o la capacidad en su implementación actual y que cambien su implementación para utilizar la alternativa proporcionada.

| Capacidades | Función en desuso | Reemplazo |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Propiedades de fragmentos de experiencias para **Estado de los medios sociales**. | La función se eliminará próximamente. |
| [!DNL Sites] | Fragmentos de contenido simples basados en plantillas. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. |
| [!DNL Assets] | `DAM Asset Update` flujo de trabajo para procesar imágenes grabadas. | Ahora, el consumo de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos. |
| [!DNL Assets] | Cargar recursos directamente a [!DNL Experience Manager]. Consulte [API de carga de recursos obsoletas](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilice la [carga binaria directa](/help/assets/add-assets.md). Para obtener más información técnica, consulte [API de carga directa](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | No se admiten [determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) en el flujo de trabajo `DAM Asset Update`, incluida la llamada a herramientas de línea de comandos como [!DNL ImageMagick]. | [Los microservicios de recursos](/help/assets/asset-microservices-overview.md) sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Fmpeg transcodificar vídeos. | Para la generación de miniaturas de FFmpeg, use los [microservicios de Asset](/help/assets/asset-microservices-overview.md). Para la transcodificación FFmpeg, utilice [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interfaz de usuario de replicación de árbol en la pestaña &quot;Distribuir&quot; del agente de replicación (eliminación después del 30 de septiembre de 2021) | [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) enfoques |

## Funciones eliminadas {#removed-features}

Esta sección enumera las funciones y capacidades que se han eliminado de [!DNL Experience Manager] con [!DNL Experience Manager] como [!DNL Cloud Service].

| Área | Función | Reemplazo | Fecha de eliminación del objetivo |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaz de usuario | La IU clásica se elimina de la interfaz de usuario del producto. Hay algunos cuadros de diálogo de IU clásica disponibles para algunas funciones seleccionadas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de Cloud Service. Próximos [actualizaciones de productos](/help/release-notes/home.md) puede eliminar aún más la disponibilidad de la IU clásica. | IU estándar | Eliminado |
| [!DNL Dynamic Media] | Integraciones anteriores con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) y [Modo híbrido de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) no están disponibles en [!DNL Experience Manager] como [!DNL Cloud Service]. | Uso [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) provisto de [!DNL Experience Manager] como [!DNL Cloud Service]. | Eliminado |
| [!DNL Sites] | Portal Director y componentes Portlet | Estas funciones quedaron obsoletas en [!DNL Experience Manager] 6.4 y se han eliminado de [!DNL Experience Manager]. | Eliminado |
| [!DNL Sites] | Importador de diseños | Esta funcionalidad se ha eliminado como secciones inmutables del [!DNL Experience Manager] no se puede acceder al repositorio durante la ejecución. | Eliminado |
| [!DNL Assets] | [!DNL Assets]El uso compartido de con el servicio principal de Experience Cloud Assets y Creative Cloud Services no está disponible. | Para la integración con [!DNL Adobe Creative Cloud], use [Vínculo de recurso de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html). | Eliminado |
| [!DNL Foundation] | Compatibilidad con fuentes de datos de Apache Sling (paquete OSGi org.apache.sling.datasource) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con plantillas de secuencias de comandos JST (paquete OSGi org.apache.sling.scripting.jst) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con la pizarra Apache Felix Http | Pizarra HTTP OSGi | Marzo de 2022 |

## API de Java {#java-api}

Consulte [esta página](/help/release-notes/deprecated-apis.md) para cualquier API de Java obsoleta o eliminada, que se introduzcan ocasionalmente.

## Configuración OSGI {#osgi-configuration}

Consulte [este artículo](/help/implementing/deploying/osgi-configuration-api.md) para cualquier restricción en torno a la configuración de las propiedades OSGI, algunas de las cuales pueden introducirse a lo largo del tiempo.
