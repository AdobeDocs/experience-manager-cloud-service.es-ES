---
title: Monitorización de infraestructura y servicios en AEM as a Cloud Service
description: Monitorización de infraestructura y servicios en AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 5%

---

# Monitorización de infraestructura y servicios en AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service ofrece funciones de observación y monitorización de: infraestructura, servicios y experiencia del usuario. Dado que se utilizan varias soluciones y hay varios niveles de monitorización, esta página está organizada en tres secciones:

* [Disponibilidad externa](#external-availability)
* [Monitorización del módulo interno](#module-monitoring)
* [Observabilidad del cliente](#customer-observability)

AEM as a Cloud Service utiliza cientos de monitores nativos de la nube para informar continuamente del estado de cada entorno (24/7) durante 365 días al año. Las definiciones de los monitores no son estáticas, sino que se revisan continuamente para mejorar la capacidad de detección precoz. Además, el Adobe tiene configurados procedimientos de atención continuada para responder a las alertas.

Si necesita información sobre otros tipos de supervisión, como el registro o la supervisión a través de Cloud Manager, consulte [Recursos adicionales](#resources).

## Disponibilidad externa {#external-availability}

La disponibilidad externa consta de dos partes: Service Edge y Monitorización personalizada.

### Service Edge {#service-edge}

La disponibilidad de todos los entornos de AEM as a Cloud Service se supervisa. Sin embargo, la Monitorización de Service Edge solo se configura para entornos de producción y las métricas se utilizan para calcular el SLA del cliente. Tiene en cuenta el tiempo de ejecución del entorno y la CDN de AEM as a Cloud Service. Service Edge Monitoring emplea cinco ubicaciones distintas cercanas a la región elegida y comprueba periódicamente la disponibilidad. Déclencheur La indisponibilidad de un sitio avisa y pone en contacto a los equipos y procesos de asistencia a petición de los Adobes.

### Monitorización personalizada {#custom-monitoring}

Con la supervisión personalizada, los clientes pueden, opcionalmente, proporcionar hasta cinco direcciones URL de propiedades web distintas antes de [publicar](/help/journey-migration/go-live.md). Estas direcciones URL deben ser válidas y devolver un código de respuesta HTTP 200. Estos monitores admiten clientes que [traen su propia CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) delante de la CDN de Adobe y cualquier enrutamiento de tráfico externo empleado delante de AEM as a Cloud Service que no esté bajo el control de Adobe. Las alertas resultantes de las comprobaciones de Supervisión personalizada involucran a los equipos y procesos de asistencia de Adobe.

>[!NOTE]
>
> Esta funcionalidad solo se ofrece para entornos de producción y clientes con [Soporte avanzado en la nube](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html?lang=es#support-add-ons). Si tiene alguna pregunta, póngase en contacto con el equipo de su cuenta de Adobe.

## Monitorización del módulo interno {#module-monitoring}

Mientras que la disponibilidad externa se centra en la monitorización del usuario final, la monitorización del módulo interno observa si los subsistemas de arquitectura funcionan nominalmente sin una degradación de las características o del rendimiento. Si hay algún problema, las alertas se activan para que las reparaciones se puedan realizar de forma automática o mediante la participación del equipo de operaciones, con el objetivo de evitar que se comprometa la disponibilidad. Existen varias categorías de monitores, que se presentan a continuación y son algunas comprobaciones de ejemplo:

* El porcentaje de espera de CPU no supera un umbral determinado.
* Las reimplementaciones de instancias no superan una frecuencia determinada.
* El uso del disco está por debajo de un determinado umbral.
* El tamaño del repositorio de creación está dentro de ciertos límites.
* Las operaciones de copia de seguridad se completaron correctamente.
* Se supervisa el estado y el rendimiento de la base de datos.
* AEM Los servicios en la nube de se comportan según lo esperado, incluidas las colas de replicación sin bloquear, los datos coherentes y las consultas con rendimiento.

Se añaden comprobaciones adicionales a los entornos aprovisionados para Forms. Las definiciones de comprobación no son estáticas y están sujetas a cambios y actualizaciones.

## Observabilidad del cliente {#customer-observability}

Los clientes pueden usar el conjunto de aplicaciones [New Relic Application Performance Monitoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=es) que proporciona datos de rendimiento en tiempo real recopilados y representados para su análisis y solución de problemas. Mediante el grupo de monitorización, los clientes pueden observar directamente varias métricas, como: métricas de rendimiento de JVM, tiempo de transacción para Java™, llamadas externas en segundo plano y llamadas a bases de datos.

## Recursos adicionales {#resources}

* [Supervisión del rendimiento de las aplicaciones New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html?lang=es)
* [Registrando para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=es)
* [Supervisar Entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html?lang=es)
