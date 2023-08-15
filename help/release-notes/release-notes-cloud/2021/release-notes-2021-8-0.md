---
title: Notas de la versión 2021.8.0 de la versión de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2021.8.0 de la versión de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 49%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] La versión actual (2021.8.0) es el 26 de agosto de 2021.
La de la siguiente versión (2021.9.0) es la del 6 de octubre de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general de la versión de agosto de 2021](https://video.tv.adobe.com/v/336277) para ver un resumen de las funciones añadidas.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Al compartir recursos digitales como vínculo, los usuarios pueden copiar la URL en el portapapeles de inmediato. La mejora permite compartir recursos de una manera más rápida y práctica. Esta funcionalidad permite un uso compartido de recursos más rápido y conveniente.

  ![Opción Copiar URL al compartir un recurso como vínculo](/help/assets/assets/link-share-copy-URL-option.png)
  *Imagen: al compartir un recurso como vínculo, ahora puede copiar la URL para compartirlo por separado.*

* Al cargar archivos TXT, los microservicios de recursos generan automáticamente una miniatura. La miniatura en PNG es una representación del archivo TXT que ayuda a los usuarios a identificar el contenido o los archivos en cierta medida, sin necesidad de abrir los archivos. Esta funcionalidad no requiere ninguna configuración y funciona de forma predeterminada.

  ![Una representación de un archivo TXT se genera automáticamente mediante [!DNL Assets] en formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Imagen: se genera automáticamente una representación de un archivo TXT para ayudarle a identificar el archivo sin abrirlo.*

### Nueva función en la [!DNL Assets] canal de prelanzamiento {#assets-prerelease-features}

* Ahora puede ordenar los recursos mostrados en los resultados de búsqueda en las vistas Columna y Tarjeta. El orden funciona en las columnas Nombre, Creada, Modificada o Ninguna.

  ![Ordenar los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta](/help/assets/assets/sort-searched-assets.png)
  *Imagen: ordenación de los resultados de búsqueda en [!DNL Assets] en las vistas Columna y Tarjeta.*

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

* Cuando un miembro del grupo colaborador navega al [!DNL Assets] Consola, un extra `POST` Se ha generado una solicitud para crear una colección. Esta solicitud no es necesaria; falla debido a problemas de permisos y crea muchos errores en los registros. (CQ-4328856)
* Cuando los usuarios vean un recurso y seleccionen [!UICONTROL Cronología] en el menú emergente del panel izquierdo, se muestra un error. En los registros, se registran muchas advertencias debido a una consulta incorrecta. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* El servicio de automated forms conversion puede [convertir PDF forms en italiano y portugués](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#language-specific-meta-model) a Forms adaptable.

* **Documento de registro basado en Acrobat**: Compatibilidad de AEM Forms as a Cloud Service con [formularios PDF de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=es) como plantilla para documentos de registro además de la plantilla de formulario basada en XFA.

* **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el modelo de datos de formulario al almacenamiento de Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=es). Permite recuperar y almacenar datos de formulario adaptables en el almacenamiento de Microsoft Azure como BLOB.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Utilizar funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para el nivel de servicio empresarial tiene la opción de ampliar las funciones de los destinatarios del contrato, más allá del firmante, para que coincidan mejor con los requisitos del flujo de trabajo. Ahora puede permitir que cada destinatario del acuerdo configure su función en un formulario adaptable, siendo la de firmante la función predeterminada.

* **Analytics para formularios adaptables**: Ahora puede capturar y hacer un seguimiento del comportamiento del usuario final mediante Adobe Analytics para que el formulario adaptable recopile información del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

* **Conecte fácilmente AEM Forms con Microsoft Dynamics y Salesforce.com**: El servicio proporciona una configuración de fuente de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce.com, lo que permite a los desarrolladores configurar Microsoft Dynamics y Salesforce.com como fuentes de datos para un formulario adaptable de forma más rápida y sencilla.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva interfaz de usuario del selector de categorías para mejorar la experiencia del usuario, aumentar la eficacia y ofrecer una mejor compatibilidad con catálogos de productos complejos

  ![Selector de nueva categoría](/help/assets/CIF/category-picker.png)

* Mejor compatibilidad con A11Y para los componentes principales del CIF

## Cloud Manager {#cloud-manager}

AEM Esta sección describe las notas de la versión para Cloud Manager en las versiones 2021.8.0 y 2021.7.0 de as a Cloud Service.

## Fecha de lanzamiento {#release-date-cm-aug}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.
La próxima versión está planificada para el 9 de septiembre de 2021.

### Novedades {#what-is-new-aug}

* Los clientes de Cloud Service ahora pueden ver los informes del Contrato de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible progresivamente en los próximos meses.
Consulte los [Informes de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html?lang=es) para obtener más información.

* El tipo y la gravedad del IndexType y `IndexDamAssetLucene` las reglas de calidad se han cambiado. Estos son ahora los dos errores de Blocker *serverity*.

* Se han introducido nuevas reglas de calidad del índice Oak para cubrir configuraciones asincrónicas y tika.

* Aumento del número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios a través de la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la generación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del arquetipo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 29.

### Correcciones de errores {#bug-fixes-aug}

* “Actualizar el estado disponible” no se debe mostrar cuando la última versión sea anterior a la versión actual.

* La incorporación inicial fallaba para nuevas organizaciones con nombres muy largos.

* En ocasiones, cuando una canalización se activa dos veces por alguna razón, el resultado es que una de las ejecuciones falla y muestra el error *no se puede actualizar el estado de ejecución de la canalización*.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.5.6 es el 11 de agosto de 2021.

### Correcciones de errores {#bug-fixes-ctt}

* En algunos casos, no todos los usuarios se migraron a la instancia de destino. AEM Para obtener esta corrección, se requiere CTT v1.5.6 junto con aem-ethos-tools 1.2.354 o una versión posterior en la instancia as a Cloud Service de Target.

* El **Detener ingesta** Se estaba desactivando el botón durante la ingesta en la instancia de publicación. Esto no es necesario porque no hay ningún paso de restauración durante la ingesta de Publish.

* El CTT no limpió el `/tmp` después de una extracción correcta. Esto a veces provocaba problemas de espacio en disco.
