---
title: Administrar listas de IP permitidas
description: Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las Listas de permitidos IP en Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 19%

---

# Administrar listas de IP permitidas {#manage-ip-allow-lists}

Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las Listas de permitidos IP en Cloud Manager.

## Ver y actualizar Listas de permitidos IP {#update-ip-allow-lists}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una Lista de permitidos IP.

**Para ver y actualizar Listas de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.
1. En la página **Información general**, en el menú de la izquierda, en **Servicios**, haga clic en ![Icono de lista de tareas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permitidos IP**.
1. Identifique la fila de las Listas de permitidos IP que desee ver o actualizar.
1. Haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho de la fila.
1. En el menú desplegable, haga clic en **Ver y actualizar**.
El cuadro de diálogo **Ver y actualizar Lista de permitidos IP** muestra el nombre, las direcciones IP (o los intervalos) que definen la regla junto con los entornos y servicios a los que se aplica.
1. Cambie el nombre o las direcciones IP que desee.

   Al agregar o eliminar un nuevo rango de IP a una Lista de permitidos IP, se aplica o deja de aplicarse automáticamente a todos los entornos o servicios correspondientes a los que se aplicó anteriormente.

   No se pueden realizar actualizaciones en una Lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.

1. Haga clic en **Actualizar**.

## Comprobar el estado de las Listas de permitidos IP {#check-allow-list-status}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. En la página **Información general**, en el menú de la izquierda, en **Servicios**, haga clic en ![Icono de lista de tareas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permitidos IP**.

1. En la columna **Estado** de la tabla de Listas de permitidos IP, pase el puntero del ratón sobre una Lista de permitidos IP verde (en uso) para ver uno o más servicios aplicados.

   Los valores de estado que se muestran en la tabla tienen los siguientes significados:

   | Estado de la Lista de permitidos IP | Descripción |
   | --- | --- |
   | Aplicado | La Lista de permitidos IP se ha aplicado correctamente a uno o más entornos. |
   | Actualizándose | Se está realizando una actualización de la Lista de permitidos IP, que puede incluir una o más aplicaciones o la anulación de la aplicación de la lista. Cada aplicación y anulación de la aplicación se enumera junto con su propio estado **No iniciada**, **En curso**, **Completada** o **Error**. |
   | Error | Error en uno o varios procesos de aplicación o de anulación de la aplicación de una actualización.<br>· Cada aplicación y anulación de la aplicación se enumera junto con su estado.<br>· El estado es **Error** si falla una aplicación/anulación de la aplicación en la actualización. El estado permanece como **Error** hasta que se borren todos los errores.<br>· Haga clic en el icono **Reintentar** junto al estado para borrar el error.<br>· No puede actualizar ni eliminar una Lista de permitidos IP con el estado **Error**. |
   | Eliminando | Se está eliminando una Lista de permitidos IP.<br>· La eliminación implica la anulación de la aplicación de la lista de todos los servicios.<br>· Cada anulación de la aplicación se enumera junto con su propio estado de **No iniciada**, **En curso**, **Completada** o **Error**.<br>· Cuando finaliza la operación de eliminación, la Lista de permitidos IP no aparece en la tabla de Lista de permitidos IP. Además, la Lista de permitidos IP no se aplica a ningún servicio del programa en Cloud Manager. |
   | Error de eliminación | Error en una o varias aplicaciones durante una operación de eliminación.<br>· Cada anulación de la aplicación se enumera junto con el estado **Completada** o **Error**.<br>· El estado pasa a ser **Error al eliminar** si falla una de las aplicaciones. El estado permanece como **Error al eliminar** hasta que se borren todos los errores. En el extremo derecho de la fila de la tabla, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, en el menú desplegable, haga clic en **Eliminar** para borrar cualquier error.<br>· No puede actualizar una Lista de permitidos IP mientras el estado sea **Error**. |

## Eliminación de una Lista de permitidos IP {#delete-allow-list}

Al eliminar una Lista de permitidos IP, esta anula automáticamente la aplicación de la lista de todos los servicios y la elimina de la tabla de Listas de permitidos IP.

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una Lista de permitidos IP.

**Para eliminar una Lista de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.
1. En la página **Información general**, en el menú de la izquierda, en **Servicios**, haga clic en ![Icono de lista de tareas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permitidos IP**.
1. Identifique la fila de la Lista de permitidos IP que desee eliminar, haga clic en ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho de la fila y, a continuación, haga clic en **Eliminar**.
1. En el cuadro de diálogo **Eliminar Lista de permitidos IP**, haga clic en **Eliminar**.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si tiene una configuración de CDN (red de distribución de contenido) preexistente para sus Listas de permitidos IP, aparecerá un mensaje informativo en la página **Lista de permitidos IP**. El mensaje le recomienda añadir estas configuraciones mediante la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Agregar una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obtener más información.

También aparecerá un mensaje similar en las páginas **Certificados SSL** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para certificados SSL o nombres de dominio personalizados.
