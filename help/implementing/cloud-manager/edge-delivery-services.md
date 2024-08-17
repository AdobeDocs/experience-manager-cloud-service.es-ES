---
title: Compatibilidad con Edge Delivery Services en Cloud Manager
description: Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 64aa010c3d840adad9e1ab6040a6d80c07cd8455
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 17%

---

# Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para [el programa de clientes pioneros.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Edge Delivery Services en resumen {#edge-overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esta capacidad le permite hacer lo siguiente:

* Crea sitios rápidos con una puntuación perfecta en Lighthouse.
* Monitorizar continuamente el rendimiento a través de RUM (Monitoreo de Uso Real).
* Aumente la eficacia de la creación desacoplando las fuentes de contenido.

AEM Puede utilizar tanto la administración de contenido de como la creación WYSIWYG mediante el Editor universal y la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar el servicio de Edge Delivery para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de los Edge Delivery Services AEM y cómo se pueden usar con los, consulte el documento [Información general sobre los Edge Delivery Services.](/help/edge/overview.md)

## Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene Edge Delivery Services con licencia como parte de Adobe Experience Manager Sites, puede incorporar su sitio con Edge Delivery Services directamente en Cloud Manager e iniciar [con una experiencia guiada de autoservicio](/help/implementing/cloud-manager/managing-code/private-repositories.md).

AEM Esta funcionalidad ofrece una experiencia unificada para administrar todas las propiedades de la. Garantiza la coherencia en los flujos de trabajo clave. Estas incluyen administración de nombres de dominio, administración de certificados SSL y asignaciones de CDN.

Edge Delivery Services está disponible para [programas de producción y de zonas protegidas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

## Habilitar Edge Delivery Services {#enabling}

Los Edge Delivery Services se pueden habilitar al agregar un nuevo programa.

![Agregar programa de producción con Edge Delivery Services](assets/add-production-program-with-edge.png)

Para obtener más información acerca de cómo agregar programas, consulte lo siguiente:

* [Creación de programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)
