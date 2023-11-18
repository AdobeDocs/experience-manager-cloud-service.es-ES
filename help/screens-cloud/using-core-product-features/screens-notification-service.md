---
title: Servicio de notificación de Screens en Screens as a Cloud Service
description: En esta página se describe cómo configurar el servicio de notificaciones en Pantallas as a Cloud Service.
index: true
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---


# Servicio de notificación de Screens {#notification-service}

## Introducción {#introduction}

### Información general

El servicio de notificaciones de AEM Screens AEM permite a los administradores recibir un correo electrónico si un reproductor de pantallas de pantalla de la aplicación no hace ping durante un período de tiempo configurable.

### Cómo configurar

En AEM Screens Cloud, los clientes pueden solicitar alertas sobre el estado de inactividad del dispositivo creando un ticket de asistencia con la siguiente información:

* Nombre del cliente
* OrgID de IMS
* Frecuencia de programación: especifique la hora o la frecuencia en horas (por ejemplo, 1) a las que este monitor debe enviar correos electrónicos.
* Tiempo de espera de ping: especifica el intervalo en minutos tras el cual se debe considerar que un dispositivo no está accesible.
* ID de correo electrónico : ID de correo electrónico a los que se enviará el informe