---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: ad80ea25abf06fd18dd781641f215e134a18a037
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 4%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las Notas de revisión generales para [!DNL Experience Manager] como Cloud Service.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2021.2.0 es el 25 de febrero de 2021.
La siguiente versión (2021.3.0) será el 25 de marzo de 2021.

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

## Novedades en [!DNL Assets] {#what-is-new-assets}

* Los recursos se pueden obtener mediante [!DNL Experience Manager Assets Brand Portal]. Ayuda a obtener recursos de los usuarios de la agencia para nuevas campañas de marketing, fotografías y proyectos.

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

## Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Cuando se crea una nueva versión de un recurso existente después de resolver el conflicto de nombres, se sobrescriben los metadatos del recurso original. (CQ-4313594)
* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta, aunque haya espacio disponible. (CQ-4314101)

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

La fecha de versión de Best Practices Analyzer v2.1.2 es el 18 de febrero de 2021.

### Novedades de Best Practices Analyzer {#what-is-new-bpa}

* Capacidad para detectar el uso de la implementación de AEM Forms y AEM Forms e indicar las áreas relevantes para migrar a AEM Forms como Cloud Service.
* Capacidad para detectar y crear informes sobre el uso y el recuento de componentes y plantillas personalizados.
* Capacidad para detectar el tipo de almacén de nodos y almacén de datos utilizado.
* Capacidad para detectar el uso de Dynamic Media.
* Capacidad para detectar la versión de Java utilizada.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. La última versión de este complemento incluye varias correcciones de errores para el Modernizador de repositorio.
Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

### Corrección de errores {#bug-fixes-crt}

* Se han realizado varias correcciones de errores en el Modernizador de repositorio.
Consulte [Recurso de GitHub: aem-cloud-service-source-Migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obtener más información.








