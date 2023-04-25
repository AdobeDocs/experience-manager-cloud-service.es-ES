---
title: Información general sobre la herramienta de asignación de usuarios (Heredado)
description: Información general sobre la herramienta de asignación de usuarios (heredada)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: f7be351c85b8db6d11033c7cf064529a46c2802a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 95%

---

# Información general sobre la herramienta de asignación de usuarios (heredada) {#overview-user-mapping-tool}


<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM as a Cloud Service. Esto lo hace la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de Adobe ID para acceder al nivel de creación.  Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar los usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en Adobe Identity Management System (IMS) que proporciona el inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=es#identity-management). Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de creación de Cloud Service.

## Herramienta de asignación de usuarios {#mapping-tool}

La herramienta de transferencia de contenido (sin asignación de usuarios) migra todos los usuarios y grupos asociados con su respectivo contenido. La herramienta de asignación de usuarios forma parte de la herramienta de transferencia de contenido y su único propósito es modificar los usuarios de modo que IMS los reconozca correctamente, la funcionalidad de inicio de sesión único que utiliza AEM as a Cloud Service. Una vez realizadas estas modificaciones, la herramienta de transferencia de contenido migra los usuarios y grupos del contenido especificado de la forma habitual.

### Siguientes pasos {#whats-next}

Una vez que sepa qué es una herramienta de asignación de usuarios, ya estará listo para revisar consideraciones importantes y casos excepcionales antes de utilizarla. Consulte [Consideraciones importantes sobre la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) para obtener más información.
