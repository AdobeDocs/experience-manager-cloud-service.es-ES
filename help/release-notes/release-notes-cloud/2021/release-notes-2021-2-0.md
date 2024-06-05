---
title: Notas de la versión 2021.2.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 34%

---


# Notas de la versión para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] La versión 2021.2.0 as a Cloud Service es el 25 de febrero de 2021.
La de la siguiente versión (2021.3.0) será el 25 de marzo de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Administración de contenido sin encabezado {#headless}

* **[API de GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)**: capacidad para consultar fragmentos de contenido utilizando sintaxis de GraphQL y esquemas basados en modelos de fragmentos de contenido para su salida en formato JSON.

* **[Compatibilidad de autenticación para solicitudes de API de GraphQL](/help/headless/security/authentication.md)**: Capacidad para autenticar solicitudes de API de GraphQL con tokens de acceso para API del lado del servidor.

* **[El componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)** SPA AEM : Se ha añadido compatibilidad para ver y editar externos en el uso de la.

* **[SPA AEM Edición de una externa dentro de un grupo de informes](/help/implementing/developing/hybrid/editing-external-spa.md)** AEM : Se ha añadido la capacidad de cargar una aplicación independiente de una sola página en una instancia de, añadir secciones de contenido editables y activar la función de creación.

* Salida JSON mejorada con la API de GraphQL, incluida la capacidad de generar texto enriquecido en formato JSON y configuraciones regionales.

* Compatibilidad con la anidación de modelos de fragmentos de contenido para permitir la creación de estructuras de fragmentos de contenido anidadas mediante tipos de datos de referencia de fragmentos de contenido dedicados o referencias de fragmentos de contenido en línea en campos de texto multilínea.

* Reglas de validación adicionales disponibles en los tipos de datos del modelo de fragmentos de contenido, incluidos &quot;único&quot;, &quot;obligatorio&quot; y &quot;traducible&quot;.

* Capacidad de etiquetar modelos de fragmentos de contenido y permitir la creación de fragmentos de contenido en una carpeta con directivas por etiquetas o rutas.

* Mejoras en la usabilidad del editor de fragmentos de contenido, incluida la acción de publicación y la visualización del modelo en el que se basa un fragmento.

* Capacidad de previsualización de salida de JSON directamente en el editor de fragmentos de contenido.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novedades de [!DNL Assets] {#what-is-new-assets}

* Los recursos se pueden obtener utilizando [!DNL Experience Manager Assets Brand Portal]. Ayuda a obtener activos de los usuarios de la agencia para nuevas campañas de marketing, fotos y proyectos.

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] tiene derecho a tener una configuración previa [!DNL Brand Portal] ejemplo. El [!DNL Cloud Manager] el usuario puede activar [!DNL Brand Portal] el [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Consulte [activar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

* Las empresas ahora pueden obtener recursos mediante [!DNL Brand Portal]. La función de obtención de recursos utiliza [!DNL Brand Portal] para ayudar a los clientes a interactuar con los usuarios de la agencia a fin de que obtengan activos para nuevas campañas de marketing, fotos y proyectos. Consulte [abastecimiento de recursos en [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=es).

* El [!DNL Brand Portal] el informe de uso ahora solo muestra los usuarios activos. Los usuarios inactivos no se muestran ahora. Los usuarios activos son aquellos cuya cuenta se asigna a un perfil de producto en [!DNL Admin Console]. Consulte [[!DNL Brand Portal] informes](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* Entrada [!DNL Brand Portal], se introduce una nueva configuración de descarga que permite crear carpetas independientes para cada recurso al descargar carpetas, colecciones, etc. Consulte [configuración de descarga](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Cuando se seleccionan varios recursos para actualizar las propiedades, a veces se produce un error o se actualizan las propiedades de un recurso no seleccionado. (CQ-4316532)
* Al intentar abrir [!UICONTROL Carril de búsqueda de administración de Assets], la página permanece en blanco y haciendo clic en [!UICONTROL Editar] > [!UICONTROL Configuración] genera un error. (CQ-4315079)
* Cuando se crea una nueva versión de un recurso existente después de resolver el conflicto de nomenclatura, los metadatos del recurso original se sobrescriben. (CQ-4313594)
* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta, incluso si hay espacio disponible. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Administración de experiencias de producto: enriquezca las páginas del catálogo de productos individualmente con fragmentos de experiencias.

* Se han ampliado las propiedades de la consola del producto para mostrar los recursos vinculados y los fragmentos de experiencias, incluida la acción para navegar rápidamente al contenido asociado.

* CIF CIF Lanzamiento del sitio de referencia de Venia el 24 de febrero de 2021, que incluye la versión más reciente de componentes principales (v1.8.0) de la versión de Venia. Consulte [CIF Sitio de referencia de Venia en](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obtener más información.

* CIF Lanzamiento de los componentes principales de la versión 1.8.0 de. Consulte [CIF Componentes principales](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de lanzamiento {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.2.0 es el 11 de febrero de 2021.

### Novedades {#what-is-new-cloud-manager}


* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar su instancia de Brand Portal de manera autoservicio mediante la interfaz de usuario de Cloud Manager. Para un programa normal (que no sea de zona protegida) con la solución Assets, Brand Portal ahora se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El arquetipo del proyecto AEM utilizado en la creación de proyectos y de zonas protegidas se ha actualizado a la versión 25.

* La lista de la API obsoletas identificadas durante la digitalización del código se ha refinado para incluir clases y métodos adicionales que ya no se utilizan en las últimas versiones del SDK de Cloud Service.

* El perfil de SonarQube para Cloud Manager se ha actualizado para eliminar la regla Sonar squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de Interrupción de subprocesos.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda agregar o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está en espera del paso de aprobación.

* Las propiedades establecidas en los archivos `pom.xml` del cliente con el prefijo “sonar” ahora se eliminan dinámicamente para evitar errores de análisis de calidad y digitalización.

* La interfaz de usuario de Cloud Manager informará al usuario de que no puede seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* Se han agregado reglas de calidad del código adicionales para cubrir los problemas de compatibilidad con Cloud Service.

### Correcciones de errores {#bug-fixes-cloud-manager}

* La coincidencia del certificado SSL con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario de Cloud Manager informará al usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error apropiado.

* La interfaz de usuario de Cloud Manager informará al usuario de que no puede seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* En algunos casos, un problema interno podía provocar que la eliminación del entorno se bloquease.

* Se notificaron incorrectamente algunos fallos de canalización como errores de canalización.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.2.4 es el 10 de febrero de 2021.

### Correcciones de errores {#bug-fixes-ctt}

* Al asignar varios usuarios, los ID de IMS de algunos usuarios se asignaban incorrectamente. Esto se ha corregido.

### Fecha de lanzamiento {#release-date-ctt-feb}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt}

* Nueva capacidad e IU agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido.
Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los elementos secundarios.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.2 es el 18 de febrero de 2021.

### Novedades del Analizador de prácticas recomendadas {#what-is-new-bpa}

* Capacidad para detectar el uso de la implementación de AEM Forms y AEM Forms e indicar las áreas relevantes para migrar a AEM Forms as a Cloud Service.
* Capacidad para detectar e informar sobre el uso y recuento de componentes y plantillas personalizadas.
* Capacidad para detectar el tipo de almacén de nodos y almacén de datos utilizado.
* Capacidad para detectar el uso de Dynamic Media.
* Capacidad para detectar la versión de Java utilizada.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. La versión más reciente de este complemento incluye varias correcciones de errores para el Modernizador de repositorios.
Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html#benefits) para obtener más información sobre este complemento.

### Correcciones de errores {#bug-fixes-crt}

* Se han realizado varias correcciones de errores en el Modernizador de repositorios.
Consulte [Recurso de GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obtener más información.
