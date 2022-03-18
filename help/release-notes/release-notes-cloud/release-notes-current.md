---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 85%

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

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.1.0) es el 3 de febrero de 2022.
La de la siguiente versión (2022.3.0) es la del 31 de marzo de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo [Información general sobre la versión de enero de 2022](https://video.tv.adobe.com/v/340120) para ver un resumen de las funciones añadidas en la versión 2022.1.0.

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* El botón **[Habilitar canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** está disponible en el carril **Sitio** de la consola Sitios para sitios que usan la versión 2 del componente principal de página. Este botón configura el sitio para cargar los temas que se implementan con la canalización de front-end sobre las bibliotecas de cliente existentes.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media]: ahora puede utilizar la interfaz de Dynamic Media de AEM para configurar los ajustes generales y de publicación en lugar de tener que pasar por la aplicación de escritorio Dynamic Media Classic.

* [!DNL Dynamic Media] ahora es compatible con la ingesta, previsualización, reproducción y publicación de vídeos MXF. Todavía no se admite la anotación ni el vídeo de ventas para vídeos MXF.

* Después de configurar una conexión entre las implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. Ahora puede realizar las operaciones de [actualización, eliminación, cambio de nombre y movimiento](/help/assets/use-assets-across-connected-assets-instances.md) en los activos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites.

### Nuevas funciones del canal de prelanzamiento de [!DNL Assets] {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] ahora proporciona la flexibilidad para [configurar una cuenta de alias](../../assets/dynamic-media/dm-alias-account.md) en la interfaz de usuario, lo que garantiza que se actualicen de forma predeterminada las URL de Dynamic Media y el código de incrustación de visor. Esto tiene un impacto positivo en el SEO, para reflejar las actualizaciones realizadas en su contexto empresarial, como el cambio de marca.

* Ahora puede usar la interfaz de usuario de [!DNL Experience Manager Assets] para:

   * Configure la detección de recursos duplicados en un repositorio.

   * Configure la adición de marcas de agua digitales a las imágenes.

* Los administradores ahora pueden configurar el servicio de correo electrónico para las descargas grandes. Permite a los usuarios [activar notificaciones por correo electrónico para descargas grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) desde la interfaz de [!DNL Experience Manager Assets]. El usuario recibe una notificación por correo electrónico que contiene el vínculo de descarga de la carpeta zip archivada al finalizar el proceso de descarga.


* La función [Administrar publicación](/help/assets/manage-publication.md) se amplía con una interfaz de usuario mejorada. Los usuarios pueden publicar o cancelar la publicación de contenido desde y hacia el destino seleccionado, [Añadir contenido](/help/assets/manage-publication.md#add-content) a la lista de publicaciones desde el repositorio de DAM, [Incluir configuración de carpeta](/help/assets/manage-publication.md#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, así como [programar la publicación](/help/assets/manage-publication.md#publish-assets-later) a una fecha u hora posterior.

### Corrección de errores {#bug-fixes}

* Los recursos sin procesar sin representación original se envían a Asset Compute para su procesamiento mientras migran recursos de AEM local a servicios en la nube.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=es) le ayudan a combinar una plantilla y los datos XML para generar documentos de impresión en distintos formatos. El servicio le permite generar documentos en modos sincrónico y por lotes. Las API le permiten crear aplicaciones con las que puede:

   * Generar documentos rellenando archivos de plantilla con datos XML.
   * Generar formularios en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Generar PDF de impresión a partir de PDF de formularios XFA.
   * Generar documentos PDF, PostScript, PCL y ZPL por lotes combinando varios conjuntos de datos con plantillas de origen.

* **Fuentes personalizadas para documentos de registro y PDF creados con API de comunicaciones**: ahora puede utilizar fuentes aprobadas por la marca en documentos de PDF generados mediante las API de comunicaciones para cumplir con los requisitos de la organización.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **[API del ensamblador](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: las API del ensamblador permiten combinar, reorganizar, aumentar y obtener información acerca de documentos PDF.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes myAccount mejorados
* El componente Recomendación de producto admite tipos de página adicionales (página de inicio, carro de compras, confirmación de pedido)
* **Lista de deseos**
   * Los visitantes con sesión iniciada pueden añadir productos a una lista de deseos
   * La administración de la lista de deseos y sus productos es posible a través de myAccount
   * El botón Añadir a la lista de deseos se puede activar o desactivar en un nivel de componente mediante una directiva (por ejemplo, teaser de productos, detalles de productos
   * Disponible como componente principal y en la AEM Venia Storefront

![Lista de deseos](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2022.01.0 es el 20 de enero de 2022. La próxima versión está planificada para el 10 de febrero de 2022.

### Novedades {#what-is-new-cm}

* Cloud Manager [evitará la reconstrucción del código base cuando detecte que se utiliza la misma confirmación git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) en varias ejecuciones de canalización full-stack.
* El acceso al registro de entorno de AEM ahora requiere el perfil de producto de **Administrador de implementación**. Los usuarios sin este perfil verán un botón deshabilitado en la interfaz de usuario.
* La IU no permitirá la configuración de canalización front-end para un programa en el que Sites no esté habilitado como solución.
* Al generar una contraseña de git, se muestra la fecha de caducidad.

### Corrección de errores {#bug-fixes-cm}

* Se han corregido las excepciones de puntero nulo encontradas en algunas implementaciones de canalización front-end.
* Ahora se pueden añadir, actualizar y eliminar variables de entorno cuando un entorno ejecuta una versión obsoleta de AEM.
* El paso de crear imagen ya no se marcará como ERROR para las canalizaciones que usaron el paso programado en algunos casos excepcionales.
* Para los programas con un solo repositorio, la pantalla de ejecución de la canalización ahora mostrará el nombre del repositorio.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.8.6 es el 3 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Validación de contenido: los usuarios tienen la capacidad de determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se ha introducido correctamente en la instancia de destino. Para utilizar esta función, deberá activarla en la `System Console` del entorno de AEM de origen. Consulte [Validación de transferencias de contenido: introducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=es#getting-started) para obtener más información.

### Corrección de errores {#bug-fixes-ctt}

* Algunos usuarios no estaban asignados porque la asignación de usuarios distinguía entre mayúsculas y minúsculas. Esto se ha solucionado. La asignación de usuarios ya no distingue entre mayúsculas y minúsculas.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.26 es el 16 de marzo de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar recursos no procesados. Si se detectan recursos no procesados, estos deben configurarse para procesarse o deben eliminarse del conjunto de migración durante la transferencia de contenido para evitar tener problemas durante la ingesta de contenido.
* Capacidad para detectar si el contenido tiene más de 1000 URL de vanidad. No se recomienda utilizar un número elevado de URL de vanidad, ya que pone una carga en los servidores de Dispatcher y Publish.
* Capacidad para identificar problemas relacionados con las definiciones de índices de Oak y detectar incompatibilidades con AEM as a Cloud Service.
* Capacidad para detectar e informar sobre el uso de configuraciones de externalizador. En AEM configuración de externalizador as a Cloud Service la establece Cloud Manager, por lo tanto, las configuraciones de externalizador existentes deben refactorizarse para mantener la compatibilidad.

### Corrección de errores {#bug-fixes-bpa}

* En algunos casos, BPA no se pudo ejecutar debido a que FormsSelectiveFeaturesAnalysis arrojó un error de aserción. Esto se ha solucionado.
* La BPA estaba presentando conclusiones relacionadas con el patrón de trabajo como PRINCIPAL en lugar de CRÍTICO. Esto se ha solucionado.
* BPA informaba incorrectamente de los resultados relacionados con las definiciones de índice OAK en ui.apps como CRITICAL. Esto se ha solucionado
