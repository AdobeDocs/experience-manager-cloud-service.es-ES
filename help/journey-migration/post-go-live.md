---
title: Publicar Go-Live
description: Obtenga información sobre cómo monitorizar los problemas y mejorar el rendimiento
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 25%

---

# Publicar Go-Live {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solución de problemas AEM"
>abstract="Revise las prácticas recomendadas para el desarrollo continuo y administre los registros junto con herramientas como Developer Console y CRXDE Lite para ayudar a solucionar problemas con AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Acceder y administrar registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM herramientas de desarrollo as a Cloud Service"

Esta es la última parte del recorrido, por lo que aprenderá a supervisar los problemas y a mejorar el rendimiento una vez completada la migración. Debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

## La historia hasta ahora {#story-so-far}

En el paso anterior del recorrido, ha aprendido a realizar la migración y [Go-live](/help/journey-migration/go-live.md) una vez que el código y el contenido estén listos para moverse a AEM as a Cloud Service.

## Objetivo {#objective}

Este documento describe las herramientas disponibles para solucionar problemas AEM entornos as a Cloud Service:

* **Developer Console**
* **CRXDE Lite**
* **Administración de registros**

## Consola de desarrollador {#developer-console}

La depuración AEM entornos as a Cloud Service de desarrollador está disponible en Developer Console para los entornos de desarrollo, fase y producción.

Consulte [ Implementación para AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) para obtener más información sobre las herramientas de desarrollo.

## CRXDE Lite {#crxde-lite}

Los clientes pueden acceder a la lista CRXDE Lite en el entorno de desarrollo, pero no en la fase o en la producción.

>[!IMPORTANT]
>Escribir en repositorios inmutables como `/libs` y `/apps` en tiempo de ejecución da como resultado errores. Además, no tiene acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo de CRXDE Lite](/help/implementing/developing/tools/crxde.md) para obtener información sobre cómo desarrollar la aplicación AEM con CRXDE Lite.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Consulte [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener información sobre cómo acceder y administrar los registros a través de la IU o desde la API de Cloud Manager.

## Contactar con el servicio de asistencia {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ayuda y asistencia"
>abstract="Póngase en contacto con nuestro equipo de asistencia AEM para obtener aclaraciones o para solucionar cualquier problema."
>additional-url="https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html" text="Compatibilidad con el Experience Cloud"

Si tiene alguna duda sobre el acceso al Cloud Service, póngase en contacto con su representante del Adobe o [Compatibilidad con el Experience Cloud](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para obtener más información.

## Aprendizaje de documentos {#document-learnings}

Una vez completada la migración, debe documentar los conocimientos adquiridos durante este proceso. Algunas preguntas que pueden ayudar en el proceso de documentación son:

* ¿Qué funcionó bien y qué no?
* ¿Cuáles fueron los principales puntos de dolor?
* Recommendations en caso de una migración futura.

A continuación, debe compartir estas lecciones posteriores a la migración con las partes interesadas y los equipos de su organización.

## El recorrido ha terminado, ¿o no? {#journey-ends}

Felicitaciones. ¡Ha completado el Recorrido de migración as a Cloud Service AEM! Debe comprender cómo:

* Introducción a la migración a AEM as a Cloud Service
* Determine si la implementación está lista para moverse a AEM as a Cloud Service
* Preparar el código y la nube de contenido
* Realizar la migración
* Monitorice los problemas y mejore el rendimiento
