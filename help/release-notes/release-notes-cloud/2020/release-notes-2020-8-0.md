---
title: Notas de la versión 2020.8.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] notas de la versión de as a Cloud Service para 2020.8.0.'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 7%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Capacidad para [restaurar páginas y subpáginas (árboles de páginas) a una versión anterior](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Capacidad para [crear lanzamientos](/help/sites-cloud/authoring/launches/overview.md) en AEM [SPA Editor.](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] como Cloud Service {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* La transcodificación de vídeo ahora se admite con los microservicios de recursos. Una nueva sección de la configuración [!UICONTROL Procesamiento de perfiles] permite establecer la velocidad de bits y las dimensiones del vídeo. El formato de salida es MP4 con códec H.264. Para obtener más información, consulte [administrar recursos de vídeo](/help/assets/manage-video-assets.md#transcode-video). Para obtener más opciones de transcodificación y para el envío de vídeo, utilice el complemento [!DNL Dynamic Media].

* En las nuevas [!DNL Experience Manager Assets] implementaciones, la funcionalidad de etiquetado inteligente ahora está configurada de forma predeterminada. No es necesario integrarlo manualmente con [!DNL Adobe Developer Console]. En implementaciones existentes, los administradores configuran la integración de etiquetas inteligentes como antes.

* Una nueva [experiencia de descarga de recursos](/help/assets/download-assets-from-aem.md) permite,

   * Descarga asíncrona de descargas grandes para que los usuarios no tengan que esperar.
   * Una nueva API modular para la extensibilidad del desarrollador.

* La extracción de metadatos para microservicios de recursos ha mejorado el rendimiento. Aumenta el rendimiento general de ingesta de recursos.

* Utilice un perfil de procesamiento para generar metadatos personalizados mediante el servicio de cómputo. Consulte [Metadatos personalizados con perfil de procesamiento](/help/assets/manage-metadata.md#metadata-compute-service).

* Una experiencia de descarga más sencilla para los usuarios de Brand Portal que los administradores pueden configurar. Consulte [descripción general de la experiencia de descarga](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Las vistas previas de documentos PDF nativos y de alta fidelidad ya están disponibles en Brand Portal. Consulte [información general del visor de documentos](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Ahora puede invalidar la caché de la CDN (Red de Entrega de Contenido) directamente desde [!DNL Dynamic Media] en AEM como Cloud Service (en lugar de usar [!DNL Dynamic Media Classic]). Garantiza que los recursos más recientes se proporcionen en minutos en lugar de horas. Consulte [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* La compatibilidad de accesibilidad mejorada se agrega a los controles de la interfaz de usuario, la navegación, la exploración y la experiencia de búsqueda en [!DNL Assets].

   * Si pulsa la tecla Escape después de seleccionar la opción [!UICONTROL Añadir representación], el enfoque vuelve a la barra de herramientas. <!-- via CQ-4293594-->
   * El foco del teclado funciona según lo esperado al utilizar el cuadro combinado Correo electrónico . <!-- via CQ-4286215 -->
   * Los elementos acordeones de la sección de filtros de búsqueda se interpretan como acordeones estándar ampliables. <!-- via CQ-4273103 -->
   * Al aplicar una etiqueta a un recurso, el cuadro de diálogo muestra las etiquetas como elementos de árbol. Los atributos ARIA se aplican correctamente a los elementos de árbol para que sean accesibles ahora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] Ya está disponible la versión 2.0.3. Mejora la compatibilidad con el Service Pack [!DNL Experience Manager] 6.5.5 y tiene una lista de compatibilidad con el sistema operativo cliente actualizada. [!DNL Windows] No se admiten las  [!DNL macOS] versiones 7 y anteriores a la 10.14.

### Errores corregidos en [!DNL Assets] {#bugs-fixed}

* La opción Relar y desrelacionar no responde cuando se hace clic en ella por primera vez. (CQ-4299022)
* Al descargar un recurso, si selecciona la opción para recibirlo por correo electrónico, el correo electrónico no se envía. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Ya está disponible la función Consola de producto . Esto permite que los especialistas en marketing y los autores de AEM vean y naveguen por las categorías y los productos almacenados en el servidor comercial. También se proporciona compatibilidad con propiedades para categorías y productos en la consola de producto.

* Se mejoraron los seleccionadores de productos y categorías para permitir que los especialistas en marketing seleccionen productos mediante SKU o categorías mediante ID de categoría.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de [!UICONTROL Cloud Manager] versión 2020.8.0 es el 6 de agosto de 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido es una función habilitada en las canalizaciones de producción de Cloud Manager Sites. La configuración de Canalización de producción para programas con Sitios ahora incluye una tercera pestaña llamada **Auditoría de contenido**. Cada vez que se ejecute un flujo de producción, se incluirá un nuevo paso de Auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).


   >[!NOTE]
   >Desde entonces, se ha cambiado el nombre de Auditoría de contenido a Auditoría de experiencias.

   Consulte [Prueba de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

* Los entornos recién creados en los programas de Assets ahora se configurarán automáticamente con Smart Content Services.

* Los entornos hibernados se pueden anular en hibernación desde la página **Información general** de Cloud Manager.

* Capacidad para realizar comprobaciones de experiencias en páginas, con tecnología de Google Lighthouse. Como parte de la canalización de Cloud Manager, se pueden comprobar y validar hasta 25 páginas con KPI de experiencia, y las puntuaciones se muestran en la interfaz de usuario de Cloud Manager.

### Corrección de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se estaban ejecutando como parte del análisis de calidad del código.

* En la página de ejecución de la canalización, el nombre de la rama tenía un formato incorrecto.

* En algunos casos, no se registró con éxito la finalización de las ejecuciones de canalización, lo que impidió nuevas ejecuciones de la canalización.

* Las ejecuciones de canalización ocasionalmente se *atascaran* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con funciones administrativas distintas de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En ciertas condiciones, el trabajo de índices de actualización se inició varias veces en paralelo, lo que resultó en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que se intentaran realizar operaciones en un entorno mientras se eliminaba.

* Había una discordancia de color en la página **Información general** de Cloud Manager.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas que llevan la puntuación media de auditoría de contenido por debajo de lo que deberían ser.

* La pestaña Auditoría de contenido muestra incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agregan páginas, se auditará la página principal.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión 1.0.4 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido ahora es compatible con Shared S3 DataStore.

### Corrección de errores {#ctt-bug-fixes}

* Se han agregado tiempos de espera adicionales para que la herramienta complete las acciones.

* La interfaz de usuario de la versión anterior a veces mostraba una extracción correcta aunque el registro mostrara errores.

## Herramientas de refactorización de código {#code-refactoring-tools}

Siga esta sección para conocer las novedades y las actualizaciones de las herramientas de refactorización de código.

### Novedades {#what-is-new-refactoring}

* Complemento AIO-CLI lanzado para unificar las herramientas de refactorización de código a fin de permitir que los desarrolladores invoquen y ejecuten las herramientas de refactorización de código desde un solo lugar. Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información.

* AEM Dispatcher Converter se ha ampliado para admitir conversiones de configuraciones On-Premise y Adobe Managed Services Dispatcher en AEM como configuraciones de Dispatcher compatibles con el Cloud Service. Consulte [Recurso de Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obtener más información.

* AEM Dispatcher Converter se reescribe en ` node.js ` e integra con el complemento AIO-CLI.
