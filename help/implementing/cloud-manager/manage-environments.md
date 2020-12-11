---
title: 'Administrar Entornos: Cloud Service'
description: 'Administrar Entornos: Cloud Service'
translation-type: tm+mt
source-git-commit: b3c577f1030ed96e5dde596c5fe01e853c3199df
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 4%

---


# Administración de entornos {#manage-environments}

En la sección siguiente se describen los tipos de entornos que puede crear un usuario y la forma en que puede crear un entorno.

## Tipos de entornos {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entornos (dentro de los límites de lo que está disponible para el inquilino específico).

* **Entorno** de producción y etapa: La producción y la fase están disponibles como dúo y se utilizan con fines de prueba y producción.

* **Desarrollo**: Se puede crear un entorno de desarrollo con fines de desarrollo y ensayo y se asociará únicamente a los oleoductos que no sean de producción.

   >[!NOTE]
   >Se configurará un entorno de desarrollo que se crea automáticamente en un programa de Simulador para pruebas para que incluya las soluciones Sitios y Recursos.

   La siguiente tabla resume los tipos de Entornos y sus atributos:

   | Nombre | Nivel de Author | Publicar nivel | El usuario puede crear | El usuario puede eliminar | Canalización que puede asociarse con entorno |
   |--- |--- |--- |--- |---|---|
   | Producción | Sí | Sí si los sitios están incluidos | Sí | No | Canalización de producción |
   | Escenario | Sí | Sí si los sitios están incluidos | Sí | No | Canalización de producción |
   | Desarrollo | Sí | Sí si los sitios están incluidos | Sí | Sí | Canalización sin producción |

   >[!NOTE]
   >La producción y la fase están disponibles como dúo y se utilizan con fines de prueba y producción.  El usuario no podrá crear solo la fase o solo el entorno de producción.

## Añadiendo Entorno {#adding-environments}

1. Haga clic en **Añadir Entorno** para agregar un entorno. Se podrá acceder a este botón desde la pantalla **Entornos**.
   ![](assets/environments-tab.png)

   La opción **Añadir Entorno** también está disponible en la tarjeta **Entornos** cuando hay cero entornos en el programa.

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


## Viendo Entorno {#viewing-environment}

La tarjeta **Entornos** de la página Información general lista hasta tres entornos.

1. Seleccione el botón **Mostrar todo** para navegar a la página de resumen **Entorno** para vista de una tabla con una lista completa de entornos.

   ![](assets/environment-view-1.png)

1. La página **Entornos** muestra la lista de todos los entornos existentes.

   ![](assets/environment-view-2.png)

1. Seleccione cualquiera de los entornos de la lista para vista de los detalles del entorno.

   ![](assets/environment-view-3.png)


## Actualizando Entorno {#updating-dev-environment}

Las actualizaciones de los entornos de fase y producción se gestionan automáticamente mediante Adobe.

Los usuarios del programa administran las actualizaciones de los entornos de desarrollo. Cuando un entorno no está ejecutando la última versión de AEM disponible públicamente, el estado de la tarjeta de Entornos en la pantalla principal mostrará **ACTUALIZACIÓN DISPONIBLE**.

![](assets/environ-update.png)


La opción **Actualizar** está disponible en la tarjeta **Entornos**.
Esta opción también está disponible si hace clic en **Detalles** desde la tarjeta **Entornos**. Se abre la página **Entornos** y una vez seleccionado el entorno de desarrollo, haga clic en **...** y seleccione **Actualizar**, como se muestra en la figura siguiente:

![](assets/environ-update2.png)

Al seleccionar esta opción, un administrador de implementación podrá actualizar la canalización asociada con este entorno a la versión más reciente y, a continuación, ejecutar la canalización.

Si la canalización ya se ha actualizado, se solicita al usuario que ejecute la canalización.

## Eliminando Entorno {#deleting-environment}

El usuario con los permisos necesarios podrá eliminar un entorno de desarrollo.

La opción **Eliminar** está disponible en el menú desplegable de la tarjeta **Entornos**. Haga clic en **...** para un entorno de desarrollo que desee eliminar.

![](assets/environ-delete.png)

La opción Eliminar también está disponible si hace clic en **Detalles** de la tarjeta **Entornos**. Se abre la página **Entornos** y una vez seleccionado el entorno de desarrollo, haga clic en **...** y seleccione **Eliminar**, como se muestra en la figura siguiente:

![](assets/environ-delete2.png)


>[!NOTE]
>
>Esta función no está disponible para el entorno de producción/fase definido en un programa normal configurado para fines de producción. Sin embargo, la función está disponible para entornos de producción/fase en un programa de Simulador para pruebas.

## Administración del acceso {#managing-access}

Seleccione **Administrar acceso** en el menú desplegable de la tarjeta **Entornos**. Puede desplazarse directamente a la instancia de creación y administrar el acceso del entorno.

Consulte [Administración de acceso a la instancia de autor](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md#manage-access-aem) para obtener más información.

![](assets/environ-access.png)


## Acceso a Developer Console {#accessing-developer-console}

Seleccione **Consola de desarrollador** en el menú desplegable de la tarjeta **Entornos**. Se abrirá una nueva ficha en el explorador con la página de inicio de sesión en **Consola de programadores**.

Solo un usuario en la función de desarrollador tendrá acceso a **Developer Console**. Excepción para los Programas de Simulador para pruebas, en los que cualquier usuario con acceso al Programa de Simulador para pruebas de Cloud Manager tendrá acceso a **Consola de desarrollador**.

Consulte [Entornos de Simulador para pruebas de hibernación y deshibernación](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obtener más detalles.


![](assets/environ-devconsole.png)

Esta opción también está disponible si hace clic en **Detalles** desde la tarjeta **Entornos**. Se abre la página **Entornos** y una vez seleccionado un entorno, haga clic en **...** y seleccione **Consola de desarrollador**.

## Iniciar sesión localmente {#login-locally}

Seleccione **Inicio de sesión local** en el menú desplegable de la tarjeta **Entornos** para iniciar sesión localmente en Adobe Experience Manager.

![](assets/environ-login-locally.png)

Además, puede iniciar sesión localmente desde la página de resumen **Entornos**.

![](assets/environ-login-locally-2.png)

## Administración de nombres de dominio personalizados {#manage-cdn}

Vaya a la página de detalles **Entornos** desde la página Resumen de Entornos.

Las siguientes acciones se pueden realizar en el servicio de publicación de su entorno como se describe a continuación:

1. [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Visualización y actualización de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

## Administración de Listas de permitidos IP {#manage-ip-allow-lists}

Acceda a la página de detalles del Entorno desde la página Resumen de Entornos. Puede realizar las siguientes acciones en los servicios Publicar y/o Autor para su entorno aquí.

### Aplicación de una Lista de permitidos IP {#apply-ip-allow-list}

La aplicación de una Lista de permitidos IP es el proceso mediante el cual todos los intervalos de IP incluidos en la definición de la lista de permitidos están asociados a un servicio de creación o publicación en un entorno. Para poder aplicar una Lista de permitidos IP, debe haber iniciado sesión un usuario con la función Propietario de la empresa o Administrador de implementación.

>[!NOTE]
>La Lista de permitidos IP debe existir en Cloud Manager para poder aplicarla a un servicio de entorno. Para obtener más información sobre las Listas de permitidos IP en Cloud Manager, vaya a [Introducción a las Listas de permitidos IP en Podría Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Siga los pasos a continuación para aplicar una Lista de permitidos IP:

1. Vaya al entorno específico desde la página de detalles **Entornos** y vaya a la tabla **Listas de permitidos IP**.
1. Utilice los campos de entrada en la parte superior de la tabla de Lista de permitidos IP para seleccionar la Lista de permitidos IP y el servicio de creación o publicación al que desee aplicarla.
1. Haga clic en **Aplicar** y confirme su envío.

### Anulación de la aplicación de una Lista de permitidos IP {#unapply-ip-allow-list}

La anulación de la aplicación de una Lista de permitidos IP es el proceso mediante el cual todos los intervalos de IP incluidos en la definición de la Lista de permitidos se desasocian de un servicio de autor o editor en un entorno. Un usuario con la función Propietario de la empresa o Administrador de implementación debe iniciar sesión para poder anular la aplicación de una Lista de permitidos IP.

Siga los pasos a continuación para anular la aplicación de una Lista de permitidos IP:

1. Vaya a la página de detalles **Entornos** específica desde la pantalla Entornos y vaya a la tabla **Listas de permitidos IP**.
1. Identifique la fila en la que se muestra la regla de Lista de permitidos IP que desea anular de la aplicación.
1. Seleccione **...** desde el extremo derecho de la fila.
1. Seleccione la opción **No aplicar** y confirme el envío.


