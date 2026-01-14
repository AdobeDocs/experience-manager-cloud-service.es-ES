---
title: Notas de la versión 2022.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 74%

---

# Notas de la versión 2022.6.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad para la versión 2022.6.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.6.0) es el 30 de junio de 2022.

La próxima versión (2022.7.0) está planificada para el 8 de agosto de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de junio de 2022 para ver un resumen de las funciones añadidas en la versión 2022.6.0.

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* Ahora hay disponible una nueva [interfaz de usuario](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) para autores y administradores de contenido que permite administrar de forma eficaz (como publicar, cancelar la publicación, copiar, mover, etc.), buscar/filtrar y crear fragmentos de contenido para casos de uso sin encabezado.

  ![Consola de fragmento de contenido](/help/release-notes/assets/cf-ui.png)

* El nuevo [Componente Tabla de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html?lang=es) funciona no solo con los componentes principales, sino con todos los componentes, procesando automáticamente ToC en las páginas de contenido. Y como se procesa en el lado del servidor y se almacena en caché completamente por parte del Dispatcher, también es eficiente para cargar.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

Experience Manager Assets usa funcionalidades de Adobe AI para ahora [distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente al ingerirlos](/help/assets/color-tag-images.md). Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen. Puede configurar el número de colores, dentro de un rango de uno a 40, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Forms] {#forms-features}

* **[Integración de formularios adaptables con Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: ahora puede configurar un formulario adaptable para ejecutar un flujo de nube Microsoft® Power Automate en el envío. El formulario adaptable configurado envía los datos capturados, los archivos adjuntos y el documento de registro al flujo de Power Automate Cloud para su procesamiento. Le ayuda a crear una experiencia de captura de datos personalizada mientras aprovecha el poder de Microsoft® Power Automate para crear lógicas empresariales en torno a los datos capturados y automatizar los flujos de trabajo de los clientes.

* **Asistente para crear un formulario adaptable**: puede utilizar el asistente para usuarios empresariales con el fin de crear formularios adaptables de forma rápida. El asistente proporciona una navegación rápida por las pestañas para seleccionar fácilmente la plantilla preconfigurada, el estilo, los campos y las opciones de envío para crear un formulario adaptable.

  ![Asistente para crear un formulario adaptable](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva página de propiedades de la cabina de productos para una descripción general mejor y simplificada

![información general sobre las propiedades de la cabina de productos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilidad y solidez mejoradas para conectores de terceros en I/O Runtime

* Compatibilidad mejorada con las sobrescrituras de configuración del cliente GQL (por ejemplo, establecer el comportamiento de almacenamiento en caché personalizado)

* Ahora se admiten varios extremos de comercio predeterminados y se pueden configurar mediante Cloud Manager. Puede encontrar detalles en el blog del CIF [aquí](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Corrección de errores {#bug-fixes-cif}

* El campo de selección de varios valores muestra el segundo y el resto de los productos adicionales como no válidos

* El selector de productos se oculta ocasionalmente detrás de los componentes

## Complemento Demostraciones de referencia {#cloud-services-demos}

### Novedades {#what-is-new-demos}

* Nueva plantilla de Contenido y comercio de WKND que amplía WKND con una experiencia de compra E2E que incluye catálogo de productos, carro de compras, cierre de compra y myAccount. Esta plantilla utiliza CIF y sus componentes principales del CIF, por lo que también debe instalar el complemento CIF. Puede encontrar detalles en el blog del CIF [aquí](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Tienda WKND](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* Como se mencionó en las notas de la versión de mayo (2022.5.0), se eliminó la opción &quot;Agregar árbol&quot; en la pestaña **Distribuir** de la pantalla del administrador del agente de replicación. Los paquetes con una jerarquía de contenido de árbol deben replicarse usando [Administrar publicación](/help/operations/replication.md#manage-publication) o el flujo de trabajo del [Árbol de contenido de publicación](/help/operations/replication.md#manage-publication#publish-content-tree-workflow).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
