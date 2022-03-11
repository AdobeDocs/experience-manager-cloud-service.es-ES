---
title: Comprobación del estado de Lista de permitidos de IP
description: Comprobación del estado de Lista de permitidos de IP
exl-id: 5ddea04f-3720-4663-90a8-9399019bfcbe
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Comprobación del estado de Lista de permitidos de IP {#check-allow-list-status}

Siga los pasos a continuación para determinar el estado de las actualizaciones de la Lista de permitidos IP:

1. Haga clic en el icono Estado de la Lista de permitidos IP en la tabla de la **Entornos** y seleccione **LISTAS DE PERMITIDOS IP** página.

1. Cloud Manager mostrará uno de los siguientes estados, como se menciona en la sección siguiente.

## Estado de una Lista de permitidos IP {#status}

Las siguientes son las definiciones de estado que aparecerán en una Lista de permitidos IP:

* **Aplicado**: La Lista de permitidos IP se aplica correctamente en los entornos.  Los entornos y el servicio se pueden ver como se muestra en la siguiente imagen.

* **Actualización**: Se está realizando una actualización de la Lista de permitidos IP que puede incluir una o más solicitudes o la anulación de la aplicación. Cada solicitud y cada cancelación de aplicación se enumerarán junto con No iniciado/En curso/Completado o Fallido.

* **Error**: Error en uno o más procesos de aplicación o anulación de la aplicación en una actualización. Cada solicitud y anulación de la aplicación se enumerarán junto con Completar o Fallido.
   * El estado será Failed, aunque falle una aplicación/cancelación de la aplicación en la actualización.
   * El estado seguirá siendo Failed hasta que se borren todos los errores. El usuario debe seleccionar el icono de reintento situado junto al estado para borrar el error.
   * El usuario no podrá actualizar ni eliminar la Lista de permitidos IP mientras el estado sea Failed.

* **Eliminación**: La solicitud de eliminación está en curso. Esto implica la no aplicación de todos los servicios. Cada una de las anulaciones de aplicación se enumerará junto con No iniciado/En curso/Completado o Fallido.
Una vez finalizada la operación de eliminación, la Lista de permitidos IP:
   * Ya no aparece en la tabla de Lista de permitidos IP.
   * Ya no se aplica en ningún servicio del programa en Cloud Manager.

* **Error al eliminar**: Error en uno o varios procesos de anulación de la aplicación en una operación de eliminación. Cada Unapply se enumerará junto con Complete o Failed.

   * El estado será Error de eliminación, aunque falle una de las opciones de anulación de la aplicación.
   * El estado seguirá siendo Error de eliminación hasta que se borren todos los errores. El usuario debe seleccionar Eliminar en la **...** en el extremo derecho de la fila de la tabla para borrar cualquier error.
   * El usuario no podrá actualizar la Lista de permitidos IP mientras el estado sea Failed.

## Configuraciones preexistentes de CDN para Listas de permitidos IP {#pre-existing-cdn}

Los clientes con entornos que incluyan configuraciones de CDN preexistentes para Listas de permitidos IP, certificados SSL o nombres de dominio personalizados verán el siguiente mensaje en la **LISTA DE PERMITIDOS IP** y **Entorno** página de detalles . El mensaje mostrado en la interfaz de usuario desaparecerá una vez que el cliente haya migrado completamente todas las configuraciones de entorno preexistentes a través de la interfaz de usuario y puede tardar entre 1 y 2 días hábiles en desaparecer el mensaje.

>[!NOTE]
>Para ver y administrar las configuraciones preexistentes, deben agregarse mediante la interfaz de usuario de . Consulte [Adición de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) para obtener más información.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
