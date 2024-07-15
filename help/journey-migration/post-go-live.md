---
title: Publicar Go-Live
description: Obtenga información sobre cómo supervisar problemas y mejorar el rendimiento
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 22%

---

# Publicar Go-Live {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Solución de problemas de AEM"
>abstract="Revise las prácticas recomendadas para el desarrollo continuo y administre los registros junto con herramientas como Developer Console y CRXDE Lite para ayudar a solucionar problemas con AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=es" text="Acceder y administrar registros"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es#aem-as-a-cloud-service-development-tools" text="Herramientas de desarrollo de AEM as a Cloud Service"

Este recorrido es la última parte, por lo que aprenderá a monitorizar los problemas y mejorar el rendimiento una vez completada la migración. Debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

## La historia hasta ahora {#story-so-far}

En el paso anterior del recorrido, aprendió a realizar la migración y [Go-live](/help/journey-migration/go-live.md) una vez que el código y el contenido estaban listos para moverse a AEM as a Cloud Service.

## Objetivo {#objective}

En este documento se describen las herramientas disponibles para solucionar problemas de entornos de AEM as a Cloud Service:

* **Developer Console**
* **CRXDE Lite**
* **Administración de registros**

## Consola de desarrollador {#developer-console}

La depuración de los entornos de desarrollador de AEM as a Cloud Service está disponible en Developer Console para los entornos de desarrollo, fase y producción.

Consulte [Implementación para AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) para obtener más información sobre las herramientas de desarrollo.

## CRXDE Lite {#crxde-lite}

Como usuario, puede acceder a CRXDE Lite en el entorno de desarrollo, pero no en la fase o en la producción.

>[!IMPORTANT]
>Escribir en repositorios inmutables como `/libs` y `/apps` en tiempo de ejecución genera errores. Además, no tiene acceso a las herramientas para desarrolladores para entornos de ensayo y producción.

Consulte [Desarrollo con CRXDE Lite AEM](/help/implementing/developing/tools/crxde.md) para obtener más información sobre cómo desarrollar su aplicación de forma que utilice el CRXDE Lite de la aplicación de la aplicación de la aplicación.

## Administración de registros {#managing-logs}

Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Consulte [Acceso y administración de registros](/help/implementing/cloud-manager/manage-logs.md) para obtener información sobre cómo acceder y administrar los registros a través de la interfaz de usuario o desde la API mediante Cloud Manager.

## Contacto con el soporte {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Ayuda y asistencia"
>abstract="Póngase en contacto con el equipo de Soporte AEM de Adobe para obtener aclaraciones o solucionar cualquier problema."
>additional-url="https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html" text="Compatibilidad con Experience Cloud"

Si tienes preguntas sobre el acceso a Cloud Service, ponte en contacto con el Adobe o con [Soporte técnico para Experience Cloud](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para obtener más información.

## Aprendizajes de documentos {#document-learnings}

Una vez completada la migración, documente los conocimientos adquiridos durante este proceso. Algunas preguntas que pueden ayudar en el proceso de documentación son las siguientes:

* ¿Qué funcionó bien y qué no?
* ¿Cuáles fueron los principales puntos problemáticos?
* Recommendations si hay una migración futura.

Comparta estos conocimientos posteriores a la migración con las partes interesadas y los equipos de su organización.

## El recorrido ha terminado, ¿o no? {#journey-ends}

Felicitaciones. Ha completado el Recorrido de migración de AEM as a Cloud Service. Debe tener conocimientos de cómo hacer lo siguiente:

* Introducción al paso a AEM as a Cloud Service
* Determine si la implementación está lista para moverse a AEM as a Cloud Service
* Preparar el código y la nube de contenido
* Realizar la migración
* Supervisar problemas y mejorar el rendimiento
