---
title: Notas de la versión 2020.8.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.8.0."
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 42%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Capacidad para [restaurar páginas y páginas secundarias (árboles de páginas) a una versión anterior](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Capacidad para [crear lanzamientos](/help/sites-cloud/authoring/launches/overview.md) AEM en el [SPA Editor de.](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* La transcodificación de vídeo ahora se admite con los microservicios de recursos. Una nueva sección de la [!UICONTROL Perfiles de procesamiento] La configuración de permite establecer dimensiones y velocidad de bits de vídeo. El formato de salida es MP4 con códec H.264. Para obtener más información, consulte [administrar recursos de vídeo](/help/assets/manage-video-assets.md#transcode-video). Para obtener más opciones de transcodificación y para la entrega de vídeo, utilice [!DNL Dynamic Media] complemento de.

* En nuevo [!DNL Experience Manager Assets] En implementaciones de, la funcionalidad de etiquetado inteligente ahora está configurada de forma predeterminada. No es necesario integrar manualmente con [!DNL Adobe Developer Console]. En implementaciones existentes, los administradores configuran la integración de etiquetas inteligentes como antes.

* Un nuevo [experiencia de descarga de recursos](/help/assets/download-assets-from-aem.md) permite,

   * Descarga asincrónica de descargas masivas para que los usuarios no tengan que esperar.
   * Una nueva API modular para la extensibilidad del desarrollador.

* La extracción de metadatos para microservicios de recursos ha mejorado el rendimiento. Aumenta el rendimiento general de la ingesta de recursos.

* Utilice un perfil de procesamiento para generar metadatos personalizados mediante Compute Service. Consulte [Metadatos personalizados con perfil de procesamiento](/help/assets/manage-metadata.md#metadata-compute-service).

* Una experiencia de descarga más sencilla para los usuarios de Brand Portal, que los administradores pueden configurar. Consulte [información general sobre la experiencia de descarga](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Las previsualizaciones de documentos nativas y de PDF de alta fidelidad ya están disponibles en Brand Portal. Consulte [información general del visor de documentos](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Ahora puede invalidar la caché de la red de distribución de contenido (CDN) directamente desde [!DNL Dynamic Media] AEM en as a Cloud Service (en lugar de usar ) [!DNL Dynamic Media Classic]). Garantiza que los recursos más recientes se proporcionen en minutos en lugar de horas. Consulte [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* La compatibilidad de accesibilidad mejorada se agrega a los controles de la interfaz de usuario, la navegación, la exploración y la experiencia de búsqueda en [!DNL Assets].

   * Si pulsa la tecla Escape después de seleccionar [!UICONTROL Agregar representación] , el enfoque vuelve a la barra de herramientas. <!-- via CQ-4293594-->
   * El foco del teclado funciona según lo esperado al utilizar el cuadro combinado Correo electrónico. <!-- via CQ-4286215 -->
   * Los elementos de acordeón de la sección de filtros de búsqueda se interpretan como acordeones expandibles estándar. <!-- via CQ-4273103 -->
   * Al aplicar una etiqueta a un recurso, el cuadro de diálogo muestra las etiquetas como elementos de árbol. Los atributos ARIA se aplican correctamente a los tres elementos para que sean accesibles ahora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] Ya está disponible la versión 2.0.3 de. Mejora la compatibilidad con [!DNL Experience Manager] El paquete de servicio 6.5.5 y tiene una lista de compatibilidad de SO de cliente actualizada. [!DNL Windows] 7 y [!DNL macOS] no son compatibles las versiones anteriores a 10.14.

### Errores corregidos en [!DNL Assets] {#bugs-fixed}

* La opción Relacionar y no relacionar no responde cuando se hace clic por primera vez. (CQ-4299022)
* Al descargar un recurso, si selecciona la opción para recibirlo por correo electrónico, este no se envía. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* La función de consola de producto ya está disponible. AEM Esto permite a los especialistas en marketing/autores en el ámbito de la visualización y la navegación por las categorías y los productos almacenados en el back-end del comercio. También se proporciona compatibilidad con propiedades para categorías y productos en la Consola de producto.

* Se mejoraron los seleccionadores de productos y categorías para permitir que los especialistas en marketing seleccionen productos mediante SKU o categorías mediante ID de categoría.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de [!UICONTROL Cloud Manager] La versión 2020.8.0 es el 6 de agosto de 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido es una característica habilitada en las canalizaciones de producción de Cloud Manager Sites. La configuración de Canalizaciones de producción para programas con Sites ahora incluye una tercera pestaña llamada **Auditoría de contenido**. Cada vez que se ejecute un flujo de producción, se incluirá un nuevo paso de Auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).


   >[!NOTE]
   >Se ha cambiado el nombre de Auditoría de contenido a Auditoría de experiencias.

   Consulte [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

* Los entornos recién creados en los programas de Assets ahora se configurarán automáticamente con Smart Content Services.

* Los entornos en hibernación se pueden quitar de la hibernación desde la página **Información general**.

* Capacidad para realizar comprobaciones de experiencias en páginas con la tecnología Google Lighthouse. Como parte de la canalización de Cloud Manager, se pueden comprobar y validar hasta 25 páginas con KPI de experiencia y las puntuaciones se muestran en la interfaz de usuario de Cloud Manager.

### Correcciones de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se ejecutaban como parte del análisis de calidad del código.

* En la página de ejecución de la canalización, el nombre de la rama tenía un formato incorrecto.

* En algunos casos, no se registraba correctamente la finalización de las ejecuciones de canalización, lo que impedía nuevas ejecuciones de la canalización.

* Las ejecuciones de canalización ocasionalmente se quedaban *atascadas* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con roles administrativos distintos de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En ciertas condiciones, el trabajo de índices de actualización se iniciaba varias veces en paralelo, lo que resultaba en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que se intentaran realizar operaciones en un entorno mientras se eliminaba.

* Había una desigualdad de color en la página de Cloud Manager **Información general**.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas con la puntuación media de auditoría de contenido por debajo de lo que deberían ser.

* La pestaña Auditoría de contenido muestra incorrectamente la dirección URL base mediante el uso del dominio Autor en lugar del dominio Publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agregan páginas, se auditará la página principal.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión 1.0.4 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido ahora es compatible con el almacén de datos compartido S3.

### Correcciones de errores {#ctt-bug-fixes}

* Se han agregado tiempos de espera adicionales para que la herramienta complete acciones.

* La IU de versiones anteriores a veces mostraba una extracción correcta aunque el registro mostraba errores.

## Herramientas de refactorización de código {#code-refactoring-tools}

Siga esta sección para conocer las novedades y las actualizaciones de las herramientas de refactorización de código.

### Novedades {#what-is-new-refactoring}

* Complemento AIO-CLI lanzado para unificar las herramientas de refactorización de código para permitir que los desarrolladores invoquen y ejecuten las herramientas de refactorización de código desde un solo lugar. Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información.

* AEM AEM Dispatcher Converter se ha ampliado para admitir las conversiones de configuraciones On-Premise y Adobe Managed Services Dispatcher en configuraciones de Dispatcher compatibles con el as a Cloud Service. Consulte [Recurso de Git: Dispatcher Converter de AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obtener más información.

* AEM Conversor de Dispatcher de reescrito en ` node.js ` e integrado con el complemento AIO-CLI.
