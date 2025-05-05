---
title: Notas de la versión 2020.7.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] notas de la versión as a Cloud Service para 2020.7.0."
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 74%

---

# Notas de la versión de [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.7.0.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Experience Manager] as a Cloud Service 2020.7.0 es el 30 de julio de 2020.

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### Novedades {#what-is-new-sites}

Conectores de [!DNL Experience Manager] as a Cloud Service para [!DNL Adobe Target] y [!DNL Adobe Analytics] se mejoran de las siguientes maneras:

* Una nueva implementación de interfaz de usuario reemplaza la implementación basada en la IU clásica.

* Se han simplificado los cuadros de diálogo de la interfaz de usuario, lo que permite crear marcos de trabajo para la asignación de variables y otras configuraciones [!DNL Adobe Launch]. Consulte [Integración de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html?lang=es) e [Integración de Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html?lang=es).

* Las configuraciones ahora se almacenan en `/conf` lugar de `/etc/cloudsettings` en el repositorio de Experience Manager.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* [!DNL Asset Compute Service] es un servicio escalable y ampliable para procesar activos. Los administradores pueden configurar [!DNL Experience Manager] para que invoque aplicaciones personalizadas creadas con [!DNL Asset Compute Service]. Los desarrolladores pueden utilizar el servicio para crear aplicaciones personalizadas especializadas que se ocupen de casos de uso complejos. Este servicio web puede generar miniaturas para diferentes tipos de archivos, representaciones de imágenes de alta calidad a partir de formatos de archivo de Adobe, codificar vídeos (futuros), extraer metadatos, extraer texto completo como precursor para la indexación y ejecutar un recurso a través de todos los servicios disponibles de [!DNL Sensei]. consulte [usar microservicios de recursos y perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).

* Se ha mejorado la configuración inicial de [!DNL Dynamic Media] en [!DNL Experience Manager] as a Cloud Service para que sea más robusta. Ahora proporciona el progreso de los procesos a los administradores.

* La publicación de recursos a [!DNL Dynamic Media] se simplifica y refuerza al convertirla en parte integral de la canalización de procesamiento de recursos global mediante microservicios de recursos y mejorar el back-end de publicación por lotes.

* Los pasos de flujo de trabajo que no son compatibles con una implementación de Cloud Service ahora se marcan con una advertencia en el editor de [!UICONTROL modelos de flujo de trabajo]. Además, al ejecutar los flujos de trabajo existentes en el entorno de Cloud Service, se omiten los pasos de flujo de trabajo incompatibles.

* Los modelos de flujo de trabajo creados por clientes que se implementan en `/conf/global` en el proyecto Git asociado con el entorno en [!DNL Cloud Manager] se implementan automáticamente en `/var` y, por lo tanto, están disponibles en [!DNL Experience Manager]. Los modelos de flujo de trabajo de productos en los `/libs` que el cliente cambió no se implementan automáticamente en `/var`.

### Errores corregidos {#assets-bugs-fixed}

* El asistente para mover recursos no se carga como se espera para los recursos incluidos en Colecciones. (CQ-4296756)
* XMP Los valores de `dam:size` y `dam:sha1` se excluyen de la reescritura de la escritura de la. (CQ-4237355)
* Al cancelar la publicación de recursos de forma masiva, [!DNL Brand Portal] genera un error que sugiere que el URI de solicitud es demasiado largo. (CQ-4299474)

## as a Cloud Service de Adobe Experience Manager Commerce {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

AEM Commerce ahora está disponible en Cloud Service.

AEM Consulte [Introducción a Commerce as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html?lang=es) para obtener más información.

## Componentes principales {#core-components}

### Novedades {#what-is-new-core-components}

La versión 2.11.0 de los [componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) ya está disponible como parte de AEM Sites, incluidos:

* Introducción a un nuevo [componente visualizador de PDF](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html).

* Ya está disponible la compatibilidad con las páginas móviles aceleradas (AMP) de los componentes principales. Produce experiencias de cliente más rápidas al hacer la transición de página instantáneamente al entrar al sitio desde un resultado de búsqueda móvil de Google, lo que mejora la participación del usuario y la optimización de los motores de búsqueda.
Consulte [Compatibilidad con AMP para los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=es) para obtener más información.

* Compatibilidad con la versión 1.0.2 de [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=es).

* Correcciones de errores y mejoras en la calidad de los códigos.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de [!UICONTROL Cloud Manager] versión 2020.7.0 es 9 de julio de 2020.

### Novedades {#what-is-new-cloud-manager}

* Se rediseñó la página entornos.

* Cuando están en hibernación, los entornos en hibernación ahora muestran el estado discreto en Cloud Manager.

* Se aumentó el número de variables de entorno por entorno a 200.

* Las canalizaciones de Cloud Manager ahora admiten las variables y los secretos establecidos por el cliente.

  Consulte las Variables de canalización para obtener más información.

* Ahora se admiten repositorios de Maven privados enlazados con la autenticación.

* El contenedor de generación de Cloud Manager ahora admite Java 8 y Java 11.
Consulte Uso de la compatibilidad con Java 11 para obtener más información.

### Correcciones de errores {#bug-fixes-cm}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa de zona protegida.

* Las opciones **Cancelar** y **Guardar** de la página de edición de la canalización sin producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Al crear un programa, el nombre sugerido a veces devolvía un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.

### Problemas conocidos {#known-issues}

* Debido a un cambio en la forma de calcular la cobertura del código, la versión *mínima* del complemento Jacoco es ahora 0.7.5.201505241946 (publicada en mayo de 2015). Los clientes que hagan referencia explícita a una versión anterior reciben un mensaje de error en el proceso de calidad del código.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Novedades {#what-is-new-foundations}

* [Los registros se pueden reenviar a cuentas de Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs), lo que permite a las organizaciones utilizar su inversión en Splunk.

* [Se puede asignar una dirección IP de salida estática y dedicada](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) para el tráfico de salida programado en código Java, lo cual puede resultar útil para algunas integraciones.

* Se ha portado la interfaz de usuario del servicio en la nube de Analytics de AEM Classic a la nueva interfaz de usuario de AEM. También se movió la ubicación del servicio en la nube de Analytics en el repositorio de AEM de `/etc` a `/conf`, para alinearlo con otros servicios de nube AEM.

* Se ha portado la interfaz de usuario del servicio en la nube de Target de AEM Classic a la nueva interfaz de usuario de AEM. También se movió la ubicación del servicio en la nube de Target en el repositorio de AEM de `/etc` a `/conf`, para alinearlo con otros servicios de nube AEM.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.0.2.

### Correcciones de errores {#cra-bug-fixes}

* La versión anterior de CRA no se podía ejecutar en Adobe Experience Manager (AEM) 6.1. Se agregó compatibilidad explícita para permitir usuarios en el grupo de administradores.

  AEM Consulte [Instalación de CRA en la versión 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html?lang=es#installing-on-aem61) de para obtener más información.

* La marca de tiempo de caducidad que se muestra en el informe de resumen era incorrecta.

* CRA detectaba componentes personalizados duplicados.

* En AEM 6.1, la inspección de contenido se cerraba antes de completar toda la inspección. Se añadió la gestión de excepciones para permitir que el inspector omita y continúe hasta completar toda la inspección.
