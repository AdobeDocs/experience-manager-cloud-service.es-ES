---
title: Notas de la versión 2021.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 27%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede ir a las notas de versiones anteriores. Por ejemplo, para los de 2020 y 2021.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.8.0) es el viernes, 26 de agosto de 2021.
La de la siguiente versión (2021.9.0) es el jueves, 06 de octubre de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo [Información general sobre la versión de agosto de 2021](https://video.tv.adobe.com/v/336277) para ver un resumen de las funciones añadidas.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Al compartir recursos digitales como vínculo, el usuario puede copiar la URL en el portapapeles de inmediato. La mejora permite compartir recursos de una manera más rápida y práctica. Esta funcionalidad permite un uso compartido de recursos más rápido y conveniente.

  ![Copiar opción de URL al compartir un recurso como vínculo](/help/assets/assets/link-share-copy-URL-option.png)
  *Imagen: al compartir un recurso como vínculo, ahora puede copiar la dirección URL para compartirlo por separado.*

* Al cargar archivos TXT, los microservicios de recursos generan automáticamente una miniatura. La miniatura en PNG es una representación de un archivo TXT que ayuda a los usuarios a identificar el contenido o los archivos en cierta medida, sin necesidad de abrir los archivos. Esta funcionalidad no requiere ninguna configuración y funciona de forma predeterminada.

  ![[!DNL Assets] genera automáticamente una representación de un archivo TXT en formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Imagen: se genera automáticamente una representación de un archivo TXT para ayudarle a identificar el archivo sin necesidad de abrirlo.*

### Nueva característica en el canal de prelanzamiento [!DNL Assets] {#assets-prerelease-features}

* Ahora puede ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. El orden funciona en las columnas Nombre, Creada, Modificada o Ninguna.

  ![Ordenar los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta](/help/assets/assets/sort-searched-assets.png)
  *Imagen: ordena los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta.*

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Cuando un miembro del grupo colaborador navega a la consola [!DNL Assets], se genera una solicitud `POST` adicional para crear una colección. Esta solicitud no es necesaria; falla debido a problemas de permisos y crea muchos errores en los registros. (CQ-4328856)
* Cuando los usuarios ven un recurso y seleccionan [!UICONTROL Cronología] en el menú emergente del panel izquierdo, se muestra un error. En los registros, se registran muchas advertencias debido a una consulta incorrecta. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* El servicio de automated forms conversion puede [convertir PDF forms en italiano y portugués](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#language-specific-meta-model) a Forms adaptable.

* **Documento de registro basado en Acrobat**: Compatibilidad de AEM Forms as a Cloud Service con [formularios PDF de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=es) como plantilla para documentos de registro además de la plantilla de formulario basada en XFA.

* **Conector del almacén de datos de Microsoft® Azure**: Ahora puede [conectar el modelo de datos de formulario a Microsoft® Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=es). Permite recuperar y almacenar datos de formulario adaptables en Microsoft® Azure Storage como BLOB.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Usar funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para los niveles de servicio empresarial y empresarial puede, opcionalmente, expandir las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Ahora puede permitir que cada destinatario del acuerdo configure su función en un formulario adaptable, siendo la de firmante la función predeterminada.

* **Analytics para Forms adaptable**: ahora puede capturar y rastrear el comportamiento del usuario final mediante Adobe Analytics para Forms adaptable con el fin de recopilar información del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conecte fácilmente AEM Forms con Microsoft® Dynamics y Salesforce.com**. El servicio proporciona la configuración de fuentes de datos y modelos de datos predeterminados para Microsoft® Dynamics y Salesforce.com. Esto hace que sea más rápido y fácil para los desarrolladores configurar Microsoft® Dynamics y Salesforce.com como fuentes de datos para un formulario adaptable.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y ofrecer una mejor compatibilidad con catálogos de productos complejos

  ![Selector de categoría nueva](/help/assets/CIF/category-picker.png)

* CIF Mejor compatibilidad con A11Y para los componentes principales de la

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.8.0 y 2021.7.0.

## Fecha de lanzamiento {#release-date-cm-aug}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.
La próxima versión está planificada para el 9 de septiembre de 2021.

### Novedades {#what-is-new-aug}

* Los clientes de Cloud Service ahora pueden ver los informes del Contrato de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible de forma progresiva en los próximos meses.
Consulte la [creación de informes de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html?lang=es).

* El tipo y la gravedad del IndexType y las reglas de calidad de `IndexDamAssetLucene` han cambiado. Estos son ahora errores del bloqueador *gravedad*.

* Se han introducido nuevas reglas de calidad del índice Oak para cubrir configuraciones asincrónicas y Tika.

* Aumento del número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios mediante la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la generación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del arquetipo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 29.

### Correcciones de errores {#bug-fixes-aug}

* Actualizar el estado disponible no debería aparecer si la última versión es anterior a la versión actual.

* La incorporación inicial fallaba para nuevas organizaciones con nombres largos.

* En ocasiones, cuando una canalización se activa dos veces por alguna razón, el resultado es que una de las ejecuciones falla con un error *`cannot update pipeline execution status`*.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.5.6 es el 11 de agosto de 2021.

### Correcciones de errores {#bug-fixes-ctt}

* En ocasiones, no todos los usuarios se migraban a la instancia de destino. Para obtener esta corrección, se requiere CTT v1.5.6 junto con aem-ethos-tools 1.2.354 o una versión posterior en la instancia de AEM as a Cloud Service de destino.

* El botón **Detener ingesta** se estaba deshabilitando durante la ingesta en la instancia de Publish. Esto no es necesario porque no hay ningún paso de restauración durante la ingesta de Publish.

* CTT no limpió el directorio `/tmp` después de una extracción correcta. Esto a veces provocaba problemas de espacio en disco.
