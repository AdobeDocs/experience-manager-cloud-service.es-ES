---
title: Digital Rights Management en [!DNL Assets]
description: Obtenga información sobre cómo administrar los estados de caducidad de recursos y la información de los recursos con licencia [!DNL Experience Manager] en un Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 7%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración del uso. Dado que [!DNL Adobe Experience Manager Assets] está totalmente integrada con la [!DNL Experience Manager] plataforma, puede administrar de forma eficaz la información de caducidad de recursos y los estados de recursos. También puede asociar información de licencias con recursos.

## Caducidad del recurso {#asset-expiration}

La caducidad de los activos es una forma eficaz de aplicar los requisitos de licencia de los activos. Garantiza que el recurso publicado no se publique cuando caduque, lo que evita la posibilidad de cualquier infracción de licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede vista del estado de caducidad de un recurso en los siguientes lugares:

* **Vista** de tarjeta: Para un recurso caducado, un indicador de la tarjeta indica que ha caducado.
* **Vista** de lista: En el caso de recursos caducados, la columna **[!UICONTROL Estado]** muestra la pancarta **[!UICONTROL Caducado]** .
* **Cronología**: Puede vista del estado de caducidad de un recurso en la línea de tiempo. Seleccione el recurso y elija Línea de tiempo.
* **Carril** de referencias: También puede vista el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]** . Gestiona los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

1. Desplácese al recurso para el que desea realizar una vista haciendo referencia a páginas web y recursos compuestos.
1. Seleccione el recurso y haga clic en el [!DNL Experience Manager] logotipo.
1. Elija **[!UICONTROL Referencias]** en el menú.
1. En el caso de los recursos caducados, el carril Referencias muestra el estado de caducidad del **[!UICONTROL recurso]** en la parte superior. Si el recurso tiene subrecursos caducados, el carril Referencias muestra el estado **[!UICONTROL Recurso con subrecursos]** Caducados.

### Buscar recursos caducados {#search-expired-assets}

Puede buscar recursos caducados, incluidos los subrecursos caducados, en el panel Buscar.

1. En la [!DNL Assets] consola, haga clic en la **[!UICONTROL opción Buscar]** de la barra de herramientas para mostrar el cuadro Omniture Search.

1. Con el cursor en el cuadro Omniture Search, presione la tecla Intro para mostrar la página de resultados de la búsqueda.

1. Haga clic en el icono de GlobalNav para mostrar el panel Buscar.

1. Pulse o haga clic en la opción **[!UICONTROL Estado de caducidad]** para expandirla.

1. Seleccione **[!UICONTROL Caducado]**. Los recursos caducados se muestran en los resultados de la búsqueda.

Al elegir la opción **[!UICONTROL Caducado]** , la [!DNL Assets] consola solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de [!DNL Experience Manager] detectar que hacen referencia a subrecursos caducados la próxima vez que se ejecute el Planificador.

Si modifica la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo de Planificador actual, el programa seguirá detectando este recurso como recurso caducado la próxima vez que se ejecute y reflejará su estado de forma acorde. La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de distintos horarios.

Además, si un fallo o error impide que el Planificador detecte los recursos caducados en el ciclo actual, el Planificador vuelve a examinar estos recursos en el siguiente ciclo y detecta su estado de caducidad.

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. Abra [!DNL Experience Manager] Configuration Manager.
1. Seleccione **[!UICONTROL Adobe CQ DAM Expiry Notification]**. De forma predeterminada, está seleccionado el Planificador **[!UICONTROL basado en]** tiempo, que programa un trabajo para comprobar en un momento específico si un recurso tiene subrecursos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

1. Para ejecutar el trabajo periódicamente, desactive el campo **[!UICONTROL Regla de planificador basada en tiempo]** y modifique el tiempo en segundos en el campo **[!UICONTROL Programador periódico]**. Por ejemplo, la expresión &#39;0 0 0 &amp;ast; &amp;ast; ?&#39; activa el trabajo a las 00 horas.

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. En el campo Notificación **[!UICONTROL previa en segundos]** , especifique el tiempo en segundos antes de que caduque un recurso cuando desee recibir una notificación con respecto a la caducidad. Si es un administrador o el creador de recursos, recibirá un mensaje antes de que caduque el recurso, en el que se le notificará que el recurso está a punto de caducar después de la hora especificada.

   Una vez caducado el recurso, recibirá otra notificación que confirma la caducidad. Además, los recursos caducados se desactivan.

1. Haga clic en **[!UICONTROL Guardar]**.

## Estados de activos {#asset-states}

La [!DNL Assets] consola puede mostrar varios estados para los recursos. Según el estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario, seleccione un recurso. [!DNL Assets]

1. Click **[!UICONTROL Publish]** from the toolbar. Si no ve **Publicar** en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque la opción **[!UICONTROL Publicar]** .

1. Elija **[!UICONTROL Publicar]** en el menú y, a continuación, cierre el cuadro de diálogo de confirmación.
1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

1. Para mostrar la página de detalles del recurso, en la [!DNL Assets] interfaz, seleccione un recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En la ficha [!UICONTROL Avanzado] , establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Caduca]** .

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, en **[!UICONTROL Cerrar]** para mostrar la consola Recursos.
1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

1. En la [!DNL Assets] consola, seleccione una carpeta y cree una tarea de revisión en ella.
1. Revise y apruebe/rechace los recursos de la tarea de revisión y haga clic en **[!UICONTROL Completar]**.
1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos aprobados/rechazados se muestra en la parte inferior de la vista de tarjetas. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

1. Para buscar recursos según su estado, haga clic en **[!UICONTROL Buscar]** para mostrar la barra de Omniture.

1. Pulse Volver y haga clic en [!DNL Experience Manager] para mostrar el panel de búsqueda.
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel Buscar y elija la opción adecuada.

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que hayan sido aprobados en una tarea de revisión y que aún no hayan caducado seleccionando las opciones correspondientes en las facetas de búsqueda.

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

Esta función fuerza la aceptación del contrato de licencia antes de poder descargar un recurso con licencia desde [!DNL Adobe Experience Manager Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia para aceptar el contrato de licencia. Si no acepta el contrato de licencia, la opción **[!UICONTROL Descargar]** no está disponible.

Si la selección contiene varios recursos protegidos, selecciónelos de uno en uno, acepte el contrato de licencia y continúe con la descarga del recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` apunta a la ruta de la página que contiene el contrato de licencia del recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el contrato de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licences` utilizada para almacenar licencias en versiones anteriores de [!DNL Experience Manager] está en desuso.
>
>Si crea o modifica páginas de licencia o las transfiere desde versiones anteriores, Adobe recomienda almacenarlas en [!DNL Experience Manager] o `/apps/settings/dam/drm/licenses` `/conf/*/settings/dam/drm/licenses`.

### Descargar recursos protegidos con DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desea descargar y haga clic en **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel [!UICONTROL Licencia] , elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Haga clic en la opción **[!UICONTROL Descargar]** .

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]** para descargar el recurso o sus representaciones.
