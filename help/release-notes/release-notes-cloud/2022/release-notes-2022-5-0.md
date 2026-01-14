---
title: Notas de la versión 2022.5.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.5.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 64%

---

# Notas de la versión 2022.5.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad para la versión 2022.5.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.5.0) es el 9 de junio de 2022.
La próxima versión (2022.6.0) está planificada para el 30 de junio de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de mayo de 2022 para ver un resumen de las funciones añadidas en la versión 2022.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones disponibles en el canal de versión preliminar de [!DNL Sites] {#prerelease-features-sites}

* Varias funcionalidades de GraphQL
* Una [nueva consola](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) optimizada para el uso sin encabezado de fragmentos de contenido

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* [Imágenes inteligentes de Dynamic Media](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) ahora es compatible con el formato de archivo AVIF: mejore aún más Google Core Web Vital (Pintado de contenido más grande), con AVIF proporcionando una reducción de tamaño adicional del 20 % con respecto a WebP. En total, AVIF proporciona una reducción de tamaño promedio de hasta el 41 % con respecto al JPEG (en algunas imágenes incluso de hasta el 76 %).

* [!UICONTROL Experience Manager Assets Brand Portal] ahora ejecuta trabajos automáticos cada 12 horas para eliminar todos los recursos de Brand Portal publicados en AEM. Como resultado, no es necesario eliminar manualmente los recursos de la carpeta Contribution para mantener el tamaño de la carpeta por debajo del límite de umbral. Consulte [Novedades de Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=es).

### Nuevas funciones disponibles en el canal de versión preliminar de [!DNL Assets] {#prerelease-features-assets}

Experience Manager Assets usa funcionalidades de Adobe AI para ahora [distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente al ingerirlos](/help/assets/color-tag-images.md). Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen. Puede configurar el número de colores, dentro de un rango de uno a 40, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en el canal de versión preliminar de [!DNL Forms] {#prerelease-features-forms}

* **Integración de formularios adaptables con Microsoft® Power Automate**: ahora puede configurar un formulario adaptable para ejecutar un flujo de nube Microsoft® Power Automate en el envío. El formulario adaptable configurado envía los datos capturados, los archivos adjuntos y el documento de registro al flujo de Power Automate Cloud para su procesamiento. Le ayuda a crear una experiencia de captura de datos personalizada mientras aprovecha el poder de Microsoft® Power Automate para crear lógicas empresariales en torno a los datos capturados y automatizar los flujos de trabajo de los clientes.

* **Asistente para crear un formulario adaptable**: puede usar el asistente para usuarios empresariales con el fin de crear Forms adaptable rápidamente. El asistente proporciona una navegación rápida por las pestañas para seleccionar fácilmente la plantilla preconfigurada, el estilo, los campos y las opciones de envío para crear un formulario adaptable.

  ![Asistente para crear un formulario adaptable](/help/release-notes/assets/wizard.png)

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Acceso rápido a la cabina de productos: acceda fácilmente a la información detallada completa del producto con un solo clic en el Editor de sitios

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* Compatibilidad con componentes de comercio de marketing adicionales: los componentes se pueden configurar para mostrar un call-to-action de complemento al carro y de complemento a la lista de deseos

  ![Acceso directo del editor de sitios a la cabina de productos](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* La opción &quot;Agregar árbol&quot; en la pantalla del administrador del agente de replicación **Distribuir pestaña**, que se anunció anteriormente como obsoleta, se eliminó el 20 de junio de 2022 o poco después. Los paquetes con una jerarquía de contenido de árbol deben replicarse usando [Administrar publicación](/help/operations/replication.md#manage-publication) o [Flujo de trabajo Publicar árbol de contenido](/help/operations/replication.md#publish-content-tree-workflow).

* El uso de la pantalla de administración del agente de replicación o la API de replicación para distribuir paquetes de contenido de más de 10 MB (nodos con propiedades, sin incluir binarios) está en desuso y se aplica el 12 de septiembre de 2022 o poco después. En su lugar, [Administrar publicación](/help/operations/replication.md#manage-publication) o [Flujo de trabajo Publicar árbol de contenido](/help/operations/replication.md#publish-content-tree-workflow) debe utilizarse para replicar estos paquetes de contenido de gran tamaño. En julio, aparecerá un mensaje de advertencia en la pantalla del administrador del agente de replicación **Pestaña Distribuir** si intenta replicar estos paquetes de contenido grande y también en el registro de errores de AEM siempre que la API de replicación se utilice para replicar estos paquetes de contenido grande. En septiembre, las advertencias se sustituyeron por errores. Ajuste los procesos según corresponda.

### Nuevas funciones disponibles en el canal de versión preliminar de [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarlo con todas las demás aplicaciones de Experience Cloud. Consulte [AEM as a Cloud Service en Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation Security {#foundation-security}

### Finalización del soporte para TLS 1.0 y 1.1

A partir del 30 de junio de 2022, Experience Manager as a Cloud Service necesitará una comunicación de red más segura y un intercambio de datos con los sistemas de los usuarios. AEM usará exclusivamente Transport Layer Security (TLS), protocolo 1.2. Las versiones anteriores de TLS 1.0 y 1.1 ya no se utilizan.

Si sigue utilizando versiones anteriores de TLS como 1.0, 1.1, podría perder el acceso al Experience Manager as a Cloud Service.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
