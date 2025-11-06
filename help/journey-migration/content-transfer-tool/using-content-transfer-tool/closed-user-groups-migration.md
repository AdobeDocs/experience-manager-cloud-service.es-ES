---
title: Migración de grupos de usuarios cerrados
description: Obtenga información acerca de las consideraciones especiales necesarias para habilitar los grupos de usuarios cerrados después de migrar contenido a Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 13%

---


# Migración de grupos de usuarios cerrados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migración de grupos de usuarios cerrados"
>abstract="La migración de grupos de usuarios cerrados (CUG) actualmente requiere algunas comprobaciones y pasos para que sea operativa después de una migración."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=es" text="Grupos de usuarios cerrados en AEM"

Actualmente, los grupos de usuarios cerrados (CUG) necesitan algunos pasos adicionales para funcionar en el entorno de destino de una migración. En este documento se explica el escenario y los pasos necesarios para que protejan los nodos de la forma prevista.

## Migración de grupos de usuarios cerrados (CUG)

Los grupos se incluyen automáticamente en una migración CTT/CAM a Adobe Experience Manager as a Cloud Service si están asociados al contenido migrado a través de la ACL de ese contenido o su nodo de política de CUG. La comprobación de la existencia del grupo y sus miembros debe realizarse antes de activarlo. Los grupos a los que se hace referencia en una política de CUG se denominan aquí &quot;grupos de CUG&quot;.

Para utilizar CUG en AEM as a Cloud Service, los usuarios deben estar presentes en la instancia de autor y ser miembros de los grupos de CUG relevantes.  Esto se puede realizar mediante paquetes o si los usuarios de CUG son usuarios de IMS, es posible que ya estén presentes.  Los usuarios de CUG deben convertirse en miembros de los grupos de CUG de AEM.

Para habilitar el comportamiento de CUG en la instancia de publicación,

1. Los grupos CUG deben activarse (lo que los duplica a ellos y a sus miembros en la instancia de publicación).
1. Se debe cancelar la publicación de *todas* las páginas protegidas con directivas CUG (para borrar el recuento global de CUG), y
1. Las páginas protegidas con políticas de CUG deben publicarse (lo que permite a la instancia de publicación y realizar un seguimiento de las políticas).
1. Una vez publicadas todas las páginas, compruebe la funcionalidad de cada página protegida con CUG.

Para obtener más información, consulte [Grupos de usuarios cerrados](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=es).
