---
title: Fase de lanzamiento posterior
description: Fase de lanzamiento posterior
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Publicar Go-live {#post-go-live}

En la fase de lanzamiento posterior, debe garantizar la limpieza de los archivos temporales, revisar las optimizaciones para el desarrollo continuo y administrar los registros.

Las siguientes herramientas están disponibles para solucionar problemas de AEM como entornos de servicio en la nube:

* **Developer Console**
* **CRXDE Lite**
* **Administración de registros**


## Developer Console {#developer-console}

La depuración de AEM como entornos de desarrollador de Cloud Service está disponible en Developer Console para entornos de desarrollo, fase y producción.

Consulte [Implementación para AEM como un servicio](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) de nube para obtener más información sobre las herramientas de desarrollo.

## CRXDE Lite {#crxde-lite}

Como usuario, puede acceder a **CRXDE Lite** en el entorno de desarrollo, pero no en el escenario o en la producción.

>[IMPORTANTE]
>Escribir en repositorios inmutables como `/libs` y `/apps` en tiempo de ejecución producirá errores. Además, como cliente, no tendrá acceso a herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo con CRXDE Lite](https://docs.adobe.com/help/en/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) para obtener información sobre cómo desarrollar la aplicación AEM con CRXDE Lite.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro disponibles para el entorno seleccionado.

Consulte [Acceso y administración de registros](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para obtener información sobre cómo acceder y administrar registros a través de la interfaz de usuario o desde la API a través de Cloud Manager.

### Asistencia técnica adicional {#additional-support}

Si tiene alguna pregunta sobre el acceso al servicio de nube, póngase en contacto con su representante de Adobe o con el portal de asistencia de Adobe AEM CQ.
