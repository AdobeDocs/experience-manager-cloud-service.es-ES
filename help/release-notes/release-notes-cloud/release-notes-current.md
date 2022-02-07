---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 5731337ff0edf5825860e6f76ed919b90402d88b
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 31%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.1.0) es el 3 de febrero de 2022.
La siguiente versión (2022.2.0) es el 24 de febrero de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de enero de 2022](https://video.tv.adobe.com/v/340120) vídeo para ver un resumen de las funciones añadidas en la versión 2022.1.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media]: ahora puede utilizar la interfaz de Dynamic Media de AEM para configurar los ajustes generales y de publicación en lugar de tener que pasar por la aplicación de escritorio Dynamic Media Classic.

* [!DNL Dynamic Media] ahora es compatible con la ingesta, previsualización, reproducción y publicación de vídeos MXF. Todavía no se admite la anotación ni el vídeo de ventas para vídeos MXF.

* Después de configurar una conexión entre las implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. Ahora puede realizar las operaciones de [actualización, eliminación, cambio de nombre y movimiento](/help/assets/use-assets-across-connected-assets-instances.md) en los activos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites.

### Nuevas funciones del canal de prelanzamiento de [!DNL Assets] {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] ahora proporciona la flexibilidad para [configurar una cuenta de alias](../../assets/dynamic-media/dm-alias-account.md) en la interfaz de usuario, lo que garantiza que se actualicen las URL de Dynamic Media y el código de incrustación de visor predeterminados. Esto tiene un impacto positivo en SEO, para reflejar las actualizaciones realizadas en su contexto empresarial, como el cambio de marca.

* Ahora puede usar la variable [!DNL Experience Manager Assets] interfaz de usuario para:

   * Configure la detección de recursos duplicados en un repositorio.

   * Configure la adición de marcas de agua digitales a las imágenes.

* Los administradores ahora pueden configurar el servicio de correo electrónico para las descargas grandes. Permite a los usuarios [activar notificaciones por correo electrónico para descargas grandes](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) de la variable [!DNL Experience Manager Assets] interfaz. El usuario recibe una notificación por correo electrónico que contiene el vínculo de descarga de la carpeta zip archivada al finalizar el proceso de descarga.


* La variable [Administrar publicación](/help/assets/manage-publication.md) se mejora con una interfaz de usuario mejorada. Los usuarios pueden publicar o cancelar la publicación de contenido desde y hacia el destino seleccionado, [Añadir contenido](/help/assets/manage-publication.md#add-content) a la lista de publicaciones desde el repositorio de DAM, [Incluir configuración de carpeta](/help/assets/manage-publication.md#include-folder-settings) para publicar contenido de las carpetas seleccionadas y aplicar filtros, y [programar publicación](/help/assets/manage-publication.md#publish-assets-later) a una fecha u hora posterior.

### Corrección de errores {#bug-fixes}

* Los recursos sin procesar sin representación original se envían a Asset compute para su procesamiento mientras migran recursos de AEM local a servicios en la nube.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=es) le ayudan a combinar una plantilla y los datos XML para generar documentos de impresión en distintos formatos. El servicio le permite generar documentos en modos sincrónico y por lotes. Las API le permiten crear aplicaciones con las que puede:

   * Genere documentos rellenando archivos de plantilla con datos XML.
   * Genere formularios en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere PDF de impresión a partir de PDF de formularios XFA.
   * Genere documentos de PDF, PostScript, PCL y ZPL de forma masiva combinando varios conjuntos de datos con plantillas de origen.

* **Fuentes personalizadas para documentos de registro y PDF creados con API de comunicaciones**: ahora puede utilizar fuentes aprobadas por la marca en documentos de PDF generados mediante las API de comunicaciones para cumplir con los requisitos de la organización.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **[API del ensamblador](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/References/assembler-sync/)**: Las API del ensamblador permiten combinar, reorganizar, aumentar y obtener información sobre documentos del PDF.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes myAccount mejorados
* El componente Recomendación de producto admite tipos de página adicionales (página de inicio, carro de compras, confirmación de pedido)
* **Lista de artículos deseados**
   * Los visitantes con sesión iniciada pueden agregar productos a una lista de deseos
   * La administración de la lista de deseos y sus productos es posible a través de myAccount
   * El botón &quot;Agregar a la lista de deseos&quot; se puede activar o desactivar en un nivel de componente mediante una directiva (por ejemplo, teaser de productos, detalles de productos)
   * Disponible como componente principal y en la Tienda Venia AEM

![Lista de artículos deseados](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.01.0 es el 20 de enero de 2022. La próxima versión está prevista para el 10 de febrero de 2022.

### Novedades {#what-is-new-cm}

* Cloud Manager [evite la reconstrucción del código base cuando detecte que se utiliza la misma confirmación git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) en varias ejecuciones de canalización de pila completa.
* El acceso al registro de entorno de AEM ahora requiere la variable **Administrador de implementación** perfil de producto. Los usuarios sin este perfil verán un botón deshabilitado en la interfaz de usuario.
* La interfaz de usuario no permitirá la configuración de canalización de front-end para un programa en el que Sites no esté habilitado como solución.
* Al generar una contraseña de git, se muestra la fecha de caducidad.

### Corrección de errores {#bug-fixes-cm}

* Se han corregido las excepciones de puntero nulo encontradas en algunas implementaciones de canalización de front-end.
* Ahora se pueden agregar, actualizar y eliminar variables de entorno cuando un entorno ejecuta una versión obsoleta de AEM.
* El paso crear imagen ya no se marcará como ERROR para las canalizaciones que usaron el paso programado en algunos casos excepcionales.
* Para los programas con un solo repositorio, la pantalla de ejecución de la canalización ahora mostrará el nombre del repositorio.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.8.6 es el 3 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Validación de contenido : los usuarios tienen la capacidad de determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se ha introducido correctamente en la instancia de destino. Para utilizar esta función, deberá activarla en la variable `System Console` del entorno de AEM de origen. Consulte [Validación de transferencias de contenido: introducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) para obtener más información.

### Corrección de errores {#bug-fixes-ctt}

* Algunos usuarios no estaban asignados porque la asignación de usuarios distinguía entre mayúsculas y minúsculas. Esto se ha solucionado. La asignación de usuarios ya no distingue entre mayúsculas y minúsculas.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.24 es el 1 de febrero de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar y crear informes sobre la cantidad de recursos con y sin etiquetas inteligentes.
* Capacidad para detectar e informar sobre la versión del componente principal utilizado.
* Capacidad para detectar e informar sobre el tipo de nivel de origen (autor o publicación) en el que se ejecutó BPA.

### Corrección de errores {#bug-fixes-bpa}

* La lógica de tamaño de BPA se hizo más rápida y eficiente.
* En algunos casos, el BPA no incrementó el recuento analizado cuando se ejecutó. Esto se ha solucionado.
