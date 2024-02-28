---
title: Servicio de notificación de Screens en Screens as a Cloud Service
description: En esta página se describe cómo configurar el servicio de notificaciones en Pantallas as a Cloud Service.
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 69798b1ac3758d37c4e2f480ccc23bae24d6a814
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# Servicio de notificación de Screens {#notification-service}

## Introducción {#introduction}

### Información general

El servicio de notificaciones de AEM Screens permite a los administradores recibir un informe con una lista de todos los reproductores de AEM Screens que no hicieron ping durante un período de tiempo configurable en un correo electrónico.

### Cómo configurar

En AEM Screens Cloud, los clientes pueden solicitar un informe sobre el estado de inactividad del dispositivo creando un ticket de asistencia con la siguiente información:

* Nombre del cliente
* OrgID de IMS
* Frecuencia de programación: especifique la hora o la frecuencia en horas (por ejemplo, 1) a las que este monitor debe enviar correos electrónicos.
* Tiempo de espera de ping: especifica el intervalo en minutos tras el cual se debe considerar que un dispositivo no está accesible.
* ID de correo electrónico : ID de correo electrónico a los que se enviará el informe

>[!NOTE]
>El reproductor solo se enviará a los correos electrónicos si el dispositivo no ha hecho ping durante el tiempo de espera de ping especificado en el momento de generar el correo electrónico.

### Ejemplo de caso de uso

Si establece el tiempo del informe en 5 a. m. y el tiempo de espera de ping en 1 hora, si el dispositivo Screens no hace ping entre las 4:00 a. m. y las 5:00 a. m., recibirá una notificación por correo electrónico que confirmará la inactividad del dispositivo.
