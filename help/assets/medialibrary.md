---
title: Uso de Media Library para la administración básica de recursos digitales
description: "[!DNL Experience Manager Assets] y Media Library para la administración de recursos."
contentOwner: AG
feature: Asset Management, Publishing
role: User, Architect, Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 9%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Uso de Media Library para la administración básica de recursos {#manage-assets-using-media-library}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

La plataforma [!DNL Adobe Experience Manager] proporciona diferentes capacidades para administrar recursos. Media Library permite a los usuarios cargar un pequeño número de recursos en el repositorio, buscarlos y utilizarlos en las páginas web y realizar tareas sencillas de administración de recursos en los recursos.

Media Library es una solución ligera de administración de activos digitales (DAM) que se suministra de forma gratuita con la licencia [!DNL Adobe Experience Manager Sites]. [!DNL Sites] es una oferta de Administración de contenido web (WCM). Media Library funciona con todas las funcionalidades de Experience Manager.

La licencia [!DNL Adobe Experience Manager Assets] está disponible por separado para su compra. [!DNL Experience Manager Assets] permite una administración sólida de los recursos a través de casos de uso empresariales, personalizaciones de metadatos, esquemas, búsquedas e interfaz de usuario, y muchas otras características además de lo que proporciona Media Library.

## Requisitos de licencia {#avail-media-library-license}

Los clientes que tengan la licencia [!DNL Sites] tienen derecho a usar Media Library. Funciona con todos los componentes de [!DNL Experience Manager].

Media Library se instala como parte de Sites. No se requiere ninguna licencia o paquete adicional más allá de la licencia e instalación de Sites.

## [!DNL Assets] frente a Media Library {#assets-and-media-library}

Experience Manager Assets proporciona funcionalidad DAM de nivel empresarial. La funcionalidad de Assets se entrega con [!DNL Experience Manager] en un solo paquete. Sin embargo, los usuarios que no hayan adquirido una licencia de Assets no tienen derecho a utilizar las funciones avanzadas de DAM. Sin la licencia de Assets, solo están disponibles [las características de Media Library](#use-media-library).

Si desea evitar el uso no intencionado de las características de [!DNL Assets] para las que no tiene licencia, quite todos los flujos de trabajo, componentes, taxonomías, opciones y el administrador de [!DNL Assets] de [!DNL Experience Manager], que son específicos de [!DNL Assets]. Al hacerlo, se evita que los usuarios usen accidentalmente características de [!DNL Assets] para las que no se obtuvo licencia.

## Uso de Media Library {#use-media-library}

Media Library cubre ampliamente los siguientes casos de uso:

* Proporcionar características básicas de DAM para las páginas web creadas con [!DNL Adobe Experience Manager Sites].
* Formularios adaptables y comunicaciones creadas con [!DNL Adobe Experience Manager Forms].
* Experiencias de pantalla digital creadas con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API de REST HTTP para operaciones sin encabezado.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Para usar la funcionalidad Media Library, puede usar la interfaz de usuario predeterminada [!DNL Experience Manager]. Media Library forma parte de la instalación de [!DNL Experience Manager Sites] y no se requiere ninguna interfaz o complemento independiente. Con la interfaz existente, los usuarios de Media Library tienen derecho a realizar las siguientes tareas:

* Cree carpetas para organizar los recursos.
* Cargar recursos.
* Recursos de Publish.
* Editar, mover y copiar recursos.
* Examinar, filtrar y buscar (incluye la búsqueda por similitudes) recursos.
* Agregue valores y edite los valores de los campos de metadatos, excepto Etiquetas inteligentes, que están disponibles en la ficha [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso de forma predeterminada.
* Agregar y eliminar representaciones estáticas.
* Descargar carpetas, recursos y representaciones de recursos.
* Crear versiones de recursos.
* Cree y realice tareas de revisión en los recursos.
* Anotar recursos.
* Agregar recursos a [!DNL Sites] páginas mediante el buscador de contenido.
* Usar [!DNL Content Fragments].
* Use las API HTTP REST y GraphQL para [!DNL Content Fragments] y los recursos de medios a los que se hace referencia en la licencia de Sites.
* Integración de Marketing Cloud.
* Personalice y amplíe la interfaz de usuario de administración de recursos.
* Acceda al Generador de consultas (API) para ampliar la funcionalidad de búsqueda.
* Crear etiquetas estáticas.
* Crear proyectos y tareas.
* Flujo de actividad (cronología).
* Comentarios y anotaciones.

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>Muchos casos de uso de DAM avanzados los ha completado [!DNL Experience Manager Assets]. La licencia de Media Library le da derecho a realizar únicamente los casos de uso enumerados mediante Media Library. Si un caso de uso no aparece en la lista, no lo utilice con la licencia de Media Library. Si tiene alguna duda, póngase en contacto con Atención al cliente.

No puede usar etiquetas inteligentes, vínculo [!DNL Asset], selector [!DNL Asset], etiquetado masivo, modificar flujos de trabajo de recursos ni interfaz de usuario estándar [!DNL Adobe Experience Manager] para acceder a Media Library sin la licencia [!DNL Assets].

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Funciones DAM en [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=es)
>* [[!DNL Experience Manager] como [!DNL Cloud Service] descripción del producto](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)
