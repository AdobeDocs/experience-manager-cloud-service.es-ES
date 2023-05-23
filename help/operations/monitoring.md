---
title: Monitorización de infraestructura y servicios en AEM as a Cloud Service
description: Monitorización de infraestructura y servicios en AEM as a Cloud Service
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 5%

---

# Monitorización de infraestructura y servicios en AEM as a Cloud Service {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service ofrece funciones de observación y monitorización de: infraestructura, servicios y experiencia del usuario. Dado que se utilizan varias soluciones y hay varios niveles de monitorización, esta página está organizada en tres secciones:

* [Disponibilidad externa](#external-availability)
* [Monitorización del módulo interno](#module-monitoring)
* [Observabilidad del cliente](#customer-observability)

AEM as a Cloud Service utiliza cientos de monitores nativos de la nube para informar continuamente del estado de cada entorno (24/7) durante 365 días al año. Las definiciones de los monitores no son estáticas, sino que se revisan continuamente para mejorar la capacidad de detección precoz. Además, el Adobe tiene configurados procedimientos de atención continuada para responder a las alertas.

Si necesita información sobre otros tipos de monitorización, como el registro o la monitorización a través de Cloud Manager, consulte [Recursos adicionales](#resources).

## Disponibilidad externa {#external-availability}

La disponibilidad externa consta de dos partes: Service Edge y Supervisión personalizada.

### Service Edge {#service-edge}

AEM Se supervisa la disponibilidad de todos los entornos de los as a Cloud Service. Sin embargo, la monitorización perimetral de servicio solo está configurada para entornos de producción y las métricas se utilizan para calcular el SLA del cliente. AEM Tiene en cuenta el tiempo de ejecución del entorno y la CDN as a Cloud Service. La Monitorización perimetral de servicio emplea cinco ubicaciones distintas cercanas a la región elegida y comprueba periódicamente la disponibilidad. Déclencheur La indisponibilidad de un sitio avisa y pone en contacto a los equipos y procesos de asistencia a petición de los Adobes.

### Monitorización personalizada {#custom-monitoring}

Con la Monitorización personalizada, los clientes pueden, opcionalmente, proporcionar hasta cinco direcciones URL de propiedad web distintas antes de que [puesta en marcha](/help/journey-migration/go-live.md). Estas direcciones URL deben ser válidas y devolver un código de respuesta HTTP 200. Estos monitores admiten clientes que [traer su propia CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) delante de la CDN de Adobe AEM y cualquier enrutamiento de tráfico externo empleado delante de la red as a Cloud Service que no esté bajo control del Adobe. Las alertas resultantes de las comprobaciones de Supervisión personalizada involucran a los equipos y procesos de asistencia de Adobe.

>[!NOTE]
>
> Esta funcionalidad solo se ofrece a los clientes con [Soporte avanzado en la nube.](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) Si tiene alguna pregunta, presente un caso de asistencia técnica a través del Admin Console.

## Monitorización del módulo interno {#module-monitoring}

Mientras que la disponibilidad externa se centra en la monitorización del usuario final, la monitorización del módulo interno observa si los subsistemas de arquitectura funcionan nominalmente sin una degradación de las características o del rendimiento. Si hay algún problema, las alertas se activan para que las reparaciones se puedan realizar de forma automática o mediante la participación del equipo de operaciones, con el objetivo de evitar que se comprometa la disponibilidad. Existen varias categorías de monitores, que se presentan a continuación y son algunas comprobaciones de ejemplo:

* El porcentaje de espera de CPU no supera un umbral determinado.
* Las reimplementaciones de instancias no superan una frecuencia determinada.
* El uso del disco está por debajo de un determinado umbral.
* El tamaño del repositorio de creación está dentro de ciertos límites.
* Las operaciones de copia de seguridad se completaron correctamente.
* Se supervisa el estado y el rendimiento de la base de datos.
* Los servicios de nube AEM se comportan según lo esperado, incluidas las colas de replicación sin bloquear, los datos coherentes y las consultas de rendimiento.

Se añaden comprobaciones adicionales a los entornos aprovisionados para Forms. Las definiciones de comprobación no son estáticas y están sujetas a cambios y actualizaciones.

## Observabilidad del cliente {#customer-observability}

Los clientes pueden utilizar el [Monitorización del rendimiento de aplicaciones New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) grupo que proporciona datos de rendimiento en tiempo real recopilados y representados para su análisis y solución de problemas. Mediante el grupo de monitorización, los clientes pueden observar directamente varias métricas, como: métricas de rendimiento de JVM, tiempo de transacción para Java™, llamadas externas en segundo plano y llamadas a bases de datos.

## Recursos adicionales {#resources}

* [Monitorización del rendimiento de aplicaciones New Relic](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [AEM Registro para la as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [Monitorización de entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
