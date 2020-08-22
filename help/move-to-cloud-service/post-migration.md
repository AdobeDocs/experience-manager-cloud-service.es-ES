---
title: Fase posterior a la migración
description: Fase posterior a la migración
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 100%

---


# Posterior a la migración {#post-migration}

En la fase Posterior a la migración, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

Las siguientes herramientas están disponibles para solucionar los problemas de los entornos de AEM as a Cloud Service:

* **Developer Console**
* **CRXDE Lite**
* **Administración de registros**


## Developer Console {#developer-console}

La depuración de los entornos de desarrollador de AEM as a Cloud Service está disponible en Developer Console para los entornos de desarrollo, fase y producción.

Consulte [ Implementación para AEM as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) para obtener más información sobre las herramientas de desarrollo.

## CRXDE Lite {#crxde-lite}

Los clientes pueden acceder a la lista **CRXDE Lite** en el entorno de desarrollo, pero no en la fase o en la producción.

>[!IMPORTANT]
>No se puede escribir en el repositorio inmutable `/libs` y `/apps` durante la ejecución, por lo que al intentar hacerlo se generan errores. Además, los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo de CRXDE Lite](https://docs.adobe.com/help/es-ES/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) para obtener información sobre cómo desarrollar la aplicación AEM con CRXDE Lite.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Consulte [Acceso y administración de registros](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para obtener información sobre cómo acceder y administrar los registros a través de la IU o desde la API de Cloud Manager.

### Asistencia técnica adicional {#additional-support}

Si surge alguna pregunta sobre el acceso a Cloud Service, ponte en contacto con el representante de Adobe o con el portal de asistencia de Adobe AEM CQ.
