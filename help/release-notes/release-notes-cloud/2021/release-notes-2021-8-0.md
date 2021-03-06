---
title: Notas de la versión 2021.8.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2021.8.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 12%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2021.8.0) es el 26 de agosto de 2021.
La siguiente versión (2021.9.0) es el 6 de octubre de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de agosto de 2021](https://video.tv.adobe.com/v/336277) vídeo para ver un resumen de las funciones añadidas.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Al compartir recursos digitales como un vínculo, los usuarios pueden copiar la URL en el portapapeles de inmediato. La mejora permite compartir recursos de una forma más rápida y práctica. Esta funcionalidad permite un uso compartido de recursos más rápido y conveniente.

   ![Opción Copiar URL al compartir un recurso como vínculo](/help/assets/assets/link-share-copy-URL-option.png)
   *Figura: Al compartir un recurso como vínculo, ahora puede copiar la dirección URL para compartirlo por separado.*

* Al cargar archivos TXT, los microservicios de recursos generan automáticamente una miniatura. La miniatura PNG es una representación del archivo TXT que ayuda a los usuarios a identificar el contenido o los archivos en cierta medida, sin necesidad de abrir los archivos. Esta funcionalidad no requiere ninguna configuración y funciona de forma predeterminada.

   ![Una representación de un archivo TXT se genera automáticamente mediante [!DNL Assets] en formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
   *Figura: Se genera automáticamente una representación de un archivo TXT para ayudarle a identificar el archivo sin necesidad de abrirlo.*

### Nueva función en la [!DNL Assets] canal de prelanzamiento {#assets-prerelease-features}

* Los usuarios ahora pueden ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. La ordenación funciona en las columnas Nombre, Creado, Modificado o Ninguno.

   ![Ordene los resultados de búsqueda en [!DNL Assets] en las vistas de columna y de tarjeta](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordene los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta.*

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Cuando un miembro del grupo colaborador navega al [!DNL Assets] Consola, una `POST` se genera para intentar crear una colección. Esta solicitud no es necesaria, falla debido a problemas de permisos y crea muchos errores en los registros. (CQ-4328856)
* Cuando los usuarios vean un recurso, seleccione la [!UICONTROL Cronología] en el menú emergente del panel izquierdo, se muestra un error. En los registros, se registran muchas advertencias debido a una consulta incorrecta. (CQ-4328919)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* el servicio de automated forms conversion puede [convertir PDF forms en italiano y portugués](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) a Forms adaptable.

* **Documento de registro basado en Acrobat**: Compatibilidad as a Cloud Service con AEM Forms [PDF de formularios de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como plantilla para Document of Record además de la plantilla de formulario basada en XFA.

* **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el Modelo de datos de formulario al almacenamiento de Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Permite recuperar y almacenar datos de formulario adaptables en Microsoft Azure Storage as a BLOB.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Uso de funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para los niveles de servicio empresarial y empresarial tiene la opción de ampliar las funciones de los destinatarios del Acuerdo, más allá del Firmante, para que coincidan mejor con sus requisitos de flujo de trabajo. Ahora puede habilitar a cada destinatario del acuerdo para que configure su función en un formulario adaptable, siendo Signer la función predeterminada.

* **Analytics para Forms adaptable**: Ahora puede capturar y rastrear el comportamiento del usuario final a través de Adobe Analytics for Adaptive Forms para recopilar perspectivas del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conexión sencilla de AEM Forms con Microsoft Dynamics y Salesforce.com**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce.com, lo que facilita y agiliza la configuración de Microsoft Dynamics y Salesforce.com como fuentes de datos para un formulario adaptable.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y mejorar la compatibilidad con catálogos de productos complejos

   ![Nuevo selector de categorías](/help/assets/CIF/category-picker.png)

* Mejor compatibilidad con A11Y para los componentes principales del CIF

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.8.0 y 2021.7.0.

## Fecha de la versión {#release-date-cm-aug}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.
La próxima versión está planificada para el 9 de septiembre de 2021.

### Novedades {#what-is-new-aug}

* Los clientes Cloud Service ahora pueden ver los informes de Acuerdo de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible progresivamente en los próximos meses.
Consulte [Informes de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para obtener más información.

* Tipo y gravedad del IndexType y `IndexDamAssetLucene` se han cambiado las reglas de calidad. Estos son ahora los dos errores de Blocker *serverity*.

* Se han introducido nuevas reglas de calidad de índice Oak para cubrir configuraciones asincrónicas y tika.

* Aumente el número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios a través de la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la compilación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 29.

### Corrección de errores {#bug-fixes-aug}

* Actualizar el estado disponible no se debe mostrar cuando la última versión sea menor que la versión actual.

* La incorporación inicial estaba fallando para nuevas organizaciones con nombres muy largos.

* En ocasiones, cuando una canalización se activa dos veces por alguna razón, el resultado es que una de las ejecuciones falla con *no se puede actualizar el estado de ejecución de la canalización* error.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.5.6 es el 11 de agosto de 2021.

### Corrección de errores {#bug-fixes-ctt}

* En algunos casos, no todos los usuarios se migraron a la instancia de destino. Para obtener esta corrección, se requiere CTT v1.5.6 junto con aem-ethos-tools 1.2.354 o una versión posterior en la instancia as a Cloud Service de AEM de destino.

* La variable **Detener Ingesta** se deshabilitaba durante la ingesta a la instancia Publicar . Esto no es necesario porque no hay ningún paso de restauración de mongo durante la ingesta de Publicar.

* CTT no limpió el `/tmp` después de una extracción correcta. Esto a veces provocaba problemas de espacio en disco.
