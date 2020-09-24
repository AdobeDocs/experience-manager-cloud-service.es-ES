---
title: Notas de la versión 2020.8.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Notas de la versión 2020.8.0.'
translation-type: tm+mt
source-git-commit: fe769e8acecbc173f2437edc292eeba2585f0509
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 7%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* Capacidad para [restaurar páginas y subpáginas (árboles de páginas) a una versión](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)anterior.

* Posibilidad de [crear inicios](/help/sites-cloud/authoring/launches/overview.md) en AEM editor de [SPA.](/help/implementing/developing/spa/introduction.md)


## [!DNL Adobe Experience Manager Assets] como Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* La transcodificación de vídeo ahora se admite con los microservicios de recursos. Una nueva sección de la configuración de Perfiles [!UICONTROL de] procesamiento le permite definir la velocidad de bits y las dimensiones del vídeo. El formato de salida es MP4 con códec H.264. Para obtener más información, consulte [Gestión de recursos](/help/assets/manage-video-assets.md#transcode-video)de vídeo. Para obtener más opciones de transcodificación y envío de vídeo, utilice [!DNL Dynamic Media] Add-on.

* En las nuevas [!DNL Experience Manager Assets] implementaciones, la funcionalidad de etiquetado inteligente ahora está configurada de forma predeterminada. No es necesario realizar la integración manualmente con [!DNL Adobe Developer Console]. En implementaciones existentes, los administradores [configuran la integración](/help/assets/smart-tags-configuration.md#aio-integration) de etiquetas inteligentes como antes.

* Una nueva experiencia [de descarga de](/help/assets/download-assets-from-aem.md) recursos permite:

   * Descarga asincrónica para grandes descargas para que los usuarios no tengan que esperar.
   * Una nueva API modular para la extensibilidad del desarrollador.

* La extracción de metadatos para los microservicios de recursos tiene un rendimiento mejorado. Aumenta el rendimiento general de ingestión de recursos.

* Utilice un perfil de procesamiento para generar metadatos personalizados mediante el servicio de cómputo. Consulte Metadatos [personalizados con perfil](/help/assets/manage-metadata.md#metadata-compute-service)de procesamiento.

* Una experiencia de descarga más sencilla para los usuarios de Brand Portal que los administradores pueden configurar. Consulte [Descripción general](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)de la experiencia de descarga.

* Las previsualizaciones de documento en PDF nativas y de alta fidelidad ya están disponibles en Brand Portal. Consulte Descripción general [del visor de](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)documento.

* Ahora puede invalidar la caché de CDN (Red de Envío de contenido) directamente desde [!DNL Dynamic Media] en AEM como Cloud Service (en lugar de usar [!DNL Dynamic Media Classic]). Garantiza que los últimos recursos se proporcionen en minutos en lugar de horas. Consulte [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* La compatibilidad de accesibilidad mejorada se agrega a los controles de interfaz de usuario, la navegación, la exploración y la experiencia de búsqueda en [!DNL Assets].

   * Si pulsa la tecla Escape después de seleccionar la opción [!UICONTROL Añadir representación] , el enfoque vuelve a la barra de herramientas. <!-- via CQ-4293594-->
   * El enfoque del teclado funciona correctamente al utilizar el cuadro combinado Correo electrónico. <!-- via CQ-4286215 -->
   * Los elementos de acordeones de la sección filtros de búsqueda se interpretan como acordeones estándar ampliables. <!-- via CQ-4273103 -->
   * Al aplicar una etiqueta a un recurso, el cuadro de diálogo muestra las etiquetas como elementos de árbol. Los atributos ARIA se aplican correctamente a los elementos de árbol para hacerlos accesibles ahora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] Ya está disponible la versión 2.0.3. Mejora la compatibilidad con el Service Pack [!DNL Experience Manager] 6.5.5 y cuenta con una lista de compatibilidad con el sistema operativo cliente actualizada. [!DNL Windows] 7 y [!DNL macOS] versiones anteriores a 10.14 no son compatibles.

### Errores corregidos en [!DNL Assets] {#bugs-fixed}

* La opción Relacionar y desrelacionar no responde cuando se hace clic en ella por primera vez. (CQ-4299022)
* Al descargar un recurso, si selecciona la opción de recibirlo por correo electrónico, el correo electrónico no se envía. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* La función de la consola de producto ya está disponible. Esto permite a los especialistas en mercadotecnia/autores en AEM realizar vistas y navegar por categorías y productos almacenados en el servidor comercial. También se proporciona compatibilidad con propiedades para categorías y productos en la consola de producto.

* Se mejoraron los seleccionadores de productos y Categorías para permitir que los especialistas en marketing seleccionen el producto mediante SKU o seleccione la categoría mediante ID de categoría.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido es una función habilitada en Cloud Manager Sites Producines. La configuración de la tubería de producción para programas con sitios ahora incluye una tercera ficha denominada Auditoría **del contenido**. Siempre que se ejecute un flujo de producción, se incluirá un nuevo paso de auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).


   >[!NOTE]
   >La auditoría de contenido se ha cambiado a Auditoría de experiencias.

   Consulte Prueba de auditoría de [experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más detalles.

* Los entornos recién creados en programas de Recursos ahora se configurarán automáticamente con Smart Content Services.

* Los entornos hibernados se pueden eliminar de la hibernación desde la página **Información general** del Administrador de nubes.

* Capacidad para realizar comprobaciones de experiencias en páginas, con tecnología de Google Lighthouse. Como parte de la canalización de Cloud Manager, se pueden comprobar y validar hasta 25 páginas con KPI de experiencia, y las puntuaciones se muestran en la interfaz de usuario del Cloud Manager.

### Corrección de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se estaban ejecutando como parte de la exploración de calidad del código.

* En la página de ejecución de la canalización, el nombre de la ramificación tenía un formato incorrecto.

* En algunos casos, las ejecuciones de los trámites terminados no se registraban correctamente por haberse completado, lo que impedía la ejecución de los nuevos trámites.

* Ocasionalmente, las ejecuciones por tuberías se *quedaban atascadas* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con funciones administrativas distintas de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En determinadas condiciones, el trabajo de índices de actualización se inició varias veces en paralelo, lo que resultó en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que las operaciones se intentaran en un entorno mientras se eliminaba.

* Hubo una discordancia de color en la página **Información general** del Administrador de nube.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas que llevan la puntuación promedio de auditoría de contenido por debajo de lo que deberían ser.

* La ficha Auditoría de contenido muestra incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agrega ninguna página, se auditará la página principal.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión v1.0.4 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido ahora es compatible con Shared S3 DataStore.

### Corrección de errores {#ctt-bug-fixes}

* Se han agregado tiempos de espera adicionales para que la herramienta complete las acciones.

* La IU de la versión anterior a veces mostraba una extracción correcta aunque el registro mostraba errores.

## Herramientas de refactorización de código {#code-refactoring-tools}

Siga esta sección para conocer las novedades y las actualizaciones de las herramientas de refactorización de código.

### Novedades {#what-is-new-refactoring}

* Complemento AIO-CLI lanzado para unificar las herramientas de refactorización de código para permitir que los desarrolladores invoquen y ejecuten las herramientas de refactorización de código desde un solo lugar. Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información.

* AEM Dispatcher Converter se ha ampliado para admitir conversiones de configuraciones de On-premise y Adobe Managed Services Dispatcher en AEM como configuraciones de Dispatcher compatibles con Cloud Service. Consulte Recurso [Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) para obtener más información.

* AEM Dispatcher Converter se reescribe ` node.js ` e integra con el complemento AIO-CLI.
