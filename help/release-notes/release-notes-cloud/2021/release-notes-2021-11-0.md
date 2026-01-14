---
title: Notas de la versión 2021.11.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.11.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 86f8ddd1-af51-4874-9111-0935b5a162c1
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 94%

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

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.11.0) es el 16 de diciembre de 2021.
La de la siguiente versión (2022.1.0) es el viernes, 03 de febrero de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo [Información general sobre la versión de diciembre de 2021](https://video.tv.adobe.com/v/339278) para ver un resumen de las funciones añadidas en la versión 2021.11.0 (noviembre de 2021).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* El recorte inteligente y la muestra de imágenes de Dynamic Media ahora cuenta con la tecnología de los últimos servicios de IA de Adobe, que generan recortes y muestras mejorados. Además, se ha lanzado una mejora para generar diferentes contenidos de recorte, para la misma proporción de aspecto pero en diferentes resoluciones. Además, las ediciones manuales se conservan al reprocesar si no hay cambios en la anchura y la altura del perfil de imagen.

### Nuevas funciones del canal de versión preliminar de [!DNL Assets] {#assets-prerelease-features}

* [!DNL Dynamic Media]: ahora puede utilizar la interfaz de Dynamic Media de AEM para configurar los ajustes generales y de publicación en lugar de tener que pasar por la aplicación de escritorio Dynamic Media Classic.

* [!DNL Dynamic Media] ahora es compatible con la ingesta, previsualización, reproducción y publicación de vídeos MXF. Todavía no se admite la anotación ni el vídeo de ventas para vídeos MXF.

* Después de configurar una conexión entre las implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. Ahora puede realizar las operaciones de [actualización, eliminación, cambio de nombre y movimiento](/help/assets/use-assets-across-connected-assets-instances.md) en los activos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Externalización de los datos de flujo de trabajo de AEM para un procesamiento seguro**: puede almacenar datos de flujos de trabajo AEM en el proceso (datos de variables de flujo de trabajo de AEM) que contengan elementos de datos personales sensibles (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Los elementos de datos y las variables de flujo de trabajo no se almacenan en el repositorio de AEM y se recuperan a petición de un repositorio administrado por el cliente mientras se procesa el flujo de trabajo.

### Nuevas funciones disponibles en el canal de versión preliminar de [!DNL Forms] {#prerelease-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=es) le ayudan a combinar una plantilla y los datos XML para generar documentos de impresión en distintos formatos. El servicio le permite generar documentos en modos sincrónico y por lotes.  Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:

   * Generar documentos rellenando archivos de plantilla (PDF y XDP) con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.

* **Fuentes personalizadas para documentos de registro y PDF creados con API de comunicaciones**: ahora puede utilizar fuentes aprobadas por la marca en documentos de PDF generados mediante las API de comunicaciones para cumplir con los requisitos de la organización.

* **Portal de Forms**: puede usar el [Portal de Forms](/help/forms/configure-forms-portal.md) para enumerar los formularios adaptables publicados en una página de AEM Sites. Ayuda al visitante del sitio a descubrir todos los formularios disponibles. Además, el visitante puede utilizar el portal de formularios para guardar y acceder al borrador de un formulario adaptable y consultar la versión PDF de un formulario adaptable enviado.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes extendidos de myAccount basados en los componentes Peregrine ampliables de Commerce

![Componentes de myAccount ampliados](/help/assets/CIF/extended-myAccount-components.png)

* Los autores pueden crear recomendaciones de producto de Commerce ad hoc utilizando tipos de recomendación adicionales

* Compatibilidad con tarjetas de regalo en AEM Storefront

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.11.0.

### Fecha de la versión {#release-date-cm-nov}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.11.0 es el 4 de noviembre de 2021.
La próxima versión está planificada para el 9 de diciembre de 2021.

### Novedades {#what-is-new-cm-nov}

* Los usuarios ahora pueden aprovechar las nuevas canalizaciones de front-end para implementar exclusivamente el código front-end de forma acelerada. Consulte [Canalizaciones principales de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) para obtener más información.

  >[!IMPORTANT]
  >Debe estar en la versión de AEM `2021.10.5933.20211012T154732Z` o superior para utilizar nuevas canalizaciones front-end.

* La duración de la canalización Calidad del código se reduce significativamente al realizar el análisis del código de una manera más eficiente sin necesidad de crear una imagen de AEM completa. Este cambio se implementará progresivamente durante las semanas siguientes a la publicación.

* El ID de compromiso de Git ahora se mostrará en los detalles de ejecución de la canalización, lo que facilita el seguimiento del código creado.

* La creación de programas ya está disponible a través de una API expuesta públicamente.

* La creación de entornos ya está disponible a través de una API expuesta públicamente.

* El encabezado de respuesta `x-request-id` ahora está visible en el sitio de pruebas de la API en [www.adobe.io](https://www.adobe.io/). Este encabezado es útil cuando se envían problemas de servicio de atención al cliente para la resolución de problemas.

* Como usuario, veo que la tarjeta de canalizaciones con cero canalizaciones me proporciona la guía adecuada.

* Ya está disponible una nueva página Actividad donde se pueden ver actividades como las ejecuciones de canalización y código junto con los detalles asociados. Con el tiempo, las actividades enumeradas en esta página se ampliarán en alcance junto con los detalles proporcionados.

* Ya está disponible una nueva página de canalizaciones con una ventana emergente de estado al pasar el ratón por encima para facilitar la vista del resumen de detalles. Las ejecuciones de canalización se pueden ver junto con los detalles asociados.

* La API Editar canalización ahora admite el cambio del entorno utilizado en las fases de implementación.

* Se ha introducido una optimización en el proceso de digitalización de OakPal para paquetes grandes.

* El archivo CSV del problema de calidad ahora contendrá la marca de tiempo para cada problema de calidad.

### Correcciones de errores {#bug-fixes-nov}

* Algunas configuraciones de generación no ortodoxas tuvieron como resultado que se almacenaran archivos innecesarios en la caché de artefactos Maven de la canalización, lo que resultó en I/O de red superfluas al iniciar y detener el contenedor de generación.

* La API PATCH de canalización falla si la fase de implementación no existe.

* La regla de calidad `ClientlibProxyResourceCheck` producía problemas de falsos positivos cuando había bibliotecas de cliente con rutas base comunes.

* El mensaje de error cuando se ha alcanzado el número máximo de repositorios no especificaba el motivo del error.

* En casos excepcionales, las canalizaciones fallaban debido a la gestión inadecuada de reintentos de ciertos códigos de respuesta.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.22 es el 1 de diciembre de 2021.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre la versión de ACS Commons utilizada.
* Capacidad para detectar y crear informes sobre la cantidad de usuarios y subgrupos de un grupo.
* Capacidad para detectar e informar sobre valores de propiedad de nodos en MongoDB que superen los 16 MB.

### Corrección de errores {#bug-fixes-bpa}

* La detección de componentes de Foundation se refinó para reducir los falsos negativos.
* Para los clientes de AEM Forms, se ha corregido la mensajería BPA con respecto a que `EMAIL_PDF_SUBMIT_ACTION` no está disponible en AEM as a Cloud Service.
