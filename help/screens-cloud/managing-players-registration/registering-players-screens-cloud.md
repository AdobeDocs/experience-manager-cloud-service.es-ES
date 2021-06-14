---
title: Registro de reproductores en Screens como Cloud Service
description: Esta página describe cómo registrar reproductores en Screens como Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---


# Registro de reproductores en Screens como Cloud Service {#registering-players-screens-cloud}

Una vez que haya instalado y configurado reproductores para Screens como Cloud Service, debe registrar los reproductores.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se registran los reproductores en el proveedor de servicios de Screens. Después de leer, debe:

* Obtenga información sobre cómo registrar jugadores.
* Poder administrar los canales en un proyecto de AEM Screens, en términos de ámbito.

## Pasos para registrar un reproductor de Screens {#register-players}

Una vez que haya instalado el reproductor en Screens como Cloud Service, estará listo para registrar el reproductor en el proveedor de servicios de Screens.

Siga los pasos a continuación para registrar el reproductor:

1. Inicie sesión en el proveedor de servicios de Screens.

1. Vaya a **Registration Codes** en **Players management** desde el panel de navegación izquierdo y haga clic en **Create code**.

   >[!NOTE]
   >Si no existen códigos válidos/no caducados, haga clic en crear código, introduzca un nombre para el código y elija la configuración de caducidad según sus necesidades.

   ![image](/help/screens-cloud/assets/player/register-player1.png)

1. Rellene los campos siguientes del cuadro de diálogo **Crear un código de registro**:

   ![image](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nombre** del código de registro: Nombre del código de registro
   1. **Caducidad** del código de registro: Fecha de caducidad del código de registro
   1. **Uso** de límites: Alterne el botón para desactivar el límite de uso del código de registro. De forma predeterminada, la opción Limitar uso está desactivada de forma predeterminada.
   1. **Límite** de uso: Elija el número de su límite de uso

1. Haga clic en **Create** para crear el código de registro. Verá su reproductor con el código de registro en la lista.

   ![image](/help/screens-cloud/assets/player/register-player3.png)

1. Haga clic en el valor debajo de la columna **REGISTRATION CODE** para copiar el valor en el portapapeles.

1. Pegue este valor en el campo **Enter code** de la pestaña **Player Registration** de la interfaz de usuario de administración del reproductor AEM Screens y haga clic en **Register**.

   ![image](/help/screens-cloud/assets/player/register-player4.png)


1. Una vez que haya añadido el código, verá que el reproductor se ha registrado desde la IU de administración del reproductor.

   ![image](/help/screens-cloud/assets/player/register-player5.png)

1. Debería ver que este reproductor ahora aparece en **Players** desde el panel de navegación izquierdo. El código que se muestra en el proveedor de servicios de Screens coincide con el panel **Información del sistema** de la interfaz de usuario del administrador en Código del reproductor.

   ![image](/help/screens-cloud/assets/player/register-player6.png)

