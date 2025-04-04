---
title: Registro de reproductores en Screens as a Cloud Service
description: En esta página se describe cómo registrar reproductores en Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 13%

---

# Registro de reproductores en Screens as a Cloud Service {#registering-players-screens-cloud}

Una vez instalados y configurados los reproductores para Screens as a Cloud Service, debe registrarlos.

## Objetivo {#objective}

Este documento le ayuda a comprender el registro de reproductores en Screens Services Provider. Después de leerlo, debe ser capaz de:

* entender cómo registrar jugadores
* Cómo completar el proceso de registro desde el proveedor de servicios de Screens

## Pasos para registrar un reproductor de Screens {#register-players}

Una vez que haya instalado el reproductor en Screens as a Cloud Service, podrá registrarlo en Screens Services Provider.

Siga los pasos a continuación para registrar su reproductor:

1. Inicie sesión en el proveedor de servicios de Screens.

1. Vaya a **Códigos de registro** en **Administración de reproductores** desde el panel de navegación izquierdo y haga clic en **Crear código**.

   >[!NOTE]
   >Si no existen códigos válidos o no caducados, haga clic en Crear código, escriba un nombre para el código y elija la configuración de caducidad según sus necesidades.

   ![imagen](/help/screens-cloud/assets/player/register-player1.png)

1. Rellene los campos siguientes en **Crear un cuadro de diálogo de código de registro**:

   ![imagen](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nombre del código de registro**: Nombre para el código de registro
   1. **Caducidad del código de registro**: Fecha de caducidad de su código de registro
   1. **Limitar uso**: cambia el botón para desactivar el límite de uso de tu código de registro. De forma predeterminada, la opción Limitar uso está desactivada.
   1. **Límite de uso**: elige el número de tu límite de uso

1. Haga clic en **Crear** para crear el código de registro. Puedes ver tu reproductor con el código de registro en la lista.

   ![imagen](/help/screens-cloud/assets/player/register-player3.png)

1. Haga clic en el valor de la columna **CÓDIGO DE REGISTRO** para copiar el valor en el portapapeles.

1. Pegue este valor en el campo **Escribir código** de la ficha **Registro del reproductor** de la interfaz de usuario de administración del reproductor de AEM Screens y haga clic en **Registrar**.

   ![imagen](/help/screens-cloud/assets/player/register-player4.png)


1. Cuando haya añadido el código, podrá ver que el reproductor está registrado desde la IU de administración del reproductor.

   ![imagen](/help/screens-cloud/assets/player/register-player5.png)

1. Debería ver este reproductor ahora en **Reproductores** desde el panel de navegación izquierdo. El código que se muestra en el proveedor de servicios de Screens coincide con el panel **Información del sistema** de la interfaz de usuario del administrador en Código del reproductor.

   ![imagen](/help/screens-cloud/assets/player/register-player6.png)

   >[!IMPORTANT]
   >**Recomendaciones de seguridad recomendadas al usar el código de registro**
   >Se recomienda limitar el uso del código de registro. Si un código de registro está comprometido, pero tiene un límite de 100 registros, entonces el atacante puede registrar solo hasta ese número, pero no más. Siempre puede actualizar el límite de uso después de crear el código de registro y de registrar a algunos de los jugadores del cliente. Si el cliente observa una actividad de registro inusual para un código de registro específico, puede reducir el límite en tiempo real mientras investiga y puede volver a aumentar el número si fue una falsa alarma, sin afectar a los jugadores ya registrados.


## Siguientes pasos {#whats-next}

Ahora que ha instalado y configurado el reproductor en el modo de nube, debe continuar con el as a Cloud Service recorrido de Screens revisando el documento [Asignación del reproductor a una pantalla en Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) del proveedor de servicios de Screens.
