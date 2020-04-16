---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.4.0
description: Notas de la versión de Experience Manager para 2020.4.0
translation-type: tm+mt
source-git-commit: 98de3a6674aaef5228e96e0bf72e67de861f858e

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

La fecha de lanzamiento de [!DNL Experience Manager] como servicio de nube 2020.4.0 es el 9 de abril de 2020.

## What&#39;s New in Assets {#assets}

Obtenga información sobre las nuevas funciones, mejoras y correcciones de errores de [!DNL Experience Manager Assets] y [!DNL Dynamic Media] en la versión actual.

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) admite los casos de uso de distribución de recursos para Experience Manager Assets. [!DNL Brand Portal] ayuda a las organizaciones a satisfacer sus necesidades de marketing mediante la distribución segura de recursos de productos y marcas aprobados a agencias externas, socios, equipos internos y distribuidores para su descarga.
   * [!DNL Brand Portal] la configuración se completa mediante [!DNL Adobe I/O] la consola. Consulte [Configuración de Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html).
   * El abastecimiento de recursos en [!DNL Brand Portal] no es compatible aún con [!DNL Experience Manager] el servicio de nube.

* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) v2.0 funciona [!DNL Experience Manager] como un servicio de nube. [!DNL Adobe Asset Link] facilita la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido mediante la conexión [!DNL Experience Manager Assets] con las aplicaciones de [!DNL Creative Cloud] escritorio [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] a través del panel en la aplicación [!DNL Asset Link] .
   * [!DNL Experience Manager] está preconfigurado para [!DNL Adobe Asset Link], lo que resulta en una configuración [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) sencilla y una implementación más rápida para los profesionales creativos.
   * [!DNL Asset Link] ahora es compatible con un conmutador [de entorno de](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) Experience Manager que permite a los usuarios creativos conectarse fácilmente a un [!DNL Experience Manager] entorno diferente. Un ejemplo en el que esta funcionalidad es útil es para diseñadores de agencias que trabajan con varios clientes mediante diferentes [!DNL Experience Manager Assets] implementaciones.

* Los usuarios pueden configurar flujos de trabajo [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) postprocesamiento para el inicio automático en la interfaz de usuario [!UICONTROL Propiedades] de la carpeta para jerarquías de carpetas específicas.
   * La interfaz de usuario [!UICONTROL Propiedades] de la carpeta se simplifica, con la nueva ficha Procesamiento [!UICONTROL de] recursos que contiene el perfil de metadatos, el perfil de procesamiento y la nueva configuración del flujo de trabajo de inicio automático.

      ![Los perfiles de procesamiento se pueden aplicar fácilmente a las carpetas y todos los recursos cargados a las carpetas se procesan mediante estos perfiles](/help/assets/assets/asset-processing-folder-properties.png)

   * La opción de reprocesamiento de recursos permite seleccionar un perfil de procesamiento específico para volver a procesar los recursos seleccionados por el usuario en las subcarpetas.

      ![Volver a procesar los recursos seleccionados mediante un perfil de procesamiento específico](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]:: Se ha Añadido la configuración de publicación selectiva para que los recursos se publiquen automáticamente solo para previsualización segura. Además, los recursos se pueden publicar explícitamente en Experience Manager sin necesidad de publicarlos en DMS7 para envío de dominio público.

### Corrección de errores {#assets-bug-fixes}

* Correcciones de problemas de procesamiento de recursos.
* Correcciones en [!DNL Dynamic Media] la configuración y publicación de recursos en el servicio de [!DNL Dynamic Media] envío.

>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurar el portal de marca](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurar Experience Manager para que funcione con Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Crear un flujo de trabajo en Experience Manager mediante los microservicios de recursos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Novedades de Cloud Manager {#whats-new-cloud-manager}

* Las direcciones URL de Publisher ya están disponibles en la página de Entorno de la interfaz de usuario del Administrador de nube.
* Cambios en la navegación para permitir que el usuario edite, cambie o agregue un programa desde la página de información general de Cloud Manager.
* Cambios que permiten al usuario editar programas desde la tarjeta de programa en la página de aterrizaje de Cloud Manager.
* Nuevo estado de canalización **La ejecución** de canalización se muestra en el entorno con el que está asociada.
* Mejoras en la comprensión de la página de ejecución de la canalización. Esto incluye la visualización del nombre de la canalización (solo para la canalización que no es de producción) y el tipo, y un distintivo para indicar si el estado de la canalización está en curso/cancelado/fallido.
* Información sobre herramientas para mejorar la experiencia del usuario y la comprensión de por qué se desactiva el botón Añadir Programa/Entorno.
* Los Entornos fallidos ahora se pueden eliminar a través de la interfaz de usuario y la API.
* El proceso utilizado para generar contraseñas de git se ha vuelto más resistente a los problemas en la capa de servicio subyacente.

### Corrección de errores {#bug-fixes-cloud-manager}

* Los vínculos al entorno del escenario en la página de detalles de la ejecución de la canalización no navegaban de manera consistente a la ubicación correcta.
* Los pasos individuales dentro del proceso de creación de entornos agotarían el tiempo de espera antes de lo necesario, lo que ocasionaría que el proceso fallara.
* La configuración Maven utilizada en el contenedor de compilación se actualizó para evitar interbloqueos al descargar metadatos de artefactos.
* En algunos casos, el paso Generar imagen no puede descargar correctamente los paquetes de clientes.
* Algunas condiciones poco frecuentes evitarían que se eliminaran entornos.
* Las notificaciones de Experience Cloud no se recibían de forma coherente.
