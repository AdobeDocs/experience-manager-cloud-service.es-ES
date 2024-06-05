---
title: Migración de grupos de usuarios cerrados
description: Obtenga información acerca de las consideraciones especiales necesarias para habilitar los grupos de usuarios cerrados después de migrar contenido a Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# Migración de grupos de usuarios cerrados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migración de grupos de usuarios cerrados"
>abstract="La migración de grupos de usuarios cerrados (CUG) actualmente requiere algunas comprobaciones y pasos para que sea operativa después de una migración."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=es" text="Grupos de usuarios cerrados en AEM"

Actualmente, los grupos de usuarios cerrados (CUG) necesitan algunos pasos adicionales para funcionar en el entorno de destino de una migración. En este documento se explica el escenario y los pasos necesarios para que protejan los nodos de la forma prevista.

## Migración de grupos

Las entidades principales (incluidos los grupos) se incluyen automáticamente en una migración a Adobe Experience Manager as a Cloud Service si están asociadas al contenido migrado a través de la ACL de ese contenido, y también se incluyen si se hace referencia a ellas en una directiva CUG sobre ese contenido.

## Grupos de usuarios cerrados en la migración

La verificación de la existencia del grupo y sus miembros debe realizarse antes de activarse. El informe principal, descargado a través de la vista Trabajo de ingesta, se puede utilizar para ver si el grupo en cuestión se incluía o no porque no estaba en una ACL o en una directiva CUG.

A continuación, se deben activar los procesos y se deben definir las propiedades para habilitar los CUG. Para ello, vuelva a publicar todas las páginas asociadas a una directiva CUG. Esto calibra la instancia de publicación para realizar un seguimiento de las directivas.

Esto habilita las políticas de CUG en Publicar y el contenido solo es accesible para los usuarios autenticados que son miembros del grupo asociado con las políticas.

## Resumen

En resumen, estos son los pasos para habilitar el CUG después de una migración:

1. Asegúrese de que cada grupo utilizado en las políticas de CUG existe en Publicar después de la migración.
   - Puede existir un grupo si se incluye en la directiva CUG de un contenido migrado o en la ACL de ese contenido.
   - Si no es así, utilice Paquetes para instalarla en la instancia de destino (o crearla manualmente allí) y activarla junto con sus miembros. A continuación, compruebe que existe en Publish.
1. Volver a publicar todas las páginas asociadas con una política de CUG, asegurándose de que se publique, por ejemplo, editando primero la página. Es importante volver a publicarlos todos.
   - Una vez que se hayan vuelto a publicar todas las páginas, compruebe la funcionalidad de cada página protegida por CUG.
