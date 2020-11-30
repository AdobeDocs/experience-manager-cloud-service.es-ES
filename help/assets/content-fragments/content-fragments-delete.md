---
title: 'Fragmentos de contenido: Eliminar consideraciones'
description: 'Fragmentos de contenido: Eliminar consideraciones'
translation-type: tm+mt
source-git-commit: bb3d90def8855e8dffdc584c0805da120faf7b12
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 12%

---


# Fragmentos de contenido: Eliminar consideraciones{#content-fragments-delete-considerations}

## Permisos - Eliminar o no eliminar {#permissions-delete-or-not-delete}

La capacidad para eliminar contenido es poderosa, pero potencialmente sensible, y muchas industrias necesitan restringir y controlar cómo se distribuyen estos privilegios.

En relación con los permisos de eliminación, los fragmentos de contenido deben considerarse en dos niveles:

1. **Fragmento de contenido como una sola entidad.**

   * **Caso** de uso: Usuario que necesita editar/actualizar un fragmento de contenido **y eliminar un fragmento** completo.
   * **Permisos**: El permiso Eliminar se puede asignar a través de Administración de usuarios y/o grupos. <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **Las varias subentidades que conforman un fragmento de contenido; por ejemplo, variaciones, subnodos.**

   El funcionamiento básico del editor de fragmentos de contenido requiere que se puedan eliminar estos subelementos transitorios. Por ejemplo, al manipular variaciones; también al editar metadatos o administrar el contenido asociado.

   * **Caso** de uso: Usuario que necesita editar/actualizar un fragmento de contenido **sin tener permiso para eliminar un fragmento** completo.
   * **Permisos**: Consulte [Permisos requeridos solo](#permissions-required-for-editor-functionality-only)para la funcionalidad del editor.

>[!NOTE]
>
>When a user does not have any Delete permissions, the Content Fragment editor operates in *read-only* mode. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Consulte también Cómo auditar las operaciones de administración de usuarios en AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Permisos requeridos solo para la funcionalidad del editor {#permissions-required-for-editor-functionality-only}

Para los usuarios que necesiten editar o actualizar un fragmento de contenido, **sin permitirles eliminar un fragmento completo**, se deben asignar permisos específicos, ya que la operación básica del editor de fragmentos de contenido requiere que se puedan eliminar subelementos transitorios.

Por ejemplo, al manipular variaciones; también al editar metadatos o administrar el contenido asociado.

>[!NOTE]
>
>Los permisos de eliminación, necesarios para editar o actualizar un fragmento de contenido, se incluyen en el permiso de eliminación asignado a través de Administración de usuarios o grupos. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

Los permisos necesarios para editar o actualizar un fragmento deben aplicarse al nodo que contiene el fragmento de contenido o a un nodo principal adecuado (en cualquier nivel debajo de `/content/dam`). Cuando se asignan a dicho nodo principal, los permisos se aplicarán a todos los nodos de esa rama.

Por ejemplo, una carpeta que contendrá todos los fragmentos de contenido, como:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>También `/content/dam` es posible establecer permisos, ya que todos los fragmentos de contenido se almacenan aquí.
>
>Sin embargo, esta acción también aplica los mismos permisos de eliminación a *todos los* demás tipos de recursos.

Los requisitos previos de permisos para permitir que un usuario o grupo específico edite o actualice un fragmento de contenido son:

>[!NOTE]
>
>Esta lista muestra todos los privilegios requeridos, no solo los privilegios de eliminación.

* Para los nodos o carpetas del fragmento de contenido:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Para el `jcr:content`nodo de todos los fragmentos de contenido:

   * `jcr:addChildNodes`, `jcr:modifyProperties` y `jcr:removeChildNodes`

* Para todos los nodos debajo `jcr:content` de todos los fragmentos de contenido:

   * `jcr:addChildNodes`, `jcr:modifyProperties` y `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
