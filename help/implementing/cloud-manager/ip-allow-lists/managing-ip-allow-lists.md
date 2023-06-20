---
title: Administrar listas de IP permitidas
description: Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las listas de IP permitidas en Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: 5311ba7f001201fc94c73fa52bc7033716c1ba78
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 57%

---

# Administrar listas de IP permitidas {#manage-ip-allow-lists}

Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las listas de IP permitidas en Cloud Manager.

## Ver y actualizar listas de IP permitidas {#update-ip-allow-lists}

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una lista de IP permitidas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta **Listas de IP permitidas** desde la pantalla **Entornos**.
1. Identifique la fila de las listas de IP permitidas que desee ver o actualizar.
1. Haga clic en el botón de los tres puntos en el extremo derecho de la fila.
1. Seleccione la opción **Ver y actualizar**.
1. El **Ver y actualizar** Este asistente muestra el nombre, las direcciones IP (o los intervalos) que definen la regla junto con los entornos y el servicio al que se aplica.
1. Cambie el nombre o las direcciones IP que desee y confirme el envío.

Al agregar o eliminar un nuevo rango de IP a una lista de IP permitidas, se aplicará/anulará su aplicación automáticamente a todos los entornos/servicios correspondientes a los que se aplicó anteriormente.

No se pueden realizar actualizaciones en una lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.

## Comprobación del estado de las listas de IP permitidas {#check-allow-list-status}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en el icono **Estado** para la lista de IP permitidas de la tabla de la pantalla **Entornos** y seleccione la página **Listas de IP permitidas**.

1. Cloud Manager muestra el estado de la lista de permitidos tal como se describe [en la sección siguiente.](#status)

### Estado de una lista de IP permitidas {#status}

[Al comprobar el estado de las listas de IP permitidas,](#check-allow-list-status) pueden tener uno de los siguientes valores.

* **Aplicada**: la lista de IP permitidas se aplica correctamente a uno o varios entornos.

* **Actualizando** - Hay una actualización en curso de la lista de permitidos IP, que puede incluir una o más aplicaciones o la anulación de la aplicación de la lista.

   * Cada aplicación y anulación de la aplicación se enumera junto con su propio estado **No iniciada**, **En curso**, **Completada** o **Error**.

* **Error** - Error en uno o varios procesos de aplicación o de cancelación de la aplicación de una actualización.
   * Cada aplicación y anulación de la aplicación se enumera junto con su estado.
      * El estado será **Error** si falla una aplicación/anulación de la aplicación en la actualización.
      * El estado se mantiene como **Error** hasta que se borren todos los errores.
         * Seleccione el **Reintentar** junto al estado para poder borrar el error.
      * No se puede actualizar ni eliminar una lista de permitidos IP con un **Error** estado.

* **Eliminando**: Se está eliminando una lista de IP permitidas.
   * La eliminación implica cancelar la aplicación de la lista de todos los servicios.
   * Cada anulación de la aplicación se enumera junto con su propio estado de **Sin iniciar**, **En curso**, **Completar**, o **Error**.
   * Una vez finalizada la operación de eliminación, la lista de IP permitidas:
      * Ya no aparece en la tabla de lista de IP permitidas.
      * Ya no se aplicará en ningún servicio del programa en Cloud Manager.

* **Error de eliminación** - Error en una o varias aplicaciones durante una operación de eliminación.

   * Cada anulación de la aplicación se enumera junto con el estado **Completar** o **Error**.
   * El estado cambia a **Error de eliminación** si falla una de las aplicaciones.
   * El estado se mantiene como **Error de eliminación** hasta que se borren todos los errores.
      * Seleccionar **Eliminar** en el menú de los tres puntos del extremo derecho de la fila de la tabla para borrar cualquier error.
   * No se puede actualizar una lista de permitidos IP mientras el estado sea **Error**.

## Eliminación de una lista de IP permitidas {#delete-allow-list}

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una lista de IP permitidas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta **Listas de IP permitidas** desde la pantalla **Entornos**.
1. Identifique la fila de la lista de IP permitidas que desee eliminar.
1. Seleccione el menú de los tres puntos del extremo derecho de la fila.
1. Haga clic en **Eliminar**.
1. Confirme el envío.

Al eliminar una lista de permitidos IP, esta se da de baja automáticamente de todos los servicios y se elimina de la tabla.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si tiene una configuración de CDN preexistente para sus listas de permitidos IP, aparece un mensaje informativo en la **LISTA DE PERMITIDOS IP** página. El mensaje le recomienda agregar estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Adición de una lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obtener más información.

También aparecerá un mensaje similar en las páginas **Certificados SSL** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para certificados SSL o nombres de dominio personalizados.
