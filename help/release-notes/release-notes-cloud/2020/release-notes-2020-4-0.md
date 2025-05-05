---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.4.0
description: "[!DNL Adobe Experience Manager] notas de la versión as a Cloud Service para 2020.4.0."
exl-id: d98a3862-76fa-4b5b-b81a-333f5f532b67
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 93%

---

# Notas de la versión de Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

Esta página describe las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Experience Manager] as a Cloud Service 2020.4.0 es el 9 de abril de 2020.

## Novedades de Assets. {#assets}

Obtenga información sobre las nuevas funciones, mejoras y correcciones de errores de [!DNL Experience Manager Assets] y [!DNL Dynamic Media] en la versión actual.

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=es) admite los casos de uso de distribución de recursos para Experience Manager Assets. [!DNL Brand Portal] ayuda a las organizaciones a satisfacer sus necesidades de marketing mediante la distribución segura de recursos de productos y marcas aprobados a agencias externas, socios, equipos internos y distribuidores para su descarga.
   * La configuración de [!DNL Brand Portal] se completa mediante la consola de [!DNL Adobe I/O]. Consulte [Configuración de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=es).
   * La fuente recursos en [!DNL Brand Portal] no es compatible aún con [!DNL Experience Manager] as a Cloud Service.

* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) v2.0 funciona [!DNL Experience Manager] como un Cloud Service. [!DNL Adobe Asset Link] facilita la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido mediante la conexión [!DNL Experience Manager Assets] con las aplicaciones de [!DNL Creative Cloud] escritorio[!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] a través del panel en la aplicación[!DNL Asset Link].
   * [!DNL Experience Manager] está preconfigurado para [!DNL Adobe Asset Link], lo que resulta en una [configuración sencilla](https://helpx.adobe.com/es/enterprise/using/configure-aem-assets-for-asset-link.html) y una implementación más rápida para los profesionales creativos.
   * [!DNL Asset Link] ahora es compatible con un [conmutador de entorno de Experience Manager](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) que permite a los usuarios creativos conectarse fácilmente a un entorno [!DNL Experience Manager] diferente. Un ejemplo en el que esta funcionalidad es útil, es para diseñadores de agencias que trabajan con varios clientes mediante diferentes [!DNL Experience Manager Assets] implementaciones.

* Los usuarios pueden configurar [flujos de trabajo de procesamiento posterior](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) para el inicio automático en la carpeta de la interfaz del usuario [!UICONTROL Propiedades] para las jerarquías de carpetas específicas.
   * La carpeta de la interfaz del usuario [!UICONTROL Propiedades] se simplifica, con la nueva pestaña [!UICONTROL Procesamiento de recursos] que contiene el perfil de metadatos, el perfil de procesamiento y la nueva configuración del flujo de trabajo de inicio automático.

     ![Los perfiles de procesamiento se pueden aplicar fácilmente a las carpetas, y todos los recursos cargados a las carpetas se procesan mediante estos perfiles](/help/assets/assets/asset-processing-folder-properties.png)

   * La opción de reprocesamiento de recursos permite seleccionar un perfil de procesamiento específico para reprocesar los recursos seleccionados por el usuario en las subcarpetas.

     ![Reprocesar los recursos seleccionados con un perfil de procesamiento específico](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]: Se añadió la configuración de publicación selectiva para que los recursos se publiquen automáticamente solo para vista previa segura. Además, los recursos se pueden publicar explícitamente en Experience Manager sin publicar en DMS7 para envío de dominio público.

### Correcciones de errores {#assets-bug-fixes}

* Correcciones de problemas de procesamiento de recursos.
* Correcciones en la configuración de [!DNL Dynamic Media] y publicación de recursos en el servicio de envío [!DNL Dynamic Media] .

>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html?lang=es)
>* [Configurar Experience Manager para que funcione con Asset Link](https://helpx.adobe.com/es/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Crear flujo de trabajo en Experience Manager mediante microservicios de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=es#post-processing-workflows)

## Novedades de Cloud Manager. {#whats-new-cloud-manager}

* Las URL de Publisher ya están disponibles en la página de Entorno de la interfaz de usuario de Cloud Manager.
* Cambios en la navegación para permitir que el usuario edite, cambie o agregue un programa desde la página de información general de Cloud Manager.
* Cambios que permiten al usuario editar programas desde la tarjeta de programa en la página de aterrizaje de Cloud Manager.
* Se muestra el nuevo estado de **Canalización ejecutándose** en el entorno con el que está asociada.
* Mejoras en la comprensión de la página de ejecución de la canalización. Esto incluye la visualización del nombre de la canalización (solo para la canalización que no es de producción) y el tipo, y un distintivo para indicar si el estado de la canalización está en curso/cancelada/con error.
* Información sobre las herramientas para mejorar la experiencia del usuario y la comprensión de por qué se desactiva el botón Agregar Programa/Entorno.
* Los entornos con error ahora se pueden eliminar a través de la interfaz de usuario y la API.
* El proceso utilizado para generar contraseñas de Git se ha vuelto más resistente a los problemas en la capa de servicio subyacente.

### Correcciones de errores {#bug-fixes-cloud-manager}

* Los vínculos al entorno de ensayo en la página de detalles de la ejecución de la canalización no navegaban de manera consistente a la ubicación correcta.
* Los pasos individuales dentro del proceso de creación de entornos agotarían el tiempo de espera antes de lo necesario, lo que causaría fallas en el proceso.
* La configuración de Maven utilizada en el contenedor de generación se actualizó para evitar interbloqueos al descargar metadatos de artefactos.
* En algunos casos, el paso Generar imagen no puede descargar correctamente los paquetes de clientes.
* Algunas condiciones poco frecuentes evitarían que se eliminaran entornos.
* Las notificaciones de Experience Cloud no se recibían de forma coherente.
