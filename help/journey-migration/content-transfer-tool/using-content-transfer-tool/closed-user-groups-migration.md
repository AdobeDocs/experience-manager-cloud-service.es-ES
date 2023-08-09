---
title: Migración de grupos de usuarios cerrados
description: Esta página proporciona las consideraciones especiales necesarias para habilitar los grupos de usuarios cerrados después de migrar contenido a Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: ca3c4bae2e652d75190d68c76b1dd4e09239f16c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Migración de grupos de usuarios cerrados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migración de grupos de usuarios cerrados"
>abstract="La migración de Grupos de usuarios cerrados (CUG) actualmente requiere algunas comprobaciones y pasos para que sea operativa después de una migración."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="AEM Grupos de usuarios cerrados en el"

Actualmente, los grupos de usuarios cerrados (CUG) necesitan algunos pasos adicionales para funcionar en el entorno de destino de una migración.  En este documento se explica el escenario y los pasos necesarios para que protejan los nodos de la forma prevista.

## Migración de grupos

Las entidades principales (incluidos los grupos) se incluyen automáticamente en una migración a Adobe Experience Manager as a Cloud Service si están asociadas al contenido migrado a través de la ACL de ese contenido.

## Grupos de usuarios cerrados en la migración

Actualmente, grupos asociados *solamente* con una directiva de grupo de usuarios cerrado (CUG) son *no* se incluye automáticamente en la ingesta. Si están asociados a cualquier contenido a través de una ACL, como se ha dicho anteriormente, se migrarán. La verificación de que el grupo existe debe realizarse antes de activarlo. El informe principal, descargado a través de la vista Trabajo de ingesta, se puede utilizar para ver si el grupo en cuestión se incluía o no porque no estaba en una ACL. Si el grupo no existe, debe crearse en la instancia de autor, incluida la adición de miembros adecuados, y activarse para que exista en la instancia de publicación.

Por último, deben activarse procesos para habilitar el CUG. Para ello, vuelva a publicar cualquier contenido que contenga la directiva CUG. Por lo tanto, en los procesos de prueba normales, si se descubre que el CUG no funciona, vuelva a publicar ese contenido (asegurándose de que se publique aunque no se modifique).

Esto debería habilitar las políticas de CUG en la publicación y el contenido solo será accesible para los usuarios autenticados que sean miembros del grupo asociado con las políticas.

## Desarrollo activo

El equipo de migración está trabajando para que las políticas de CUG migren y funcionen automáticamente, sin ningún paso adicional después de ingerir el contenido.
Es aconsejable incluir la funcionalidad de CUG en cualquier proceso de prueba antes de intentar publicar.

## Resumen

En resumen, estos son los pasos para habilitar el CUG después de una migración:

1. Asegúrese de que cada grupo utilizado en las políticas de CUG existe en Publicar después de la migración.
   - Puede que ya exista un grupo si se incluye en la ACL de un contenido migrado.
   - Si no es así, utilice paquetes para instalarla en la instancia de destino (o crearla manualmente allí) y activarla junto con sus miembros. A continuación, compruebe que existe en Publish.
1. Si la política de grupos de usuarios compartidos aún no protege el nodo, vuelva a publicar la página (asegurándose de que se publique aunque no se hayan realizado cambios en esa página).
   - Verifique para cada nodo protegido por CUG.
