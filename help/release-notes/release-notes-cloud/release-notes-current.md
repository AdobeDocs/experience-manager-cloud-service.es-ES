---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9c76ff2e0b789894ef5492ee940ce79cddb47e11
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 17%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.6.0) es el 30 de junio de 2022.

La próxima versión (2022.7.0) está planificada para el 28 de julio de 2022.

## Vídeo de la versión {#release-video}

Consulte el vídeo Información general de la versión de junio de 2022 para ver un resumen de las funciones agregadas en la versión 2022.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* Un nuevo [interfaz de usuario](/help/headless/content-fragments/content-fragment-console.md) ya está disponible para administradores de contenido y autores de contenido para administrar de forma eficaz (realizar acciones como publicar, cancelar la publicación, copiar, mover, etc.), buscar/filtrar y crear fragmentos de contenido para casos de uso sin encabezado.

   ![Consola de fragmento de contenido](/help/release-notes/assets/cf-ui.png)

* El nuevo [Componente Tabla de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) funciona no solo con los componentes principales, sino con todos los componentes, procesando automáticamente ToCs en las páginas de contenido. Y como se procesa en el lado del servidor y se almacena en caché completamente por parte del Dispatcher, también es eficiente cargar.

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

Experience Manager Assets utiliza las capacidades de Adobe Sensei AI ahora [distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente al ingerirlos](../../assets/color-tag-images.md). Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen. Puede configurar el número de colores, dentro de un rango de uno a cuarenta, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Forms] {#forms-features}

* **[Integración de Forms adaptable con Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**: Ahora puede configurar un formulario adaptable para ejecutar un flujo de nube Microsoft® Power Automate en el envío. El formulario adaptable configurado envía los datos capturados, los archivos adjuntos y el documento de registro al flujo de Power Automate Cloud para su procesamiento. Le ayuda a crear una experiencia de captura de datos personalizada mientras aprovecha el poder de Microsoft® Power Automate para crear lógicas empresariales en torno a los datos capturados y automatizar los flujos de trabajo de los clientes.

* **Asistente para crear un formulario adaptable**: Puede utilizar el asistente para usuarios empresariales con el fin de crear Forms adaptable rápidamente. El asistente proporciona un desplazamiento rápido por las fichas para seleccionar fácilmente la plantilla preconfigurada, el estilo, los campos y las opciones de envío para crear un formulario adaptable.

   ![Asistente para crear un formulario adaptable](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nueva página de propiedades de la cabina de productos para una descripción general mejor y simplificada

![información general sobre las propiedades de la cabina de productos](/help/assets/CIF/product_cockpit_properties_overview.png)

* Compatibilidad y solidez mejoradas para conectores de terceros en I/O Runtime

* Compatibilidad mejorada con las sobrescrituras de configuración del cliente GQL (p. ej., establecer el comportamiento de almacenamiento en caché personalizado)

* Ahora se admiten varios extremos de comercio predeterminados y se pueden configurar mediante Cloud Manager. Puede encontrar detalles en el blog del CIF [here](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### Corrección de errores {#bug-fixes-cif}

* El campo de selección de varios valores muestra el segundo y el resto de los productos adicionales como no válidos

* El selector de productos se oculta ocasionalmente detrás de los componentes

## Complemento Demostraciones de Referencia {#cloud-services-demos}

### Novedades {#what-is-new-demos}

* Nueva plantilla de Contenido y comercio de WKND que amplía WKND con una experiencia de compra E2E que incluye catálogo de productos, carro de compras, cierre de compra y myAccount. Esta plantilla utiliza CIF y sus componentes principales del CIF, por lo que también debe instalar el complemento CIF. Puede encontrar detalles en el blog del CIF [here](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![Tienda WKND](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* AEM as a Cloud Service está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarlo con todas las demás aplicaciones de Experience Cloud. Consulte [AEM as a Cloud Service en el shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

* Como se menciona en las notas de la versión de mayo (2022.5.0), la opción &quot;Agregar árbol&quot; en la pantalla del administrador del agente de replicación **Distribuir** se ha eliminado. Los paquetes con una jerarquía de contenido de árbol deben replicarse usando [Administrar publicación](/help/operations/replication.md#manage-publication) o [Árbol de contenido de publicación](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) flujo de trabajo.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [here](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [here](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
