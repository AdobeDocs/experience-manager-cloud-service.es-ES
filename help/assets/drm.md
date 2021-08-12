---
title: Digital Rights Management en [!DNL Assets]
description: Obtenga información sobre cómo administrar los estados de caducidad de recursos y la información para los recursos con licencia en [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Administración de recursos,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 2%

---

# Digital Rights Management para recursos digitales {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración del uso. Con la plataforma [!DNL Experience Manager], puede administrar de forma eficaz la información de caducidad de recursos y la información de licencias.

## Caducidad del recurso {#asset-expiration}

Para hacer cumplir los requisitos de licencia de los recursos, utilice la información de caducidad de los recursos. La información de caducidad garantiza que el recurso publicado se cancele cuando caduque, lo que impide que se infrinja la licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en los siguientes lugares:

* **Vista** de tarjeta: Para un recurso caducado, un indicador de la tarjeta indica que ha caducado.
* **Vista** de lista: Para un recurso caducado, la  **** columna Estado muestra el  **** titular Caducado.
* **Cronología**: Puede ver el estado de caducidad de un recurso en la cronología. Seleccione el recurso y elija Línea de tiempo.
* **Carril** de referencias: También puede ver el estado de caducidad de los recursos en el  **** carril de referencia. Administra los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

Para ver las páginas web de referencia y los recursos compuestos de un recurso, siga estos pasos:

1. Vaya al recurso, seleccione el recurso y haga clic en ![icono de referencias de contenido del carril izquierdo](assets/do-not-localize/content-rail-icon.png). Se abre el carril izquierdo.
1. Seleccione **[!UICONTROL Referencias]** en el carril izquierdo.
1. Para los recursos caducados, la [!UICONTROL References] muestra el estado de caducidad como **[!UICONTROL Asset is Expired]**. Si el recurso tiene subrecursos caducados, el carril [!UICONTROL References] muestra el estado **[!UICONTROL Asset has Expired Sub-Assets]**.

### Buscar recursos caducados {#search-expired-assets}

Para buscar un recurso caducado, incluidos los subrecursos caducados, siga estos pasos:

1. En la consola [!DNL Assets], haga clic en **[!UICONTROL Buscar]** en la barra de herramientas y presione `Enter`.

1. Haga clic en el icono de navegación global y seleccione la opción **[!UICONTROL Estado de caducidad]**.

1. Seleccione **[!UICONTROL Expired]**. Los resultados de la búsqueda muestran los recursos caducados.

Al elegir la opción **[!UICONTROL Expired]**, la consola [!DNL Assets] solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que [!DNL Experience Manager] detecte que hacen referencia a subrecursos caducados la próxima vez que se ejecute el planificador.

Es posible modificar la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del planificador actual. Sin embargo, la programación sigue detectando un recurso como activo caducado cuando se ejecuta la próxima vez y [!DNL Experience Manager] refleja el estado en su informe. La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de diferentes zonas horarias.

Además, si un error impide que el planificador detecte activos caducados en el ciclo actual, el planificador vuelve a examinar estos activos en el siguiente ciclo y detecta su estado caducado.

Para permitir que la consola [!DNL Assets] muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure el flujo de trabajo **[!UICONTROL Adobe CQ DAM Expiry Notification]** en [!DNL Experience Manager]. El planificador basado en el tiempo programa un trabajo para comprobar en un momento específico si un recurso tiene subactivos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

1. Acceda al repositorio de Git [!DNL Cloud Manager] asociado a su entorno.
1. Confirme un archivo denominado `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` en el repositorio con el siguiente contenido.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga las instrucciones de [cómo realizar la configuración de OSGi en [!DNL Experience Manager] como a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puede configurar el planificador con las siguientes propiedades:

* Un valor `true` de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` inicia el planificador. * El valor de la propiedad `cq.dam.expiry.notification.scheduler.timebased.rule` es la expresión regular para definir el tiempo. El ejemplo anterior inicia el trabajo del planificador a las 00 horas.
* Si `send_email` está establecido en `true`, el creador de recursos (la persona que carga un recurso en particular en [!DNL Assets]) recibe un correo electrónico cuando caduca el recurso.
* El número máximo de recursos caducados en una iteración del planificador es el valor de la propiedad `asset_expired_limit`.
* Para ejecutar el trabajo periódicamente, establezca el valor de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` como `false` y establezca el valor de la propiedad `cq.dam.expiry.notification.scheduler.period.rule` con el tiempo en segundos.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Estados de los recursos {#asset-states}

La consola [!DNL Assets] puede mostrar varios estados para los recursos. En función del estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario [!DNL Assets], seleccione un recurso.

1. Seleccione **[!UICONTROL Publicar]** en la barra de herramientas. Si no ve la opción [!UICONTROL Publicar] en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque la opción **[!UICONTROL Publicar]**.

1. Elija **[!UICONTROL Publicar]** en el menú y cierre el cuadro de diálogo de confirmación.

1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

1. Para mostrar la página de detalles del recurso, en la interfaz [!DNL Assets], seleccione un recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En la pestaña [!UICONTROL Advanced], establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Expires]**.

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Cerrar]** para mostrar la consola de recursos.

1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Expired]**.

1. En la consola [!DNL Assets], seleccione una carpeta y cree una tarea de revisión en la carpeta.

1. Revise y apruebe/rechace los recursos en la tarea de revisión y haga clic en **[!UICONTROL Completar]**.

1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos que ha aprobado o rechazado se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

1. Para buscar recursos en función de su estado, haga clic en **[!UICONTROL Buscar]** para mostrar la barra de búsqueda.

1. Seleccione `Return` y haga clic en [!DNL Experience Manager].

1. En el panel de búsqueda, haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en [!DNL Assets].

1. Para buscar recursos aprobados o rechazados, seleccione **[!UICONTROL Approval Status]** y seleccione la opción adecuada.

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel de búsqueda y seleccione la opción adecuada.

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que estén aprobados en una tarea de revisión y que no hayan caducado. Para buscar estos recursos, seleccione las opciones adecuadas en las facetas de búsqueda.

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

La funcionalidad DRM exige la aceptación del acuerdo de licencia antes de poder descargar un recurso con licencia desde [!DNL Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia para aceptar el acuerdo de licencia. Si no acepta el acuerdo de licencia, la opción **[!UICONTROL Download]** no está disponible.

Si la selección contiene varios recursos protegidos, seleccione un recurso a la vez, acepte el acuerdo de licencia y continúe descargando el recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos de recursos `xmpRights:WebStatement` apunta a la ruta de la página que contiene el acuerdo de licencia para el recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el acuerdo de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licences` se utilizó para almacenar licencias en las versiones anteriores de [!DNL Experience Manager]. La ubicación ya no se utiliza. Si crea o modifica páginas de licencia o transfiere las páginas de versiones anteriores de [!DNL Experience Manager] , Adobe recomienda que almacene dichos activos en ubicaciones `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses` .

### Descargar recursos protegidos por DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desee descargar y seleccione **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel [!UICONTROL Licencia], elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Seleccione la opción **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Download]** solo se habilita cuando se decide aceptar el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel y la opción **[!UICONTROL Descargar]** está disponible para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

1. Para descargar el recurso o sus representaciones, seleccione **[!UICONTROL Descargar]** en el cuadro de diálogo.
