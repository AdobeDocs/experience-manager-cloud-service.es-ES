---
title: Introducción a Edge Delivery Services en Cloud Manager
description: Aprenda a enviar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: a7e3c154f36b194cde223c11e9e06ecbe3a872f5
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 53%

---


# Introducción a Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esto le permite hacer lo siguiente:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta.
* Monitorizar de forma continua del rendimiento mediante la telemetría operativa.
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido.

Puede usar tanto la administración de contenido de AEM como la creación WYSIWYG utilizando el editor universal además de la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar el servicio de Edge Delivery para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de Edge Delivery Services y cómo se pueden usar con AEM, consulte la [información general de Edge Delivery Services](/help/edge/overview.md#how-does-it-work).

## Acerca de Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene licencia para Edge Delivery Services como parte de Adobe Experience Manager Sites, puede integrar su sitio con Edge Delivery Services directamente en Cloud Manager y ponerlo en marcha [con una experiencia de autoservicio guiada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

Además, podrá acceder a una experiencia unificada para administrar todas sus propiedades AEM y garantizar la coherencia de los flujos de trabajo clave. Estos flujos de trabajo incluyen la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

Cloud Manager ofrece dos tipos de implementación para Edge Delivery Services en CDN administrada por Adobe con distintas funcionalidades. [Más información](#edge-delivery-deployment-options).

>[!NOTE]
>
>Edge Delivery Services también se puede integrar en entornos de as a Cloud Service de AEM Sites existentes utilizando la Canalización de configuración y los selectores de origen. Para obtener más información, consulte [Envío de proxy a Edge Delivery Services](/help/implementing/dispatcher/cdn-configuring-traffic.md#proxying-to-edge-delivery) y [Configuración de un proxy desde un entorno existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment).

## Opciones de implementación de Edge Delivery Services en CDN administrada por Adobe {#edge-delivery-deployment-options}

Existen dos tipos de implementación para Edge Delivery Services en CDN administrada por Adobe:

1. **Con un entorno AEMaaCS existente**: configure un proxy HTTP desde un entorno AEM Sites as a Cloud Service existente. Este método se suele utilizar cuando ya tiene un entorno y desea migrar parte de un sitio a Edge Delivery Services. Ver [Configurar un proxy desde un entorno existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment).

1. **Sin un entorno AEMaaCS existente (entorno Edge)**: configure un nuevo sitio Edge Delivery independientemente de un entorno AEM Sites as a Cloud Service. Este método se utiliza cuando no tiene un entorno de creación o publicación de AEM y desea utilizar Edge Delivery Services por su cuenta. Ver [Configurar un sitio de Edge Delivery sin un entorno existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment).

Estas dos opciones también tienen diferentes capacidades:

* **La canalización de configuración** está disponible para los entornos de AEM as a Cloud Service.
* **La canalización de configuración** solo está disponible actualmente para entornos de Edge a través del programa Beta limitado.

Para obtener instrucciones de configuración completas, consulte [CDN administrada por Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed)


## Acerca de Edge Delivery Services con la creación de AEM {#eds-aem-authoring}

Las experiencias web modernas requieren un envío de alto rendimiento, pero muchas organizaciones también dependen de los flujos de trabajo de creación de AEM establecidos, el control y los patrones de reutilización de contenido. Para ayudar a sus equipos a modernizar la entrega sin interrumpir la creación, Cloud Manager introduce funcionalidades que le permiten hacer lo siguiente:

* Ofrezca experiencias con Edge Delivery Services.
* Siga utilizando AEM Author para crear contenido.
* Aprovisionar solo la infraestructura necesaria para su arquitectura.

Estas capacidades permiten a las organizaciones adoptar la entrega moderna de forma gradual, sin sacrificar los flujos de trabajo existentes.

### Opciones de creación para sitios de Edge Delivery {#authoring-options-eds}

Al crear un sitio de Edge Delivery en Cloud Manager, puede elegir el método de creación que prefiera:

* Creación basada en documentos: contenido de autor en Google Drive o SharePoint. No se requiere ningún entorno de AEM.
* Creación de AEM: cree contenido en AEM mediante el Editor universal. Este método requiere un entorno de AEM Author. Con esta opción, no se requiere un nivel de publicación cuando Edge Delivery administra la entrega de contenido.

Las organizaciones pueden elegir entre estos enfoques o utilizar ambos de forma incremental, según sus preferencias de flujo de trabajo. Ver [Crea tu primer sitio Edge Delivery con un solo clic](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md).

### Nivel de publicación flexible {#flexible-publish-tier}

Cloud Manager le permite configurar si un nivel de publicación está aprovisionado para los entornos del programa. No todas las arquitecturas requieren un nivel de publicación, como se ve en la siguiente tabla:

| Arquitectura | Publicar nivel |
| --- | --- |
| AEM Sites tradicional | Requerido |
| Sin encabezado/API-First | Requerido |
| Edge Delivery Services | No obligatorio |

Al habilitar el nivel de publicación solo cuando es necesario, los equipos pueden aprovisionar entornos más rápido, simplificar la infraestructura y reducir los componentes innecesarios. Consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

## Ventajas de utilizar la ruta recomendada por Adobe para Edge Delivery Services {#recommended-path-eds}

Maximice sus ventajas de Adobe accediendo a sus licencias de Edge Delivery Services y consumiéndolas a través de Cloud Manager. Al hacerlo, puede aprovechar varias ventajas clave.

* [Consuma su licencia en el programa elegido](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md), [actualice otros programas](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md) o ambos.
* [Use un repositorio Git externo](/help/implementing/cloud-manager/managing-code/external-repositories.md) (Traiga su propio Git) para sincronizar e implementar el código de sitio de Edge Delivery Services. Para aprovechar esta capacidad, primero debe [incorporar su sitio en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). <!-- NEW from CQDOC-22867 -->
* [Use la canalización de configuración de Edge Delivery](/help/implementing/dispatcher/cdn-configuring-traffic.md) para establecer la configuración de CDN administrada por Adobe para su sitio de Edge Delivery mediante la definición de reglas como filtros de tráfico, selectores de origen y redirecciones. <!-- NEW from CQDOC-22867 -->
* Aproveche los beneficios del enfoque [API primero](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para realizar operaciones CRUD (crear, leer, actualizar y eliminar).
* [Informes de acceso a SLA](/help/implementing/cloud-manager/reports/report-sla.md).
* [Obtenga acceso a la compatibilidad con Adobe](/help/edge/overview.md#support-ticket) para sus programas de producción registrados.

Si tiene una licencia de Edge Delivery Services (EDS), puede usar una [CDN administrada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) para su sitio de Edge Delivery. Al hacerlo, se habilita la administración de CDN de autoservicio y los certificados DV que se renuevan automáticamente cada tres meses a menos que elimine el certificado.

O bien, si decide utilizar su CDN (es decir, una CDN no administrada por Adobe), independientemente de las licencias de Edge Delivery Services, debe configurarla en la plataforma `aem.live`. Consulte [Configuración de BYO CDN](https://www.aem.live/docs/byo-cdn-setup).


## Acerca de la adición de Edge Delivery Services a un programa de producción o de zona protegida {#about-adding-eds-to-prod-sandbox}

Se puede añadir Edge Delivery Services de varias formas diferentes, en función de cómo haya iniciado el proyecto o de cuándo desee crear el sitio.

| Caso de uso | Descripción |
| --- | --- |
| Deseo añadir Edge Delivery Services a un nuevo programa de producción. | Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>En el asistente, en la pestaña **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo añadir Edge Delivery Services a un programa de producción existente. | Consulte [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>En el cuadro de diálogo **Editar programa**, en la pestaña **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Añadir un sitio de Edge Delivery a Cloud Manager | Consulte [Añadir un sitio de Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md). |
| Deseo crear un sitio de Edge Delivery ahora | Consulte [Crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md). |
| Deseo añadir Edge Delivery Services a un programa de zona protegida nuevo o existente. | Consulte [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Al crear un programa de zona protegida, Edge Delivery Services se añade al programa por defecto; no es necesario que lo seleccione.<br>Los programas de zona protegida existentes antes de la disponibilidad general de Edge Delivery heredan Edge Delivery Services automáticamente. |
| Deseo crear un sitio de Edge Delivery que utilice la creación de AEM | Ver [Crear un sitio de Edge Delivery](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site). Al utilizar la creación de AEM con Edge Delivery, un nivel de publicación es opcional. Consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier). |

>[!NOTE]
>
>* Para añadir o editar programas, debe ser miembro de la función **Propietario del negocio** o tener permiso para hacerlo.
>* Su organización debe tener una licencia de Edge Delivery Services no utilizada para poder aplicarla a un programa de producción.
>* Una vez que la licencia de Edge Delivery Services se aplica a un programa o se elimina de él, el cambio entra en vigor inmediatamente sin necesidad de ejecutar una canalización.


## Acerca de la lista de tareas pendientes de Edge Delivery en Cloud Manager {#ed-todo-list}

La **lista de tareas pendientes de Edge Delivery** en Cloud Manager es una lista de comprobación de tareas de incorporación diseñada para guiarlo a través de la incorporación y administrar su sitio de Edge Delivery hasta [el lanzamiento](/help/journey-onboarding/go-live-checklist.md).

![Lista de tareas pendientes del sitio de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

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

>[!VIDEO](https://video.tv.adobe.com/v/3441564?captions=spa&learn=on)

## Registro de un vale de asistencia {#eds-support-ticket}

{{support-ticket}}



