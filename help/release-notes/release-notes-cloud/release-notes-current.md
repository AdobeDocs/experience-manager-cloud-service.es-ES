---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: b72d5fca4113f6d3b9cbabab655e36f2370231d9
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 42%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2024.11.0) de [!DNL Cloud Service] es el viernes, 21 de noviembre de 2024. La próxima versión de la funcionalidad (2024.12.0) está planificada para el viernes, 12 de diciembre de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the November 2024 Release Overview video for a summary of the features added in the 2024.11.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]plantillas de página con creación de editor universal**

Convierta rápidamente cualquier página de Edge Delivery en una plantilla de página. Esto le permite iniciar una nueva página con una estructura y contenido predefinidos en lugar de una página en blanco. [Más información](/help/sites-cloud/authoring/universal-editor/templates.md).

AEM Importador de CSV **[!DNL Edge Delivery Services]para la publicación a través de una instancia de**

Administre sus datos de hojas de cálculo de Edge Delivery AEM de forma eficaz (p. ej., redirecciones) en su herramienta de hoja de cálculo favorita y cárguelos a través del nuevo importador de CSV a la hora de cargar los datos en su archivo de hoja de cálculo a través del nuevo importador de CSV. [Más información](/help/edge/wysiwyg-authoring/tabular-data.md#importing).

### Programa para primeros usuarios {#sites-early-adopter}

**AEM REST OpenAPI para la entrega de fragmentos de contenido**

[AEM REST OpenApi para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md), ya está disponible para AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funciones de acceso anticipado en Dynamic Media {#dm-early-access}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. La IA analiza la pista de audio del vídeo para transcribir la voz y crear subtítulos, que se pueden editar para mejorar la precisión o la personalización. Estos subtítulos ayudan a cumplir con los requisitos de accesibilidad y mejorar la participación en vídeo de los públicos que dependen de la compatibilidad con vídeo basado en texto o la prefieren.

Para obtener acceso anticipado a la compatibilidad con subtítulos generados por IA en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](/help/assets/dynamic-media/video.md##enable-dash).

**informe de envío de Dynamic Media**

Obtenga perspectivas de entrega para los recursos entregados con Dynamic Media, con recuento de entregas a nivel de recurso, información de referencia, ruta de recursos en AEM Assets e ID de recurso único. Se pueden generar informes para todos los recursos entregados mediante Dynamic Media para el repositorio de AEM Assets o para una jerarquía de carpetas específica en AEM Assets. Las perspectivas ayudan a medir el retorno de la inversión de los recursos entregados, medir el rendimiento del canal y realizar tareas de administración de recursos informadas para los recursos.

Para obtener acceso anticipado al informe de entrega de Dynamic Media en su cuenta de Dynamic Media, [cree y envíe un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Panel de Dynamic Media**

La vista de Assets ahora le permite acceder a Dynamic Media y Dynamic Media con representaciones de OpenAPI desde un panel independiente disponible. Puede copiar la dirección URL de envío o descargar las representaciones en función del recurso y el tipo de representación. Para obtener más información, consulte [representaciones de Dynamic Media](/help/assets/renditions.md#dynamic-media-renditions) y [representaciones de Dynamic Media con capacidades de OpenAPI](/help/assets/renditions.md#dm-with-openapi-renditions).

![representaciones dinámicas](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms {#forms-new-features}

* **[Actualizar los ámbitos de Adobe Sign fácilmente](/help/forms/adobe-sign-integration-adaptive-forms.md)**: puede modificar los ámbitos de una configuración de Adobe Sign directamente desde la página Configuraciones de nube de AEM, lo que facilita y agiliza la actualización de las configuraciones existentes.

* **[Compatibilidad con funciones asincrónicas para formularios adaptables](/help/forms/using-async-funct-in-rule-editor.md)**: cuando el formulario adaptable requiera operaciones asincrónicas, como esperar procesos externos o recuperar datos, puede implementar estas operaciones con funciones personalizadas y configurarlas en el Editor de reglas.

### Funciones previas al lanzamiento en AEM Forms {#forms-new-prerelease-features}

* **Administrar publicación**: puede usar el flujo de trabajo Administrar publicación para publicar o cancelar la publicación de formularios en entornos, generalmente desde la instancia de autor a las instancias de publicación y vista previa. Permite a los usuarios publicar, cancelar la publicación o programar la publicación de contenido de una manera optimizada.

* **[Guardar automáticamente un borrador para formularios adaptables basados en componentes principales](/help/forms/save-core-component-based-form-as-draft.md)**: los usuarios ahora pueden beneficiarse de una función de guardado automático que guarda automáticamente un formulario parcialmente completado como borrador. Pueden volver más tarde para terminar de rellenarlo en el mismo dispositivo o en otro distinto. Esta función mejora las tasas de conversión para las organizaciones al reducir el abandono de formularios, ya que los usuarios no tienen que volver a empezar a rellenar el formulario desde el principio.

* **[Mejoras del editor de reglas](/help/forms/invoke-service-enhancements-rule-editor.md)**: para Forms adaptable basado en componentes principales, ahora puede rellenar opciones desplegables usando la salida de Invocar servicio, establecer paneles repetibles usando la salida de Invocar servicio, establecer paneles individuales usando la salida de Invocar servicio y usar el parámetro de salida de Invocar servicio para validar otros campos.

* **[Mejorar la experiencia del usuario con botones de navegación en los diseños de panel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: ahora puede añadir botones de navegación a los diseños de panel, como Pestañas horizontales, Pestañas verticales, Acordeones o el Asistente. Estos botones mejoran la experiencia del usuario al simplificar las transiciones entre paneles y se centran en el panel seleccionado.


### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo. 

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Integraciones

* **[Integrar Forms adaptable con Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**: AEM Forms as a Cloud Service ahora incluye una opción fácil de usar para conectar Forms adaptable con Adobe Marketo Engage. Esta integración le permite crear Forms adaptable directamente con la captura de posibles clientes de Marketo Engage y los objetos personalizados relacionados. Ahora puede rellenar previamente los campos de formulario con datos del Marketo Engage y enviar datos de vuelta para automatizar flujos de trabajo como las campañas inteligentes y la automatización de correo electrónico. También puede conectar un formulario adaptable con la biblioteca de Munchkin para realizar un seguimiento del número de visitas, clics y envíos de formularios.

#### Forms adaptable y HTML5 Forms

* **[Crear Forms adaptable basado en una plantilla XFA existente](/help/forms/create-adaptive-form-using-xfa-templates.md)**: ahora puede crear Forms adaptable basado en componentes principales mediante plantillas de formulario XFA (archivos*.XDP). Esta capacidad facilita a los clientes locales de AEM Forms las inversiones existentes en tecnología XFA para adoptar AEM Forms as a Cloud Service.

* **Forms de HTML5 (formularios web basados en XFA)**: Ahora, los clientes locales de AEM Forms que utilizan la tecnología XFA pueden realizar la transición sin esfuerzo al as a Cloud Service de AEM Forms, conservando al mismo tiempo su experiencia de usuario existente con Forms de HTML 5 (formularios web basados en XFA). Esta capacidad permite procesar plantillas de formulario XFA en formato HTML 5, lo que hace que los formularios sean accesibles en dispositivos que no admiten PDF forms basados en XFA.

  ![Forms de HTML (formularios web basados en XFA)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[Compatibilidad con cadenas codificadas en Base64 para archivos adjuntos](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**: El componente Archivo adjunto en Forms adaptable basado en componentes principales ahora incluye una opción para enviar archivos adjuntos como cadenas codificadas en Base64.

#### Comunicaciones interactivas y API de comunicación

* **Editor de comunicaciones interactivas**: el editor de comunicaciones interactivas es una herramienta gráfica de diseño de comunicaciones fácil de usar que simplifica la creación de correspondencia personalizada basada en datos y se ejecuta en cualquier explorador moderno. Admite una integración de datos perfecta, definición de lógica compleja e integración de medios enriquecidos, lo que garantiza la generación profesional y compatible de documentos, comunicaciones y plantillas para diversas necesidades comerciales.

  ![Editor de comunicaciones interactivas](/help/forms/assets/ic-editor.png)


* **[Mejoras en el cumplimiento de las normas de PDF/A](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**: ahora puede usar las API de comunicación para convertir documentos de PDF a formatos de PDF/A (1a, 2a, 3a) con fines de archivo, al tiempo que garantiza la accesibilidad y comprueba el cumplimiento de estos estándares.


* **[API de firma (documento Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**: una nueva API RESTful en las API de comunicación permite administrar fácilmente las firmas de PDF. Admite operaciones como las siguientes:
   * Borrar firma: quita una firma de un campo especificado.
   * Quitar campo de firma: elimina un campo de firma especificado.


<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## Servicio de conversión automatizada de formularios 

* **[Convertir PDF forms a Forms adaptable basado en componentes principales](https://experienceleague.adobe.com/en/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**: ahora puede usar el servicio de Automated forms conversion para transformar PDF forms, AcroForms o formularios basados en XFA en Forms adaptable basado en componentes principales.


>[!IMPORTANT]
>
> ¿Le interesa unirse al programa de acceso rápido para disponer de cualquier innovación de los formularios? Envíe un correo electrónico desde su dirección de correo electrónico oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con la lista de capacidades que le interesan.CIF ## Complemento de {#cloud-services-cif}

## Complemento CIF {#cif}

### Correcciones de errores {#bug-fixes-cif}

* Se han corregido las pruebas de interfaz de usuario para que funcionen correctamente con los componentes principales de CIF.
* Se ha resuelto un problema con el formato de URL de la categoría que no funcionaba tal como se esperaba en la instancia en la nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Rendimiento mejorado de replicación de árbol (y desaprobación del flujo de trabajo del árbol de contenido de Publish) {#tree-replication-performance}

[El paso ](/help/operations/replication.md#tree-activation) del flujo de trabajo de activación de árbol es un nuevo paso recomendado para replicar jerarquías de contenido profundo. Tenga en cuenta que permite que las duplicaciones independientes (por ejemplo, mediante la publicación rápida o la administración de publicaciones) se realicen en paralelo con el flujo de trabajo de replicación de árbol en curso. Esto resulta especialmente útil si necesita publicar contenido con distinción de tiempo mientras una replicación masiva sigue en curso. El paso de replicación de árbol reemplaza al flujo de trabajo del árbol de contenido de Publish y a su paso de flujo de trabajo relacionado, que ya no se utilizan.

### API basadas en OpenAPI: programa de adopción anticipada {#open-apis-earlyadopter}

AEM Los desarrolladores pueden integrar profundamente las funciones de los Cloud Service de la integración de los en sus propias aplicaciones y herramientas. Las nuevas API de AEM as a Cloud Service seguirán la especificación de OpenAPI, con el objetivo de ser coherentes, bien documentadas y fáciles de usar. Las credenciales de los extremos que requieren autenticación se generarán creando proyectos de Adobe Developer Console.

AEM Obtenga más información acerca de las API de basadas en OpenAPI y pruebe un tutorial completo que ilustre la configuración y el uso.

En concreto, los puntos finales de API que se enumeran a continuación están disponibles como parte de un programa de usuarios que lo adoptaron por primera vez. Si está interesado, envíe un correo electrónico a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) en el que se describa cómo piensa utilizarlos.
* [API de fragmentos de contenido de sitios](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API de Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API de sitios y carpetas de Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API de comunicaciones de Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Informática Edge - ¡Solicitud de comentarios! {#edge-computing-feedback}

La informática de Edge acerca el procesamiento de datos al navegador, lo que ofrece ventajas como una menor latencia. AEM Como entrada en la hoja de ruta, nos encantaría saber si esta tecnología le resulta útil para los proyectos de entrega y Edge Delivery Services de Publish y para los que prevé utilizarla. Enviar un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con preguntas y comentarios.

### Nuevo AEM Developer Console (Beta pública) {#aem-developer-console-beta}

Pruebe la [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñada, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

Cualquiera puede acceder a la versión beta pública haciendo clic en el botón *Nueva consola disponible* en la versión actual de AEM Developer Console. El Adobe agradece los comentarios, que puede enviar por correo electrónico a [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com)

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Puede encontrar una lista completa de las versiones del editor universal [aquí](/help/release-notes/universal-editor/current.md).

## Generar variaciones {#generate-variations}

Puede encontrar una lista completa de las versiones de generar variaciones [aquí](/help/generative-ai/release-notes-generate-variations.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
