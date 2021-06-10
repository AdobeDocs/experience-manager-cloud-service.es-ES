---
title: 'Administrar entornos: Cloud Service'
description: 'Administrar entornos: Cloud Service'
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 11d12e43de7a71a59f565379e95ba57b13180fed
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 3%

---

# Administración de entornos {#manage-environments}

En la siguiente sección se describen los tipos de entorno que un usuario puede crear y cómo puede hacerlo.

## Tipos de entorno {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entorno (dentro de los límites de lo que está disponible para el inquilino específico).

* **Entorno** de producción y fase: Producción y fase está disponible como dúo y se utiliza para pruebas y producciones.

* **Desarrollo**: Se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se asociará con canalizaciones que no sean de producción.

   >[!NOTE]
   >Se configurará un entorno de desarrollo creado automáticamente en un programa de espacio aislado para pruebas para que incluya las soluciones de Sites y Assets.

   La tabla siguiente resume los tipos de entorno y sus atributos:

   | Nombre | Nivel de Author | Nivel de publicación | El usuario puede crear | El usuario puede eliminar | Canalización que puede asociarse con el entorno |
   |--- |--- |--- |--- |---|---|
   | Producción | Sí | Sí si se incluyen sitios | Sí | No | Canalización de producción |
   | Escenario | Sí | Sí si se incluyen sitios | Sí | No | Canalización de producción |
   | Desarrollo | Sí | Sí si se incluyen sitios | Sí | Sí | Canalización que no es de producción |

   >[!NOTE]
   >Producción y fase está disponible como dúo y se utiliza para pruebas y producciones.  El usuario no podrá crear solo entorno de fase o de producción.

## Adición de entorno {#adding-environments}

1. Haga clic en **Agregar entorno** para agregar un entorno. Se puede acceder a este botón desde la pantalla **Environments**.
   ![](assets/environments-tab.png)

   La opción **Agregar entorno** también está disponible en la tarjeta **Entornos** cuando no hay ningún entorno en el programa.

   ![](assets/no-environments.png)

   >[!NOTE]
   >La opción **Agregar entorno** se deshabilitará por falta de permisos o por lo que se pueda contratar.

1. Aparece el cuadro de diálogo **Agregar entorno**. El usuario debe enviar detalles como **Tipo de entorno**, **Nombre de entorno** y **Descripción de entorno** (según el objetivo del usuario al crear el entorno dentro de los límites de lo que está disponible para el inquilino específico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Al crear un entorno, se crean una o más *integraciones* en Adobe I/O. Son visibles para los usuarios clientes que tienen acceso a la consola de Adobe I/O y no deben eliminarse. Esto se rechaza en la descripción de la Consola de Adobe I/O.

   ![](assets/add-environment-image1.png)

1. Haga clic en **Guardar** para agregar un entorno con los criterios rellenados.  Ahora, la pantalla *Información general* muestra la tarjeta desde la que puede configurar la canalización.

   >[!NOTE]
   >En caso de que aún no haya configurado la canalización que no es de producción, la pantalla *Overview* muestra la tarjeta desde la que puede crear la canalización que no es de producción.

## Detalles del entorno {#viewing-environment}

La tarjeta **Environments** de la página Información general enumera hasta tres entornos.

1. Seleccione el botón **Show All** para navegar a la página de resumen **Environment** para ver una tabla con una lista completa de entornos.

   ![](assets/environment-view-1.png)

1. La página **Entornos** muestra la lista de todos los entornos existentes.

   ![](assets/environment-view-2.png)

1. Seleccione cualquiera de los entornos de la lista para ver los detalles del entorno.

   >[!NOTE]
   >El servicio de vista previa se implementará progresivamente en todos los programas. Se notificará al producto a los clientes cuando su programa esté habilitado para el servicio de vista previa. Consulte la sección [Acceso al servicio de vista previa](#access-preview-service) para obtener más información.

   ![](assets/environ-preview1.png)


### Acceso al servicio de vista previa {#access-preview-service}

La función de servicio de vista previa ofrece un servicio de vista previa (publicación) adicional a cada AEM como entorno de Cloud Service a través de Cloud Manager.

Obtenga una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente. Antes de poder ver y utilizar el servicio de vista previa, puede utilizar algunos punteros:

1. **AEM versión**: El entorno debe estar en AEM versión  `2021.5.5343.20210542T070738Z` o superior. Asegúrese de que una canalización de actualización se haya ejecutado correctamente en su entorno para lograr esto.

1. **Bloqueo** de Lista de permitidos IP predeterminado: Una vez creado, el servicio de vista previa tendrá una Lista de permitidos IP predeterminada aplicada, etiquetada  `Preview Default [Env ID]`.

   >[!NOTE]
   >Al crearla por primera vez, debe anular la aplicación de la Lista de permitidos IP predeterminada del servicio de vista previa en su entorno para habilitar el acceso.

   Un usuario con los permisos necesarios debe realizar una de las siguientes acciones para *desbloquear* el acceso al servicio de vista previa y proporcionar el acceso deseado:

   * Cree una Lista de permitidos IP adecuada y aplíquela al servicio de vista previa. Siga esto inmediatamente anulando la aplicación `Preview Default [Env ID] IP Allow List` del servicio de vista previa. Consulte [Cancelar la aplicación de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/unapply-ip-allow-list.md) para obtener más información.

      *O*,

   * Utilice el flujo de trabajo de actualización de la Lista de permitidos IP para eliminar la IP predeterminada y agregar las IP según corresponda. Consulte [Visualización y actualización de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md) para obtener más información.

      >[!NOTE]
      >Los pasos anteriores deben realizarse antes de compartir la URL del servicio de vista previa con cualquiera de sus equipos para garantizar que los miembros adecuados de su equipo puedan acceder a la URL de vista previa.

      Una vez desbloqueado el acceso al servicio de vista previa, ya no se mostrará el icono de bloqueo (como se muestra en la figura siguiente).

      ![](/help/implementing/cloud-manager/assets/preview-service1.png)

1. **Publicar contenido para vista previa**: Puede publicar contenido en el servicio de vista previa utilizando la interfaz de usuario Administrar publicación dentro de AEM. Consulte [Vista previa del contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/fundamentals/previewing-content.html?lang=en) para obtener más información.

## Actualización del entorno {#updating-dev-environment}

Las actualizaciones de los entornos de fase y producción se administran automáticamente mediante Adobe.

Los usuarios del programa administran las actualizaciones de los entornos de desarrollo. Cuando un entorno no ejecuta la última versión de AEM disponible públicamente, el estado de la tarjeta de entornos en la pantalla principal mostrará **ACTUALIZACIÓN DISPONIBLE**.

![](assets/environ-update.png)


La opción **Update** está disponible en la tarjeta **Environments**.
Esta opción también está disponible si hace clic en **Details** en la tarjeta **Environments**. Se abre la página **Entornos** y una vez que seleccione el entorno de desarrollo, haga clic en **...** y seleccione **Actualizar**, como se muestra en la figura siguiente:

![](assets/environ-update2.png)

Al seleccionar esta opción, un administrador de implementación podrá actualizar la canalización asociada con este entorno a la última versión y luego ejecutar la canalización.

Si la canalización ya se ha actualizado, se solicita al usuario que la ejecute.

## Eliminación del entorno {#deleting-environment}

Los usuarios con los permisos necesarios podrán eliminar un entorno de desarrollo.

La opción **Eliminar** está disponible en el menú desplegable de la tarjeta **Entornos**. Haga clic en **...** para un entorno de desarrollo que desee eliminar.

![](assets/environ-delete.png)

La opción Eliminar también está disponible si hace clic en **Details** en la tarjeta **Environments**. Se abre la página **Entornos** y una vez que seleccione el entorno de desarrollo, haga clic en **...** y seleccione **Eliminar**, como se muestra en la figura siguiente:

![](assets/environ-delete2.png)


>[!NOTE]
>Esta función no está disponible para entornos de producción/fase establecidos en un programa de producción configurado para fines de producción. Sin embargo, la función está disponible para entornos de producción/fase en un programa de espacio aislado.

## Administración del acceso {#managing-access}

Seleccione **Administrar acceso** en el menú desplegable de la tarjeta **Entornos**. Puede navegar a la instancia de autor directamente y administrar el acceso para su entorno.

Consulte [Administración del acceso a la instancia de autor](/help/onboarding/what-is-required/accessing-aem-instance.md) para obtener más información.

![](assets/environ-access.png)


## Acceso a Developer Console {#accessing-developer-console}

Seleccione **Developer Console** en el menú desplegable de la tarjeta **Environments**. Se abrirá una nueva pestaña en el explorador con la página de inicio de sesión en **Developer Console**.

Solo los usuarios con la función de desarrollador tendrán acceso a **Developer Console**. La excepción es para los Programas de espacio aislado, donde cualquier usuario con acceso al programa de espacio aislado de Cloud Manager tendrá acceso a **Developer Console**.

Consulte [Entorno de espacio aislado en hibernación y dehibernación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obtener más información.


![](assets/environ-devconsole.png)

Esta opción también está disponible si hace clic en **Details** en la tarjeta **Environments**. La página **Entornos** se abre y una vez que seleccione un entorno, haga clic en **...** y seleccione **Developer Console**.

## Iniciar sesión localmente {#login-locally}

Seleccione **Inicio de sesión local** en el menú desplegable de la tarjeta **Entornos** para iniciar sesión localmente en Adobe Experience Manager.

![](assets/environ-login-locally.png)

Además, puede iniciar sesión localmente desde la página de resumen **Environments**.

![](assets/environ-login-locally-2.png)


## Administración de nombres de dominio personalizados {#manage-cdn}

Vaya a la página de detalles **Entornos** en la página Resumen de Entornos.

>[!NOTE]
>Los nombres de dominio personalizados ahora se admiten en los programas de Cloud Manager para sitios tanto para los servicios de publicación como de vista previa. Cada entorno de Cloud Manager puede alojar hasta un máximo de 250 dominios personalizados por entorno.

Se pueden realizar las siguientes acciones en el servicio Publicar para su entorno, como se describe a continuación:

1. [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Visualización y actualización de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [Comprobación del estado del nombre de dominio personalizado ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o de un certificado  [SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn).

1. [Comprobación del estado de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)


## Administración de Listas de permitidos IP {#manage-ip-allow-lists}

Vaya a la página Detalles del entorno desde la página Resumen de entornos . Aquí puede realizar las siguientes acciones en los servicios Publicar o Autor para su entorno.

>[!NOTE]
>La función de Lista de permitidos IP ahora es compatible con Cloud Manager para servicios de autor, publicación y vista previa (disponible en programas de Sites).

### Aplicación de una Lista de permitidos IP {#apply-ip-allow-list}

La aplicación de una Lista de permitidos IP es el proceso mediante el cual todos los rangos de IP incluidos en la definición de la lista de permitidos están asociados a un servicio de Autor o Publicación en un entorno. Un usuario con la función Propietario empresarial o Administrador de implementación debe haber iniciado sesión para poder aplicar una Lista de permitidos IP.

>[!NOTE]
>La Lista de permitidos IP debe existir en Cloud Manager para aplicarla a un servicio de entorno. Para obtener más información sobre las Listas de permitidos IP en Cloud Manager, vaya a [Introducción a las Listas de permitidos IP en Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Siga los pasos a continuación para aplicar una Lista de permitidos IP:

1. Vaya al entorno específico desde la página de detalles **Environments** y vaya a la tabla **IP Lista de permitidos** .
1. Utilice los campos de entrada de la parte superior de la tabla de Lista de permitidos IP para seleccionar la Lista de permitidos IP y el servicio Autor o Publicación al que desea aplicarla.
1. Haga clic en **Aplicar** y confirme el envío.

### Desaplicación de una Lista de permitidos IP {#unapply-ip-allow-list}

La cancelación de la aplicación de una Lista de permitidos IP es el proceso mediante el cual todos los rangos de IP incluidos en la definición de la Lista de permitidos se desasocian de un servicio Autor o Editor en un entorno. Un usuario con la función Propietario empresarial o Administrador de implementación debe haber iniciado sesión para poder anular la aplicación de una Lista de permitidos IP.

Siga los pasos a continuación para anular la aplicación de una Lista de permitidos IP:

1. Vaya a la página de detalles **Environments** específica desde la pantalla Environments y vaya a la tabla **IP Lista de permitidos** .
1. Identifique la fila en la que se muestra la regla de Lista de permitidos IP que desea anular la aplicación.
1. Seleccione el **...** desde el extremo derecho de la fila.
1. Seleccione la opción **Unapply** y confirme el envío.
