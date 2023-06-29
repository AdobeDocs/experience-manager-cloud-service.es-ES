---
title: Notas de la versión 2021.1.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2021.1.0."
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 25%

---


# Notas de la versión para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] La versión as a Cloud Service 2021.1.0 es el 3 de febrero de 2021.
La de la siguiente versión (2021.2.0) será el 25 de febrero de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md)**: Añada la capacidad de añadir/actualizar y eliminar variaciones de fragmentos de contenido mediante la API HTTP.

* **[API de GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)**: capacidad para consultar fragmentos de contenido utilizando sintaxis de GraphQL y esquemas basados en modelos de fragmentos de contenido para su salida en formato JSON.

* **[Compatibilidad de autenticación para solicitudes de API de GraphQL](/help/headless/security/authentication.md)**: Capacidad para autenticar solicitudes de API de GraphQL con tokens de acceso para API del lado del servidor.

* Salida JSON mejorada con la API de GraphQL, incluida la capacidad de generar texto enriquecido en formato JSON y configuraciones regionales.

* Compatibilidad con la anidación de modelos de fragmentos de contenido para permitir la creación de estructuras de fragmentos de contenido anidadas mediante tipos de datos de referencia de fragmentos de contenido dedicados o referencias de fragmentos de contenido en línea en campos de texto multilínea.

* Reglas de validación adicionales disponibles en los tipos de datos del modelo de fragmentos de contenido, incluidos &quot;único&quot;, &quot;obligatorio&quot; y &quot;traducible&quot;.

* Capacidad de etiquetar modelos de fragmentos de contenido y permitir la creación de fragmentos de contenido en una carpeta con directivas por etiquetas o rutas.

* Mejoras en la usabilidad del editor de fragmentos de contenido, incluida la acción de publicación y la visualización del modelo en el que se basa un fragmento.

* Capacidad de previsualización de salida de JSON directamente en el editor de fragmentos de contenido.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a [!DNL Cloud Service] amplía la funcionalidad Etiquetas inteligentes para admitir la identificación de palabras clave y entidades en recursos basados en texto. El texto se identifica, se indexa y se publica en forma de metadatos para mejorar la experiencia de búsqueda sin necesidad de ninguna configuración. Consulte [Etiquetas inteligentes](/help/assets/smart-tags.md).

* Ahora se admite el formato de archivo MXF. Consulte [formatos de archivo compatibles](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Product Experience Management: nueva pestaña de propiedades Comercio, para Recursos y Fragmentos de experiencias. Esta pestaña le permite vincular productos/categorías a Recursos y Fragmentos de experiencias. La pestaña también muestra datos en tiempo real de productos o categorías vinculados, y un vínculo para mostrar detalles en la consola de productos.

* Lanzamiento del sitio de referencia de CIF Venia el 2 de febrero de 2021, que incluye la versión más reciente de los componentes principales de CIF v1.7.0. Consulte [Sitio de referencia de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obtener más información.

* Componentes principales de CIF v1.7.0. Consulte [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de lanzamiento {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.1.0 es el 14 de enero de 2021.

### Correcciones de errores {#bug-fixes-cloud-manager}

* En ocasiones, la instancia de producción de recursos puede mostrar el estado de Brand Portal en la página de detalles **Entornos** como *Pendiente* y no permite al usuario realizar ninguna acción.

* Al activar una deshibernación desde Cloud Manager, a veces se mostraba un mensaje de error incluso cuando la deshibernación se iniciaba correctamente.

* Se han solucionado casos raros de fallos en la creación o eliminación de entornos.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. AEM La versión más reciente de este complemento incluye correcciones de errores para el Conversor de Dispatcher de y el Modernizador de repositorios, y también admite una nueva utilidad: Convertidor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

* AEM Index Converter es una utilidad que se puede utilizar para transformar las definiciones de índice OAK personalizadas de un cliente para que sean compatibles con las definiciones de índice OAK as a Cloud Service. Consulte [Conversor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más información.

* Nueva función añadida a [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para contener todas las configuraciones de OSGi.

### Correcciones de errores {#crt-bug-fixes}

* AEM Se han realizado varias correcciones de errores en las herramientas Conversor de Dispatcher y Modernizador de repositorios de la aplicación de manera. Consulte [AEM Conversor de Dispatcher de](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM Base as a Cloud Service {#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* AEM Llamadas de API autenticadas de servidor a servidor: genere los tokens de acceso adecuados para realizar llamadas de API de servidor a servidor autenticadas entre sus aplicaciones externas y entornos as a Cloud Service de la. Obtenga más información leyendo [la documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consultando al [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### Analizadores de creación de SDK {#sdk-build-analyzers}

El complemento Maven de AEM as a Cloud Service SDK Build Analyzer detecta problemas en un proyecto maven, incluidas las dependencias que faltan. Proporciona a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en entornos de nube con Cloud Manager.

Se han añadido dos nuevos analizadores para esta versión:

* repoinit analyzer
* paquete-códigonativo

Para obtener más información, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing).

## Herramientas de Transición de nube {#code-transition-tools}

### Fecha de lanzamiento {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido versión 1.2.2 es el 01 de febrero de 2021.

### Novedades de [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nueva capacidad e IU agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=es) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los elementos secundarios.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.
