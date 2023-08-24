---
title: Migración de grupos de usuarios cerrados
description: Esta página proporciona las consideraciones especiales necesarias para habilitar los grupos de usuarios cerrados después de migrar contenido a Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: 9da813d39d154e81da5b9814aa86b8318dc0bb3a
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 8%

---

# Migración de grupos de usuarios cerrados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migración de grupos de usuarios cerrados"
>abstract="La migración de grupos de usuarios cerrados (CUG) actualmente requiere algunas comprobaciones y pasos para que sea operativa después de una migración."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=es" text="Grupos de usuarios cerrados en AEM"

Actualmente, los grupos de usuarios cerrados (CUG) necesitan algunos pasos adicionales para funcionar en el entorno de destino de una migración.  En este documento se explica el escenario y los pasos necesarios para que protejan los nodos de la forma prevista.

## Migración de grupos

Las entidades principales (incluidos los grupos) se incluyen automáticamente en una migración a Adobe Experience Manager as a Cloud Service si están asociadas al contenido migrado a través de la ACL de ese contenido.

## Grupos de usuarios cerrados en la migración

Actualmente, grupos asociados *solamente* con una directiva de grupo de usuarios cerrado (CUG) son *no* se incluye automáticamente en la ingesta. Como se ha dicho anteriormente, se migrarán si están asociados a cualquier contenido a través de una ACL. La verificación de la existencia del grupo y sus miembros debe realizarse antes de activarse. El informe principal, descargado a través de la vista Trabajo de ingesta, se puede utilizar para ver si el grupo en cuestión se incluía o no porque no estaba en una ACL. Si el grupo no existe, debe crearse en la instancia de autor, incluida la adición de miembros adecuados, y activarse para que exista en la instancia de publicación. Esto se puede hacer utilizando paquetes creados en el origen.

Finalmente, deben activarse los procesos y deben establecerse las propiedades para habilitar los CUG. Para ello, vuelva a publicar todas las páginas asociadas a una directiva CUG. Esto calibrará la instancia de publicación para realizar un seguimiento de las directivas.

Esto habilitará las políticas de CUG en la publicación y el contenido solo estará accesible para los usuarios autenticados que sean miembros del grupo asociado con las políticas.

## Desarrollo activo

El equipo de migración está trabajando para que las políticas de CUG migren y funcionen automáticamente, sin ningún paso adicional después de ingerir el contenido.
Es aconsejable incluir la funcionalidad de CUG en cualquier proceso de prueba antes de intentar publicar.

## Resumen

En resumen, estos son los pasos para habilitar el CUG después de una migración:

1. Asegúrese de que cada grupo utilizado en las políticas de CUG existe en Publicar después de la migración.
   - Puede que ya exista un grupo si se incluye en la ACL de un contenido migrado.
   - Si no es así, utilice paquetes para instalarla en la instancia de destino (o crearla manualmente allí) y activarla junto con sus miembros. A continuación, compruebe que existe en Publish.
1. Volver a publicar todas las páginas asociadas con una directiva de CUG, asegurándose de que se publique, por ejemplo, editando primero la página. Es importante volver a publicar todos ellos.
   - Una vez que se hayan vuelto a publicar todas las páginas, compruebe la funcionalidad de cada página protegida por CUG.

