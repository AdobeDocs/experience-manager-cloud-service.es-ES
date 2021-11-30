---
title: Registro de reproductores en Screens as a Cloud Service
description: Esta página describe cómo registrar reproductores en Screens as a Cloud Service.
exl-id: 1a0d6b22-71b1-4f3c-acaa-82d8d9c0f81a
source-git-commit: 489cc9963910ba9f94d30906127beb75f9ad37df
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Registro de reproductores en Screens as a Cloud Service {#registering-players-screens-cloud}

Una vez que haya instalado y configurado reproductores para Screens as a Cloud Service, debe registrar los reproductores.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se registran los reproductores en el proveedor de servicios de Screens. Después de leer, debe ser capaz de:

* comprender cómo registrar reproductores
* cómo completar el proceso de registro del proveedor de servicios de Screens

## Pasos para registrar un reproductor de Screens {#register-players}

Una vez que haya instalado el reproductor en Screens as a Cloud Service, estará listo para registrar el reproductor en el proveedor de servicios de Screens.

Siga los pasos a continuación para registrar el reproductor:

1. Inicie sesión en el proveedor de servicios de Screens.

1. Vaya a **Códigos de registro** under **Administración de reproductores** en el panel de navegación izquierdo y haga clic en **Crear código**.

   >[!NOTE]
   >Si no existen códigos válidos/no caducados, haga clic en crear código, introduzca un nombre para el código y elija la configuración de caducidad según sus necesidades.

   ![image](/help/screens-cloud/assets/player/register-player1.png)

1. Rellene los campos siguientes en **Creación de un código de registro** cuadro de diálogo:

   ![image](/help/screens-cloud/assets/player/register-player2.png)

   1. **Nombre del código de registro**: Nombre del código de registro
   1. **Caducidad del código de registro**: Fecha de caducidad del código de registro
   1. **Uso del límite**: Alterne el botón para desactivar el límite de uso del código de registro. De forma predeterminada, la opción Limitar uso está desactivada de forma predeterminada.
   1. **Límite de uso**: Elija el número de su límite de uso

1. Haga clic en **Crear** para crear el código de registro. Verá su reproductor con el código de registro en la lista.

   ![image](/help/screens-cloud/assets/player/register-player3.png)

1. Haga clic en el valor debajo de la columna **CÓDIGO DE REGISTRO**  para copiar el valor en el portapapeles.

1. Pegue este valor en la variable **Introducir código** en el campo **Registro del reproductor** en la interfaz de usuario de administración del reproductor AEM Screens y haga clic en **Registro**.

   ![image](/help/screens-cloud/assets/player/register-player4.png)


1. Una vez que haya añadido el código, verá que el reproductor se ha registrado desde la IU de administración del reproductor.

   ![image](/help/screens-cloud/assets/player/register-player5.png)

1. Debería ver que este reproductor ahora aparece en **Reproductores** del panel de navegación izquierdo. El código que se muestra en el proveedor de servicios de Screens coincide con la variable **Información del sistema** en la interfaz de usuario de administración, en Código de reproductor.

   ![image](/help/screens-cloud/assets/player/register-player6.png)

>[!IMPORTANT]
>**Recomendaciones de prácticas recomendadas de seguridad al usar código de registro
>Como práctica recomendada, puede limitar el uso del código de registro. Si un código de registro está comprometido, pero tiene un límite de 100 registros, el atacante puede registrar solamente hasta ese número, pero no más. Siempre puede actualizar el límite de uso después de crear el código de registro y de registrar algunos de los reproductores del cliente. Si el cliente observa una actividad de registro inusual para un código de registro específico, puede reducir el límite en tiempo real mientras investiga y puede aumentar el número de vuelta si se trata de una falsa alarma, sin afectar a los reproductores ya registrados.


## Siguientes pasos {#whats-next}

Ahora que ha instalado y configurado el reproductor en el modo de nube, debe continuar con el recorrido as a Cloud Service de Screens revisando el documento, [Asignación del reproductor a una pantalla en Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/assigning-player-display.md) del proveedor de servicios de Screens.
