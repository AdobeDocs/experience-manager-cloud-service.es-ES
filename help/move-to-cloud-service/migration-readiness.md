---
title: Fase de preparación
description: Fase de preparación
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: 6fcde5440a5e2eec57b69b14dca93192634b3c3a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 87%

---

# Preparación {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planificación de la transición"
>abstract="Antes de comenzar el viaje de transición a Cloud Service, debe familiarizarse con AEM as a Cloud Service, revisar los cambios importantes que se le han realizado y también las funciones que se han sustituido o están en desuso."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Analizador de prácticas recomendadas"

Antes de comenzar el viaje de transición a Cloud Service, debe familiarizarse con AEM as a Cloud Service, revisar los cambios importantes que se le han realizado y también las funciones que se han sustituido o están en desuso.

## Cambios importantes {#notable-changes}

AEM as a Cloud Service ofrece muchas nuevas funciones y posibilidades para la gestión de sus proyectos AEM.

Sin embargo, existen varias diferencias entre AEM On-Premise o en Adobe Managed Services en comparación con AEM as a Cloud Service.

Consulte los [Cambios destacados en AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html) para comprender las diferencias importantes.

## Funciones en desuso {#deprecated-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Consulte las [Funciones en desuso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) para obtener más información sobre las funciones y capacidades que se han marcado como en desuso en Experience Manager as a Cloud Service.

## Explicación de la fase de planificación {#introduction}

La siguiente figura muestra los pasos clave involucrados durante la fase de planificación:

![image](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Evaluación de la preparación de Cloud Service {#access-cloud-readiness}

El primer paso en la fase de planificación es evaluar la preparación para pasar de la versión de AEM existente a Cloud Service y determinar las áreas que requerirán refactorización para que sean compatibles con AEM as a Cloud Service.

Deberá realizar una evaluación completa del código origen actual de AEM en relación con los cambios notables y las funciones en desuso para determinar el nivel de esfuerzo esperado en el viaje de transición.

Puede acelerar el paso de evaluación ejecutando el Analizador de prácticas recomendadas en su versión AEM actual. Para obtener más información, consulte [Best Practices Analyzer](/help/move-to-cloud-service/best-practices-analyzer/overview-best-practices-analyzer.md).

>[!NOTE]
>Si ya tiene acceso a Cloud Manager y a un entorno de servicios en la nube, se recomienda ejecutar el código actual en una canalización de calidad de código de Cloud Manager para evaluar los cambios de código necesarios y que sean compatibles con Cloud Service.

### Revisión de la planificación de recursos {#review-resource-planning}

Una vez que haya calculado el nivel de esfuerzo que se requerirá para pasar a Cloud Service, debe identificar los recursos, crear un equipo y asignar funciones y responsabilidades para el proceso de transición.

### Establecimiento de los KPI {#establish-kpis}

Si no ha establecido los indicadores de rendimiento clave (KPI) anteriormente, se recomienda establecer los KPI para la implementación de Adobe Experience Manager (AEM) para ayudar a su equipo a centrarse en lo que más importa.

Consulte el [Desarrollo de los KPI](https://guided.adobe.com/welcome/aem/part6.html) para conocer cómo elegir los KPI adecuados para sus objetivos empresariales.
