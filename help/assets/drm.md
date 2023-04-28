---
title: Digital Rights Management en [!DNL Assets]
description: Obtenga información sobre cómo administrar los estados de caducidad de los recursos y la información de los recursos con licencia en [!DNL Experience Manager] como [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 4%

---

# Digital Rights Management para recursos digitales {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración del uso. Al usar la variable [!DNL Experience Manager] , puede administrar de forma eficaz la información de caducidad de recursos y la información de licencias.

## Caducidad del recurso {#asset-expiration}

Para hacer cumplir los requisitos de licencia de los recursos, utilice la información de caducidad de los recursos. La información de caducidad garantiza que el recurso publicado se cancele cuando caduque, lo que impide que se infrinja la licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en los siguientes lugares:

* **Vista de tarjeta**: Para un recurso caducado, un indicador de la tarjeta indica que ha caducado.
* **Vista de lista**: Para un recurso caducado, la variable **[!UICONTROL Estado]** muestra la columna **[!UICONTROL Caducado]** banner.
* **Cronología**: Puede ver el estado de caducidad de un recurso en la cronología. Seleccione el recurso y elija Línea de tiempo.
* **Carril de referencias**: También puede ver el estado de caducidad de los recursos en la **[!UICONTROL Referencias]** carril. Administra los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

Para ver las páginas web de referencia y los recursos compuestos de un recurso, siga estos pasos:

1. Vaya al recurso, selecciónelo y haga clic en ![icono de referencias de contenido del carril izquierdo](assets/do-not-localize/content-rail-icon.png). Se abre el carril izquierdo.
1. Select **[!UICONTROL Referencias]** desde el carril izquierdo.
1. Para los recursos caducados, la variable [!UICONTROL Referencias] muestra el estado de caducidad como **[!UICONTROL El recurso ha caducado]**. Si el recurso tiene subrecursos caducados, la variable [!UICONTROL Referencias] el carril muestra el estado **[!UICONTROL El recurso tiene subrecursos caducados]**.

### Buscar recursos caducados {#search-expired-assets}

Para buscar un recurso caducado, incluidos los subrecursos caducados, siga estos pasos:

1. En el [!DNL Assets] consola, haga clic en **[!UICONTROL Buscar]** en la barra de herramientas y pulse `Enter`.

1. Haga clic en el icono de navegación global y seleccione la **[!UICONTROL Estado de caducidad]** .

1. Select **[!UICONTROL Caducado]**. Los resultados de la búsqueda muestran los recursos caducados.

Al elegir el **[!UICONTROL Caducado]** , la opción [!DNL Assets] la consola solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de [!DNL Experience Manager] detecta que hace referencia a subrecursos caducados la próxima vez que se ejecute el planificador.

Es posible modificar la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del planificador actual. Sin embargo, la programación sigue detectando un recurso como activo caducado cuando se ejecuta la próxima vez y [!DNL Experience Manager] refleja la situación en su informe. La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de diferentes zonas horarias.

Además, si un error impide que el planificador detecte activos caducados en el ciclo actual, el planificador vuelve a examinar estos activos en el siguiente ciclo y detecta su estado caducado.

Para habilitar la variable [!DNL Assets] para mostrar los recursos compuestos de referencia junto con los subrecursos caducados, configure **[!UICONTROL Notificación de caducidad de Adobe CQ DAM]** flujo de trabajo en [!DNL Experience Manager]. El planificador basado en el tiempo programa un trabajo para comprobar en un momento específico si un recurso tiene subactivos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

1. Acceda a la [!DNL Cloud Manager] Repositorio de Git asociado con su entorno.
1. Confirmar un archivo con el nombre `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` en el repositorio con los siguientes contenidos.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga las instrucciones de [cómo realizar la configuración de OSGi en [!DNL Experience Manager] como [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puede configurar el planificador con las siguientes propiedades:

* A `true` valor de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` inicia el planificador. * El valor de la propiedad `cq.dam.expiry.notification.scheduler.timebased.rule` es la expresión regular para definir el tiempo. El ejemplo anterior inicia el trabajo del planificador a las 00 horas.
* If `send_email` está configurado como `true`, el creador de recursos (la persona que carga un recurso en particular en [!DNL Assets]) recibe un correo electrónico cuando caduca el recurso.
* El número máximo de recursos caducados en una iteración del planificador es el valor de la propiedad `asset_expired_limit`.
* Para ejecutar el trabajo periódicamente, establezca el valor de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` como `false` y establecer el valor de la propiedad `cq.dam.expiry.notification.scheduler.period.rule` con tiempo en segundos.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Estados de los recursos {#asset-states}

La variable [!DNL Assets] La consola puede mostrar varios estados para los recursos. En función del estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En el [!DNL Assets] interfaz de usuario, seleccione un recurso.

1. Select **[!UICONTROL Publicación]** en la barra de herramientas. Si no ve [!UICONTROL Publicación] en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque **[!UICONTROL Publicación]** .

1. Choose **[!UICONTROL Publicación]** en el menú y, a continuación, cierre el cuadro de diálogo de confirmación.

1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

1. Para mostrar la página de detalles del recurso, en la sección [!DNL Assets] interfaz, seleccione un recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En el [!UICONTROL Avanzadas] , establezca una fecha de caducidad para el recurso desde la pestaña **[!UICONTROL Caduca]** campo .

1. Haga clic en **[!UICONTROL Guardar]** y haga clic en **[!UICONTROL Cerrar]** para mostrar la consola de recursos.

1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

1. En el [!DNL Assets] , seleccione una carpeta y cree una tarea de revisión en la carpeta .

1. Revise y apruebe/rechace los recursos en la tarea de revisión y haga clic en **[!UICONTROL Completar]**.

1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos que ha aprobado o rechazado se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

1. Para buscar recursos en función de su estado, haga clic en **[!UICONTROL Buscar]** para mostrar la barra de búsqueda.

1. Select `Return` y haga clic en [!DNL Experience Manager].

1. En el panel de búsqueda, haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en [!DNL Assets].

1. Para buscar recursos aprobados o rechazados, seleccione **[!UICONTROL Estado de aprobación]** y seleccione la opción adecuada.

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel de búsqueda y seleccione la opción adecuada.

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que estén aprobados en una tarea de revisión y que no hayan caducado. Para buscar estos recursos, seleccione las opciones adecuadas en las facetas de búsqueda.

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

La funcionalidad DRM exige la aceptación del acuerdo de licencia antes de poder descargar un recurso con licencia desde [!DNL Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirige a una página de licencia para aceptar el acuerdo de licencia. Si no acepta el acuerdo de licencia, la variable **[!UICONTROL Descargar]** no está disponible.

Si la selección contiene varios recursos protegidos, seleccione un recurso a la vez, acepte el acuerdo de licencia y continúe descargando el recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` apunta a la ruta de la página que contiene el acuerdo de licencia para el recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el acuerdo de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licences` se utilizó para almacenar licencias en versiones anteriores de [!DNL Experience Manager]. La ubicación ya no se utiliza. Si crea o modifica páginas de licencia, o transfiere las páginas de anteriores [!DNL Experience Manager] versiones, Adobe recomienda almacenar estos recursos en `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses` ubicaciones.

### Descargar recursos protegidos por DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desee descargar y seleccione **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el [!UICONTROL Licencia] panel, elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Seleccione el **[!UICONTROL Descargar]** .

   >[!NOTE]
   >
   >La variable **[!UICONTROL Descargar]** solo está activada si decide aceptar el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel y en el **[!UICONTROL Descargar]** está disponible para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

1. Para descargar el recurso o sus representaciones, seleccione **[!UICONTROL Descargar]** en el cuadro de diálogo.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
