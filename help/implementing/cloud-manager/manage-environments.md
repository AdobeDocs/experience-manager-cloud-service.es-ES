---
title: Administración de entornos
description: Obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 4631ab86ae1b4405e31d8bb8eae8edbbe2272c2c
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 100%

---

# Administración de entornos {#managing-environments}

Obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager.

## Tipos de entornos {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entornos (dentro de los límites de lo que está disponible para el inquilino específico).

* **Producción + Fase**: los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente.

* **Desarrollo**: se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se puede asociar con canalizaciones que no sean de producción.

* **Desarrollo rápido**: Un entorno de desarrollo rápido (RDE) permite al desarrollador implementar y revisar cambios rápidamente, minimizando la cantidad de tiempo necesario para probar funciones que han demostrado funcionar en un entorno de desarrollo local. Consulte [la documentación del entorno de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) para obtener detalles acerca de cómo utilizar un RDE.

Las funcionalidades de los entornos individuales dependen de las soluciones habilitadas en el [programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) del entorno.

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Los entornos de producción y ensayo solo se crean como un par. No puede crear solo un entorno de ensayo o de producción.

## Agregar un entorno {#adding-environments}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea agregar un entorno.

1. En la página **Información general del programa**, haga clic en **Agregar entorno** en la tarjeta **Entornos** para agregar un entorno.

   ![Tarjeta Entornos](assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la pestaña **Entornos**.

      ![Pestaña Entornos](assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Agregar entorno** que aparece:

   * Seleccione un [**tipo de entorno**.](#environment-types)
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del nombre de tipo de entorno.
   * Proporcione un **Nombre** del entorno.
   * Proporcione una **Descripción** del entorno.
   * Seleccione una **Región principal** de la lista desplegable.
      * Tenga en cuenta que esto no se puede cambiar después de la creación.
   * Si va a agregar un entorno de **Producción + Fase**, debe proporcionar un nombre de entorno y una descripción para los entornos de producción y ensayo.
      ![Cuadro de diálogo Agregar entorno](assets/add-environment2.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

La pantalla **Información general** ahora muestra el nuevo entorno en la tarjeta **Entornos**. Ahora puede configurar canalizaciones para su nuevo entorno.

## Detalles del entorno {#viewing-environment}

Puede usar la tarjeta **Entornos** en la página de información general para acceder a los detalles de un entorno de dos formas.

1. En la página **Información general**, haga clic en la pestaña **Entornos** en la parte superior de la pantalla.

   ![Pestaña Entornos](assets/environments-tab2.png)

   * También puede hacer clic en el botón **Mostrar todo** en la tarjeta **Entornos** para saltar directamente a la pestaña **Entornos**.

      ![Mostrar todas las opciones](assets/environment-showall.png)

1. Los **Entornos** se abrirán y enumerarán todos los entornos del programa.

   ![La pestaña de entornos](assets/environment-view-2.png)

1. Haga clic en un entorno de la lista para mostrar sus detalles.

   ![Detalles del entorno](assets/environ-preview1.png)

También puede hacer clic en el botón de los tres puntos del entorno que desee y seleccionar **Ver detalles**.

![Ver detalles del entorno](assets/view-environment-details.png)

>[!NOTE]
>
>La tarjeta **Entornos** solo enumera tres entornos. Haga clic en el botón **Mostrar todo** como se describió anteriormente para ver todos los entornos del programa.

### Acceso al servicio Vista previa {#access-preview-service}

Cloud Manager proporciona un servicio de vista previa (entregado como servicio de publicación adicional) para cada entorno de AEM as a Cloud Service.

Con el servicio puede obtener una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación real y de que esté disponible públicamente.

Una vez creado, el servicio de vista previa tendrá aplicada una lista de IP predeterminadas permitidas, etiquetada como `Preview Default [<envId>]`, que bloqueará todo el tráfico en el servicio de vista previa. Debe anular la aplicación de la lista de IP predeterminadas permitidas del servicio de vista previa para habilitar el acceso.

![Servicio de vista previa y lista de permitidos](assets/preview-ip-allow.png)

Un usuario con los permisos necesarios debe completar los siguientes pasos antes de compartir la URL del servicio de vista previa para garantizar el acceso a él.

1. Cree una lista de IP permitidas adecuada, aplíquela al servicio de vista previa y cancele inmediatamente la aplicación de la lista de permitidos `Preview Default [<envId>]`.

   * Consulte el documento [Aplicar y cancelar la aplicación de listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) para obtener más información.

1. Use la actualización del flujo de trabajo **Lista de IP permitidas** para eliminar la IP predeterminada y agregar direcciones IP según corresponda. Consulte [Administrar listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) para obtener más información.

Una vez desbloqueado el acceso al servicio de vista previa, ya no se mostrará el icono de bloqueo antes del nombre del servicio de vista previa.

Una vez activado, puede publicar contenido en el servicio de vista previa mediante la IU Administrar publicación dentro de AEM. Consulte el documento [Vista previa del contenido](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obtener más información.

>[!NOTE]
>
>Su entorno debe estar en la versión `2021.05.5368.20210529T101701Z` de AEM o más reciente para utilizar el servicio de vista previa. Asegúrese de que una canalización de actualización se haya ejecutado correctamente en su entorno para hacerlo.

## Actualizar entornos {#updating-dev-environment}

Como servicio nativo de la nube, las actualizaciones de los entornos de ensayo y producción dentro de los programas de producción se administran automáticamente mediante Adobe.

Sin embargo, las actualizaciones de los entornos de desarrollo, así como de los entornos de los programas de zonas protegidas, se administran dentro de los programas. Cuando un entorno de este tipo no ejecuta la última versión de AEM disponible públicamente, el estado de la tarjeta **Entornos** en la pantalla **Información general** del programa se mostrará **Actualización disponible**.

![Estado de actualización del entorno](assets/environ-update.png)

### Actualizaciones y canalizaciones {#updates-pipelines}

Las canalizaciones son la única manera de [implementar código en los entornos de AEM as a Cloud Service.](deploy-code.md) Por este motivo, cada canalización está asociada a una versión de AEM particular.

Si Cloud Manager detecta que hay una versión de AEM disponible más reciente que la implementada por última vez con la canalización, mostrará el estado **Actualización disponible** para el entorno.

Por lo tanto, el proceso de actualización consta de dos pasos:

1. Actualización de la canalización con la última versión AEM
1. Ejecución de la canalización para implementar la nueva versión de AEM en un entorno

### Actualizar entornos {#updating-your-environments}

La opción **Actualizar** está disponible en la tarjeta **Entornos** para entornos de desarrollo en programas de zona protegida al hacer clic en el botón de los tres puntos del entorno.

![Opción Actualizar de la tarjeta Entornos](assets/environ-update2.png)

Esta opción también está disponible si hace clic en la pestaña **Entornos** del programa y, a continuación, selecciona el botón de los tres puntos del entorno.

![Opción Actualizar de la pestaña Entornos](assets/environ-update3.png)

Un usuario con el rol de **Administrador de implementación** puede utilizar esta opción para actualizar la canalización asociada con este entorno a la última versión de AEM.

Una vez que la versión de la canalización se actualice a la última versión de AEM disponible públicamente, se solicitará al usuario que ejecute la canalización asociada para implementar la última versión en el entorno.

![Solicitud para ejecutar la canalización para actualizar el entorno](assets/update-run-pipeline.png)

El comportamiento de la opción **Actualizar** varía según la configuración y el estado actual del programa.

* Si la canalización ya se ha actualizado, la opción **Actualizar** solicitará al usuario que ejecute la canalización.
* Si la canalización ya se está actualizando, la opción **Actualizar** informará al usuario de que ya se está ejecutando una actualización.
* Si no existe una canalización adecuada, la opción **Actualizar** solicitará al usuario que cree una.

## Eliminar entornos de desarrollo {#deleting-environment}

Los usuarios con los permisos necesarios podrán eliminar un entorno de desarrollo.

En la pantalla **Información general** del programa, en la tarjeta **Entornos**, haga clic en el botón de los tres puntos del entorno de desarrollo que desee eliminar.

![La opción Eliminar](assets/environ-delete.png)

La opción Eliminar también está disponible en la pestaña **Entornos** de la ventana **Información general** del programa. Haga clic en el botón de los tres puntos del entorno y seleccione **Eliminar**.

![La opción Eliminar de la pestaña Entornos](assets/environ-delete2.png)

>[!NOTE]
>
>* Los entornos de producción y ensayo creados en un programa de producción no se pueden eliminar.
>* Se pueden eliminar los entornos de producción y ensayo de un programa de zona protegida.


## Administrar el acceso {#managing-access}

Seleccione **Administrar el acceso** del menú de los tres puntos del entorno en la tarjeta **Entornos**. Puede navegar hasta la instancia de autor directamente y administrar el acceso para su entorno.

![Opción Administrar el acceso](assets/environ-access.png)

## Acceder a la consola de desarrollador {#accessing-developer-console}

Seleccione **Consola de desarrollador** del menú de los tres puntos del entorno en la tarjeta **Entornos**. Se abrirá una nueva pestaña en el explorador con la página de inicio de sesión en la **Consola de desarrollador**.

![](assets/environ-devconsole.png)

Solo un usuario con el rol de **Desarrollador** tendrá acceso a la **Consola de desarrollador**. Sin embargo, para los programas de zonas protegidas, cualquier usuario con acceso a la zona protegida tendrá acceso a la **Consola de desarrollador**.

Consulte el documento [Entornos de zona protegida en hibernación y dehibernación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html?lang=es#hibernating-introduction) para obtener más información.

Esta opción también está disponible en la pestaña **Entorno** de la ventana **Información general** al hacer clic en el menú de los tres puntos de un entorno individual.

## Iniciar sesión localmente {#login-locally}

Seleccione **Iniciar sesión localmente** del menú de los tres puntos del entorno en la tarjeta **Entornos** para iniciar sesión localmente en Adobe Experience Manager.

![Iniciar sesión localmente](assets/environ-login-locally.png)

Además, puede iniciar sesión localmente desde la pestaña **Entornos** de la página **Información general**.

![Iniciar sesión localmente desde la pestaña Entornos](assets/environ-login-locally-2.png)

## Administrar los nombres de dominio personalizados {#manage-cdn}

Los nombres de dominio personalizados se admiten en los programas de Cloud Manager para los programas de Sites, tanto para los servicios de publicación como para los de vista previa. Cada entorno de Cloud Manager puede alojar hasta un máximo de 250 dominios personalizados.

Para configurar los nombres de dominio personalizados, navegue hasta la pestaña **Entornos** y haga clic en un entorno para ver los detalles del mismo.

![Detalles del entorno](assets/domain-names.png)

Se pueden realizar las siguientes acciones en el servicio de publicación de su entorno.

* [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Administrar los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o un [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Administrar listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Administrar listas de IP permitidas {#manage-ip-allow-lists}

Las listas de IP permitidas son compatibles con Cloud Manager para los servicios de creación, publicación y vista previa de los programas de Sites.

Para administrar las listas de IP permitidas, navegue hasta la pestaña **Entornos** de la página **Información general** del programa. Haga clic en un entorno individual para administrar sus detalles.

### Aplicar una lista de IP permitidas {#apply-ip-allow-list}

La aplicación de una lista de IP permitidas asocia todos los rangos de IP incluidos en la definición de la lista de permitidos con un servicio de autor o publicación en un entorno. Para que un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** pueda aplicar una lista de IP permitidas, deberá iniciar sesión.

La lista de IP permitidas debe existir en Cloud Manager para aplicarla a un entorno. Para obtener más información sobre las listas de IP permitidas en Cloud Manager, consulte el documento [Introducción a las listas de IP permitidas en Cloud Manager.](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

Siga estos pasos para aplicar una lista de IP permitidas.

1. Vaya al entorno específico desde la pestaña **Entornos** de la pantalla del programa **Información general** y navegue hasta la tabla **Listas de IP permitidas**.
1. Utilice los campos de entrada de la parte superior de la tabla de lista de IP permitidas para seleccionar la lista de IP permitidas y el servicio de autor o publicación al que desee aplicarla.
1. Haga clic en **Aplicar** y confirme su envío.

### Anular la aplicación de una lista de IP permitidas {#unapply-ip-allow-list}

Al anular la aplicación de una lista de IP permitidas, se desasocian todos los rangos de IP incluidos en la definición de la lista de permitidos de un servicio de autor o editor de un entorno. Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** debe haber iniciado sesión para poder anular la aplicación de una lista de IP permitidas.

Siga estos pasos para anular la aplicación de una lista de IP permitidas.

1. Vaya al entorno específico desde la pestaña **Entornos** de la pantalla del programa **Información general** y navegue hasta la tabla **Listas de IP permitidas**.
1. Identifique la fila en la que aparece la regla de la lista de IP permitidas que desea anular.
1. Seleccione el botón de los tres puntos del final de la fila.
1. Seleccione **No aplicar** y confirme su envío.
