---
title: Administración de listas de permitidos de IP
description: Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las listas de permitidos IP en Cloud Manager.
exl-id: 6efabe53-3f45-47d4-ac1f-979cae0ab33e
source-git-commit: 3080427529bb65e27721e05069012b33579fdd73
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---

# Administración de listas de permitidos de IP {#manage-ip-allow-lists}

Obtenga información sobre cómo ver, editar, eliminar y comprobar el estado de las listas de permitidos IP en Cloud Manager.

## Visualización y actualización de Listas de permitidos IP {#update-ip-allow-lists}

Un usuario en la variable **Propietario empresarial** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.
1. Vaya a **Entornos** de la **Información general** página.
1. Vaya a la **LISTAS DE PERMITIDOS IP** desde la página **Entornos** en el Navegador.
1. Identifique la fila de las listas de permitidos IP que desee ver o actualizar.
1. Haga clic en el botón de puntos suspensivos en el extremo derecho de la fila.
1. Seleccione el **Ver y actualizar** .
1. La variable **Ver y actualizar** El asistente mostrará el nombre, las direcciones IP (o los intervalos) que definen la regla junto con los entornos y el servicio al que se aplica.
1. Realice cambios en el nombre o las direcciones IP y confirme el envío.

Al agregar o eliminar un nuevo rango de IP a una lista de permitidos IP, se aplicará/anulará su aplicación automáticamente a todos los entornos/servicios correspondientes a los que se aplicó anteriormente.

No se pueden realizar actualizaciones en una lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.

## Comprobación del estado de las Listas de permitidos IP {#check-allow-list-status}

Siga estos pasos para comprobar el estado de las listas de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a **Entornos** de la **Información general** página.

1. Haga clic en el **Estado** para la lista de permitidos IP de la tabla de la **Entornos** y seleccione **LISTAS DE PERMITIDOS IP** página.

1. Cloud Manager mostrará el estado de la lista de permitidos como se describe [en la siguiente sección.](#status)

### Estado de una Lista de permitidos IP {#status}

[Al comprobar el estado de las listas de permitidos IP,](#check-allow-list-status) pueden tener uno de los siguientes valores.

* **Aplicado** : la lista de permitidos IP se aplica correctamente a uno o varios entornos.

* **Actualización** - Hay una actualización en curso de la lista de permitidos IP, que puede incluir una o más aplicaciones o la anulación de la aplicación de la lista.

   * Cada aplicación/aplicación se enumera junto con su propio estado de **No iniciado**, **En curso**, **Completar** o **Error**.

* **Error** - Error en uno o más procesos de aplicación o de cancelación de la aplicación de una actualización.
   * Cada aplicación y anulación de la aplicación se enumera junto con su estado.
      * El estado es **Error** si falla una aplicación/desaplicación en la actualización.
      * El estado permanecerá como **Error** hasta que se borren todos los errores.
         * Debe seleccionar el **Reintentar** junto al estado para borrar el error.
      * No se puede actualizar ni eliminar una lista de permitidos IP con una **Error** estado.

* **Eliminación** : Se está eliminando una lista de permitidos IP.
   * La eliminación implica anular la aplicación de la lista de todos los servicios.
   * Cada una de las aplicaciones aparece junto con su propio estado de **No iniciado**, **En curso**, **Completar** o **Error**.
   * Una vez finalizada la operación de eliminación, la lista de permitidos IP:
      * Ya no aparece en la tabla de lista de permitidos IP.
      * Ya no se aplica en ningún servicio del programa en Cloud Manager.

* **Error al eliminar** - Error de una o varias aplicaciones durante una operación de eliminación.

   * Cada una de las aplicaciones se enumera junto con el estado **Completar** o **Error**.
   * El estado será **Error al eliminar** si falla una de las aplicaciones.
   * El estado permanecerá como **Error al eliminar** hasta que se borren todos los errores.
      * Debe seleccionar **Eliminar** en el menú elipsis situado en el extremo derecho de la fila de la tabla para borrar cualquier error.
   * No puede actualizar una lista de permitidos IP mientras el estado sea **Error**.

## Eliminación de una lista de permitidos de IP {#delete-allow-list}

Un usuario en la variable **Propietario empresarial** o **Administrador de implementación** puede seguir estos pasos para ver y actualizar una lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.
1. Vaya a **Entornos** de la **Información general** página.
1. Vaya a la **LISTAS DE PERMITIDOS IP** desde la página **Entornos** en el Navegador.
1. Identifique la fila de la lista de permitidos IP que desea eliminar.
1. Seleccione el menú elipsis en el extremo derecho de la fila.
1. Haga clic en **Eliminar**.
1. Confirme el envío.

Al eliminar una lista de permitidos IP, esta se da de baja automáticamente de todos los servicios y se elimina de la tabla.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si tiene una configuración de CDN preexistente para sus listas de permitidos IP, habrá un mensaje informativo en la variable **LISTA DE PERMITIDOS IP** , lo que le anima a añadir estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario de . El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte el documento [Adición de una lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obtener más información.

También se proporciona un mensaje similar en la variable **Certificados SSL** y **Entornos** páginas para entornos que tienen configuraciones de CDN preexistentes para certificados SSL o nombres de dominio personalizados.
