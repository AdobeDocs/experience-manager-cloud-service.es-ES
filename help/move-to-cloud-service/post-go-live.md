---
title: Fase de Publicar Go-live
description: Fase de Publicar Go-live
translation-type: ht
source-git-commit: 0565d053b6040bc99ae79823711d56eb9aecdfb3
workflow-type: ht
source-wordcount: '242'
ht-degree: 100%

---


# Publicar Go-live {#post-go-live}

En la fase de Publicar Go-live, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

Las siguientes herramientas están disponibles para solucionar los problemas de los entornos de AEM as a Cloud Service:

* **Developer Console**
* **CRX/DE Lite**
* **Administración de registros**


## Developer Console {#developer-console}

La depuración de los entornos de desarrollador de AEM as a Cloud Service está disponible en Developer Console para los entornos de desarrollo, fase y producción.

Consulte [ Implementación para AEM as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) para obtener más información sobre las herramientas de desarrollo.

## CRX/DE Lite {#crxde-lite}

Los clientes pueden acceder a la lista CRX/DE Lite en el entorno de desarrollo, pero no en la fase o en la producción.

>[IMPORTANTE]
>No se puede escribir en el repositorio inmutable `/libs` y `/apps` durante la ejecución, por lo que al intentar hacerlo se generan errores. Además, los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo de CRX/DE Lite](https://docs.adobe.com/help/es-ES/experience-manager-65/developing/devtools/developing-with-crxde-lite.html) para obtener información sobre cómo desarrollar la aplicación AEM con CRX/DE Lite.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Consulte [Acceso y administración de registros](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para obtener información sobre cómo acceder y administrar los registros a través de la IU o desde la API de Cloud Manager.

### Asistencia técnica adicional {#additional-support}

Si surge alguna pregunta sobre el acceso a Cloud Service, ponte en contacto con el representante de Adobe o con el portal de asistencia de Adobe AEM CQ.
