---
title: Compatibilidad con Edge Delivery Services en Cloud Manager
description: Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 28%

---

# Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para [el programa de clientes pioneros.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Edge Delivery Services en resumen {#edge-overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esto le permite:

* Cree sitios rápidos con una puntuación de Lighthouse perfecta y monitorice continuamente el rendimiento a través de la monitorización de uso real (RUM).
* Aumente la eficacia de la creación desacoplando las fuentes de contenido.

AEM Puede utilizar tanto la administración de contenido de como la creación WYSIWYG mediante el Editor universal, así como la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar el servicio de Edge Delivery para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de los Edge Delivery Services AEM y cómo se pueden usar con los, consulte el documento [Información general sobre los Edge Delivery Services.](/help/edge/overview.md)

## Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene Edge Delivery Services con licencia como parte de Adobe Experience Manager Sites, puede incorporar su sitio con Edge Delivery Services directamente en Cloud Manager e iniciar sesión [con una experiencia de autoservicio guiada.](/help/implementing/cloud-manager/managing-code/private-repositories.md)

Esto permite tener una experiencia unificada para todas las propiedades de AEM, lo que garantiza la coherencia con todos los flujos de trabajo críticos, incluida la administración de nombres de dominio, la administración de certificados SSL y las asignaciones de CDN.

Edge Delivery Services está disponible para [programas de producción y de zonas protegidas.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Activación de Edge Delivery Services {#enabling}

Los Edge Delivery Services se pueden habilitar al agregar un nuevo programa.

![Agregar programa de producción con Edge Delivery Services](assets/add-production-program-with-edge.png)

Para obtener más información sobre cómo agregar programas, consulte los siguientes documentos.

* [Creación de programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Creación de programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
