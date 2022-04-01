---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 372e40eb90d87d9ed366e08a3c0117068542680b
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 34%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.3.0) es el 31 de marzo de 2022.
La siguiente versión (2022.4.0) es el 28 de abril de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de marzo de 2022](https://video.tv.adobe.com/v/341465) vídeo para ver un resumen de las funciones añadidas en la versión 2022.3.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [!DNL AEM Dynamic Media] ahora proporciona la flexibilidad para [configurar una cuenta de alias](/help/assets/dynamic-media/dm-alias-account.md) en la interfaz de usuario, lo que garantiza que se actualicen de forma predeterminada las URL de Dynamic Media y el código de incrustación de visor. Esto tiene un impacto positivo en el SEO, para reflejar las actualizaciones realizadas en su contexto empresarial, como el cambio de marca.

* Ahora puede usar la interfaz de usuario de [!DNL Experience Manager Assets] para:

   * Configure las variables [detección de activos duplicados](/help/assets/manage-digital-assets.md#detect-duplicate-assets) en un repositorio.

   * Configurar [adición de marcas de agua digitales](/help/assets/watermark-assets.md) a imágenes.

* Los administradores ahora pueden configurar el servicio de correo electrónico para las descargas grandes. Permite a los usuarios [activar notificaciones por correo electrónico para descargas grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) desde la interfaz de [!DNL Experience Manager Assets]. El usuario recibe una notificación por correo electrónico que contiene el vínculo de descarga de la carpeta zip archivada al finalizar el proceso de descarga.

* La función [Administrar publicación](/help/assets/manage-publication.md) se amplía con una interfaz de usuario mejorada. Los usuarios pueden publicar o cancelar la publicación de contenido desde y hacia el destino seleccionado, [Añadir contenido](/help/assets/manage-publication.md#add-content) a la lista de publicaciones desde el repositorio de DAM, [Incluir configuración de carpeta](/help/assets/manage-publication.md#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, así como [programar la publicación](/help/assets/manage-publication.md#publish-assets-later) a una fecha u hora posterior.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

* Puede [ordenar etiquetas](/help/assets/organize-assets.md#use-tags-to-organize-assets) al crear etiquetas inteligentes, así como al aplicar filtros de búsqueda utilizando el predicado de etiquetas.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [API de generación de documentos](/help/forms/aem-forms-cloud-service-communications.md) ayuda a combinar, reorganizar y validar documentos de PDF. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede:

   * Ensamble los documentos del PDF.
   * Desmonte los documentos del PDF.
   * Convierta y valide documentos compatibles con PDF/A.

* **Convertir automáticamente PDF forms de más de 15 páginas en formularios adaptables**: Ahora puede utilizar el servicio de automated forms conversion para convertir PDF forms con hasta 40 páginas en formularios adaptables. El servicio ahora proporciona la opción de convertir secciones de formularios de más de 15 páginas a fragmentos de formulario adaptables. Ayuda a mejorar la velocidad de procesamiento de los formularios convertidos y facilita la carga de formularios grandes en el editor de formularios adaptables.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Usar XCI personalizado para generar un documento de registro**: Ahora puede utilizar un archivo XCI personalizado para establecer varias propiedades de un documento de registro. Anula el XCI maestro con los cambios personalizados.

* **Utilizar CAPTCHA invisible en forma adaptable**: Puede utilizar el CAPTCHA invisible para mostrar el desafío CAPTCHA solo en el caso de una actividad sospechosa. Si no se encuentra ninguna actividad sospechosa, no se muestra el desafío CAPTCHA.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Beta: Compatibilidad del componente principal de búsqueda del CIF de AEM con Commerce LiveSearch
* SEO mejorado para escenarios de varias tiendas: Los formatos de URL para PDP/PLP ahora se pueden configurar a nivel de tienda mediante las propiedades de configuración de la nube del CIF
* El selector de productos es compatible con los productos clasificados mediante la nueva opción de filtro en la interfaz de usuario.  Esto permite a los profesionales del contenido preparar la administración del contenido del producto para próximos lanzamientos del producto
* Administración simplificada de la configuración del CIF y gestión de errores mediante el uso del nombre de configuración de la nube del CIF en lugar de la url del proxy de configuración
* Selección manual de categorías para la lista de productos y los componentes de carrusel. Esto permite a los profesionales del contenido utilizar estos componentes en páginas de contenido, fuera de la experiencia del catálogo

## [!DNL Experience Manager] como [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* Para una solución de problemas más eficaz y eficaz de las funciones personalizadas en los entornos de Cloud, hemos lanzado una nueva herramienta para desarrolladores: [Navegador de repositorios](/help/implementing/developing/tools/repository-browser.md). Es un explorador HTML ligero, de solo lectura que puede iniciar desde Developer Console. Obtenga visibilidad del repositorio de contenido en los niveles de editor, autor y vista previa, y en todos los entornos, incluida la producción, el escenario y el desarrollo. Examine la estructura de contenido, vea las propiedades y obtenga una vista previa y descargue los binarios.

   ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* Las credenciales utilizadas para autenticar llamadas de API de servidor a servidor (por ejemplo, para solicitudes de API de GraphQL) ahora se pueden actualizar antes de la caducidad de forma automática desde Developer Console. Consulte la [documentación](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) para obtener más información.

* Las tareas de mantenimiento de purga de versiones y depuración de registros de auditoría, que no se habían habilitado anteriormente, se habilitarán para nuevos entornos. Consulte los valores asociados en la [Tarea de mantenimiento](/help/operations/maintenance.md) artículo.

* AEM herramientas as a Cloud Service de SDK Dispatcher ahora admiten equipos Mac con el chip M1

## Cloud Manager {#cloud-manager}

### Fecha de versión de febrero {#release-date-cm-feb}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0 es el 10 de febrero de 2022. La próxima versión está prevista para el 10 de marzo de 2022.

### Novedades {#what-is-new-cm-feb}

* Nueva aceleración [Canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) se han introducido para implementar exclusivamente la configuración de HTTPD/Dispatcher.
   * Debe estar en AEM versión `2021.12.6151.20211217T120950Z` o más reciente y [inclusión en el modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para utilizar esta función.
   * Esta función se implementará por fases en las dos semanas siguientes a la versión de 2022.02.0.
* La experiencia de página de aterrizaje de Cloud Manager se ha actualizado para ofrecer una navegación mejorada, un fácil cambio entre las vistas de cuadrícula/mosaico y ventanas emergentes para obtener un resumen rápido del programa.
* Un nuevo umbral fallido (`< D`) se ha agregado a la variable [métrica de clasificación de fiabilidad.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Los clientes con problemas de calidad graves que afectan a la estabilidad del sistema, relacionados principalmente con índices no válidos y procesos de flujo de trabajo, no podrán realizar implementaciones hasta que se resuelvan dichos problemas.
* La gravedad de la variable `BannedPath` [regla de calidad](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) se ha cambiado de bloqueador a crítico.
* El asistente de canalización informará al usuario cuando sea necesario actualizar el entorno de AEM antes de configurar un [Canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) asociada a él.

### Correcciones de errores {#bug-fixes-cm-feb}

* Las contraseñas antiguas del repositorio de Git ahora siempre se invalidan cuando se genera una nueva contraseña.
* La actualización de variables de entorno a través de la API ya no interfiere con la ejecución de una canalización en situaciones excepcionales.

### Fecha de la versión de marzo {#release-date-cm-march}

La fecha de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service del 10 de marzo de 2022. La próxima versión está prevista para el 7 de abril de 2022.

### Novedades {#what-is-new-cm-march}

* El acceso a AEM registro de entorno se puede realizar con la función de desarrollador .

### Correcciones de errores {#bug-fixes-cm-march}

* Un subconjunto de repositorios Git creados manualmente tenía un valor de nombre incorrecto que impedía que la función de reutilización de artefactos de compilación fuera efectiva. Los nombres de esos repositorios se han cambiado y los usuarios verán el nombre corregido en la interfaz de usuario/API de Cloud Manager.
* Los artefactos de compilación de las canalizaciones que no son de producción se reutilizaron incorrectamente en las canalizaciones de pila completas de producción.
* Al añadir o editar una canalización de calidad de código, ya no se muestran las opciones para gestionar errores de métricas.
* Algunas configuraciones de variables de canalización inesperadas podrían causar en el paso de compilación.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.9.0 es el 28 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Comprobar protecciones de tamaño : la función Tamaño de comprobación de la herramienta de transferencia de contenido ayuda a reducir las transferencias de contenido fallidas.  Con la función Tamaño de comprobación, los usuarios pueden 1) determinar si tienen suficiente espacio en disco en la variable `crx-quickstart` antes de la extracción y 2) estime el tamaño del conjunto de migración y verifique si es compatible. Si se infringen una o ambas comprobaciones, los usuarios verán advertencias en la interfaz de usuario de CTT. Con esta protección, puede evitar fallos en la transferencia de contenido y discutir de forma proactiva las opciones de migración con el Servicio de atención al cliente de Adobe. Consulte [Determinación del tamaño del conjunto de migración y el espacio en disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) para obtener más información.

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
