---
title: Notas de la versión 2022.3.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.3.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 83%

---

# Notas de la versión 2022.3.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la función para la versión 2022.3.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.3.0) es el 31 de marzo de 2022.
La próxima versión (2022.4.0) está planificada para el 5 de mayo de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo [Información general sobre la versión de marzo de 2022](https://video.tv.adobe.com/v/341465) para ver un resumen de las funciones añadidas en la versión 2022.3.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Sites] {#prerelease-features-sites}

* Los tipos de datos del modelo de contenido ahora se pueden definir como traducibles mediante una sencilla casilla de verificación en el editor de modelos de contenido. AEM Además, las reglas y configuraciones de traducción de la se actualizan automáticamente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] ahora proporciona la flexibilidad para [configurar una cuenta de alias](/help/assets/dynamic-media/dm-alias-account.md) en la interfaz de usuario, lo que garantiza que se actualicen de forma predeterminada las URL de Dynamic Media y el código de incrustación de visor. Esto tiene un impacto positivo en el SEO, para reflejar las actualizaciones realizadas en su contexto empresarial, como el cambio de marca.

* Ahora puede usar la interfaz de usuario de [!DNL Experience Manager Assets] para:

   * Configure la [detección de recursos duplicados](/help/assets/detect-duplicate-assets.md) en un repositorio.

   * Configure la [adición de marcas de agua digitales](/help/assets/watermark-assets.md) a las imágenes.

* Los administradores ahora pueden configurar el servicio de correo electrónico para las descargas grandes. Permite a los usuarios [activar notificaciones por correo electrónico para descargas grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) desde la interfaz de [!DNL Experience Manager Assets]. El usuario recibe una notificación por correo electrónico que contiene el vínculo de descarga de la carpeta zip archivada al finalizar el proceso de descarga.

* La función [Administrar publicación](/help/assets/manage-publication.md) se amplía con una interfaz de usuario mejorada. Los usuarios pueden publicar o cancelar la publicación de contenido desde y hacia el destino seleccionado, [Añadir contenido](/help/assets/manage-publication.md#add-content) a la lista de publicaciones desde el repositorio de DAM, [Incluir configuración de carpeta](/help/assets/manage-publication.md#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, así como [programar la publicación](/help/assets/manage-publication.md#publish-assets-later) a una fecha u hora posterior.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

* Ahora puede [ordenar etiquetas](/help/assets/organize-assets.md#use-tags-to-organize-assets) en la ventana del selector de etiquetas en orden de subida o de bajada, según el nombre de la etiqueta, la fecha de creación o la fecha de modificación.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: la [API de generación de documentos](/help/forms/aem-forms-cloud-service-communications.md) ayuda a combinar, reorganizar y validar documentos PDF. El servicio le permite generar documentos en modo sincrónico.  Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:

   * Montar los documentos PDF.
   * Desmontar los documentos PDF.
   * Convertir y validar documentos compatibles con PDF/A.

* **Convertir automáticamente formularios PDF de más de 15 páginas en formularios adaptables**: ahora puede utilizar el servicio de conversión automatizada de formularios para convertir formularios PDF de hasta 40 páginas en formularios adaptables. El servicio ahora proporciona la opción de convertir secciones de formularios de más de 15 páginas a fragmentos de formulario adaptables. Ayuda a mejorar la velocidad de procesamiento de los formularios convertidos y facilita la carga de formularios grandes en el editor de formularios adaptables.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Usar XCI personalizados para generar un documento de registro**: ahora puede utilizar un archivo XCI personalizado para establecer varias propiedades de un documento de registro. Anula el XCI maestro con los cambios personalizados.

* **Utilizar un CAPTCHA invisible en un formulario adaptable**: puede utilizar un CAPTCHA invisible para mostrar una prueba CAPTCHA solo en el caso de actividad sospechosa. Si no se encuentra ninguna actividad sospechosa, no se muestra el desafío CAPTCHA.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* SEO mejorado para escenarios de varias tiendas: los formatos de URL para PDP/PLP ahora se pueden configurar en el nivel de tienda mediante las propiedades de configuración en la nube del CIF
* El selector de productos es compatible con los productos clasificados mediante una nueva opción de filtro en la interfaz de usuario.  Esto permite a los profesionales del contenido preparar la administración de contenido de producto para próximos lanzamientos del producto
* Administración simplificada de la configuración del CIF y gestión de errores mediante el uso del nombre de configuración en la nube del CIF, en lugar de la URL del proxy de configuración
* Selección manual de categorías para la lista de productos y los componentes de carrusel. Esto permite a los profesionales del contenido utilizar estos componentes en páginas de contenido, fuera de la experiencia del catálogo

### Nuevas funciones disponibles en el canal de prelanzamiento de CIF {#prerelease-features-cif}

* Compatibilidad del componente principal de búsqueda del CIF de AEM con Commerce LiveSearch.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* Para una solución de problemas más eficiente y efectiva de las características personalizadas en los entornos de la nube, hemos lanzado una nueva herramienta para desarrolladores: [el Explorador de repositorios](/help/implementing/developing/tools/repository-browser.md). Es un explorador ligero, de solo lectura y HTML que puede iniciar desde Developer Console. Obtenga visibilidad del repositorio de contenido en los niveles de editor, autor y vista previa, y en todos los entornos, incluida la producción, la fase y el desarrollo. Examine la estructura de contenido, vea las propiedades y previsualice y descargue los binarios.

  ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* Las credenciales utilizadas para autenticar llamadas de API de servidor a servidor (por ejemplo, para solicitudes de API de GraphQL) ahora se pueden actualizar antes de la caducidad de forma automática desde Developer Console. Consulte la [documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) para obtener más información.

* Las tareas de mantenimiento de purga de versiones y depuración de registros de auditoría, que no se habían habilitado anteriormente, ahora están habilitadas para nuevos entornos. Consulte los valores asociados en el artículo [Tarea de mantenimiento](/help/operations/maintenance.md).

* Las herramientas del SDK de Dispatcher de AEM as a Cloud Service ahora admiten equipos Mac con el chip M1

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido versión 1.9.0 es el 28 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Comprobar protecciones de tamaño: la función de comprobación de tamaño de la herramienta de transferencia de contenido ayuda a reducir las transferencias de contenido fallidas.  Con la función Comprobar tamaño, los usuarios pueden 1) determinar si tienen suficiente espacio en disco en el subdirectorio `crx-quickstart` antes de la extracción, y 2) estimar el tamaño del conjunto de migración y comprobar si es compatible. Si se infringen una o ambas comprobaciones, los usuarios ven advertencias en la IU de CTT. Con esta protección, puede evitar errores en la transferencia de contenido y discutir de forma proactiva las opciones de migración con el Servicio de atención al cliente de Adobe. Consulte [Determinación del tamaño del conjunto de migración y el espacio en disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es#migration-set-size) para obtener más información.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

El 16 de marzo de 2022 es la fecha de lanzamiento del Analizador de prácticas recomendadas versión 2.1.26.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar recursos no procesados. Si se detectan recursos no procesados, estos deben configurarse para procesarse o deben eliminarse del conjunto de migración durante la transferencia de contenido para evitar tener problemas durante la ingesta de contenido.
* Capacidad para detectar si el contenido tiene más de 1000 URL personalizadas. No se recomienda utilizar un número elevado de URL personalizadas, ya que suponen una carga en los servidores de Dispatcher y Publish.
* Capacidad para identificar problemas relacionados con las definiciones de índices de Oak y detectar incompatibilidades con AEM as a Cloud Service.
* Capacidad para detectar e informar sobre el uso de configuraciones de externalizador. En AEM as a Cloud Service, la configuración de externalizador la establece Cloud Manager. Por lo tanto, las configuraciones de externalizador existentes deben refactorizarse para mantener la compatibilidad.

### Correcciones de errores {#bug-fixes-bpa}

* En algunos casos, BPA no se pudo ejecutar debido a que FormsSelectiveFeaturesAnalysis arrojó un error de aserción. Esto se ha corregido.
* BPA informaba de conclusiones relacionadas con el patrón de WRK como IMPORTANTE en lugar de como CRÍTICO. Esto se ha corregido.
* BPA informaba incorrectamente de conclusiones relacionadas con las definiciones de índice OAK en ui.apps como CRÍTICO. Esto se ha corregido.
