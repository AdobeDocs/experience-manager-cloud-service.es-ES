---
title: Información general sobre la herramienta de asignación de usuarios (heredada)
description: Información general sobre la herramienta de asignación de usuarios (heredada)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 69dfe7f98628ab67cc3a994c32b1530550ec6a01
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 11%

---

# Información general sobre la herramienta de asignación de usuarios {#overview-user-mapping-tool}


<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager AEM () as a Cloud Service AEM AEM, debe mover usuarios y grupos de su sistema de existente a los que se vean as a Cloud Service en el proceso de migración a la. Esto se realiza mediante la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los Adobe ID para acceder al nivel de creación.  Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de autor de Cloud Service.

## Herramienta de asignación de usuarios {#mapping-tool}

La herramienta de transferencia de contenido (sin asignación de usuarios) migrará cualquier usuario y grupo asociado con el contenido que se está migrando. AEM La herramienta de asignación de usuarios forma parte de la herramienta de transferencia de contenido y su único propósito es modificar los usuarios para que IMS, la funcionalidad de inicio de sesión único utilizada por as a Cloud Service, pueda reconocerlos correctamente. Una vez realizadas estas modificaciones, la herramienta de transferencia de contenido migra los usuarios y grupos del contenido especificado como de costumbre.

### Siguientes pasos {#whats-next}

Una vez que haya aprendido qué es una herramienta de asignación de usuarios, ya está listo para revisar consideraciones importantes y casos excepcionales antes de utilizar la herramienta de asignación de usuarios. Consulte [Consideraciones importantes sobre la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) para obtener más información.
