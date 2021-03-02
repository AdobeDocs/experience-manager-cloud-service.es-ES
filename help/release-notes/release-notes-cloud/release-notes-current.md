---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: 5b702dd33169939d7b16df07f29f8149cafa82bd
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 4%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 es el 25 de febrero de 2021.
La siguiente versión (2021.3.0) será el 25 de marzo de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service  {#sites}

* **[El componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: Se ha agregado compatibilidad con la visualización y edición de SPA externas dentro de AEM mediante .

* **[Edición de un SPA externo en AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Se ha añadido la capacidad de cargar una aplicación independiente de una sola página en una instancia de AEM, añadir secciones de contenido editables y habilitar la creación.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novedades de [!DNL Assets] {#what-is-new-assets}

* Las empresas ahora pueden crear recursos mediante [!DNL Brand Portal]. La función de abastecimiento de recursos aprovecha [!DNL Brand Portal] para ayudar a los clientes a interactuar con los usuarios de la agencia para obtener recursos para nuevas campañas de marketing, sesiones fotográficas y proyectos. Consulte [abastecimiento de recursos en [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* El informe de uso [!DNL Brand Portal] ahora muestra solamente los usuarios activos. Los usuarios inactivos no se muestran ahora. Los usuarios activos son aquellos cuya cuenta se asigna a un perfil de producto en [!DNL Admin Console]. Consulte [[!DNL Brand Portal] informes](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* En [!DNL Brand Portal], se introduce una nueva configuración de descarga que permite crear carpetas independientes para cada recurso al descargar carpetas, colecciones, etc. Consulte [configuración de descarga](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Cuando se crea una nueva versión de un recurso existente después de resolver el conflicto de nombres, los metadatos del recurso original se sobrescriben. (CQ-4313594)
* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta aunque haya espacio disponible. (CQ-4314101)
* Cuando se seleccionan varios recursos para actualizar las propiedades, a veces se produce un error o se actualizan las propiedades de un recurso no seleccionado. (CQ-4316532)
* Al intentar abrir [!UICONTROL Carril de búsqueda de administración de Assets], la página permanece en blanco y al hacer clic en [!UICONTROL Editar] > [!UICONTROL Configuración] se genera un error. (CQ-4315079)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Administración de experiencia del producto: Enriquezca las páginas del catálogo de productos individualmente con fragmentos de experiencias.

* Se han ampliado las propiedades de la consola de producto para mostrar los recursos vinculados y los fragmentos de experiencia, incluida la acción para navegar rápidamente al contenido asociado.

* Sitio de referencia de Venia del CIF publicado - 2021.02.24 que incluye la versión más reciente de los componentes principales del CIF v1.8.0. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obtener más información.

* Componentes principales de CIF v1.8.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.2.0 es el 11 de febrero de 2021.

### Novedades {#what-is-new-cloud-manager}


* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar su instancia de Brand Portal de forma independiente a través de la interfaz de usuario de Cloud Manager. Para un programa normal (que no sea de espacio aislado) con la solución Assets, Brand Portal se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El tipo de archivo del proyecto AEM utilizado en la creación de proyectos y entornos limitados se ha actualizado a la versión 25.

* La lista de API obsoletas identificadas durante la digitalización de código se ha refinado para incluir clases y métodos adicionales en desuso en las últimas versiones del SDK de Cloud Service.

* El perfil de SonarQube para Cloud Manager se ha actualizado para eliminar la regla Sonar squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de Interrupción de subprocesos.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda añadir o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está en espera del paso de aprobación.

* Las propiedades configuradas en los archivos `pom.xml` del cliente con el prefijo sonar ahora se eliminarán dinámicamente para evitar errores de análisis de calidad y compilación.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* Se han añadido reglas de calidad de código adicionales para cubrir los problemas de compatibilidad de Cloud Service.

### Corrección de errores {#bug-fixes-cloud-manager}

* La coincidencia del certificado SSL con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario de Cloud Manager informará a un usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error apropiado.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* En algunos casos, un problema interno puede provocar que la eliminación del entorno se bloquee.

* Algunos errores de canalización se notificaron incorrectamente como errores de canalización.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.2.4 es el 10 de febrero de 2021.

### Corrección de errores {#bug-fixes-ctt}

* Al asignar varios usuarios, los ID de IMS de algunos usuarios se asignaban incorrectamente. Esto se ha solucionado.

### Fecha de la versión {#release-date-ctt-feb}

La fecha de versión de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID del sistema de administración de identidades de Adobe como parte de la actividad de migración de contenido.
Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los niños.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.2 es el 18 de febrero de 2021.

### Novedades de Best Practices Analyzer {#what-is-new-bpa}

* Capacidad para detectar el uso de la implementación de AEM Forms y AEM Forms e indicar áreas relevantes para la migración a AEM Forms as a Cloud Service.
* Capacidad para detectar y crear informes sobre el uso y el recuento de componentes y plantillas personalizados.
* Capacidad para detectar el tipo de almacén de nodos y almacén de datos utilizado.
* Capacidad para detectar el uso de Dynamic Media.
* Capacidad para detectar la versión de Java utilizada.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Se ha lanzado una nueva versión del complemento AIO-CLI. La última versión de este complemento incluye varias correcciones de errores para el Modernizador de repositorio.
Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

### Corrección de errores {#bug-fixes-crt}

* Se han hecho varias correcciones de errores en el Modernizador de repositorio.
Consulte [Recurso de GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obtener más información.








