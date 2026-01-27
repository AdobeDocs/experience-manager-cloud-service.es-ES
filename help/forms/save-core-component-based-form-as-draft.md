---
title: Guardar el formulario adaptable basado en componentes principales como borrador y utilizar el componente Borradores y envíos para enumerar borradores y envíos.
description: Aprenda a guardar formularios adaptables basados en componentes principales como borrador. ¿También comprende cómo utilizar el componente Borradores y envíos para enumerar borradores y envíos para los usuarios que iniciaron sesión?
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 13%

---


# Guardar formularios como borradores y mostrarlos en la página de Sites

<!--This article provides information about the Auto-save feature, which is currently available as a pre-release feature. The pre-release feature is accessible only through our [pre-release channel](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features).-->

Considere a un usuario que comienza a rellenar un formulario pero necesita pausar y volver más tarde. AEM ofrece la opción `save-as-draft`, que permite al usuario guardar el formulario como borrador para una futura finalización. Para facilitarle este proceso, AEM proporciona el componente **Borradores y envíos** del portal de Forms de forma predeterminada, que muestra borradores y envíos en páginas de AEM Sites. El componente enumera los formularios que se han guardado como borradores para su posterior finalización, así como los que se han enviado. Solo los usuarios que inicien sesión pueden editar sus borradores o ver los formularios enviados. Sin embargo, si un usuario anónimo navega por la lista de formularios usando el componente **Buscar y listar** y guarda un formulario como borrador, ese borrador no aparecerá en la lista del componente **Borradores y envíos**. Para ver los borradores y los envíos, los usuarios deben haber iniciado sesión en el momento del envío del formulario.

![Icono Borradores](assets/drafts-component.png)

## Requisitos previos

* [Configurar el almacenamiento de Azure y el conector de almacenamiento unificado para el componente del portal de Forms Borradores y envíos](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### Configuración del almacenamiento de Azure y el conector de almacenamiento unificado para el componente del portal de Forms Borradores y envíos

El componente **Borradores y envíos** necesita una configuración de almacenamiento para guardar y enumerar borradores en la página de AEM Sites. El conector de almacenamiento unificado ofrece un marco para vincular AEM con el almacenamiento externo. Para guardar el formulario como borrador, asegúrese de que dispone de una cuenta de almacenamiento de Azure y una clave de acceso para autorizar el acceso a la cuenta de almacenamiento de [!DNL Azure]. Una vez que tenga la cuenta de almacenamiento de Azure y la clave de acceso, realice los siguientes pasos para crear una configuración de almacenamiento de Azure:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.

   ![Selección de tarjeta de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Seleccione una carpeta de configuración para crear la configuración y seleccione **[!UICONTROL Crear]**.

   ![Seleccionar carpeta de configuración de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.
1. Especifique el nombre de la cuenta de almacenamiento [!DNL Azure] en los campos **[!UICONTROL Cuenta de almacenamiento de Azure]** y **[!UICONTROL Clave de acceso de Azure]**.

   ![Configuración de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

   Escriba `Connection String` en el cuadro de texto `Azure Storage Account` y `Azure Key` en el cuadro de texto `Azure Access key`.

1. Haga clic en **Guardar**.

   >[!NOTE]
   >
   > Puede recuperar la **[!UICONTROL cuenta de almacenamiento de Azure]** y la **[!UICONTROL clave de acceso de Azure]** del [Portal de Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

   Después de crear correctamente la Configuración de almacenamiento de Azure, configure el Conector de almacenamiento unificado para el portal de Forms, para ello, siga los siguientes pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Formularios]** > **[!UICONTROL Conector de almacenamiento unificado]**.

   ![Almacenamiento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. En el **[!UICONTROL portal de Forms]**, seleccione **[!UICONTROL Azure]** de la lista desplegable **[!UICONTROL Almacenamiento]**.
1. Especifique la ruta de configuración para la configuración del almacenamiento de Azure en el campo **[!UICONTROL Ruta de configuración del almacenamiento]**.

   ![Configuración de almacenamiento del conector unificado](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Seleccione **[!UICONTROL Guardar]**.

>[!NOTE]
>
> Si necesita configurar una opción de almacenamiento que no sea Azure, escriba a <aem-forms-ea@adobe.com> desde su dirección de correo electrónico oficial con los requisitos detallados.

Una vez que haya configurado correctamente el almacenamiento de Azure y el conector de almacenamiento unificado para almacenar los borradores y los formularios enviados, agregue el componente **Borradores y envíos** en la página de AEM Sites.

## ¿Cómo se agrega el componente Borradores y envíos a una página de AEM Sites?

Puede utilizar los componentes listos para usar del portal de Forms para enumerar borradores y envíos en la página de Sites. Realice los siguientes pasos para agregar el componente de portal **Borradores y envíos**:

1. Abra la página de AEM Sites en el modo **Editar**.
1. Vaya a la **[!UICONTROL Información de la página]** > **[!UICONTROL Editar plantilla]**
   ![Editar la política de plantilla](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Haga clic en la **[!UICONTROL directiva]** y seleccione la casilla de verificación **[!UICONTROL Borradores y envíos]** bajo el **[Nombre del proyecto de tipo de archivo de AEM] - Forms y el portal de comunicaciones**.

   ![Selección de política](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Haga clic en **[!UICONTROL Listo]**.
1. Ahora vuelva a abrir la página de AEM Sites en el modo Autor.
1. Busque la sección en el editor de páginas que le permite añadir el componente del Portal de formularios.
1. Haga clic en el icono **Añadir**. El icono es un signo más (+) que representa la opción de añadir nuevos componentes.

   Al hacer clic en el icono **Añadir** aparece un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   >[!NOTE]
   >
   > También puede arrastrar y soltar el componente.

1. Examine los componentes disponibles en el cuadro de diálogo y seleccione el componente que desee en la lista. Por ejemplo, seleccione el componente **Borradores y envíos** de la lista para agregar el componente **Borradores y envíos** del portal de Forms.

   ![Agregar componente de borrador y envío](/help/forms/assets/save-form-as-draft-add-dns.png)

Ahora, configure las propiedades del componente **Borradores y envíos** según los requisitos.

## Configurar propiedades del componente Borradores y envíos

Puede configurar las propiedades de **Borradores y envíos**:

1. Seleccione el componente **Borradores y envíos**.
1. Haga clic en el icono ![Configurar](assets/configure_icon.png) y aparecerá el cuadro de diálogo.
1. En el cuadro de diálogo **[!UICONTROL Borradores y envíos]**, especifique lo siguiente:

   * **Título** Para identificar un componente en una página de Sites y de forma predeterminada, el título aparece en la parte superior del componente.
   * **Seleccionar tipo**: para indicar la lista de formularios como formularios en borrador o enviados. Si elige **Borrador de Forms**, se mostrarán los formularios guardados como borradores. Como alternativa, al seleccionar **Forms enviado** se muestran los formularios enviados por los usuarios que iniciaron sesión.
   * **Diseño**: para mostrar una lista de formularios en borrador o enviados en formato de tarjeta o lista.

   ![Propiedades del componente Borradores y envíos](/help/forms/assets/save-form-as-draft-dns-properties.png)

## Configurar formularios para guardarlos como borradores

Puede configurar Forms adaptable de las dos formas siguientes para guardarlos como borradores para usarlos más adelante:

* [Acción del usuario](#user-action)
* [Guardar automáticamente](#auto-save)

### Acción del usuario

>[!NOTE]
>
> Asegúrese de que la versión de [componentes principales esté establecida en 3.0.24 o posterior](https://github.com/adobe/aem-core-forms-components) para guardar formularios como borradores mediante la regla **Guardar formulario**.

Para guardar un formulario como borrador, cree una regla **Guardar formulario** en un componente de formulario, como un botón. Cuando se hace clic en el botón, la regla entra en déclencheur y el formulario se guarda como borrador. Realice los siguientes pasos para crear una regla **Guardar formulario** en un componente de botón:

1. Abra un formulario adaptable en modo de edición.
1. Seleccione el icono **[!UICONTROL Editar reglas]** para abrir el Editor de reglas para el componente **Button**.
1. Seleccione **[!UICONTROL Crear]** para configurar y crear la regla para el botón.
1. En la sección **[!UICONTROL Cuándo]**, seleccione **se hace clic** y en la sección **[!UICONTROL Entonces]**, seleccione la opción **Guardar formulario**.
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

   ![Crear regla para el botón](/help/forms/assets/save-form-as-drfat-create-rule.png)

Cuando obtiene una vista previa de un formulario adaptable, lo rellena y hace clic en el botón **Guardar formulario**, el formulario se guarda como borrador.

### Borradores

>[!NOTE]
>
> Asegúrese de que la versión de [componentes principales está establecida en 3.0.52 o posterior](https://github.com/adobe/aem-core-forms-components) para guardar formularios como borradores mediante la característica de guardado automático.

También puede configurar un formulario adaptable para que se guarde automáticamente en función de un evento basado en el tiempo, asegurándose de que el formulario se guarde después de la duración especificada. Cuando [habilita los componentes del portal de Forms para su entorno](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment), la pestaña **Guardar automáticamente** aparece en las propiedades del contenedor de Forms. Puede configurar la función de guardado automático para un formulario adaptable:

1. En la instancia Autor, abra un formulario adaptable en modo de edición.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de las propiedades del contenedor de la guía ![Propiedades de la guía](/help/forms/assets/configure-icon.svg) y abra la pestaña **[!UICONTROL Borradores]**.

   ![Guardar automáticamente](/help/forms/assets/auto-save.png)

1. Active la casilla de verificación **[!UICONTROL Guardar borradores automáticamente]** para habilitar el guardado automático del formulario como borradores.
1. Configure **[!UICONTROL Guardar preferencia]** como **Guardar borradores a intervalos regulares** para guardar automáticamente el formulario <!--based on the occurrence of an event or--> después de un intervalo de tiempo específico.
1. Especifique el intervalo de tiempo en **[!UICONTROL Guardar frecuencia de intervalo (segundos)]** para establecer la duración que almacena en déclencheur el guardado automático del formulario en el intervalo definido.
1. Haga clic en **[!UICONTROL Listo]**.

## Ver borradores/formularios enviados en la página de Sites mediante el componente Borradores y envíos

Para ver los borradores guardados o los formularios enviados, usa el componente **Borradores y envíos** del portal de Forms.
Cuando **[!UICONTROL Seleccionar tipo]** se selecciona como **Borrador de Forms** en el cuadro de diálogo [configurar del componente Borradores y envíos](#configure-properties-of-the-drafts--submissions-component), los formularios guardados como borradores aparecerán en la página Sitios. Puede abrir los borradores haciendo clic en los puntos suspensivos (...) para completar el formulario.

![Icono Borradores](assets/drafts-component.png)

Cuando se selecciona **[!UICONTROL Seleccionar tipo]** como **Forms enviado** en el cuadro de diálogo [configurar del componente Borradores y envíos](#configure-properties-of-the-drafts--submissions-component), aparecen los formularios enviados. Puede ver los formularios enviados, pero no puede editarlos.

![Icono Envíos](assets/submission-listing.png)

También puede descartar los formularios haciendo clic en los puntos suspensivos (...) que aparecen en la esquina inferior derecha del formulario.

>[!NOTE]
>
> En el portal de Forms, el componente Borradores y envíos solo admite los envíos de formularios basados en Foundation.

## Próximos pasos

En el artículo siguiente, aprenderemos [cómo agregar referencias a formularios en la página de Sites mediante el componente Vínculo al portal de Forms](/help/forms/add-form-link-to-aem-sites-page.md).

## Artículos relacionados

{{forms-portal-see-also}}

## Ver también {#see-also}

{{see-also}}
