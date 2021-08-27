---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 2451a29b71b113f28ffc00737ed825381dd5ad07
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 2%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] como Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.8.0) es el 26 de agosto de 2021.
La siguiente versión (2021.9.0) es el 30 de septiembre de 2021.

## Vídeo de la versión {#release-video}

Consulte el vídeo [Información general de la versión de agosto de 2021](https://video.tv.adobe.com/v/336277) para ver un resumen de las funciones agregadas.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones en [!DNL Assets] {#assets-features}

* Al compartir recursos digitales como un vínculo, los usuarios pueden copiar la URL en el portapapeles de inmediato. La mejora permite compartir recursos de una forma más rápida y práctica. Esta funcionalidad permite un uso compartido de recursos más rápido y conveniente.

   ![Opción Copiar URL al compartir un recurso como vínculo](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Al compartir un recurso como vínculo, ahora puede copiar la dirección URL para compartirlo por separado.*

* Al cargar archivos TXT, los microservicios de recursos generan automáticamente una miniatura. La miniatura PNG es una representación del archivo TXT que ayuda a los usuarios a identificar el contenido o los archivos en cierta medida, sin necesidad de abrir los archivos. Esta funcionalidad no requiere ninguna configuración y funciona de forma predeterminada.

   ![Una representación de un archivo TXT se genera automáticamente  [!DNL Assets] en formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Se genera automáticamente una representación de un archivo TXT para ayudarle a identificar el archivo sin necesidad de abrirlo.*

### Nueva función en el canal de prelanzamiento [!DNL Assets] {#assets-prerelease-features}

* Los usuarios ahora pueden ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. La ordenación funciona en las columnas Nombre, Creado, Modificado o Ninguno.

   ![Ordene los resultados de búsqueda  [!DNL Assets] en las vistas Columna y Tarjeta](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordene los resultados de búsqueda  [!DNL Assets] en las vistas Columna y Tarjeta.*

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Cuando un miembro del grupo colaborador navega a la consola [!DNL Assets] , se genera una solicitud `POST` adicional para intentar crear una colección. Esta solicitud no es necesaria, falla debido a problemas de permisos y crea muchos errores en los registros. (CQ-4328856)
* Cuando los usuarios ven un recurso y seleccionan la [!UICONTROL Línea de tiempo] en el menú emergente del panel izquierdo, se muestra un error. En los registros, se registran muchas advertencias debido a una consulta incorrecta. (CQ-4328919)

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

* AEM proyecto de tipo de archivo para Forms as a Cloud Service ahora incluye [tema de lienzo 3.0 y modelos de datos de formulario para Microsoft Dynamics y Salesforce.com](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/setup-environment/setup-local-development-environment.html?#forms-cloud-service-local-development-environment).

* **Documento de registro basado en Acrobat**: AEM Forms as a Cloud Service admite el uso de  [Adobe Acrobat Form PDF (Acrobat PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)  como plantilla para Documento de registro además de la plantilla de formulario basada en XFA.

* **Conector** del almacén de datos de Microsoft Azure: Ahora puede  [conectar el Modelo de datos de formulario al Almacenamiento](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html) de Microsoft Azure. Permite recuperar y almacenar datos de formulario adaptables en Microsoft Azure Storage as a BLOB.

### Función beta de [!DNL Forms] {#aug-what-is-new-forms-prerelease}

* **Conector de almacenamiento unificado:** utilice el conector de almacenamiento unificado para externalizar los datos en proceso en repositorios administrados por el cliente. Por ejemplo, puede
   * Habilite la funcionalidad de guardar y reanudar de Forms Portal y almacene borradores de formularios adaptables en un repositorio de datos administrado por el cliente.
   * Almacene datos de flujos de trabajo AEM en proceso (AEM datos de variables de flujo de trabajo) que contengan datos personales confidenciales (SPD) en un repositorio administrado por el cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) APIShelp permite combinar plantillas XDP y datos XML para generar documentos de impresión en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones que le permitan:
   * Genere documentos rellenando archivos de plantilla con datos XML.
   * Genere formularios de salida en varios formatos, incluidas secuencias de impresión PDF no interactivas.
   * Genere archivos PDF de impresión desde un formulario XFA PDF y un formulario Adobe Acrobat.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Nuevas funciones disponibles en el canal de prelanzamiento [!DNL Forms] {#prerelease-features-forms}

* **Uso de funciones de Adobe Sign en un formulario** adaptable: Adobe Sign para los niveles de servicio empresarial y empresarial tiene la opción de ampliar las funciones de los destinatarios del Acuerdo, más allá del Firmante, para que coincidan mejor con sus requisitos de flujo de trabajo. Ahora puede [habilitar a cada destinatario del acuerdo para que configure su función en un formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html?#addsignerstoanadaptiveform), siendo Signer la función predeterminada.

* **Analytics para Forms adaptable**: Ahora puede capturar y rastrear el comportamiento del usuario final a través de Adobe Analytics for Adaptive Forms para recopilar perspectivas del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conecte AEM Forms fácilmente con Microsoft Dynamics y Salesforce.com**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce.com, lo que facilita y  [agiliza la configuración de Microsoft Dynamics y Salesforce.com como fuentes de datos para un formulario](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html) adaptable.

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Novedades {#what-is-new-screens}

* Como autor de contenido, ahora puede definir una miniatura para los vídeos, de modo que pueda utilizar esa imagen como marcador de posición y probar correctamente la reproducción y el destino del contenido, mientras el equipo adecuado está finalizando el vídeo en sí.
Consulte [Monitorización de reproducción básica](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) para obtener más información.

* Compatibilidad con miniaturas para vídeos en ahora se admite en Screens as a Cloud Service. Un autor de contenido puede definir una miniatura para los vídeos, de modo que la imagen pueda utilizarse como marcador de posición y probar correctamente la reproducción y el destino del contenido, mientras el equipo adecuado está finalizando el vídeo en sí. También se puede utilizar la imagen en caso de que falle la reproducción del vídeo.

### Corrección de errores {#bug-fixes-screens}

* El reproductor no pudo mostrar contenido de la página integrada y este problema se ha corregido.

* Después de iniciar sesión correctamente, la navegación a la página predeterminada (canales) terminó en una página de error interno del servidor.

* Las entradas de etiquetas asociadas no se eliminaban al quitar listas de reproducción.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y mejorar la compatibilidad con catálogos de productos complejos

   ![Nuevo selector de categorías](/help/assets/CIF/category-picker.png)

* Mejor compatibilidad con A11Y para los componentes principales del CIF

## Cloud Manager {#cloud-manager}

Esta sección describe las Notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.8.0 y 2021.7.0.

## Fecha de la versión {#release-date-cm-aug}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.
La próxima versión está planificada para el 9 de septiembre de 2021.

### Novedades {#what-is-new-aug}

* Los clientes Cloud Service ahora pueden ver los informes de Acuerdo de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible progresivamente en los próximos meses.
Consulte [Informes de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para obtener más información.

* Se ha cambiado el tipo y la gravedad de las reglas de calidad IndexType y `IndexDamAssetLucene` . Estos son ahora errores del bloqueador *serverity*.

* Se han introducido nuevas reglas de calidad de índice Oak para cubrir configuraciones asincrónicas y tika.

* Aumente el número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios a través de la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la compilación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 29.

### Corrección de errores {#bug-fixes-aug}

* Actualizar el estado disponible no se debe mostrar cuando la última versión sea menor que la versión actual.

* La incorporación inicial estaba fallando para nuevas organizaciones con nombres muy largos.

* En ocasiones, cuando una canalización se activa dos veces por algún motivo, el resultado es que una de las ejecuciones falla con el error *no puede actualizar el estado de ejecución de la canalización*.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.5.6 es el 11 de agosto de 2021.

### Corrección de errores {#bug-fixes-ctt}

* En algunos casos, no todos los usuarios se migraron a la instancia de destino. Para obtener esta corrección, se requiere CTT v1.5.6 junto con aem-ethos-tools 1.2.354 o una versión posterior en el AEM de destino como instancia de Cloud Service.

* El botón **Stop Ingestion** se deshabilitaba durante la ingesta a la instancia de publicación. Esto no es necesario porque no hay ningún paso de restauración de mongo durante la ingesta de Publicar.

* CTT no limpió el directorio `/tmp` después de una extracción correcta. Esto a veces provocaba problemas de espacio en disco.

