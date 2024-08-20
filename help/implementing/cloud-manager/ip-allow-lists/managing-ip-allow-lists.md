---
title: Administrar listas de IP permitidas
description: Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las Listas de permitidos IP en Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 44%

---

# Administrar listas de IP permitidas {#manage-ip-allow-lists}

Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las Listas de permitidos IP en Cloud Manager.

## Ver y actualizar Listas de permitidos IP {#update-ip-allow-lists}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una Lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta **Listas de IP permitidas** desde la pantalla **Entornos**.
1. Identifique la fila de las Listas de permitidos IP que desee ver o actualizar.
1. Haga clic en el botón de los tres puntos en el extremo derecho de la fila.
1. Seleccione la opción **Ver y actualizar**.
1. El asistente **Ver y actualizar** muestra el nombre, las direcciones IP (o los intervalos) que definen la regla junto con los entornos y servicios a los que se aplica.
1. Cambie el nombre o las direcciones IP que desee y confirme el envío.

Al agregar o eliminar un nuevo rango de IP a una Lista de permitidos IP, se aplica o deja de aplicarse automáticamente a todos los entornos o servicios correspondientes a los que se aplicó anteriormente.

No se pueden realizar actualizaciones en una Lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.

## Comprobar el estado de las Listas de permitidos IP {#check-allow-list-status}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en el icono **Estado** de la Lista de permitidos IP en la tabla de la pantalla **Entornos** y seleccione la página **Listas de permitidos IP**.

1. Cloud Manager muestra el estado de la Lista de permitidos tal como se describe [en la siguiente sección](#status).

### Estado de una lista de IP permitidas {#status}

[Al comprobar el estado de las Listas de permitidos IP](#check-allow-list-status), pueden tener uno de los siguientes valores.

* **Aplicada**: la Lista de permitidos IP se ha aplicado correctamente a uno o varios entornos.

* **Actualizando**: hay una actualización en curso de la Lista de permitidos IP, que puede incluir una o más aplicaciones o la anulación de la aplicación de la lista.

   * Cada aplicación y anulación de la aplicación se enumera junto con su propio estado **No iniciada**, **En curso**, **Completada** o **Error**.

* **Error**: error en uno o más procesos de aplicación o de cancelación de la aplicación de una actualización.
   * Cada aplicación y anulación de la aplicación se enumera junto con su estado.
      * El estado será **Error** si falla una aplicación/anulación de la aplicación en la actualización.
      * El estado permanece como **Error** hasta que se borren todos los errores.
         * Seleccione el icono de **Reintentar** situado junto al estado para poder borrar el error.
      * No puede actualizar ni eliminar una Lista de permitidos IP con un estado **Failed**.

* **Eliminando**: hay una eliminación de una Lista de permitidos IP en curso.
   * La eliminación implica anular la aplicación de la lista de todos los servicios.
   * Cada una de las aplicaciones aparece junto con su propio estado de **No iniciada**, **En curso**, **Completada** o **Error**.
   * Cuando finalice la operación de eliminación:
      * La Lista de permitidos IP no aparece en la tabla de Listas de permitidos IP.
      * La Lista de permitidos IP no se aplica a ningún servicio del programa en Cloud Manager.

* **Error al eliminar**: error de una o varias aplicaciones durante una operación de eliminación.

   * Cada una de las aplicaciones se enumera junto con el estado **Completada** o **Error**.
   * El estado cambia a **Error de eliminación** si falla una de las aplicaciones.
   * El estado permanece como **Error al eliminar** hasta que se borren todos los errores. En el extremo derecho de la fila de la tabla, haga clic en el menú de puntos suspensivos y, a continuación, haga clic en **Eliminar** para borrar cualquier error.
   * No puede actualizar una Lista de permitidos IP mientras el estado sea **Failed**.

## Eliminación de una Lista de permitidos IP {#delete-allow-list}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una Lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta **Listas de IP permitidas** desde la pantalla **Entornos**.
1. Identifique la fila de la Lista de permitidos IP que desea eliminar.
1. Seleccione el menú de los tres puntos del extremo derecho de la fila.
1. Haga clic en **Eliminar**.
1. Confirme el envío.

Al eliminar una Lista de permitidos IP, esta se da de baja automáticamente de todos los servicios y se elimina de la tabla.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si tiene una configuración de CDN (red de distribución de contenido) preexistente para sus Listas de permitidos IP, aparecerá un mensaje informativo en la página **Lista de permitidos IP**. El mensaje le recomienda añadir estas configuraciones mediante la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Agregar una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obtener más información.

También aparecerá un mensaje similar en las páginas **Certificados SSL** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para certificados SSL o nombres de dominio personalizados.
