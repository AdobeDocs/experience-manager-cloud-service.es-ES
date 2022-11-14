---
title: Notificaciones
description: Obtenga información sobre cómo recibir información sobre las implementaciones de canalización mediante el sistema de notificación de Adobe Experience Cloud.
exl-id: c1c740b0-c873-45a8-9518-a856db2be75b
source-git-commit: 451b5a089645004c58c2674fd1fb13afbe1201cf
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 12%

---


# Notificaciones {#notifications}

Descubra cómo Cloud Manager le notifica de los eventos importantes.

## Notificaciones en Cloud Manager {#cloud-manager-notifications}

[!UICONTROL Cloud Manager] envía notificaciones cuando se inicia y finaliza una canalización de producción (con éxito o sin éxito), al principio de una implementación de producción.

Estas notificaciones se envían a través de la variable [!UICONTROL Experience Cloud] sistema de notificaciones a los usuarios de **Propietario empresarial**, **Administrador de programas** y **Administrador de implementación** funciones.

Las notificaciones aparecen en una barra lateral dentro de [!UICONTROL Cloud Manager] y en todo el Adobe [!UICONTROL Experience Cloud]. El icono de campana del encabezado se señala cuando tiene nuevas notificaciones.

![Icono de notificaciones](assets/notifications-bell-badged.png)

Haga clic en el icono de campana para abrir la barra lateral y ver las notificaciones. La variable **Notificaciones** en la barra lateral, se muestran las notificaciones más recientes, como las confirmaciones de implementación. Las notificaciones afectan a sus entornos.

![Barra lateral de notificaciones](assets/notifications-activities.png)

La variable **Anuncios** incluye anuncios de productos de Adobe. Los anuncios hacen referencia al producto.

![Barra lateral de notificaciones](assets/notificaitons-announcements.png)

Haga clic en una notificación o anuncio para ver sus detalles. Las notificaciones vinculadas a actividades como las implementaciones de canalización le llevan al detalle de esa actividad, como la ventana de ejecución de la canalización.

Haga clic en el **Ver todo** en la parte inferior del panel para ver todos los anuncios de la bandeja de entrada.

Haga clic en el **Marcar todo como leído** en la parte inferior del panel para marcar todas las notificaciones no leídas como leídas y borrar el distintivo del icono de la campana.

## Configuración de notificaciones {#configuration}

Puede personalizar cómo recibe las notificaciones y qué notificaciones recibe.

Haga clic en el icono de engranaje en la parte superior de la barra lateral de notificaciones.

![Icono de configuración de notificaciones](assets/notifications-configuration.png)

Esto abre el **preferencias del Experience Cloud** , donde puede definir las suscripciones de notificación y cómo recibe las notificaciones.

### Suscripciones {#subscriptions}

Las suscripciones definen para qué productos recibe notificaciones y qué notificaciones.

![Suscripciones de notificaciones](assets/notifications-subscriptions.png)

De forma predeterminada, recibirá todas las notificaciones de todos los productos. Haga clic en **Personalizar** junto a un producto para definir los tipos de notificaciones que recibe para ese producto.

![Personalización de la suscripción de notificaciones](assets/notifications-subscriptions-customize.png)

### Prioridad {#priority}

Las alertas prioritarias se marcarán con un **ALTO** y se pueden configurar para que se reciban exclusivamente como alertas. En el **Prioridad** , puede definir qué categorías se clasifican como notificaciones de prioridad.

![Prioridad de notificación](assets/notifications-priority.png)

Utilice la lista desplegable para añadir a la lista de categorías que cumplen los requisitos de prioridad. Haga clic en la X situada junto a los nombres de las categorías para eliminarlos.

### Alertas {#alerts}

Las alertas aparecen en la esquina superior derecha de la ventana durante unos segundos. Utilice la variable **Alertas** para definir para qué notificaciones recibe alertas.

![Alertas de notificación](assets/notifications-alerts.png)

Puede definir el comportamiento de las alertas.

* **Mostrar alertas para** - Define los tipos de notificaciones que déclencheur alertas
* **Las alertas deben permanecer en la pantalla hasta que las descarte** - Controla si las alertas deben persistir a menos que las descarte activamente
* **Duración** - Define cuánto tiempo debe permanecer la alerta en la pantalla si no ha elegido que permanezcan en ella.

### Correo electrónico {#emails}

Las notificaciones están disponibles en la interfaz de usuario web en todo el Adobe [!UICONTROL Experience Cloud] soluciones. También puede optar por que estas notificaciones se envíen por correo electrónico en la variable **Correos electrónicos** para obtener más información.

![Correos electrónicos de notificación](assets/notifications-emails.png)

De forma predeterminada, no se envían correos electrónicos. Puede optar por recibir correos electrónicos como:

* Instantáneamente
* Cada día
* Cada semana

When **Notificaciones instantáneas** se selecciona, los correos electrónicos se envían inmediatamente para cada notificación. Para **Resumen diario** y **Resumen semanal** puede elegir cuándo se envía el compendio diario y en qué día y cuándo se envía el compendio semanal.