---
title: Digital Rights Management en  [!DNL Assets]
description: Aprenda a administrar los estados de caducidad de los recursos y la información de los recursos con licencia en  [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User, Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 6%

---

# Digital Rights Management para recursos digitales {#digital-rights-management-in-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración de uso. Con la plataforma [!DNL Experience Manager], puede administrar de manera eficaz la información de caducidad de recursos y la información de licencias.

## Caducidad de recursos {#asset-expiration}

Para aplicar los requisitos de licencia a los recursos, utilice la información de caducidad del recurso. La información de caducidad garantiza que el recurso publicado se cancele la publicación cuando caduque, lo que evita la infracción de licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en los siguientes lugares:

* **Vista de tarjeta**: Para un recurso caducado, un indicador en la tarjeta indica que ha caducado.
* **Vista de lista**: Para un recurso caducado, la columna **[!UICONTROL Estado]** muestra el titular **[!UICONTROL Caducado]**.
* **Cronología**: puede ver el estado de caducidad de un recurso en la cronología. Seleccione el recurso y elija Cronología.
* **Carril de referencias**: también puede ver el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]**. Administra los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los recursos secundarios, las colecciones y los proyectos a los que se hace referencia.

Para ver las páginas web de referencia y los recursos compuestos de un recurso, siga estos pasos:

1. Vaya al recurso, selecciónelo y haga clic en ![icono de referencias de contenido del carril izquierdo](assets/do-not-localize/content-rail-icon.png). Se abrirá el carril izquierdo.
1. Seleccione **[!UICONTROL Referencias]** del carril izquierdo.
1. Para los recursos caducados, [!UICONTROL Referencias] muestra el estado de caducidad como **[!UICONTROL El recurso ha caducado]**. Assets Si el recurso tiene recursos secundarios caducados, el carril [!UICONTROL Referencias] muestra el estado **[!UICONTROL El recurso tiene un subrecurso caducado]**.

### Buscar recursos caducados {#search-expired-assets}

Para buscar un recurso caducado, incluidos los subrecursos caducados, siga estos pasos:

1. En la consola [!DNL Assets], haga clic en **[!UICONTROL Buscar]** en la barra de herramientas y presione `Enter`.

1. Haga clic en el icono GlobalNav y seleccione la opción **[!UICONTROL Estado de caducidad]**.

1. Seleccione **[!UICONTROL Caducado]**. Los resultados de la búsqueda muestran los recursos caducados.

Al elegir la opción **[!UICONTROL Caducado]**, la consola [!DNL Assets] solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que [!DNL Experience Manager] detecte que hacen referencia a recursos secundarios caducados la próxima vez que se ejecute el programador.

Es posible modificar la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del programador actual. Sin embargo, la programación sigue detectando un recurso de este tipo como un recurso caducado cuando se ejecute la próxima vez y [!DNL Experience Manager] refleja el estado en su informe. La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de diferentes zonas horarias.

Además, si un error impide que el programador detecte los recursos caducados en el ciclo actual, vuelve a examinarlos en el ciclo siguiente y detecta su estado caducado.

Para permitir que la consola [!DNL Assets] muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure el flujo de trabajo **[!UICONTROL Notificación de caducidad de Adobe CQ DAM]** en [!DNL Experience Manager]. El programador basado en tiempo programa una tarea para comprobar en un momento específico si un recurso tiene recursos secundarios caducados. Una vez finalizado el trabajo, los recursos que tienen recursos secundarios caducados y los recursos a los que se hace referencia se muestran como caducados en los resultados de búsqueda.

1. Acceda al repositorio Git [!DNL Cloud Manager] asociado a su entorno.
1. Confirme un archivo de nombre `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` en el repositorio con el siguiente contenido.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Siga las instrucciones de [cómo hacer la configuración de OSGi en [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puede configurar el planificador mediante las siguientes propiedades:

* Un valor `true` de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` inicia el programador. * El valor de la propiedad `cq.dam.expiry.notification.scheduler.timebased.rule` es la expresión regular para definir la hora. El ejemplo anterior inicia el trabajo del planificador a las 00 horas.
* Si `send_email` se establece en `true`, el creador del recurso (la persona que carga un recurso en particular en [!DNL Assets]) recibe un mensaje de correo electrónico cuando caduca el recurso.
* El número máximo de recursos caducados en una iteración del programador es el valor de la propiedad `asset_expired_limit`.
* Para ejecutar el trabajo periódicamente, establezca el valor de la propiedad `cq.dam.expiry.notification.scheduler.istimebased` como `false` y establezca el valor de la propiedad `cq.dam.expiry.notification.scheduler.period.rule` con el tiempo en segundos.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Estados de los recursos {#asset-states}

La consola [!DNL Assets] puede mostrar varios estados para los recursos. Según el estado actual de un recurso determinado, la vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario [!DNL Assets], seleccione un recurso.

1. Seleccione **[!UICONTROL Publicar]** en la barra de herramientas. Si no ve la opción [!UICONTROL Publish] en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque la opción **[!UICONTROL Publish]**.

1. Elija **[!UICONTROL Publicar]** en el menú y luego cierre el cuadro de diálogo de confirmación.

1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora a la que se publicó el recurso.

1. Para mostrar la página de detalles del recurso, en la interfaz [!DNL Assets], seleccione un recurso y haga clic en **[!UICONTROL Propiedades]**.

1. En la ficha [!UICONTROL Avanzado], establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Caduca]**.

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Cerrar]** para mostrar la consola Recursos.

1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

1. En la consola [!DNL Assets], seleccione una carpeta y cree una tarea de revisión en la carpeta.

1. Revise y apruebe o rechace los recursos en la tarea de revisión y haga clic en **[!UICONTROL Completar]**.

1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos que aprobó o rechazó se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

1. Para buscar recursos en función de su estado, haga clic en **[!UICONTROL Buscar]** para mostrar la barra de búsqueda.

1. Seleccione `Return` y haga clic en [!DNL Experience Manager].

1. En el panel de búsqueda, haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en [!DNL Assets].

1. Para buscar recursos aprobados o rechazados, seleccione **[!UICONTROL Estado de aprobación]** y seleccione la opción adecuada.

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel de búsqueda y seleccione la opción adecuada.

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que se hayan aprobado en una tarea de revisión y que no hayan caducado. Para buscar estos recursos, seleccione las opciones adecuadas en las facetas de búsqueda.

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

La funcionalidad DRM exige la aceptación del acuerdo de licencia para poder descargar un recurso con licencia de [!DNL Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia para aceptar el acuerdo de licencia. Si no acepta el contrato de licencia, la opción **[!UICONTROL Descargar]** no estará disponible.

Si la selección contiene varios recursos protegidos, seleccione un recurso a la vez, acepte el acuerdo de licencia y proceda a descargar el recurso.

Un activo se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` señala a la ruta de acceso de la página que contiene el contrato de licencia del recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es una HTML sin procesar que especifica el contrato de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licences` se usó para almacenar licencias en las versiones anteriores de [!DNL Experience Manager]. La ubicación ya no se utiliza. Si crea o modifica páginas de licencias o transfiere las páginas de versiones anteriores de [!DNL Experience Manager], Adobe recomienda almacenar estos recursos en `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses` ubicaciones.

### Descarga de recursos protegidos por DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desee descargar y seleccione **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel [!UICONTROL Licencia], elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Seleccione la opción **[!UICONTROL Descargar]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Descargar]** solo está habilitada cuando acepta el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel, y la opción **[!UICONTROL Descargar]** está disponible para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

1. Para descargar el recurso o sus representaciones, seleccione **[!UICONTROL Descargar]** en el cuadro de diálogo.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
