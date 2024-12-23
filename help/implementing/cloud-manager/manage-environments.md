---
title: Administrar entornos
description: Obtenga información sobre los tipos de entornos que puede crear y cómo para su proyecto de Cloud Manager.
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '2357'
ht-degree: 62%

---


# Administrar entornos {#managing-environments}

Obtenga información sobre los tipos de entornos que puede crear y cómo para su proyecto de Cloud Manager.

## Tipos de entorno {#environment-types}

Un usuario con los permisos necesarios puede crear los siguientes tipos de entornos (dentro de los límites de lo que está disponible para el inquilino específico).

* **Producción + Fase**: los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente. Realizar pruebas de rendimiento y seguridad en el entorno de ensayo. Tiene el mismo tamaño que la producción.

* **Desarrollo**: se puede crear un entorno de desarrollo con fines de desarrollo y prueba, y solo se puede asociar con canalizaciones que no sean de producción.  Los entornos de desarrollo no tienen el mismo tamaño que los de fase y producción, y no deben utilizarse para realizar pruebas de rendimiento y seguridad.

* **Desarrollo rápido**: un entorno de desarrollo rápido (RDE) permite al desarrollador implementar y revisar cambios rápidamente, minimizando la cantidad de tiempo necesario para probar funciones que han demostrado su eficacia en un entorno de desarrollo local. Consulte [la documentación del entorno de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) para obtener detalles acerca de cómo utilizar un RDE.

Las funcionalidades de los entornos individuales dependen de las soluciones habilitadas en el [programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) del entorno.

* [Sites](/help/overview/introduction.md)
* [Assets](/help/assets/overview.md)
* [Forms](/help/forms/home.md)
* [Screens](/help/screens-cloud/introduction/introduction.md)

>[!NOTE]
>
>Los entornos de producción y ensayo solo se crean como un par. No puede crear solo un entorno de ensayo o de producción.

## Añadir un entorno {#adding-environments}

Para agregar o editar un entorno, un usuario debe ser miembro del rol **Propietario del negocio**.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en el programa para el que desea agregar un entorno.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en **Agregar entorno** en la tarjeta **Entornos** para agregar un entorno.

   ![Tarjeta Entornos](assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la ficha ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.

     ![Pestaña Entornos](assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Agregar entorno**:

   * Seleccione un [**tipo de entorno**](#environment-types).
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del nombre de tipo de entorno.
   * Proporcione un **Nombre** del entorno.
      * El nombre del entorno no se puede cambiar una vez creado el entorno.
   * Proporcione una **Descripción** del entorno.
   * Si va a agregar un entorno de **Producción + Fase**, debe proporcionar un nombre de entorno y una descripción tanto para los entornos de producción como de ensayo.
   * Seleccione una **Región principal** de la lista desplegable.
      * La región principal no se puede cambiar después de crearse.
      * En función de los derechos disponibles, puede configurar [varias regiones](#multiple-regions).

   ![Cuadro de diálogo Agregar entorno](assets/add-environment2.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

La pantalla **Información general** ahora muestra el nuevo entorno en la tarjeta **Entornos**. Ahora puede configurar canalizaciones para su nuevo entorno.

## Varias regiones de publicación {#multiple-regions}

Un usuario con la función de **Propietario de empresa** puede configurar entornos de producción y ensayo para incluir hasta tres regiones de publicación adicionales, además de la región principal. Las regiones de publicación adicionales pueden mejorar la disponibilidad. Consulte la [Documentación adicional de regiones de publicación](/help/operations/additional-publish-regions.md) para obtener más información.

>[!TIP]
>
>Puede usar el complemento [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/api-usage/creating-programs-and-environments/#creating-aem-cloud-service-environments) para consultar una lista actual de regiones disponibles.

### Agregar varias regiones de publicación a un entorno nuevo {#add-regions}

Al añadir un entorno nuevo, puede elegir configurar regiones adicionales además de la principal.

1. Seleccione la **Región principal**.
   * La región principal no se puede cambiar después de la creación del entorno.
1. Seleccione la opción **Agregar regiones de publicación adicionales** y aparecerá una nueva **lista desplegable de Regiones de publicación adicionales**. 
1. En el menú desplegable **Regiones de publicación adicionales**, seleccione una región adicional.
1. La región seleccionada se añade debajo del menú desplegable para indicar su selección.
   * Seleccione el(la) `X` que se encuentra junto a la región seleccionada para que pueda anular su selección.
1. Seleccione otra región en el menú desplegable **Regiones de publicación adicionales** para añadir otra región.
1. Seleccione **Guardar** cuando esté listo para crear su entorno.

![Selección de varias regiones](assets/select-multiple-regions.png)

Las regiones seleccionadas se aplican a los entornos de producción y ensayo.

Si no especifica ninguna región adicional, [puede hacerlo más tarde después de crear los entornos](#edit-regions).

Si desea proporcionar [redes avanzadas](/help/security/configuring-advanced-networking.md) para el programa, se recomienda hacerlo antes de añadir regiones de publicación adicionales a los entornos mediante la API de Cloud Manager. De lo contrario, el tráfico de las regiones de publicación adicionales pasará a través del proxy de la región principal.

### Editar varias regiones de publicación {#edit-regions}

Si no ha especificado ninguna región adicional inicialmente, puede hacerlo después de crear los entornos si tiene los derechos necesarios.

También puede quitar regiones de publicación adicionales. Sin embargo, solo puede añadir o eliminar regiones en una transacción. Si necesita añadir una región y quitar una región, primero añádala, guarde el cambio y, a continuación, quítela (o viceversa).

1. En la consola Información general del programa de su programa, haga clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg para su entorno de producción y seleccione **Editar** en el menú.

   ![Editar entorno](assets/select-edit-environment.png)

1. En el cuadro de diálogo **Editar entorno de producción**, realice los cambios necesarios en las regiones de publicación adicionales.
   * Utilice el menú desplegable **Regiones de publicación adicionales** para seleccionar regiones adicionales.
   * Haga clic en la X situada junto a las regiones de publicación adicionales seleccionadas para anular su selección.

   ![Editar entorno](assets/edit-environment.png)

1. Seleccione **Guardar** para guardar los cambios.

Los cambios realizados en el entorno de producción se aplican tanto a los entornos de producción como a los de ensayo. Los cambios en varias regiones de publicación solo se pueden editar en el entorno de producción.

Si desea proporcionar [redes avanzadas](/help/security/configuring-advanced-networking.md) para el programa, se recomienda hacerlo antes de añadir regiones de publicación adicionales a los entornos. De lo contrario, el tráfico de las regiones de publicación adicionales pasará a través del proxy de la región principal.

## Detalles del entorno {#viewing-environment}

Desde la página **Información general**, puede acceder a los detalles de un entorno de dos formas.

1. En la página **Información general**, haga clic en la ficha **Entornos** del menú de la izquierda.

   ![Pestaña Entornos](assets/environments-tab2.png)

   * También puede hacer clic en el botón **Mostrar todo** en la tarjeta **Entornos** para ir directamente a la pestaña **Entornos**.

     ![Mostrar todas las opciones](assets/environment-showall.png)

1. Los **Entornos** se abrirán y enumerarán todos los entornos del programa.

   ![La pestaña de entornos](assets/environments-tab2.png)

1. Haga clic en un entorno de la lista para mostrar sus detalles.

   ![Detalles del entorno](assets/environ-preview1.png)

También puede hacer clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg del entorno que desee y seleccionar **Ver detalles**.

![Ver detalles del entorno](assets/view-environment-details.png)

>[!NOTE]
>
>La tarjeta **Entornos** solo enumera tres entornos. Haga clic en el botón **Mostrar todo** como se describió anteriormente para ver todos los entornos del programa.

### Acceso al servicio de vista previa {#access-preview-service}

Cloud Manager proporciona un servicio de vista previa (ofrecido como un servicio de publicación adicional) para cada entorno de AEM as a Cloud Service.

Con el servicio puede obtener una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación real y de que esté disponible públicamente.

Una vez creado, al servicio de vista previa se le aplica la lista de IP permitidas predeterminadas, etiquetada como `Preview Default [<envId>]`, que bloquea todo el tráfico en el servicio de vista previa. Anule la aplicación de la lista de IP permitidas predeterminadas del servicio de vista previa para poder habilitar el acceso.

![Servicio de vista previa y lista de permitidos](assets/preview-ip-allow.png)

Un usuario con los permisos necesarios debe completar los siguientes pasos antes de compartir la URL del servicio de vista previa para garantizar el acceso a él.

1. Cree una lista de IP permitidas adecuada, aplíquela al servicio de vista previa y cancele inmediatamente la aplicación de la lista de `Preview Default [<envId>]` permitidas.

   * Consulte [aplicación y cancelación de la aplicación de listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) para obtener más información.

1. Use la actualización del flujo de trabajo **Lista de IP permitidas** para eliminar la IP predeterminada y agregar direcciones de IP según corresponda. Consulte [administración de listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md) para obtener más información.

Una vez desbloqueado el acceso al servicio de vista previa, ya no se mostrará el icono de bloqueo antes del nombre del servicio de vista previa.

Una vez activado, puede publicar contenido en el servicio de vista previa mediante la IU Administrar publicación dentro de AEM. Consulte la [vista previa del contenido](/help/sites-cloud/authoring/sites-console/previewing-content.md) para obtener más información.

>[!NOTE]
>
>Su entorno debe estar en la versión `2021.05.5368.20210529T101701Z` de AEM o más reciente para utilizar el servicio de vista previa. Asegúrese de que la canalización de actualización se haya ejecutado correctamente en su entorno para que pueda utilizar el servicio de vista previa.

### Estado de las regiones de publicación adicionales {#additional-region-status}

Si ha activado regiones de publicación adicionales, puede comprobar el estado de estas regiones desde la tarjeta **Entornos**.

1. En la página **Información general**, busque la tarjeta **Entornos**.

1. En la tarjeta **Entornos**, la columna **Estado** se reflejará si hay algún problema con las regiones de publicación adicionales configuradas. Haga clic en el icono **Información** para ver los detalles de las regiones.

   ![Información adicional del estado de las regiones de publicación en la tarjeta Entornos](assets/additional-publish-region-status-environments-card.png)

También puede obtener acceso a la misma información desde la ficha **Entornos**.

1. En la página **Información general**, seleccione la pestaña **Entornos**.

1. En la ficha **Entornos**, seleccione el entorno que desee consultar en el menú de la izquierda.

1. Una vez seleccionado un entorno:

   * La tabla **Información del entorno** mostrará qué regiones están configuradas para el entorno seleccionado.
   * La columna **Estado** de la tabla **Segmentos de entorno** reflejará si hay algún problema con las regiones de publicación adicionales configuradas. Pase el ratón sobre el estado para ver los detalles de cualquier problema.

   ![Información adicional del estado de las regiones de publicación en la ficha Entornos](assets/additional-publish-region-status-environments-tab.png)

Si hay algún problema con regiones de publicación adicionales:

1. Ten paciencia. Cloud Manager intenta continuamente recuperar la región y puede estar disponible en cualquier momento.
1. Si el problema persiste después de varias horas, puede quitar la región de publicación adicional y volver a agregarla (en la misma región u otra región) para almacenar en déclencheur una implementación completa.

El tiempo que espera a que el sistema se recupere por sí solo antes de realizar acciones adicionales depende del impacto que el fallo de esa región tenga en sus sistemas.

En cualquier caso, el tráfico de [siempre se redirige a la otra región más cercana que está en línea](/help/operations/additional-publish-regions.md). Si sigue teniendo problemas, póngase en contacto con el Servicio de atención al cliente de Adobe.

## Actualizar entornos {#updating-dev-environment}

Como servicio nativo de la nube, las actualizaciones de los entornos de desarrollo, ensayo y producción dentro de los programas de producción se administran automáticamente mediante el Adobe.

Sin embargo, las actualizaciones de los entornos de los programas de zonas protegidas se administran dentro de los programas. Cuando un entorno de este tipo no ejecuta la última versión de AEM disponible públicamente, el estado de la tarjeta **Entornos** en la pantalla **Información general** del programa muestra **Actualización disponible**.

![Estado de actualización del entorno](assets/environ-update.png)

### Actualizaciones y canalizaciones {#updates-pipelines}

Las canalizaciones son la única manera de [implementar código en los entornos de AEM as a Cloud Service](deploy-code.md). AEM Por este motivo, cada canalización está asociada a una versión en particular de la.

Si Cloud Manager detecta que hay una versión de AEM disponible más reciente que la implementada por última vez con la canalización, muestra el estado **Actualización disponible** para el entorno.

Por lo tanto, el proceso de actualización consta de dos pasos:

1. Actualización de la canalización con la última versión AEM
1. Ejecución de la canalización para implementar la nueva versión de AEM en un entorno

### Actualizar los entornos {#updating-your-environments}

>[!NOTE]
> A partir de 2024, las instancias de desarrollo y algunos programas de zonas protegidas ya se actualizan automáticamente, por lo que no es necesario administrar las actualizaciones para ellos manualmente. Como resultado de esta transición, es posible que la opción de Actualizar el entorno manualmente para instancias de desarrollo no esté disponible para _algunos_ de sus programas.

La opción **Actualizar** está disponible en la tarjeta **Entornos** para algunos entornos de desarrollo en programas de zonas protegidas al hacer clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg del entorno.

![Opción Actualizar de la tarjeta Entornos](assets/environ-update2.png)

Esta opción también está disponible si hace clic en la ficha **Entornos** del programa y, a continuación, hace clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg del entorno.

![Opción Actualizar de la pestaña Entornos](assets/environ-update3.png)

AEM Un usuario con el rol **Administrador de implementación** o **Propietario del negocio** puede usar esta opción para actualizar la canalización asociada con este entorno a la última versión de la.

Una vez que la versión de la canalización se actualice a la última versión de AEM disponible públicamente, se solicitará al usuario que ejecute la canalización asociada para implementar la última versión en el entorno.

![Solicitud para ejecutar la canalización para actualizar el entorno](assets/update-run-pipeline.png)

El comportamiento de la opción **Actualizar** varía según la configuración y el estado actual del programa.

* Si la canalización ya se ha actualizado, la opción **Actualizar** solicitará al usuario que ejecute la canalización.
* Si la canalización ya se está actualizando, la opción **Actualizar** informará al usuario de que ya se está ejecutando una actualización.
* Si no existe una canalización adecuada, la opción **Actualizar** solicitará al usuario que cree una.

## Eliminar entornos de desarrollo {#deleting-environment}

Un usuario con el rol **Administrador de implementación** o **Propietario del negocio** puede eliminar un entorno de desarrollo.

En la pantalla **Información general** del programa que se encuentra en la tarjeta **Entornos**, haga clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg del entorno de desarrollo que desee eliminar.

![La opción Eliminar](assets/environ-delete.png)

La opción Eliminar también está disponible en la pestaña **Entornos** de la ventana **Información general** del programa. Haga clic en https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg del entorno y seleccione **Eliminar**.

![La opción Eliminar de la pestaña Entornos](assets/environ-delete2.png)

>[!NOTE]
>
>* Los entornos de producción y ensayo creados en un programa de producción no se pueden eliminar.
>* Se pueden eliminar los entornos de producción y ensayo de un programa de zona protegida.

## Administrar acceso {#managing-access}

Seleccione **Administrar el acceso** del menú de los tres puntos del entorno en la tarjeta **Entornos**. Puede navegar hasta la instancia de autor directamente y administrar el acceso para su entorno.

![Opción Administrar el acceso](assets/environ-access.png)

>[!TIP]
>
>[Perfiles de producto y equipo de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): aprenda cómo los perfiles de producto y el equipo de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones con la licencia de Adobe.

## Acceso a la consola de desarrollador {#accessing-developer-console}

Seleccione **Consola de desarrollador** del menú de los tres puntos del entorno en la tarjeta **Entornos**. Se abre una nueva pestaña en el explorador con la página de inicio de sesión en **Developer Console**.

![Inicie sesión en Developer Console](assets/environ-devconsole.png)

Solo un usuario con la función **Desarrollador** tendrá acceso a la **Consola de desarrollador**. Sin embargo, para los programas de zonas protegidas, cualquier usuario con acceso a la zona protegida tendrá acceso a **Developer Console**.

Consulte [Entornos de zona protegida en hibernación y cancelación de la hibernación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/introduction-sandbox-programs.html#hibernation) para obtener más información.

Esta opción también está disponible en la pestaña **Entorno** de la ventana **Información general** al hacer clic en el menú de los tres puntos de un entorno individual.

## Iniciar sesión localmente {#login-locally}

Seleccione **Inicio de sesión local** del menú de los tres puntos del entorno en la tarjeta **Entornos** para iniciar sesión localmente en Adobe Experience Manager.

![Iniciar sesión localmente](assets/environ-login-locally.png)

Además, puede iniciar sesión localmente desde la pestaña **Entornos** de la página **Información general**. 

![Iniciar sesión localmente desde la pestaña Entornos](assets/environ-login-locally-2.png)

## Administrar nombres de dominio personalizados {#manage-cdn}

Los nombres de dominio personalizados se admiten en los programas de Cloud Manager para Sites tanto para los servicios de publicación como de vista previa.

>[!TIP]
>
>Para obtener más información, vea [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

## Administrar listas de IP permitidas {#manage-ip-allow-lists}

Las listas de IP permitidas son compatibles con Cloud Manager para los servicios de creación, publicación y vista previa de los programas de Sites.

Para administrar las listas de IP permitidas, navegue hasta la pestaña **Entornos** de la página **Información general** del programa. Haga clic en un entorno individual para poder administrar sus detalles.

### Aplicar una Lista de permitidos IP {#apply-ip-allow-list}

La aplicación de una lista de permitidos IP asocia todos los rangos de IP incluidos en la definición de la lista de permitidos con un servicio de autor o publicación en un entorno.

>[!TIP]
>
>Para obtener más información, vea [Introducción a las Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).
