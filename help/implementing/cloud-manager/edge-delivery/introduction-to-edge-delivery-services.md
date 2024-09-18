---
title: Introducción a los Edge Delivery Services en Cloud Manager
description: Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ad6a0e13f27839b9900e440d60948158ddf75d99
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 6%

---


# Introducción a los Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esta capacidad le permite hacer lo siguiente:

* Crea sitios rápidos con una puntuación perfecta en Lighthouse.
* Monitorizar continuamente el rendimiento a través de RUM (Monitoreo de Uso Real).
* Aumente la eficacia de la creación desacoplando las fuentes de contenido.

AEM Puede utilizar tanto la administración de contenido de como la creación WYSIWYG mediante el Editor universal y la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar el servicio de Edge Delivery para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de los Edge Delivery Services AEM y cómo se pueden usar con los, consulte [descripción general de los Edge Delivery Services](/help/edge/overview.md).

## Acerca de los Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene Edge Delivery Services con licencia como parte de Adobe Experience Manager Sites, puede incorporar su sitio con Edge Delivery Services directamente en Cloud Manager e iniciar [con una experiencia guiada de autoservicio](/help/implementing/cloud-manager/managing-code/private-repositories.md).

AEM Además, puede acceder a una experiencia unificada para administrar todas las propiedades de la y garantizar la coherencia en los flujos de trabajo clave. Estas incluyen administración de nombres de dominio, administración de certificados SSL y asignaciones de CDN.

## Acerca de la adición de Edge Delivery Services a un programa de producción o de zona protegida

Se pueden agregar Edge Delivery Services de varias formas diferentes, en función de cómo haya iniciado el proyecto.

| Caso de uso | Descripción |
| --- | --- |
| Deseo agregar Edge Delivery Services a un nuevo programa de producción. | Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>En el asistente, en la ficha **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo agregar Edge Delivery Services a un programa de producción existente. | Ver [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>En el cuadro de diálogo **Editar programa**, en la ficha **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo agregar un sitio de Edge Delivery a Cloud Manager | Consulte [Agregar un sitio Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Deseo agregar Edge Delivery Services a un programa de zona protegida nuevo o existente. | Consulte [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Al crear un programa de zona protegida, los Edge Delivery Services se agregan al programa de forma predeterminada; no es necesario seleccionarlo.<br>Los programas de zonas protegidas existentes antes de la disponibilidad general de Edge Delivery, heredan los Edge Delivery Services automáticamente. |

>[!NOTE]
>
>* Para agregar o editar programas, debe ser miembro del rol **Propietario del negocio** o tener permiso para hacerlo.
>* Su organización debe tener una licencia de Edge Delivery Services no utilizada para poder aplicarla a un programa de producción.
>* Una vez que la licencia de Edge Delivery Services se aplica a un programa o se elimina de él, el cambio entra en vigor inmediatamente sin necesidad de ejecutar una canalización.

## Ruta recomendada de Adobe para Edge Delivery Services {#recommended-path-eds}

Maximice sus ventajas con el Adobe accediendo a sus licencias de Edge Delivery Services y consumiéndolas a través de Cloud Manager. Al hacerlo, puede aprovechar varias ventajas clave.

* [Consume tu licencia en el programa que hayas elegido](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [actualiza otros programas](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o ambos.
* Aproveche los beneficios de [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para realizar operaciones CRUD (crear, leer, actualizar, eliminar).
* [Informes de acceso a SLA](/help/implementing/cloud-manager/sla-reporting.md) (*próximamente*)
* [Obtenga acceso a la compatibilidad con el Adobe](/help/edge/overview.md#support-ticket) para sus programas de producción registrados.

Además, el uso de Cloud Manager le permite usar [CDN administrada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) para su sitio de Edge Delivery y aprovechar ventajas clave como la administración de CDN de autoservicio, incluida la configuración y adición de certificados DV. Además, después de crear un certificado DV, Adobe lo renueva automáticamente cada tres meses, a menos que se elimine. Si no tiene una licencia de Edge Delivery Services con Adobe y decide evitar estos beneficios, solo puede utilizar su propia CDN autoadministrada. Esta configuración debe estar en la plataforma [`aem.live`](https://www.aem.live/docs/go-live-checklist#cdn-configuration).

## Acerca de la lista de tareas pendientes de Edge Delivery {#ed-todo-list}

La **lista de tareas pendientes de Edge Delivery** es una lista de comprobación de tareas de incorporación diseñada para guiarle a través de la incorporación, y administrar su sitio Edge Delivery hasta [go-live](/help/journey-onboarding/go-live-checklist.md).

![Lista de tareas pendientes del sitio de Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | Tarea | Descripción |
| --- | --- | --- |
| 1 | Únase al canal de colaboración de productos | Al hacer clic en **Enviar solicitud ahora** se envía una solicitud al Adobe para crear un canal para su compañía. Si el canal ya existe, se le reenviará al canal de la empresa. |
| 2 | Complete los requisitos previos | Al hacer clic en **Ver tutorial de introducción**, accederá al [Tutorial de introducción para desarrolladores](https://www.aem.live/developer/tutorial). |
| 3 | Agregar sitio de Edge Delivery | Consulte [Agregar un sitio Edge Delivery](#eds-add-site). |
| 4 | Añadir dominio | Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Añadir certificado SSL | Consulte [Agregar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configuración de la CDN del sitio de Edge Delivery | Consulte [Agregar una configuración de CDN](#add-cdn). |

<!-- &#x2460; for "1" inside circle -->

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)
