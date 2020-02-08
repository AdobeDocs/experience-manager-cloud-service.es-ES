---
title: Cambios notables en Recursos Adobe Experience Manager como servicio de nube
description: Cambios notables en los recursos de Adobe Experience Manager en el servicio de nube de AEM en comparación con Experience Manager 6.5
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Cambios notables en Experience Manager Assets como un servicio de nube {#notable-changes}

Adobe Experience Manager como servicio de nube ofrece muchas funciones y posibilidades nuevas para administrar sus proyectos de AEM. Sin embargo, existen varias diferencias entre los recursos de Experience Manager in situ o en los servicios administrados de Adobe en comparación con Experience Manager como servicio de nube. Este documento destaca las importantes diferencias.

>[!NOTE]
>
>En este documento se destacan los cambios notables específicos de Experience Manager Assets como servicio de nube. Consulte los [cambios genéricos realizados en Experience Manager como un servicio](/help/release-notes/aem-cloud-changes.md)de nube.

Las principales diferencias en comparación con Experience Manager 6.5 se encuentran en las siguientes áreas:

* [Ingesta de recursos](#asset-ingestion)
* [Eliminación de la IU clásica](#classic-ui)

## Ingesta de recursos {#asset-ingestion}

La carga de recursos se ha optimizado para que sea más eficaz, lo que permite una mejor ampliación de la ingesta de recursos y cargas más rápidas. Se han actualizado las capacidades del producto (interfaces de usuario web, clientes de escritorio). Sin embargo, esto puede afectar a algunos códigos personalizados existentes.

* Experience Manager utiliza el principio de acceso binario directo para los microservicios de carga y descarga y de recursos para el procesamiento de recursos. Consulte [información general sobre la ingesta de recursos](/help/assets/asset-microservices-overview.md)
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * Para obtener información técnica, consulte el protocolo de carga binaria [directa y las API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* El flujo de trabajo predeterminado de actualización **[!UICONTROL de recursos]** DAM en versiones anteriores de AEM ya no está disponible. En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos, extracción de texto para indexación)
   * Consulte [Configuración y uso de microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos personalizados de flujo de trabajo en el procesamiento, se pueden utilizar flujos de trabajo [](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) posteriores al procesamiento
* Los recursos que se incluyen mediante el Administrador de paquetes requieren un reprocesamiento manual mediante la acción **[!UICONTROL Volver a procesar recursos]** de la interfaz de Recursos.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos (las mismas convenciones de nombres).

## Desarrollar y probar microservicios de activos {#developing-testing-asset-microservices}

Asset microservices es un servicio en la nube nativo que se aprovisiona automáticamente y se envía por cable a Experience Manager en programas y entornos de clientes administrados en Cloud Manager. Los desarrolladores que trabajen para ampliar Experience Manager o para realizar personalizaciones pueden utilizar el contenido existente (o los recursos con representaciones generadas en un entorno de nube) para probar y validar su código mediante el uso, la visualización y la descarga de recursos.

Para realizar una validación completa del código y del proceso, incluida la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante la canalización y realice pruebas con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en Experience Manager como servicio de nube.
