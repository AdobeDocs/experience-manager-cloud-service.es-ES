---
title: Comprobación del estado de Lista de permitidos de IP
description: Comprobación del estado de Lista de permitidos de IP
translation-type: tm+mt
source-git-commit: c6fe5e9dab0e119271c6cea272dddabe7babb1e4
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# Comprobación del estado de Lista de permitidos de IP {#check-allow-list-status}

Siga los pasos a continuación para determinar el estado de las actualizaciones de la Lista de permitidos IP:

1. Haga clic en el icono Estado de la Lista de permitidos IP de la tabla en la pantalla **Entornos** y seleccione la página **Listas de permitidos IP**.

1. Cloud Manager mostrará uno de los siguientes estados, como se menciona en la sección siguiente.

## Estado de una Lista de permitidos IP {#status}

Las siguientes son las definiciones de estado que aparecerán en una Lista de permitidos IP:

* **Aplicado**: La Lista de permitidos de IP se aplica correctamente en los entornos.  Los entornos y el servicio se pueden ver como se muestra en la siguiente imagen.

* **Actualizando**: Se está realizando una actualización de la Lista de permitidos IP que puede incluir una o más solicitudes o la anulación de la aplicación. Cada solicitud y cada cancelación de aplicación se enumerarán junto con No iniciado/En curso/Completado o Fallido.

* **Error**: Error en uno o más procesos de aplicación o anulación de la aplicación en una actualización. Cada solicitud y anulación de la aplicación se enumerarán junto con Completar o Fallido.
   * El estado será Failed, aunque falle una aplicación/cancelación de la aplicación en la actualización.
   * El estado seguirá siendo Failed hasta que se borren todos los errores. El usuario debe seleccionar el icono de reintento situado junto al estado para borrar el error.
   * El usuario no podrá actualizar ni eliminar la Lista de permitidos IP mientras el estado sea Failed.

* **Eliminación**: La solicitud de eliminación está en curso. Esto implica la no aplicación de todos los servicios. Cada una de las anulaciones de aplicación se enumerará junto con No iniciado/En curso/Completado o Fallido.
Una vez finalizada la operación de eliminación, la Lista de permitidos IP:
   * Ya no aparece en la tabla de Lista de permitidos IP.
   * Ya no se aplica en ningún servicio del programa en Cloud Manager.

* **Error** de eliminación: Error en uno o varios procesos de anulación de la aplicación en una operación de eliminación. Cada Unapply se enumerará junto con Complete o Failed.

   * El estado será Error de eliminación, aunque falle una de las opciones de anulación de la aplicación.
   * El estado seguirá siendo Error de eliminación hasta que se borren todos los errores. El usuario debe seleccionar Eliminar del **...** en el extremo derecho de la fila de la tabla para borrar cualquier error.
   * El usuario no podrá actualizar la Lista de permitidos IP mientras el estado sea Failed.

## Configuraciones preexistentes de CDN para Listas de permitidos IP {#pre-existing-cdn}

Los clientes con entornos que incluyan configuraciones de CDN preexistentes para Listas de permitidos IP, certificados SSL o nombres de dominio personalizados verán el siguiente mensaje en la página de detalles **IP Lista de permitidos** y **Environment**. El mensaje mostrado en la interfaz de usuario desaparecerá una vez que el cliente haya migrado completamente todas las configuraciones de entorno preexistentes a través de la interfaz de usuario y puede tardar entre 1 y 2 días hábiles en desaparecer el mensaje.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>Para ver y administrar las configuraciones preexistentes, deben agregarse a través de la interfaz de usuario, como se muestra en la figura siguiente.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)

