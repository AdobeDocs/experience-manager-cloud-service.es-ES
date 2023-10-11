---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: ab0fc832eb66bcf9a0fcd4f08b481845f3664e14
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 20%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] La versión de la función actual (2023.9.0) es el 28 de septiembre de 2023. La próxima versión de la funcionalidad (2023.10.0) está planificada para el 26 de octubre de 2023.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de septiembre de 2023 para ver un resumen de las funciones añadidas en la versión 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## Servicios de entrega perimetral {#edge-delivery}

Edge Delivery es un nuevo conjunto de servicios componibles centrados en maximizar el impacto del contenido para impulsar resultados comerciales mensurables en el punto de interacción del cliente.

Obtenga más información acerca de los Edge Delivery Services en el artículo [aquí](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-features}

**Asignar un formulario de metadatos a una carpeta**

Ahora puede asignar un formulario de metadatos a una carpeta específica dentro de la implementación. Todos los recursos de la carpeta, incluidos los de las subcarpetas, muestran las propiedades definidas en el formulario de metadatos asignado.

![asignar formulario de metadatos a una carpeta](/help/release-notes/assets/assign-to-folder.png)

### Nuevas funciones en la vista de administración {#admin-view-features}

* **Integrar AEM Assets as a Cloud Service con la creación basada en documentos para Edge Delivery Services**: integre AEM Assets con la creación basada en documentos para Edge Delivery Services para permitir que los autores de sitios web [utilizar imágenes disponibles en repositorios de AEM Assets al crear documentos en Microsoft Word o Google Docs](/help/edge/using.md#integrate-assets-edge).

* **Extraer archivos .zip**: capacidad para seleccionar archivos ZIP administrados en Experience Manager y [extracción de los archivos directamente en el Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sin descargarlos.

  ![Anclar elementos para grupos](/help/release-notes/assets/extract-archive.png)

### Funciones previas al lanzamiento disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Compatibilidad con subtítulos múltiples y pistas de audio múltiple para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): ahora se pueden añadir fácilmente varios subtítulos y varias pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para toda la audiencia global. Puede personalizar un solo vídeo principal publicado a una audiencia global en varios idiomas y adherirse a las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Experience Manager Forms] {#forms-features}

* [**Soporte empresarial de Google reCAPTCHA**](/help/forms/captcha-adaptive-forms-core-components.md): utilice Google reCAPTCHA Enterprise en un formulario adaptable para proporcionar una protección mejorada contra la actividad fraudulenta y el correo no deseado, lo que ofrece una experiencia de usuario más segura. Con un análisis de riesgo avanzado y una integración perfecta, los usuarios genuinos pueden enviar fácilmente formularios mientras los bots están bloqueados de manera efectiva.

* [**Adobe Analytics con automatización de la configuración de Experience Cloud para Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): Ahora puede habilitar Adobe Analytics con la automatización de la configuración de Experience Cloud con un par de botones. Permite conectar AEM Forms as a Cloud Service con etiquetas de Experience Platform y Adobe Analytics para capturar y realizar un seguimiento de las métricas de rendimiento de los formularios publicados.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Plantilla de informe de Adobe Analytics para Forms adaptable**](/help/forms/view-understand-aem-forms-analytics-reports.md): Forms as a Cloud Service ahora proporciona un informe OOTB de Adobe Analytics. Le ayuda a comprender fácilmente el rendimiento de sus formularios. Las métricas de nivel de formulario proporcionan una perspectiva del rendimiento del formulario en varios indicadores clave de rendimiento (KPI) como, representaciones, visitantes, envíos o tiempo medio de cumplimentación. Al realizar un seguimiento del comportamiento y los comentarios de los usuarios, se pueden identificar las áreas del formulario que causan confusión y guiar las mejoras en el diseño y la funcionalidad del formulario.

  ![Informe de Adobe Analytics de participación del usuario del formulario adaptable](/help/forms/assets/forms-analytics-report.png)

* **[Fragmento de formulario en Forms adaptable basado en componentes principales](/help/forms/adaptive-form-fragments-core-components.md)**: Diga adiós a la duplicación, optimice su inventario digital y mejore la colaboración a medida que eleva su experiencia de creación de formularios con fragmentos de formularios. Estos componentes reutilizables se integran perfectamente en varios formularios, lo que optimiza la creación de formularios coherentes y de aspecto profesional. Los fragmentos de formulario garantizan la reutilización, la estandarización y la coherencia de la marca mediante la funcionalidad &quot;cambiar una vez y reflejar en todas partes&quot;. Experimente una mayor capacidad de mantenimiento y eficacia, ya que las actualizaciones realizadas en un solo lugar se propagan automáticamente a todos los formularios que utilizan estos fragmentos.

* **[Paso de flujo de trabajo de Adobe Sign mejorado](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: El paso del flujo de trabajo de Adobe Sign se ha mejorado para incluir lo siguiente:
   * **Autenticación basada en documentos de identidad oficiales para Adobe Sign**: la autenticación basada en documentos de identidad oficiales de Adobe Acrobat Sign ofrece un nivel adicional de verificación al permitir a los usuarios autenticarse con documentos de identidad emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al aprovechar los documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Pista de auditoría para documentos de Adobe Sign**: utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de los documentos de Adobe Sign. Con la pista de auditoría, ahora puede mantener un registro completo de todas las acciones e interacciones relacionadas con sus documentos. Esto incluye detalles como quién vio, editó o firmó el documento, junto con marcas de tiempo para cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.

   * **Nuevas funciones para los destinatarios del acuerdo más allá del firmante**: Adobe Acrobat Sign tiene la opción de ampliar las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función configurable individualmente, con firmante como predeterminado.

* **Compatibilidad con recuentos de páginas en las API de comunicación**: Ahora, junto con recuperar el documento a través de las API de comunicación, también puede recibir la información valiosa sobre el número de páginas que contiene el documento.

* **[Tratamiento de errores con controladores de error personalizados en el editor de reglas](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: Ahora puede invocar una función personalizada en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.

* **[Versión de 64 bits de AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: la versión de 64 bits de AEM Forms Designer ofrece un rendimiento, una escalabilidad y una administración de memoria mejorados para potenciar su experiencia de creación de formularios. Con la arquitectura de 64 bits, puede abordar proyectos aún más grandes y complejos con facilidad, lo que garantiza flujos de trabajo de diseño sin problemas y eficiencia optimizada. Aumente sus capacidades de diseño de formularios y disfrute del futuro de AEM Forms Designer con esta versión de vanguardia.

### Programa de adopción temprana {#forms-early-adopter}

* **[Protect sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa reforzada de protección no solo protege los datos valiosos de los ojos no autorizados, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos de Adobe PDF que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-early-adopter-program@adobe.com` desde su id de correo electrónico oficial para unirse al programa de usuarios que lo adoptaron por primera vez y solicitar acceso a esta capacidad.

* **[Forms adaptable sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es)**: utilice Forms adaptable sin encabezado para permitir que los desarrolladores creen, publiquen y administren formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de hacerlo a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

   * crear formularios multicanal de alta calidad en el lenguaje de programación que desee
   * integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
   * reutilizar los componentes de IU propios con aplicaciones de formularios
   * aprovechar la potencia de Adobe Experience Manager Forms

  Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Nuevo comportamiento de almacenamiento en caché de CDN para parámetros de URL relacionados con campañas {#cache-url-params}

Para los nuevos entornos, la CDN eliminará los parámetros de consulta relacionados con el marketing de forma predeterminada para aumentar el rendimiento de la campaña de marketing y las relaciones de visitas de la caché. Los entornos existentes no se ven afectados. [Más información.](/help/implementing/dispatcher/caching.md#marketing-parameters)

### Programa de adopción anticipada de Reglas de filtro de tráfico (incluidas las Reglas WAF) {#waf-early-adopter}

Filtre el tráfico en la CDN en función de lo siguiente:
* encabezados y propiedades de solicitud (por ejemplo, dirección IP)
* patrones de tráfico asociados a tráfico malintencionado

¿Quiere probar la función y compartir sus comentarios? Envíe un correo electrónico a **aemcs-waf-adopter@adobe.com** desde su ID de correo electrónico oficial para obtener más información sobre el programa de usuarios que lo adoptaron por primera vez. El espacio es limitado.

Obtenga más información acerca de la función en el artículo [aquí](/help/security/cdn-and-waf-rules.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
