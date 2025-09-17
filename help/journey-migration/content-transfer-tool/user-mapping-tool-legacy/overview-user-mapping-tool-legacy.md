---
title: Información general sobre la herramienta de asignación de usuarios (heredada)
description: Información general sobre la herramienta de asignación de usuarios (heredada)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 21%

---


# Información general sobre la herramienta de asignación de usuarios (heredada) {#overview-user-mapping-tool}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de la herramienta. Para obtener más información sobre la versión más reciente, consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (that is, not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, debe mover usuarios y grupos de su sistema AEM existente a AEM as a Cloud Service. Esta migración se realiza mediante la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los Adobe ID para acceder al nivel de Author. Esta integración requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en Adobe Identity Management System (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de autor de Cloud Service.

## Herramienta de asignación de usuarios {#mapping-tool}

La herramienta de transferencia de contenido (sin asignación de usuarios) migra cualquier usuario y grupo asociado con el contenido que se migra. La herramienta de asignación de usuarios forma parte de la herramienta de transferencia de contenido. Su único propósito es editar a los usuarios para que IMS, la funcionalidad de inicio de sesión único utilizada por AEM as a Cloud Service, los reconozca correctamente. Una vez realizadas estas modificaciones, la herramienta de transferencia de contenido migra los usuarios y grupos del contenido especificado como de costumbre.

### Siguientes pasos {#whats-next}

Una vez que sepa qué es una herramienta de asignación de usuarios, ya estará listo para revisar consideraciones importantes y casos excepcionales antes de utilizarla. Consulte [Consideraciones importantes sobre la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) para obtener más información.
