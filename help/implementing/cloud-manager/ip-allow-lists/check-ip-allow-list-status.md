---
title: Comprobación del estado de Lista de permitidos IP
description: Comprobación del estado de Lista de permitidos IP
translation-type: tm+mt
source-git-commit: e6a8d69ea87ac56a51cde2f131c4accff1bea527
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Comprobando estado de Lista de permitidos IP {#check-allow-list-status}

Siga los pasos a continuación para determinar el estado de las actualizaciones de su Lista de permitidos IP:

1. Haga clic en el icono Estado de la Lista de permitidos IP en la tabla de la pantalla **Entornos** y seleccione la página **Listas de permitidos IP**.

1. Cloud Manager mostrará uno de los siguientes estados, como se indica en la sección siguiente.

## Estado de una Lista de permitidos IP {#status}

Las siguientes son las definiciones de estado que aparecerán en una Lista de permitidos IP:

* **Aplicado**: La Lista de permitidos IP se aplica correctamente en entornos.  Los entornos y el servicio se pueden ver como se muestra en la siguiente imagen.

* **Actualizando**: Está en proceso una actualización de la Lista de permitidos IP que puede incluir una o más solicitudes o no solicitudes. Se enumerarán todas las solicitudes de aplicación y de anulación de la aplicación junto con No iniciado/En curso/Completado o Fallido.

* **Error**: Error en uno o varios procesos de aplicación o anulación de la aplicación en una actualización. Se enumerarán todas las opciones Aplicar y No aplicar junto con Completado o Fallido.
   * El estado será Error, aunque se produzca un error al aplicar o anular la aplicación en la actualización.
   * El estado seguirá siendo Fallido hasta que se borren todos los errores. El usuario debe seleccionar el icono de reintento junto al estado para borrar el error.
   * El usuario no podrá actualizar o eliminar la Lista de permitidos IP mientras el estado sea Fallado.

* **Eliminando**: La solicitud de eliminación está en curso. Esto implica no aplicar todos los servicios. Cada Unapply aparecerá junto con Not Started/In Progress/Complete o Failed.
Una vez finalizada la operación de eliminación, la Lista de permitidos IP:
   * Ya no aparece en la tabla de Lista de permitidos IP.
   * Ya no se aplica a ningún servicio del programa en Cloud Manager.

* **Error** al eliminar: Error en uno o varios procesos de anulación de la aplicación en una operación de eliminación. Cada Unapply aparecerá junto con Complete o Failed.

   * El estado será Error al eliminar, aunque se produzca un error al anular la aplicación.
   * El estado seguirá siendo Error de eliminación hasta que se borren todos los errores. El usuario debe seleccionar Eliminar en el **...** en el extremo derecho de la fila de la tabla para borrar cualquier error.
   * El usuario no podrá actualizar la Lista de permitidos IP mientras el estado sea Fallado.

