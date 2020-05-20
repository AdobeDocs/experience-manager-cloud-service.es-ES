---
title: Administrar Entornos - Servicio de nube
description: Administrar Entornos - Servicio de nube
translation-type: tm+mt
source-git-commit: 1f72e8c935dc6cfe1124afd9f1a0fe37a97ded34
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 9%

---


# Administrar entornos {#manage-environments}

En la sección siguiente se describen los tipos de entornos que puede crear un usuario y la forma en que puede crear un entorno.

## Tipos de Entornos {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entornos (dentro de los límites de lo que está disponible para el inquilino específico).

* **Entorno**de producción y etapa:
La producción y la fase están disponibles como dúo y se utilizan con fines de prueba y producción.

* **Desarrollo**: Se puede crear un entorno de desarrollo con fines de desarrollo y ensayo y se asociará únicamente a los oleoductos que no sean de producción.

   >[!NOTE]
   >Se configurará un entorno de desarrollo que se crea automáticamente en un programa de Simulador para pruebas para que incluya las soluciones Sitios y Recursos.

   La siguiente tabla resume los tipos de Entornos y sus atributos:

   | Nombre | Nivel de autor | Publicar nivel | El usuario puede crear | El usuario puede eliminar | Canalización que puede asociarse con entorno |
   |--- |--- |--- |--- |---|---|
   | Producción | Sí | Sí si los sitios están incluidos | Sí | No | Canalización de producción |
   | Escenario | Sí | Sí si los sitios están incluidos | Sí | No | Canalización de producción |
   | Desarrollo | Sí | Sí si los sitios están incluidos | Sí | Sí | Canalización sin producción |

   >[!NOTE]
   >La producción y la fase están disponibles como dúo y se utilizan con fines de prueba y producción.  El usuario no podrá crear solo la fase o solo el entorno de producción.

## Añadir un Entorno {#adding-environments}


1. Haga clic en **Añadir Entorno** para agregar un entorno. Se puede acceder a este botón desde la pantalla **Entornos** .
   ![](assets/no-environment-2.png)


   La opción **Añadir Entorno** también está disponible en la tarjeta de **Entornos** cuando hay cero entornos en el programa.

   ![](assets/no-environments.png)

   >[!NOTE]
   >La opción **Añadir Entorno** se desactivará por falta de permisos o por lo que se pueda contratar.

1. Aparece el cuadro de diálogo **Agregar entorno**. El usuario debe enviar detalles como **Tipo de entorno**, **Nombre de entorno** y **Descripción de entorno** (según el objetivo del usuario al crear el entorno dentro de los límites de lo que está disponible para el inquilino específico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Al crear un entorno, se crean una o más *integraciones* en Adobe I/O. Son visibles para los usuarios clientes que tienen acceso a la consola de Adobe I/O y no deben eliminarse. Esto se rechaza en la descripción de la consola de Adobe I/O.

   ![](assets/add-environment-image1.png)

1. Haga clic en **Guardar** para agregar un entorno con los criterios rellenados.  Ahora, la pantalla *Información general* muestra la tarjeta desde la que puede configurar la canalización.

   >[!NOTE]
   >En caso de que aún no haya configurado la canalización sin producción, la pantalla *Información general* muestra la tarjeta desde la que puede crear la canalización sin producción.

## Actualizando Entorno {#updating-dev-environment}

Adobe administra automáticamente las actualizaciones de los entornos de fase y producción.

Los usuarios del programa administran las actualizaciones de los entornos de desarrollo. Cuando un entorno no está ejecutando la última versión de AEM disponible para el público, el estado de la tarjeta de Entornos en la pantalla de inicio mostrará **ACTUALIZACIÓN DISPONIBLE**.

![](assets/manage-environments2.png)


La opción **Actualizar** está disponible en el menú desplegable de la tarjeta de **Entornos** .
Esta opción también está disponible desde el botón **Administrar** , si hace clic en **Detalles** desde la tarjeta de **Entornos** .

![](assets/update-environment2.png)

Si selecciona esta opción en el menú desplegable, un administrador de implementación podrá actualizar la canalización asociada con este entorno a la última versión y, a continuación, ejecutar la canalización.

Si la canalización ya se ha actualizado, se solicita al usuario que ejecute la canalización.

## Eliminación de Entorno {#deleting-environment}

El usuario con los permisos necesarios podrá eliminar un entorno de desarrollo.

La opción **Eliminar** está disponible en el menú desplegable de la tarjeta de **Entornos** .
Esta opción también está disponible desde el botón **Administrar** , si hace clic en **Detalles** desde la tarjeta de **Entornos** .

![](assets/deleting-environment1.png)

>[!NOTE]
Esta función no está disponible para el entorno de producción/fase definido en un programa normal configurado para fines de producción. Sin embargo, la función está disponible para entornos de producción/fase en un programa de Simulador para pruebas.

## Acceso a Developer Console {#accessing-developer-console}

Seleccione **Developer Console** en el menú desplegable de la tarjeta de **Entornos** .

![](assets/dev-console1.png)

También puede seleccionar esta opción desde el botón **Administrar** , si hace clic en **Detalles** desde la tarjeta de **Entornos** .

