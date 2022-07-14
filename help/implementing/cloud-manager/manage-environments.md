---
title: Administración de entornos
description: Obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 2%

---

# Administración de entornos {#managing-environments}

Obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager.

## Tipos de entorno {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entorno (dentro de los límites de lo que está disponible para el inquilino específico).

* **Producción y fase** - Los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente.

* **Desarrollo** - Se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se puede asociar con tuberías que no sean de producción.


Las capacidades de los entornos individuales dependen de las soluciones habilitadas en la variable [programa.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/home.md)

>[!NOTE]
>
>Los entornos de producción y ensayo solo se crean como un par. No puede crear solo un entorno de ensayo o de producción.

## Adición de un entorno {#adding-environments}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea agregar un entorno.

1. En el **Información general del programa** página, haga clic en **Agregar entorno** en el **Entornos** para agregar un entorno.

   ![Tarjeta de entorno](assets/no-environments.png)

   * La variable **Agregar entorno** también está disponible en la **Entornos** pestaña .

      ![Pestaña Entornos](assets/environments-tab.png)

   * La variable **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el **Agregar entorno** que aparece:

   * Seleccione un **Tipo de entorno**.
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del tipo de entorno de desarrollo .
   * Proporcione un **Nombre del entorno**.
   * Proporcione un **Descripción del entorno**.
   * Seleccione un **Región de nube**.

   ![Agregar cuadro de diálogo de entorno](assets/add-environment2.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

La variable **Información general** ahora muestra el nuevo entorno en la **Entornos** tarjeta. Ahora puede configurar canalizaciones para su nuevo entorno.

## Detalles del entorno {#viewing-environment}

Puede usar la variable **Entornos** en la página de información general para acceder a los detalles de un entorno de dos formas.

1. En el **Información general** , haga clic en el botón **Entornos** en la parte superior de la pantalla.

   ![Pestaña Entornos](assets/environments-tab2.png)

   * También puede hacer clic en el botón **Mostrar todo** en el **Entornos** para saltar directamente a la **Entornos** pestaña .

      ![Mostrar todas las opciones](assets/environment-showall.png)

1. La variable **Entornos** abre y enumera todos los entornos del programa.

   ![La pestaña entornos](assets/environment-view-2.png)

1. Haga clic en un entorno de la lista para mostrar sus detalles.

   ![Detalles del entorno](assets/environ-preview1.png)

También puede hacer clic en el botón de puntos suspensivos del entorno que desee y seleccionar **Ver detalles**.

![Ver detalles del entorno](assets/view-environment-details.png)

>[!NOTE]
>
>La variable **Entornos** solo contiene tres entornos. Haga clic en el **Mostrar todo** como se describió anteriormente para ver todos los entornos del programa.

### Acceso al servicio de vista previa {#access-preview-service}

Cloud Manager proporciona un servicio de vista previa (entregado como servicio de publicación adicional) a cada entorno as a Cloud Service AEM.

Con el servicio puede obtener una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación real y que esté disponible públicamente.

Una vez creado, el servicio de vista previa tendrá aplicada una lista de permitidos IP predeterminada, etiquetada `Preview Default [<envId>]`, que bloquea todo el tráfico en el servicio de vista previa. Debe anular la aplicación de la lista de permitidos IP predeterminada del servicio de vista previa para habilitar el acceso.

![Vista previa del servicio y su lista de permitidos](assets/preview-ip-allow.png)

Un usuario con los permisos necesarios debe completar los pasos de las siguientes opciones antes de compartir la URL del servicio de vista previa con cualquiera de sus equipos para garantizar el acceso a la URL de vista previa.

1. Cree una lista de permitidos IP adecuada, aplíquela al servicio de vista previa y cancele inmediatamente la aplicación de `Preview Default [<envId>]` lista de permitidos.

   * Consulte el documento [Aplicación y cancelación de la aplicación de Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) para obtener más información.

1. Usar la actualización **LISTA DE PERMITIDOS IP** flujo de trabajo para eliminar la IP predeterminada y agregar direcciones IP según corresponda. Consulte [Administración de Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) para obtener más información.

Una vez desbloqueado el acceso al servicio de vista previa, ya no se mostrará el icono de bloqueo antes del nombre del servicio de vista previa.

Una vez activado, puede publicar contenido en el servicio de vista previa utilizando la IU Administrar publicación dentro de AEM. Consulte el documento [Vista previa del contenido](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obtener más información.

>[!NOTE]
>
>El entorno debe estar en AEM versión `2021.05.5368.20210529T101701Z` o posterior. Asegúrese de que una canalización de actualización se haya ejecutado correctamente en su entorno para hacerlo.

## Actualización de entornos {#updating-dev-environment}

Como servicio nativo de la nube, las actualizaciones de los entornos de ensayo y producción dentro de los programas de producción se administran automáticamente mediante Adobe.

Sin embargo, las actualizaciones de los entornos de desarrollo, así como de los entornos de los programas de entornos limitados, se administran dentro de los programas. Cuando un entorno de este tipo no ejecuta la última versión de AEM disponible públicamente, el estado de la variable **Entornos** en el **Información general** pantalla del programa se mostrará **Actualización disponible**.

![Estado de actualización del entorno](assets/environ-update.png)

### Actualizaciones y canalizaciones {#updates-pipelines}

Los gasoductos son la única manera de [implementar código en los entornos de AEM as a Cloud Service.](deploy-code.md) Por este motivo, cada canalización está asociada a una versión AEM particular.

Si Cloud Manager detecta que hay una versión de AEM disponible más reciente que la implementada por última vez con la canalización, muestra la variable **Actualización disponible** para el entorno.

Por lo tanto, el proceso de actualización es de dos pasos:

1. Actualización de la canalización con la última versión AEM
1. Ejecución de la canalización para implementar la nueva versión de AEM en un entorno

### Actualización de entornos {#updating-your-environments}

La variable **Actualizar** está disponible en la **Entornos** para entornos de desarrollo en programas de entorno limitado haciendo clic en el botón elipsis del entorno.

![Opción Actualizar de la tarjeta Entornos](assets/environ-update2.png)

Esta opción también está disponible haciendo clic en la **Entornos** del programa y, a continuación, seleccione el botón de elipsis del entorno.

![Opción Actualizar de la pestaña Entornos](assets/environ-update3.png)

Un usuario con la variable **Administrador de implementación** puede utilizar esta opción para actualizar la canalización asociada con este entorno a la última versión de AEM.

Una vez que la versión de la canalización se actualiza a la última versión de AEM disponible públicamente, se solicita al usuario que ejecute la canalización asociada para implementar la última versión en el entorno.

![Solicitar la ejecución de la canalización para actualizar el entorno](assets/update-run-pipeline.png)

La variable **Actualizar** el comportamiento de la opción varía según la configuración y el estado actual del programa.

* Si la canalización ya se ha actualizado, la variable **Actualizar** solicita al usuario que ejecute la canalización.
* Si la canalización ya se está actualizando, la variable **Actualizar** informa al usuario de que ya se está ejecutando una actualización.
* Si no existe una canalización adecuada, la variable **Actualizar** solicita al usuario que cree una.

## Eliminación de entornos de desarrollo {#deleting-environment}

Los usuarios con los permisos necesarios podrán eliminar un entorno de desarrollo.

En el **Información general** del programa en la **Entornos** , haga clic en el botón elipsis del entorno de desarrollo que desee eliminar.

![La opción eliminar](assets/environ-delete.png)

La opción Eliminar también está disponible en la **Entornos** de la pestaña **Información general** del programa. Haga clic en el botón de elipsis del entorno y seleccione **Eliminar**.

![La opción Eliminar de la ficha Entornos](assets/environ-delete2.png)

>[!NOTE]
>
>* Los entornos de producción y ensayo creados en un programa de producción no se pueden eliminar.
>* Se pueden eliminar los entornos de producción y ensayo de un programa de simulación de pruebas.


## Administración del acceso {#managing-access}

Select **Administrar acceso** del menú elipsis del entorno en la **Entornos** tarjeta. Puede navegar a la instancia de autor directamente y administrar el acceso para su entorno.

![Opción Administrar acceso](assets/environ-access.png)

## Acceso a Developer Console {#accessing-developer-console}

Select **Developer Console** del menú elipsis del entorno en la **Entornos** tarjeta. Se abrirá una nueva pestaña en el explorador con la página de inicio de sesión en el **Developer Console**.

![](assets/environ-devconsole.png)

Solo un usuario con la variable **Desarrollador** tendrá acceso a la función **Developer Console**. Sin embargo, para los programas de simulación de pruebas, cualquier usuario con acceso al programa de simulación de pruebas tendrá acceso a **Developer Console**.

Consulte el documento [Entornos de espacio aislado en hibernación y dehibernación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) para obtener más información.

Esta opción también está disponible en el **Entorno** de la pestaña **Información general** al hacer clic en el menú elipsis de un entorno individual.

## Iniciar sesión localmente {#login-locally}

Select **Inicio de sesión local** del menú elipsis del entorno en la **Entornos** para iniciar sesión localmente en Adobe Experience Manager.

![Iniciar sesión localmente](assets/environ-login-locally.png)

Además, puede iniciar sesión localmente desde el **Entornos** de la pestaña **Información general** página.

![Iniciar sesión localmente desde la pestaña Entornos](assets/environ-login-locally-2.png)

## Administración de nombres de dominio personalizados {#manage-cdn}

Los nombres de dominio personalizados se admiten en los programas de Cloud Manager para sitios tanto para los servicios de publicación como de vista previa. Cada entorno de Cloud Manager puede alojar hasta un máximo de 250 dominios personalizados.

Para configurar los nombres de dominio personalizados, vaya a la **Entornos** y haga clic en un entorno para ver los detalles del entorno.

![Detalles del entorno](assets/domain-names.png)

Se pueden realizar las siguientes acciones en el servicio de publicación de su entorno.

* [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn).

* [Administración de listas de permitidos de IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## Administración de listas de permitidos de IP {#manage-ip-allow-lists}

Las listas de permitidos IP son compatibles con Cloud Manager para los servicios de creación, publicación y vista previa de los programas de Sites.

Para administrar las listas de permitidos IP, vaya a la **Entornos** de la pestaña **Información general** del programa. Haga clic en un entorno individual para administrar sus detalles.

### Aplicación de una lista de permitidos de IP {#apply-ip-allow-list}

La aplicación de una lista de permitidos IP asocia todos los rangos de IP incluidos en la definición de la lista de permitidos con un servicio de autor o publicación en un entorno. Un usuario en la variable **Propietario empresarial** o **Administrador de implementación** para poder aplicar una lista de permitidos IP, debe iniciar sesión en .

La lista de permitidos IP debe existir en Cloud Manager para aplicarla a un entorno. Para obtener más información sobre las listas de permitidos IP en Cloud Manager, consulte el documento[Introducción a las Listas de permitidos IP en Cloud Manager.](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)

Siga estos pasos para aplicar una lista de permitidos IP.

1. Vaya al entorno específico desde la **Entornos** pestaña del programa **Información general** y vaya a **LISTAS DE PERMITIDOS IP** tabla.
1. Utilice los campos de entrada de la parte superior de la tabla de lista de permitidos IP para seleccionar la lista de permitidos IP y el servicio de autor o publicación al que desee aplicarla.
1. Haga clic en **Aplicar** y confirme su envío.

### Cancelación de la aplicación de una Lista de permitidos IP {#unapply-ip-allow-list}

Al anular la aplicación de una lista de permitidos IP, se desasocian todos los rangos de IP incluidos en la definición de la lista de permitidos de un servicio de autor o editor de un entorno. Un usuario en la variable **Propietario empresarial** o **Administrador de implementación** debe haber iniciado sesión en para poder anular la aplicación de una lista de permitidos IP.

Siga estos pasos para anular la aplicación de una lista de permitidos IP.

1. Vaya al entorno específico desde la **Entornos** pestaña del programa **Información general** y vaya a **LISTAS DE PERMITIDOS IP** tabla.
1. Identifique la fila en la que se muestra la regla de lista de permitidos IP que desea anular la aplicación.
1. Seleccione el botón de puntos suspensivos al final de la fila.
1. Select **No aplicar** y confirme su envío.
