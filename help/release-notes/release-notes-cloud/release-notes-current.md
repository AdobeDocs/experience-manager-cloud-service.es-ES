---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: 77d0ae925ed3837c70e58c110b6c8360790b6aee
workflow-type: tm+mt
source-wordcount: '1103'
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

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

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

La fecha de versión de Cloud Manager en AEM como Cloud Service 2021.2.0 es el 11 de febrero de 2021.

### Novedades {#what-is-new-cloud-manager}


* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar la instancia de Brand Portal de forma automática mediante la interfaz de usuario de Cloud Manager. Para un programa normal (sin simulación de pruebas) con la solución Assets, Brand Portal ahora se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El arquetipo del proyecto AEM utilizado en la creación de proyectos y Simuladores para pruebas se ha actualizado a la versión 25.

* La lista de las API obsoletas identificadas durante el análisis de código se ha refinado para incluir clases y métodos adicionales que ya no se utilizan en las últimas versiones del SDK de Cloud Service.

* SonarQube perfil para Cloud Manager actualizado para eliminar Sonar rule squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de interrupción del subproceso.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda agregar o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está esperando el paso de aprobación.

* Las propiedades configuradas en los archivos `pom.xml` del cliente con el prefijo sonar ahora se eliminarán dinámicamente para evitar errores de compilación y de análisis de calidad.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda seleccionar temporalmente un certificado SSL si está siendo utilizado por un nombre de dominio que se está implementando actualmente.

* Se han agregado reglas de calidad de código adicionales para cubrir los problemas de compatibilidad con Cloud Service.

### Corrección de errores {#bug-fixes-cloud-manager}

* El certificado SSL que coincide con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario del Administrador de nube ahora informará al usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error adecuado.

* La interfaz de usuario del Administrador de nube informará al usuario que no pueda seleccionar temporalmente un certificado SSL si está siendo utilizado por un nombre de dominio que se está implementando actualmente.

* En algunos casos, un problema interno puede hacer que la eliminación de entornos se quede atascada.

* Algunos errores de canalización se notificaron incorrectamente como errores de canalización.

## AEM como Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* Llamadas de API autenticadas de servidor a servidor: genere los tokenes de acceso adecuados para realizar llamadas de API autenticadas de servidor a servidor entre sus aplicaciones externas y AEM como entornos de Cloud Service. Obtenga más información leyendo [la documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consultando el [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK Build Analyzers {#sdk-build-analyzers}

El AEM como Cloud Service SDK Build Analyzer Maven Plugin detecta problemas en un proyecto determinado, incluyendo dependencias que faltan. Ofrece a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en Cloud entornos con Cloud Manager.

Se han agregado dos nuevos analizadores para esta versión:

* analizador de informes
* bundle-nativecode

Para obtener más información, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.2.4 es el 10 de febrero de 2021.

### Corrección de errores {#bug-fixes-ctt}

* Al asignar varios usuarios, los ID de IMS de algunos usuarios se asignaban incorrectamente. Esto se ha solucionado.

### Fecha de la versión {#release-date-ctt-feb}

La fecha de versión de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades de Content Transfer Tool {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido.
Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los elementos secundarios.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.

## Analizador de optimizaciones {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.0 es el 11 de febrero de 2021.

### Novedades de Best Practices Analyzer {#what-is-new-bpa}

* Capacidad para detectar el uso de la implementación de AEM Forms y AEM Forms e indicar las áreas relevantes para migrar a AEM Forms como Cloud Service.
* Capacidad para detectar y crear informes sobre el uso y el recuento de componentes y plantillas personalizados.
* Capacidad para detectar el tipo de almacén de nodos y almacén de datos utilizado.
* Capacidad para detectar el uso de Dynamic Media.
* Capacidad para detectar la versión de Java utilizada.







