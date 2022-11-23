---
title: Información general sobre la herramienta de asignación de usuarios
description: Información general sobre la herramienta de asignación de usuarios
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
source-git-commit: 99af299c3f401ce898366a75563d2b933f120e40
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 11%

---

# Información general sobre la herramienta de asignación de usuarios {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Herramienta de asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema AEM existente a AEM as a Cloud Service. Los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de creación del Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Consideraciones importantes sobre el uso de la herramienta de asignación de usuarios"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Uso de la herramienta de asignación de usuarios"

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM as a Cloud Service. Esto lo hace la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los Adobe ID para acceder al nivel de creación.  Esto requiere el uso de la variable [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS) que proporciona el inicio de sesión único en todas las aplicaciones de nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de creación del Cloud Service.

## Herramienta de asignación de usuarios {#mapping-tool}

La herramienta de transferencia de contenido (sin asignación de usuarios) migrará todos los usuarios y grupos asociados con el contenido que se migra. La herramienta de asignación de usuarios forma parte de la herramienta de transferencia de contenido y su único propósito es modificar los usuarios de modo que IMS los reconozca correctamente, la funcionalidad de inicio de sesión único que utiliza AEM as a Cloud Service. Una vez realizadas estas modificaciones, la herramienta de transferencia de contenido migra los usuarios y grupos del contenido especificado de la forma habitual.

### Siguientes pasos {#whats-next}

Una vez que sepa qué es una herramienta de asignación de usuarios, ya estará listo para revisar consideraciones importantes y casos excepcionales antes de utilizar la herramienta de asignación de usuarios. Consulte [Consideraciones importantes sobre la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) para obtener más información.
