---
title: Monitorización de infraestructura y servicios en AEM as a Cloud Service
description: Monitorización de infraestructura y servicios en AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 34fed4e64b49ab32e7025c9654d930e3fa362a52
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Monitorización de infraestructura y servicios en AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service proporciona capacidad de observación y supervisión de: infraestructura, servicios y experiencia del usuario. Dado que se utilizan varias soluciones y que hay varias capas de monitorización, esta página está organizada en tres secciones:

* [Disponibilidad externa](#external-availability)
* [Supervisión interna del módulo](#module-monitoring)
* [Observabilidad del cliente](#customer-observability)

AEM as a Cloud Service utiliza cientos de monitores nativos de la nube para informar continuamente sobre el estado de cada entorno (24 horas al día, 7 días a la semana) durante 365 días al año. Las definiciones de monitor no son estáticas, se revisan continuamente para mejorar la capacidad de detección temprana. Además, el Adobe tiene configurados procedimientos de llamada para responder a las alertas.

Si necesita información sobre otros tipos de supervisión, como el registro o la supervisión a través de Cloud Manager, consulte la [Recursos adicionales](#resources) para obtener más información.

## Disponibilidad externa {#external-availability}

La disponibilidad externa consta de dos partes: Monitorización personalizada y perimetral de servicio.

### Edge de servicio {#service-edge}

Todos los entornos as a Cloud Service AEM están monitoreados para verificar la disponibilidad. Sin embargo, la supervisión de servidor perimetral solo está configurada para entornos de producción y las métricas se utilizan para calcular el SLA del cliente. Tiene en cuenta el tiempo de ejecución del entorno y la AEM CDN as a Cloud Service. La supervisión de servidor perimetral emplea cinco ubicaciones distintas cercanas a la región elegida y comprueba periódicamente la disponibilidad. La falta de disponibilidad de un sitio generará un déclencheur y activará los procesos y equipos de asistencia de Adobe que estén disponibles durante la llamada.

### Supervisión personalizada {#custom-monitoring}

Con la supervisión personalizada, los clientes tienen la opción de proporcionar hasta cinco direcciones URL de propiedades web distintas antes de [going live](/help/journey-migration/go-live.md). Estas direcciones URL deben ser válidas y devolver un código de respuesta HTTP 200. Estos monitores admiten a los clientes que [traer su propia CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) delante de la CDN de Adobe y cualquier enrutamiento de tráfico externo empleado frente a AEM as a Cloud Service que no esté bajo control del Adobe. Las alertas resultantes de las comprobaciones de supervisión personalizada activarán los equipos y procesos de asistencia de Adobe.

>[!NOTE]
>
> Esta funcionalidad solo se ofrece a los clientes con compatibilidad avanzada con Cloud. Si tiene alguna pregunta, plantee un caso de asistencia técnica a través de Admin Console.

## Supervisión del módulo interno {#module-monitoring}

Si bien la disponibilidad externa se centra en la supervisión de los usuarios finales, la supervisión interna de los módulos observa si los subsistemas arquitectónicos funcionan nominalmente sin deterioro de las características o del rendimiento. En caso de problema, las alertas se activan para que las reparaciones se puedan realizar de forma automática o mediante la participación del equipo de operaciones, con el objetivo de evitar la disponibilidad comprometida. Existen varias categorías de monitores, a continuación se presentan algunos ejemplos de comprobaciones:

* El porcentaje de espera de CPU no supera un determinado umbral.
* Las redistribuciones de instancias no superan una determinada frecuencia.
* El uso del disco está por debajo de un cierto umbral.
* El tamaño del repositorio del autor está dentro de ciertos límites.
* Las operaciones de copia de seguridad se completan correctamente.
* Se supervisa el estado y el rendimiento de la base de datos.
* Los servicios de AEM Cloud se comportan del modo esperado, incluida la ausencia de colas de replicación bloqueadas, datos coherentes y consultas de rendimiento.

Se agregan comprobaciones adicionales a los entornos aprovisionados para Forms. Tenga en cuenta que las definiciones de comprobación no son estáticas y están sujetas a cambios y actualizaciones.

## Observabilidad del cliente {#customer-observability}

Los clientes pueden usar la variable [Supervisión del rendimiento de las aplicaciones de New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) que proporciona datos de rendimiento en tiempo real recopilados y marcados para su análisis y resolución de problemas. Mediante el grupo de monitorización, los clientes pueden observar directamente varias métricas, tales como: Métricas de rendimiento de JVM, tiempo de transacción para Java, llamadas externas en segundo plano y llamadas de base de datos.

## Recursos adicionales {#resources}

* [Supervisión del rendimiento de las aplicaciones de New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [Registro para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Monitorización de entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
