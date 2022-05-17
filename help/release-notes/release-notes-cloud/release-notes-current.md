---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 4fce645a436f820181fd3f0b98c1826e2e1b7195
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 30%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.4.0) es el 5 de mayo de 2022.
La próxima versión (2022.5.0) está planificada para el 2 de junio de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de abril de 2022](https://video.tv.adobe.com/v/342612?quality=12) vídeo para ver un resumen de las funciones añadidas en la versión 2022.4.0.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* Los tipos de datos del modelo de contenido ahora se pueden definir como [traducible](/help/assets/content-fragments/content-fragments-models.md#properties) uso de una casilla de verificación sencilla en el editor de modelos de contenido. Además, AEM reglas y configuraciones de traducción se actualizan automáticamente.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Ahora puede [ordenar etiquetas](/help/assets/organize-assets.md#use-tags-to-organize-assets) en la ventana del selector de etiquetas en orden ascendente o descendente, según el nombre de la etiqueta, la fecha de creación o la fecha de modificación.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Comunicaciones: Compatibilidad con las API de manipulación de documentos en el SDK as a Cloud Service de Forms**: [API de manipulación de documentos](/help/forms/aem-forms-cloud-service-communications.md) ayuda a combinar, reorganizar y validar documentos de PDF. Ahora puede utilizar las API de Communications - Document Generation en un entorno de desarrollo local con la ayuda del SDK as a Cloud Service de AEM Forms.

* **Usar XCI personalizados para generar un documento de registro**[: ahora puede utilizar un archivo XCI personalizado para establecer varias propiedades de un documento de registro](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Anula el XCI maestro con los cambios personalizados. Proporciona más control sobre la generación de Documentos de Registro, lo que aumenta la personalización y las oportunidades de personalización.

* **Utilizar un CAPTCHA invisible en un formulario adaptable**[: puede utilizar un CAPTCHA invisible para mostrar una prueba CAPTCHA solo en el caso de actividad sospechosa](/help/forms/captcha-adaptive-forms.md). Si no se encuentra ninguna actividad sospechosa, no se muestra el desafío CAPTCHA. Ayuda a evaluar la cumplimentación de formularios humanos sin requisitos de casilla de verificación, reducir los esfuerzos de personalización y mejorar la experiencia del usuario final.

* **Configuraciones del modelo de datos de formulario**: Ahora puede [reutilizar las configuraciones del modelo de datos de formulario en entornos](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config), simplificar las integraciones de datos y reducir los costes de TI.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Acceso rápido a la cabina de productos: Acceda fácilmente a la información detallada completa del producto con un solo clic en el Editor de sitios

   ![Habilitar lista de deseos](/help/assets/CIF/enable-wishlist.png)

* Compatibilidad con componentes de comercio de marketing adicionales: Los componentes se pueden configurar para mostrar una llamada a acción de complemento al carro y de complemento a la lista de deseos

   ![Acceso directo del editor de sitios a la cabina de productos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Analizadores de creación de SDK {#sdk-build-analyzers}

El complemento Maven de AEM as a Cloud Service SDK Build Analyzer detecta problemas en un proyecto maven, incluidas dependencias que faltan. Proporciona a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en entornos de nube con Cloud Manager.

Se ha añadido recientemente un nuevo analizador:

* `content-packages-validation` : valida la sintaxis y estructura del contenido bien formadas para los paquetes que se instalarán durante la implementación

Se recomienda actualizar el proyecto maven con la última versión del analizador o incluir el analizador si aún no lo ha hecho. Para obtener más información, consulte la documentación [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] como [!DNL Cloud Service] Seguridad de la base {#foundation-security}

### Finalización del soporte para TLS 1.0 y 1.1

A partir del 30 de junio de 2022, el Experience Manager as a Cloud Service necesitará una comunicación de red más segura y un intercambio de datos con los sistemas de los usuarios. AEM usará exclusivamente Transport Layer Security (TLS), protocolo 1.2. Las versiones anteriores de TLS 1.0 y 1.1 quedarán obsoletas.

Si sigue utilizando versiones anteriores de TLS como 1.0, 1.1, podría perder el acceso al Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [here](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
