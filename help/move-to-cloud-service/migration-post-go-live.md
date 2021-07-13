---
title: Fase de Publicar Go Live
description: Fase de Publicar Go Live
exl-id: f9b0b2fa-e29c-4faa-a5e7-e5edd04b25ca
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 60%

---

# Publicar Go Live {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solución de problemas AEM"
>abstract="Revise las prácticas recomendadas para el desarrollo continuo y administre los registros junto con herramientas como Developer Console y CRXDE Lite para ayudar a solucionar problemas con AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Acceder y administrar registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="Herramientas de desarrollo de AEM as a Cloud Service"


En la fase de Publicar Go-live, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

Las siguientes herramientas están disponibles para solucionar los problemas de los entornos de AEM as a Cloud Service:

* **Developer Console**
* **CRX/DE Lite**
* **Administración de registros**


## Developer Console {#developer-console}

La depuración de los entornos de desarrollador de AEM as a Cloud Service está disponible en Developer Console para los entornos de desarrollo, fase y producción.

Consulte [ Implementación para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools) para obtener más información sobre las herramientas de desarrollo.

## CRX/DE Lite {#crxde-lite}

Los clientes pueden acceder a la lista CRX/DE Lite en el entorno de desarrollo, pero no en la fase o en la producción.

>[!IMPORTANT]
>No se puede escribir en el repositorio inmutable `/libs` y `/apps` durante la ejecución, por lo que al intentar hacerlo se generan errores. Además, los clientes no tendrán acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo de CRX/DE Lite](/help/implementing/developing/tools/crxde.md) para obtener información sobre cómo desarrollar la aplicación AEM con CRX/DE Lite.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Consulte [Acceso y administración de registros](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html) para obtener información sobre cómo acceder y administrar los registros a través de la IU o desde la API de Cloud Manager.

### Asistencia técnica adicional {#additional-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ayuda y asistencia"
>abstract="Póngase en contacto con nuestro equipo de asistencia AEM para obtener aclaraciones o para solucionar cualquier problema."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Compatibilidad con el Experience Cloud"

Si tiene alguna pregunta sobre el acceso al Cloud Service, póngase en contacto con su representante de Adobes o [Soporte para Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obtener más información.
