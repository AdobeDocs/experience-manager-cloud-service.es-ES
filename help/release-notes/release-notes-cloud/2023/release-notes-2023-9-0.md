---
title: Notas de la versión 2023.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
feature: Release Information
role: Admin
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 81%

---


# Notas de la versión 2023.9.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.9.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.9.0) fue el viernes, 28 de septiembre de 2023. La próxima versión con funcionalidades (2023.10.0) se planificó para el viernes, 26 de octubre de 2023.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de septiembre de 2023 para ver un resumen de las funciones añadidas en la versión 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEM Edge Delivery Services {#edge-delivery}

Edge Delivery es un nuevo conjunto de servicios componibles centrados en maximizar el impacto del contenido para impulsar resultados comerciales mensurables en el punto de interacción del cliente.

Obtenga más información acerca de Edge Delivery Services en el artículo [aquí](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-features}

**Asignar un formulario de metadatos a una carpeta**

Ahora puede asignar un formulario de metadatos a una carpeta específica dentro de la implementación. Todos los recursos de la carpeta, incluidos los de las subcarpetas, muestran las propiedades definidas en el formulario de metadatos asignado.

![asignar formulario de metadatos a una carpeta](/help/release-notes/assets/assign-to-folder.png)

### Nuevas funciones de la vista Administrador {#admin-view-features}

* **Integrar AEM Assets as a Cloud Service con la creación basada en documentos para Edge Delivery Services**: integre AEM Assets con la creación basada en documentos para Edge Delivery Services para permitir que los autores de sitios web [utilicen imágenes disponibles en repositorios de AEM Assets al crear documentos en Microsoft Word o Google Docs](/help/edge/overview.md).

* **Extraer archivos ZIP**: Posibilidad de seleccionar archivos ZIP administrados en Experience Manager y [extraer los archivos directamente en Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) sin descargarlos.

  ![Fijar elementos para grupos](/help/release-notes/assets/extract-archive.png)

### Nuevas funciones disponibles en [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [compatibilidad con subtítulos y pistas de audio múltiples para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma). Ahora se pueden añadir fácilmente varios subtítulos y pistas de audio a un vídeo principal. Esta posibilidad significa que los vídeos son accesibles para todo el público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

  ![Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.](/help/release-notes/assets/msma-aem-cs.png)*Pestaña Subtítulos y pistas de audio en la página Propiedades de un recurso de vídeo seleccionado.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Experience Manager Forms] {#forms-features}

* [**Soporte empresarial de Google reCAPTCHA**](/help/forms/captcha-adaptive-forms-core-components.md): utilice Google reCAPTCHA empresarial en un formulario adaptable para proporcionar una protección mejorada contra la actividad fraudulenta y el correo no deseado, lo que ofrece una experiencia de usuario más segura. Con un análisis de riesgos avanzado y una integración optimizada, los usuarios compradores pueden enviar fácilmente formularios mientras los bots están bloqueados de manera efectiva.

* [**Adobe Analytics con automatización de la configuración de Experience Cloud para Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): ahora se puede habilitar Adobe Analytics con la automatización de la configuración de Experience Cloud con un par de botones. Esto permite conectar AEM Forms as a Cloud Service con las etiquetas de Experience Platform y Adobe Analytics para capturar y rastrear las métricas de rendimiento de los formularios publicados.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Plantilla de informe de Adobe Analytics para formularios adaptables**](/help/forms/view-understand-aem-forms-analytics-reports.md): Forms as a Cloud Service ahora proporciona un informe listo para usar de Adobe Analytics. Le ayuda a comprender fácilmente el rendimiento de sus formularios. Las métricas de nivel de formulario proporcionan una perspectiva del rendimiento del formulario en varios indicadores clave de rendimiento (KPI) como representaciones, visitantes, envíos o tiempo promedio de cumplimentación. Al rastrear el comportamiento del usuario y los comentarios, usted puede identificar las áreas del formulario que están causando frustración o confusión, lo que guía las mejoras en el diseño y la funcionalidad del formulario.

  ![Informe de Adobe Analytics de participación del usuario del formulario adaptable](/help/forms/assets/forms-analytics-report.png)

* **[Fragmentos de formulario adaptables basados en componentes principales](/help/forms/adaptive-form-fragments-core-components.md)**: Despídase de la duplicación, optimice su inventario digital y mejore la colaboración a medida que mejora su experiencia de creación de formularios con fragmentos de formularios. Estos componentes reutilizables se integran a la perfección en múltiples formularios, agilizando la creación de formularios coherentes y de aspecto profesional. Los fragmentos de formulario garantizan la reutilización, la estandarización y la coherencia de la marca mediante la funcionalidad “cambiar una vez y reflejar en todas partes”. Experimente una mayor capacidad de mantenimiento y eficacia, ya que las actualizaciones realizadas en un solo lugar se propagan automáticamente a todos los formularios que utilizan estos fragmentos.

* **[Paso del flujo de trabajo de Adobe Sign mejorado](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: este se ha mejorado e incluye lo siguiente:
   * **Autenticación basada en documentos de identidad oficiales para Adobe Sign**: la autenticación basada en documentos de identidad oficiales de Adobe Acrobat Sign ofrece un nivel adicional de verificación al permitir a los usuarios autenticarse con documentos de identidad emitidos por el gobierno (licencia de conducir, identificación nacional, pasaporte). Al utilizar documentos de identificación de confianza, esta mejora añade un nivel adicional de confianza al proceso de firma, lo que lo hace ideal para situaciones que requieren una mayor seguridad, conformidad y validación del usuario.

   * **Pista de auditoría para documentos de Adobe Sign**: utilice la función Pista de auditoría para obtener información detallada sobre el ciclo de vida de los documentos de Adobe Sign. Con la pista de auditoría, se puede mantener un registro completo de todas las acciones e interacciones relacionadas con los documentos. Esto incluye detalles como quién vio, editó o firmó el documento, junto con marcas de tiempo para cada evento. Esta mejora es crucial para mantener el cumplimiento, resolver disputas y garantizar la integridad de los acuerdos digitales.

   * **Nuevas funciones para los destinatarios del acuerdo más allá del firmante**: Adobe Acrobat Sign tiene la opción de ampliar las funciones de los destinatarios del acuerdo más allá del firmante para que coincidan mejor con sus requisitos de flujo de trabajo. Cuando se habilita, cada destinatario de un acuerdo tiene su función que se configura de forma individual, siendo la de Firmante la predeterminada.

* **Compatibilidad con recuentos de páginas en las API de comunicación**: ahora, junto con recuperar el documento a través de las API de comunicación, también puede recibir información valiosa sobre el número de páginas que contiene el documento.

* **[Tratamiento de errores con controladores de error personalizados en el editor de reglas](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ahora se puede invocar una función personalizada en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta adaptada a los usuarios finales. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.

* **[Versión de 64 bits de AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: La versión de 64 bits de AEM Forms Designer ofrece rendimiento, escalabilidad y administración de memoria mejorados para potenciar su experiencia de creación de formularios. Con la arquitectura de 64 bits, puede abordar proyectos aún más grandes y complejos con facilidad, lo que garantiza flujos de trabajo de diseño sin problemas y eficiencia optimizada. Aumente sus capacidades de diseño de formularios y disfrute del futuro de AEM Forms Designer con esta versión de vanguardia.

### Programa para primeros usuarios {#forms-early-adopter}

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-ea@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

* **[Forms adaptable sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es)**: use Forms adaptable sin encabezado para permitir que los desarrolladores creen, publiquen y administren formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de usar una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

   * crear formularios multicanal de alta calidad en el lenguaje de programación que desee
   * integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
   * reutilizar los componentes de IU propios con aplicaciones de formularios
   * aprovechar la potencia de Adobe Experience Manager Forms

  Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Nuevo comportamiento de almacenamiento en caché de CDN para parámetros de URL relacionados con campañas {#cache-url-params}

Para los nuevos entornos, la CDN eliminará los parámetros de consulta relacionados con el marketing de forma predeterminada para aumentar el rendimiento de la campaña de marketing y las proporciones de visitas de la caché. Los entornos existentes no se ven afectados. [Más información](/help/implementing/dispatcher/caching.md#marketing-parameters).

### Programa de adopción anticipada de reglas de filtro de tráfico (incluidas las reglas de WAF) {#waf-early-adopter}

Filtre el tráfico en la red de distribución de contenido (CDN) en función de lo siguiente:

* encabezados y propiedades de solicitud (por ejemplo, dirección IP)
* patrones de tráfico asociados a tráfico malintencionado

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a **aemcs-waf-adopter@adobe.com** desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios. El espacio es limitado.

Obtenga más información acerca de la función en el artículo [aquí](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
