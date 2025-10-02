---
title: Introducción a Edge Delivery Services en Cloud Manager
description: Aprenda a enviar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac918008c3f99d74e01be59c9841083abf3604aa
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 93%

---


# Introducción a Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esto le permite hacer lo siguiente:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta.
* Monitorizar de forma continua del rendimiento mediante la telemetría operativa.
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido.

Puede usar tanto la administración de contenido de AEM como la creación WYSIWYG utilizando el editor universal además de la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar Edge Delivery Services para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de Edge Delivery Services y cómo se pueden usar con AEM, consulte la [información general de Edge Delivery Services](/help/edge/overview.md).

## Acerca de Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene licencia para Edge Delivery Services como parte de Adobe Experience Manager Sites, puede integrar su sitio con Edge Delivery Services directamente en Cloud Manager y ponerlo en marcha [con una experiencia de autoservicio guiada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

Además, podrá acceder a una experiencia unificada para administrar todas sus propiedades AEM y garantizar la coherencia de los flujos de trabajo clave. Estos flujos de trabajo incluyen la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

## Ventajas de utilizar la ruta recomendada por Adobe para Edge Delivery Services {#recommended-path-eds}

Maximice sus ventajas de Adobe accediendo a sus licencias de Edge Delivery Services y consumiéndolas a través de Cloud Manager. Al hacerlo, puede aprovechar varias ventajas clave.

* [Consuma su licencia en el programa elegido](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [actualice otros programas](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o ambos.
* Aproveche los beneficios del enfoque [API primero](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para realizar operaciones CRUD (crear, leer, actualizar y eliminar).
* [Acceso a informes de SLA](/help/implementing/cloud-manager/reports/report-sla.md)
* [Obtenga acceso a la compatibilidad con Adobe](/help/edge/overview.md#support-ticket) para sus programas de producción registrados.

Si tiene una licencia de Edge Delivery Services (EDS), puede usar una [CDN administrada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) para su sitio de Edge Delivery. Al hacerlo, se habilita la administración de CDN de autoservicio y los certificados DV que se renuevan automáticamente cada tres meses a menos que elimine el certificado.

O bien, si decide utilizar su CDN (es decir, una CDN no administrada por Adobe), independientemente de las licencias de Edge Delivery Services, debe configurarla en la plataforma `aem.live`. Consulte [Configuración de BYO CDN](https://www.aem.live/docs/byo-cdn-setup).


## Acerca de la adición de Edge Delivery Services a un programa de producción o de zona protegida

Se puede añadir Edge Delivery Services de varias formas diferentes, en función de cómo haya iniciado el proyecto o de cuándo desee crear el sitio.

| Caso de uso | Descripción |
| --- | --- |
| Deseo añadir Edge Delivery Services a un nuevo programa de producción. | Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>En el asistente, en la pestaña **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo añadir Edge Delivery Services a un programa de producción existente. | Consulte [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>En el cuadro de diálogo **Editar programa**, en la pestaña **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Añadir un sitio de Edge Delivery a Cloud Manager | Consulte [Añadir un sitio de Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Deseo crear un sitio de Edge Delivery ahora | Consulte [Crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| Deseo añadir Edge Delivery Services a un programa de zona protegida nuevo o existente. | Consulte [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Al crear un programa de zona protegida, Edge Delivery Services se añade al programa por defecto; no es necesario que lo seleccione.<br>Los programas de zona protegida existentes antes de la disponibilidad general de Edge Delivery heredan Edge Delivery Services automáticamente. |

>[!NOTE]
>
>* Para añadir o editar programas, debe ser miembro de la función **Propietario del negocio** o tener permiso para hacerlo.
>* Su organización debe tener una licencia de Edge Delivery Services no utilizada para poder aplicarla a un programa de producción.
>* Una vez que la licencia de Edge Delivery Services se aplica a un programa o se elimina de él, el cambio entra en vigor inmediatamente sin necesidad de ejecutar una canalización.


## Acerca de la lista de tareas pendientes de Edge Delivery en Cloud Manager {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

La **lista de tareas pendientes de Edge Delivery** en Cloud Manager es una lista de comprobación de tareas de incorporación diseñada para guiarlo a través de la incorporación y administrar su sitio de Edge Delivery hasta [el lanzamiento](/help/journey-onboarding/go-live-checklist.md).

![Lista de tareas pendientes del sitio de Edge Delivery en Cloud Manager.](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Tarea | Descripción |
| --- | --- | --- |
| 1 | Únase al canal de colaboración de productos | Al hacer clic en **Enviar solicitud ahora**, se envía una solicitud a Adobe para crear un canal para su compañía. Si el canal ya existe, se le reenviará al canal de su compañía. |
| 2 | Complete los requisitos previos | Consulte [Ver el tutorial de introducción](https://www.aem.live/developer/tutorial). |
| 3 | Agregar sitio Edge Delivery O <br>Crear un sitio ahora | Consulte [Añadir un sitio de Edge Delivery](#eds-add-site).<br>Consulte [Crear un sitio de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| 4 | Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo | Consulte la [Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md). |
| 5 | Añadir dominio | Consulte [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 6 | Añadir certificado SSL | Consulte [Añadir certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 7 | Configure la CDN de su sitio de Edge Delivery | Consulte [Añadir una asignación de dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md). |
| 8 | Configuración de validación push | Ver [Configuración de validación push para un sitio Edge Delivery](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md). |
| 9 | Go-Live | Consulte [Lista de comprobación de lanzamiento](https://www.aem.live/docs/go-live-checklist). |

>[!VIDEO](https://video.tv.adobe.com/v/3441564?learn=on&captions=spa)

## Registro de un vale de asistencia {#eds-support-ticket}

{{support-ticket}}



