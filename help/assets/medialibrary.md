---
title: Uso de la biblioteca de medios para la administración básica de recursos digitales
description: '[!DNL Experience Manager Assets] y la biblioteca de medios para la administración de recursos.'
contentOwner: AG
feature: Asset Management, Publishing
role: User, Developer, Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 9%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# Usar la biblioteca de medios para la administración básica de recursos {#manage-assets-using-media-library}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

La plataforma [!DNL Adobe Experience Manager] proporciona diferentes capacidades para administrar recursos. La biblioteca de medios permite a los usuarios cargar un pequeño número de recursos en el repositorio, buscarlos y utilizarlos en las páginas web y realizar tareas sencillas de administración de recursos en los recursos.

La biblioteca multimedia es una solución ligera de administración de activos digitales (DAM) que se suministra de forma gratuita con la licencia [!DNL Adobe Experience Manager Sites]. [!DNL Sites] es una oferta de Administración de contenido web (WCM). La biblioteca de medios funciona con todas las funciones de Experience Manager.

La licencia [!DNL Adobe Experience Manager Assets] está disponible por separado para su compra. [!DNL Experience Manager Assets] permite una administración sólida de los recursos mediante casos de uso empresarial, personalizaciones de metadatos, esquemas, búsquedas e interfaz de usuario, y muchas otras características además de lo que proporciona la Biblioteca de medios.

## Requisitos de licencia {#avail-media-library-license}

Los clientes que tengan la licencia [!DNL Sites] tienen derecho a usar la Biblioteca de medios. Funciona con todos los componentes de [!DNL Experience Manager].

La biblioteca de medios se instala como parte de Sites. No se requiere ninguna licencia o paquete adicional más allá de la licencia e instalación de Sites.

## [!DNL Assets] frente a Biblioteca de medios {#assets-and-media-library}

Experience Manager Assets proporciona funcionalidad DAM de nivel empresarial. La funcionalidad de Assets se entrega con [!DNL Experience Manager] en un solo paquete. Sin embargo, los usuarios que no hayan adquirido una licencia de Assets no tienen derecho a utilizar las funciones avanzadas de DAM. Sin la licencia de Assets, solo están disponibles [las características de la biblioteca multimedia](#use-media-library).

Si desea evitar el uso no intencionado de las características de [!DNL Assets] para las que no tiene licencia, quite todos los flujos de trabajo, componentes, taxonomías, opciones y el administrador de [!DNL Assets] de [!DNL Assets], que son específicos de [!DNL Experience Manager]. Al hacerlo, se evita que los usuarios usen accidentalmente características de [!DNL Assets] para las que no se obtuvo licencia.

## Usar la biblioteca de medios {#use-media-library}

La biblioteca de medios abarca, en términos generales, los siguientes casos de uso:

* Proporcionar características básicas de DAM para las páginas web creadas con [!DNL Adobe Experience Manager Sites].
* Formularios adaptables y comunicaciones creadas con [!DNL Adobe Experience Manager Forms].
* Experiencias de pantalla digital creadas con [!DNL Adobe Experience Manager Screens].
* [!DNL Assets] API de REST HTTP para operaciones sin encabezado.

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

Para usar la funcionalidad Biblioteca de medios, puede usar la interfaz de usuario predeterminada [!DNL Experience Manager]. La biblioteca multimedia forma parte de la instalación de [!DNL Experience Manager Sites] y no se requiere ninguna interfaz o complemento independiente. Con la interfaz existente, los usuarios de la biblioteca de medios pueden realizar las siguientes tareas:

* Cree carpetas para organizar los recursos.
* Cargar recursos.
* Publicar recursos.
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
>Muchos casos de uso de DAM avanzados los ha completado [!DNL Experience Manager Assets]. La licencia de Biblioteca de medios le da derecho a cumplir solo los casos de uso enumerados mediante Biblioteca de medios. Si un caso de uso no aparece en la lista, no lo utilice con una licencia de Media Library. Si tiene alguna duda, póngase en contacto con Atención al cliente.

No puede usar etiquetas inteligentes, vínculo [!DNL Asset], selector [!DNL Asset], etiquetado masivo, modificar flujos de trabajo de recursos ni interfaz de usuario estándar [!DNL Adobe Experience Manager] para acceder a la biblioteca multimedia sin la licencia [!DNL Assets].

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
