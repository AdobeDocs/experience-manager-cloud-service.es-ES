---
title: Notas de la versión 2021.1.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2021.1.0."'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 7%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] El as a Cloud Service 2021.1.0 es el 3 de febrero de 2021.
La siguiente versión (2021.2.0) será el 25 de febrero de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP del fragmento de contenido](/help/assets/content-fragments/assets-api-content-fragments.md)**: Agregue la capacidad de agregar, actualizar y eliminar variaciones de fragmento de contenido mediante la API HTTP.

* **[API de GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)**: Capacidad para consultar fragmentos de contenido mediante la sintaxis de GraphQL y esquemas basados en modelos de fragmento de contenido para obtener resultados en formato JSON.

* **[Compatibilidad con autenticación para solicitudes de API de GraphQL](/help/headless/security/authentication.md)**: Posibilidad de autenticar solicitudes de API de GraphQL con tokens de acceso para API del lado del servidor.

* Se ha mejorado la salida JSON de la API de GraphQL, incluida la capacidad de generar texto enriquecido en formato JSON y configuraciones regionales.

* Compatibilidad para anidar modelos de fragmento de contenido para permitir la creación de estructuras de fragmento de contenido anidadas, a través de tipos de datos de referencia de fragmento de contenido o referencias de fragmento de contenido en línea en campos de texto multilínea.

* Reglas de validación adicionales disponibles en los tipos de datos del modelo de fragmento de contenido, incluidos &quot;únicos&quot;, &quot;obligatorios&quot; y &quot;traducibles&quot;.

* Posibilidad de etiquetar modelos de fragmento de contenido y permitir la creación de fragmentos de contenido en una carpeta con directivas por etiquetas o rutas.

* Mejoras de uso en el editor de fragmentos de contenido, incluida la acción de publicación y la visualización del modelo en el que se basa un fragmento.

* Capacidad para previsualizar la salida JSON directamente en el editor de fragmentos de contenido.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] como [!DNL Cloud Service] amplía la funcionalidad Etiquetas inteligentes para admitir la identificación de palabras clave y entidades en recursos basados en texto. El texto se identifica, indexa y está disponible como metadatos para mejorar la experiencia de búsqueda sin necesidad de ninguna configuración. Consulte [Etiquetas inteligentes](/help/assets/smart-tags.md).

* Ahora se admite el formato de archivo MXF. Consulte [formatos de archivo compatibles](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Administración de experiencia del producto: Nueva pestaña de propiedades &quot;Comercio&quot; para Recursos y Fragmentos de experiencias. Esta pestaña le permite vincular productos y categorías a Recursos y fragmentos de experiencias. La pestaña también muestra datos en tiempo real de productos o categorías vinculados y un vínculo para mostrar detalles en la consola del producto.

* Sitio de referencia de Venia del CIF publicado - 2021.02.02 que incluye la última versión v1.7.0 de los componentes principales del CIF. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obtener más información.

* Componentes principales de CIF v1.7.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.1.0 es el 14 de enero de 2021.

### Corrección de errores {#bug-fixes-cloud-manager}

* En ocasiones, la instancia de producción de recursos puede mostrar el estado de Brand Portal en la variable **Entornos** página de detalles como *Pendiente* sin permitir al usuario realizar ninguna acción.

* Al activar una deshibernación desde Cloud Manager, a veces se mostraba un mensaje de error incluso cuando la deshibernación se iniciaba correctamente.

* Se han solucionado casos raros de fallo en la creación o eliminación de entornos.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado una nueva versión del complemento AIO-CLI. La versión más reciente de este complemento incluye correcciones de errores para el conversor AEM Dispatcher y el modernizador de repositorio, y también admite una nueva utilidad: Conversor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

* El conversor de índices es una utilidad que puede utilizarse para transformar las definiciones de índice OAK personalizadas de un cliente en AEM definiciones de índice OAK compatibles as a Cloud Service. Consulte [Conversor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más información.

* Nueva función agregada a [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para que contenga todas las configuraciones de OSGi.

### Corrección de errores {#crt-bug-fixes}

* Se han hecho varias correcciones de errores en las herramientas AEM Dispatcher Converter y Modernizador de repositorio. Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## Base as a Cloud Service AEM {#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* Llamadas de API autenticadas de servidor a servidor : genere los tokens de acceso adecuados para realizar llamadas de API autenticadas de servidor a servidor entre sus aplicaciones externas y AEM entornos as a Cloud Service. Obtenga más información leyendo [la documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consultando al [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### Analizadores de creación de SDK {#sdk-build-analyzers}

El complemento Maven de AEM as a Cloud Service SDK Build Analyzer detecta problemas en un proyecto maven, incluidas dependencias que faltan. Proporciona a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en entornos de nube con Cloud Manager.

Se han agregado dos nuevos analizadores para esta versión:

* analizador de informes
* bundle-nativcode

Para obtener más información, consulte la documentación [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing).

## Herramientas de Transición de nube {#code-transition-tools}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades de [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los niños.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.
