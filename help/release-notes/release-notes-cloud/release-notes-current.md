---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: 135fe0d4172af12f091268e9ffc45295e6645fd7
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 4%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las Notas de revisión generales para [!DNL Experience Manager] como Cloud Service.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2021.1.0 es el 3 de febrero de 2021.
La siguiente versión (2021.2.0) será el 25 de febrero de 2021.

## [!DNL Adobe Experience Manager Sites] como Cloud Service  {#sites}

### Administración de contenido sin encabezado {#headless}

* **[Envío](/help/assets/content-fragments/graphql-api-content-fragments.md)** de la API de GraphQL para fragmentos de contenido: Capacidad de consulta de fragmentos de contenido mediante la sintaxis de GraphQL y esquemas basados en modelos de fragmentos de contenido para su salida en formato JSON.

* **[Compatibilidad de autenticación para solicitudes](/help/assets/content-fragments/graphql-authentication-content-fragments.md)** de API de GraphQL: Capacidad para autenticar solicitudes de API de GraphQL con tokenes de acceso para API de servidor.

* **[Componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: Se añadió la compatibilidad con la visualización y edición de SPA externos en AEM uso.

* **[Edición de un SPA externo en AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Se ha añadido la capacidad de cargar una aplicación independiente de una sola página en una instancia de AEM, añadir secciones de contenido editables y activar la creación.

* Salida JSON mejorada de la API de GraphQL, incluida la capacidad de generar texto enriquecido en formato JSON y configuraciones regionales.

* Compatibilidad con la anidación de modelos de fragmento de contenido para permitir la creación de estructuras de fragmento de contenido anidadas mediante tipos de datos de referencia de fragmento de contenido dedicados o referencias de fragmento de contenido en línea en campos de texto multilínea.

* Hay reglas de validación adicionales disponibles en los tipos de datos del modelo de fragmento de contenido, incluidos &quot;único&quot;, &quot;obligatorio&quot; y &quot;traducible&quot;.

* Posibilidad de etiquetar modelos de fragmento de contenido y permitir la creación de fragmentos de contenido en una carpeta con directivas por etiquetas o rutas.

* Mejoras de uso en el editor de fragmentos de contenido, incluida la acción de publicación y la visualización del modelo en el que se basa un fragmento.

* Posibilidad de previsualización de salida JSON directamente en el editor de fragmentos de contenido.

### Aplicaciones Web progresivas (PWA) {#pwa}

* [Una versión de aplicación web progresiva (PWA) de un ](/help/sites-cloud/authoring/features/enable-pwa.md)  sitecan ahora se habilita en el nivel de proyecto mediante una configuración simple.

## [!DNL Adobe Experience Manager Assets] como un  [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] como  [!DNL Cloud Service] amplía la funcionalidad Etiquetas inteligentes para admitir la identificación de palabras clave y entidades en recursos basados en texto. El texto se identifica, se indexa y se pone a disposición como metadatos para mejorar la experiencia de búsqueda sin necesidad de ninguna configuración. Consulte [Etiquetas inteligentes](/help/assets/smart-tags.md).

* Ahora se admite el formato de archivo MXF. Consulte [formatos de archivo admitidos](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Administración de experiencia del producto: Nueva ficha de propiedades &quot;Comercio&quot; para Recursos y Fragmentos de experiencia. Esta ficha le permite vincular productos/categorías a Recursos y Fragmentos de experiencia. La ficha también muestra datos en tiempo real de productos o categorías vinculados y un vínculo para mostrar detalles en la consola de productos.

* Sitio de referencia de CIF Venia publicado - 2021.02.02 que incluye la versión más reciente de componentes principales de CIF v1.7.0. Consulte [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) para obtener más detalles.

* Componentes principales de CIF v1.7.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) para obtener más detalles.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2021.1.0 es el 14 de enero de 2021.

### Corrección de errores {#bug-fixes-cloud-manager}

* En ocasiones, la instancia de Producción de recursos puede mostrar el estado de Brand Portal en la página de detalles **Entornos** como *Pendiente* sin permitir al usuario realizar ninguna acción.

* Al activar una deshibernación desde Cloud Manager, a veces se mostraba un mensaje de error incluso cuando la deshibernación se iniciaba correctamente.

* Se han abordado casos raros de fallo en la creación o eliminación de entornos.

## AEM como Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* Llamadas de API autenticadas de servidor a servidor: genere los tokenes de acceso adecuados para realizar llamadas de API autenticadas de servidor a servidor entre sus aplicaciones externas y AEM como entornos de Cloud Service. Obtenga más información leyendo [la documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consultando el [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK Build Analyzers {#sdk-build-analyzers}

El AEM como Cloud Service SDK Build Analyzer Maven Plugin detecta problemas en un proyecto determinado, incluyendo dependencias que faltan. Ofrece a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en Cloud entornos con Cloud Manager.

Se han agregado dos nuevos analizadores para esta versión:

* analizador de informes
* bundle-nativecode

Para obtener más información, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Herramientas de Transición de nube {#code-transition-tools}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades en [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los elementos secundarios.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.
