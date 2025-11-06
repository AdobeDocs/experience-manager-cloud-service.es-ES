---
title: Notas de la versión 2023.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 7866d94c-e54c-4bb2-aaa6-66c019e46336
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# Notas de la versión 2023.7.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.7.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.7.0) es el 27 de junio de 2023. La próxima versión con funcionalidades (2023.8.0) está planificada para el 31 de agosto de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de julio de 2023 para ver un resumen de las funcionalidades añadidas en la versión 2023.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* MSM para fragmentos de contenido. El Administrador de varios sitios de AEM ya está disponible para los fragmentos de contenido, lo que permite crear Live Copies de fragmentos de contenido para la distribución de contenido por lotes. Los controles de herencia granulares están disponibles hasta el nivel de Variación y Elemento de fragmentos de contenido.

### Nuevas funciones en la versión preliminar de [!DNL Experience Manager Sites] {#prerelease-sites}

* La [Consola de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=es) ahora permite a los usuarios ver etiquetas y buscar por etiquetas aplicadas como metadatos a fragmentos de contenido. Los usuarios ya no tendrán que cambiar a la IU de Assets para esta capacidad, lo que reduce el cambio de contexto y mejora la eficacia.

![Etiquetado en la consola de fragmentos de contenido](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**Marco de trabajo de inteligencia artificial mejorado para las etiquetas inteligentes de imagen**

Experience Manager Assets ahora utiliza un marco de inteligencia artificial mejorado para las etiquetas inteligentes de imagen. Esta inteligencia de contenido mejora la relevancia y precisión de las etiquetas inteligentes disponibles para todos los recursos de imagen durante la ingesta.

**Configurar la visualización de columnas para la vista Lista de recursos**

Assets Essentials ahora permite seleccionar las columnas que se muestran en la vista Lista de recursos, como Estado, Formato, Dimensión, Tamaño, etc.

![Configuración de las columnas](/help/release-notes/assets/configure-columns.png)

**Ordenar resultados de búsqueda según la relevancia**

Assets Essentials ahora ordena los resultados de la búsqueda según la relevancia de forma predeterminada. Puede ordenar los recursos buscados en orden creciente o descendente de `Name`, `Relevance`, `Size`, `Modified` y `Created`.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Temáticas**](/help/forms/using-themes-in-core-components.md) **y plantillas** listas para usar: inicie su proceso de creación de formularios con nuestras temáticas y plantillas listas para usar, diseñadas para potenciar tanto a profesionales experimentados como a autores de formularios principiantes. Estas temáticas y plantillas creadas de forma optimizada y seleccionada, con los componentes principales de Formularios adaptables, le permiten empezar a crear formularios rápidamente para los casos de uso más comunes.

* **[Componentes de React para formularios sin encabezado](https://github.com/adobe/aem-forms-headless-components/tree/main/packages/react-vanilla-components)**: ahora puede obtener una vista previa y personalizar las representaciones de formularios adaptables sin encabezado con los componentes de React predeterminados. Estos componentes utilizan las clases de BEM de los componentes principales de Formularios adaptables para el estilo, lo que facilita la personalización de su aspecto según sus necesidades específicas.

* [**Crear formularios adaptables con secciones repetibles**](/help/forms/create-forms-repeatable-sections.md): ahora puede hacer repetibles los componentes [Acordeón](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms//adaptive-forms-components/accordion.html?lang=es), [Asistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=es), [Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) y [pestañas horizontales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=es) basados en formularios adaptables para capturar varios registros de datos.  Estas secciones repetibles le permiten proporcionar varias entradas de datos fácilmente. Resulta útil cuando se desconocen de antemano las instancias de datos requeridas. El usuario que rellena el formulario puede agregar o quitar secciones fácilmente, lo que permite que los formularios se adapten a diferentes escenarios de entrada de datos y simplifica la recopilación de varias ocurrencias de los mismos datos.


### Funciones de versión preliminar disponibles en [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Soporte empresarial de Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): utilice Google reCAPTCHA empresarial en un formulario adaptable para proporcionar una protección mejorada contra la actividad fraudulenta y el correo no deseado, lo que ofrece una experiencia de usuario más segura. Con un análisis de riesgos avanzado y una integración optimizada, los usuarios compradores pueden enviar fácilmente formularios mientras los bots están bloqueados de manera efectiva.

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Centro de acciones {#actions-center}

Suscríbase a notificaciones por correo electrónico que le avisen cuando ocurran incidentes críticos que requieran una acción inmediata y también se envían recomendaciones personalizadas para optimizar su sitio. El [Centro de acciones](/help/operations/actions-center.md) sirve como una plataforma donde puede revisar estas alertas, como colas de replicación bloqueadas o credenciales que caducan, y marcarlas como resueltas.

![Captura de pantalla del Centro de acciones](/help/assets/assets/actions-center.png)

### Programa de adopción temprana de reglas CDN y WAF {#waf-early-adopter}

Filtre el tráfico en la red de distribución de contenido (CDN) en función de lo siguiente:

* encabezados y propiedades de solicitud (por ejemplo, dirección IP)
* patrones de tráfico asociados a tráfico malintencionado

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a **aemcs-waf-adopter@adobe.com** desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios. El espacio es limitado.

Obtenga más información acerca de la función en el artículo [aquí](/help/security/traffic-filter-rules-including-waf.md).

### Otros cambios de base {#other-foundation-changes}

* Durante la semana del 7 de agosto, el usuario devolverá el código de error 429 en lugar del código de error 503 cuando las solicitudes a instancias de AEM superen un nivel correcto. [Más información](/help/implementing/developing/introduction/development-guidelines.md).

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
