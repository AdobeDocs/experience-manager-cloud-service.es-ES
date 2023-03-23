---
title: Funciones en desuso y eliminadas
description: Notas de versión específicas de las funciones en desuso y eliminadas de  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 459e6cbf91f9b7f995bd1fd9c8758962c41c9341
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 98%

---

# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funciones en desuso y eliminadas en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service tiene un modelo de implementación nativo de la nube. Algunas funciones y características se han reemplazado con homólogos nativos de la nube y esta pestaña muestra esas funciones."


Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores. Además, como [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] proporciona un modelo de implementación nativo de la nube, ciertas funciones y características se han reemplazado con homólogos nativos de la nube.

Para comunicar la eliminación o el reemplazo inminente de las capacidades de [!DNL Experience Manager], se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Las funciones en desuso siguen estando disponibles, pero no se siguen actualizando.
1. Las funciones anunciadas como obsoletas se eliminan en la siguiente versión principal, como pronto. Se anuncia la auténtica fecha límite para la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección enumera las funciones que se han marcado como en desuso en [!DNL Experience Manager] as a [!DNL Cloud Service]. Normalmente, las funciones que se quieren eliminar en una versión futura se establecen en primer lugar como en desuso, con una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Capacidades | Función en desuso | Reemplazo |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. | La función se eliminará próximamente. |
| [!DNL Sites] | Fragmentos de contenido simples basados en plantillas. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. |
| [!DNL Assets] | `DAM Asset Update` flujo de trabajo para procesar imágenes grabadas. | Ahora, el consumo de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos. |
| [!DNL Assets] | Cargue los recursos directamente en [!DNL Experience Manager]. Consulte [API de carga de recursos en desuso](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilice la [carga binaria directa](/help/assets/add-assets.md). Para obtener más información técnica, consulte [API de carga directa](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | No se admiten [determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) en el flujo de trabajo `DAM Asset Update`, incluida la llamada a herramientas de línea de comandos como [!DNL ImageMagick]. | [Los microservicios de recursos](/help/assets/asset-microservices-overview.md) sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | FFmpeg transcodificar vídeos. | Para la generación de miniaturas de FFmpeg, use los [microservicios de Asset](/help/assets/asset-microservices-overview.md). Para la transcodificación FFmpeg, utilice [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | IU de replicación de árbol en la pestaña Distribuir del agente de replicación (eliminación después del 30 de septiembre de 2021) | Enfoques [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Ni la pestaña Distribuir de la pantalla del administrador del agente de replicación ni la API de replicación pueden utilizarse para replicar paquetes de contenido de más de 10 MB (aplicación después del 12 de septiembre de 2022) | Enfoques [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) |


| [!DNL Foundation] | Ni la pestaña Distribuir de la pantalla del administrador del agente de replicación ni la API de replicación pueden utilizarse para replicar paquetes de contenido de más de 10 MB. En su lugar, utilice [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) |

## Funciones eliminadas {#removed-features}

En esta sección se enumeran las funciones que se han eliminado de [!DNL Experience Manager] con [!DNL Experience Manager] as a [!DNL Cloud Service].

| Área | Función | Reemplazo | Fecha de eliminación objetivo |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaz de usuario | La IU clásica se elimina de la interfaz de usuario del producto. Hay algunos cuadros de diálogo de IU clásica disponibles para algunas funciones seleccionadas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de Cloud Service. Próximas [actualizaciones de productos](/help/release-notes/home.md) pueden eliminar aún más la disponibilidad de la IU clásica. | IU estándar | Eliminado |
| [!DNL Dynamic Media] | Las integraciones anteriores con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=es#integration) y el [modo híbrido de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=es#dynamic) no están disponibles en [!DNL Experience Manager] as a [!DNL Cloud Service]. | Utilice [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) proporcionado con [!DNL Experience Manager] as a [!DNL Cloud Service]. | Eliminado |
| [!DNL Sites] | Portal Director y componentes Portlet | Estas funciones quedaron obsoletas en [!DNL Experience Manager] 6.4 y ahora se han eliminado de [!DNL Experience Manager]. | Eliminado |
| [!DNL Sites] | Importador de diseños | Esta capacidad se ha eliminado porque no se puede acceder a las secciones inmutables del repositorio de [!DNL Experience Manager] durante la ejecución. | Eliminado |
| [!DNL Assets] | El uso compartido de [!DNL Assets] con el servicio principal de Experience Cloud Assets y Creative Cloud Services no está disponible. | Para la integración con [!DNL Adobe Creative Cloud], utilice [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html). | Eliminado |
| [!DNL Foundation] | Compatibilidad con fuentes de datos de Apache Sling (paquete OSGi org.apache.sling.datasource) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con plantillas de scripts JST (paquete OSGi org.apache.sling.scripting.jst) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con la pizarra Apache Felix Http | Pizarra Http OSGi | Marzo de 2022 |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de Adobe IMS | Marzo de 2023 |


## API de Java {#java-api}

Consulte [esta página](/help/release-notes/deprecated-apis.md) para cualquier API de Java en desuso o eliminada, que se introducen ocasionalmente.

## Configuración OSGi {#osgi-configuration}

Consulte [este artículo](/help/implementing/deploying/osgi-configuration-api.md) para cualquier restricción en torno a la configuración de las propiedades OSGi, algunas de las cuales pueden introducirse a lo largo del tiempo.
