---
title: Notas de la versión de 2020.7.0 [!DNL Adobe Experience Manager] de Cloud Service.
description: '[!DNL Adobe Experience Manager] como Cloud Service Notas de la versión 2020.7.0.'
translation-type: tm+mt
source-git-commit: 85f5262c2af7502e98fcb60b51b9b13d2c2c0f2c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 37%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.7.0.

## Fecha de la versión {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager Sites como Cloud Service {#cloud-services-sites}

### Novedades {#what-is-new-sites}

[!DNL Experience Manager] como conectores de Cloud Service para [!DNL Adobe Target] y [!DNL Adobe Analytics] se mejoran de las siguientes maneras:

* Una nueva implementación de interfaz de usuario reemplaza la implementación basada en la IU clásica.

* Se han simplificado los cuadros de diálogo de la interfaz de usuario, lo que permite crear marcos para la asignación de variables y otras configuraciones [!DNL Adobe Launch]. Consulte [Integración de Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) e [Integración de Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html).

* Las configuraciones ahora se almacenan en `/conf` lugar de `/etc/cloudsettings` en el repositorio de Experience Manager.

## Adobe Experience Manager Assets as a Cloud Service {#assets}

### Novedades {#what-is-new-assets}

* [!DNL Asset Compute Service] es un servicio ampliable y ampliable para procesar recursos. Los administradores pueden configurar el Experience Manager para que invoque las aplicaciones personalizadas creadas con el [!DNL Asset Compute Service]. Los desarrolladores pueden utilizar el servicio para crear aplicaciones personalizadas especializadas que se ocupen de casos de uso complejos. Este servicio Web puede generar miniaturas para diferentes tipos de archivos, representaciones de imágenes de alta calidad a partir de formatos de archivo Adobe, codificar vídeos (futuros), extraer metadatos, extraer texto completo como precursor para la indexación y ejecutar un recurso a través de todos los servicios Sensei disponibles. consulte [Uso de microservicios de recursos y perfiles](/help/assets/asset-microservices-configure-and-use.md)de procesamiento.

* Se ha mejorado la configuración inicial de [!DNL Dynamic Media] en [!DNL Experience Manager] calidad de Cloud Service para que sea más robusta. Ahora proporciona el progreso de los procesos a los administradores.

* La publicación de recursos a [!DNL Dynamic Media] se simplifica y refuerza al convertirla en parte integral de la canalización de procesamiento de recursos global mediante microservicios de recursos y mejorar el back-end de publicación por lotes.

* Los pasos de flujo de trabajo que no son compatibles con una implementación de Cloud Service ahora se marcan con una advertencia en el editor de modelos [!UICONTROL de] flujo de trabajo. Además, al ejecutar los flujos de trabajo existentes en el entorno de Cloud Service, se omiten los pasos de flujo de trabajo incompatibles.

* Los modelos de flujo de trabajo creados por clientes implementados `/conf/global` en el proyecto Git asociado con el entorno en Cloud Manager se implementan automáticamente en `/var` y, por lo tanto, están disponibles en Experience Manager. Los modelos de flujo de trabajo de productos en los `/libs` que el cliente cambió no se implementan automáticamente en `/var`.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

AEM Comercio ahora está disponible en Cloud Service.

Consulte [Introducción a AEM comercio como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html) para obtener más información.

## Componentes principales {#core-components}

### Novedades {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* Introducción a un nuevo componente [de visor de](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)PDF.

* Ya está disponible la compatibilidad con las páginas móviles aceleradas (AMP) de los componentes principales. Ayuda a producir experiencias de cliente más rápidas al hacer que la página se transición instantáneamente al entrar al sitio desde un resultado de búsqueda móvil de Google, lo que mejora la participación del usuario y la optimización para motores de búsqueda.
Consulte Compatibilidad con [AMP para los componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) principales para obtener más detalles.

* Compatibilidad con la versión 1.0.2 de la capa [de datos del cliente de](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)Adobe.

* Correcciones de errores y mejoras en la calidad del código.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de [!UICONTROL Cloud Manager] versión 2020.7.0 es 9 de julio de 2020.

### Novedades {#what-is-new-cloud-manager}

* Se rediseñó la página entornos.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* Se aumentó el número de variables de entorno por entorno a 200.

* Las canalizaciones de Cloud Manager ahora admiten las variables y los secretos establecidos por el cliente.

   Consulte [Variables de canalización](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) para obtener más detalles.

### Corrección de errores {#bug-fixes-cm}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Las opciones **Cancelar** y **Guardar** de la página de edición de la canalización sin producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Algunas veces al crear un nuevo programa, el nombre sugerido era un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.

### Problemas conocidos {#known-issues}

* Debido a un cambio en la forma de calcular la cobertura del código, la versión *mínima* del complemento Jacoco es ahora 0.7.5.201505241946 (publicada en mayo de 2015). Los clientes que hacen referencia explícita a una versión anterior reciben un mensaje de error en el proceso de calidad del código.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-foundation}

### Novedades {#what-is-new-foundations}

* [Los registros se pueden reenviar a cuentas](/help/implementing/developing/introduction/logging.md#splunk-logs)de Splunk, lo que permite a las organizaciones aprovechar su inversión en Splunk.

* [Se puede asignar una dirección](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) IP de salida estática y dedicada para el tráfico de salida programado en código Java, lo cual puede resultar útil para algunas integraciones.

* Se ha trasladado la interfaz de usuario del servicio en la nube de Analytics de AEM Classic a la nueva interfaz de usuario de AEM. También se ha movido la ubicación del servicio en la nube de Analytics en AEM repositorio de `/etc` a `/conf`, para alinearlo con otros servicios en la nube de AEM.

* Se ha transferido AEM interfaz de usuario del servicio de nube de Destinatario de la IU clásica a la nueva interfaz de usuario de AEM. También se ha movido la ubicación del servicio de nube de Destinatario en AEM repositorio de `/etc` a `/conf`, para alinearlo con otros servicios de nube de AEM.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.0.2.

### Corrección de errores {#cra-bug-fixes}

* La versión anterior de CRA no se podía ejecutar en Adobe Experience Manager (AEM) 6.1. Se agregó compatibilidad explícita para permitir usuarios en el grupo de administradores.

   Consulte [Instalar CRA en AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obtener más información.

* La marca de tiempo de caducidad que se muestra en el informe de resumen era incorrecta.

* CRA detectaba componentes personalizados duplicados.

* En AEM 6.1, la inspección de contenido se cerraba antes de completar toda la inspección. Se añadió la gestión de excepciones para permitir que el inspector omita y continúe hasta completar toda la inspección.
