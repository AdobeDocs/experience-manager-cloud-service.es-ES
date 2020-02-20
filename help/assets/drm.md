---
title: Administración de derechos digitales en recursos de Adobe Experience Manager
description: Obtenga información sobre cómo administrar los estados de caducidad de recursos y la información de los recursos con licencia en AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# Administración de derechos digitales en Experience Manager Assets {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia, que especifica sus términos y duración de uso. Puesto que Recursos Adobe Experience Manager (AEM) está totalmente integrado con la plataforma AEM, puede administrar de forma eficaz la información de caducidad de recursos y los estados de los mismos. También puede asociar información de licencias con recursos.

## Caducidad del recurso {#asset-expiration}

La caducidad de los activos es una forma eficaz de aplicar los requisitos de licencia de los activos. Garantiza que el recurso publicado no se publique cuando caduque, lo que evita la posibilidad de cualquier infracción de licencia. Un usuario sin derechos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en los siguientes lugares:

* **Vista** de tarjeta: Para un recurso caducado, un indicador de la tarjeta indica que ha caducado.
* **Vista** de lista: En el caso de recursos caducados, la columna **[!UICONTROL Estado]** muestra la pancarta **[!UICONTROL Caducado]** .
* **Cronología**: Puede ver el estado de caducidad de un recurso en la línea de tiempo. Seleccione el recurso y elija Línea de tiempo.
* **Carril** de referencias: También puede ver el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]** . Gestiona los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

1. Vaya al recurso para el que desea ver las páginas Web de referencia y los recursos compuestos.
1. Seleccione el recurso y toque o haga clic en el icono de navegación global.
1. Elija **[!UICONTROL Referencias]** en el menú.
1. En el caso de los recursos caducados, el carril Referencias muestra el estado de caducidad del **[!UICONTROL recurso]** en la parte superior. Si el recurso tiene subrecursos caducados, el carril Referencias muestra el estado **[!UICONTROL Recurso con subrecursos]** Caducados.

### Buscar recursos caducados {#search-expired-assets}

Puede buscar recursos caducados, incluidos los subrecursos caducados, en el panel Buscar.

1. En la consola Recursos, haga clic en el icono Buscar en la barra de herramientas para mostrar el campo Omniture Search.

1. Con el cursor en el cuadro Omniture Search, presione la tecla Intro para mostrar la página de resultados de la búsqueda.

1. Haga clic en el icono de GlobalNav para mostrar el panel Buscar.

1. Toque o haga clic en la opción Estado de **[!UICONTROL caducidad]** para expandirla.

1. Seleccione **[!UICONTROL Caducado]**. Los recursos caducados se muestran en los resultados de la búsqueda.

Al elegir la opción **[!UICONTROL Caducado]** , la consola Recursos solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que Recursos AEM detecte que hacen referencia a subrecursos caducados la próxima vez que se ejecute el programador.

Si modifica la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del programador actual, el programa seguirá detectando este recurso como recurso caducado la próxima vez que se ejecute y reflejará su estado en consecuencia.

Además, si un fallo o error impide que el programador detecte los recursos caducados en el ciclo actual, el programador vuelve a examinar estos recursos en el siguiente ciclo y detecta su estado caducado.

Para permitir que la consola Recursos muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure un flujo de trabajo de notificación **[!UICONTROL de caducidad de]** Adobe CQ DAM en AEM Configuration Manager.

1. Abra AEM Configuration Manager.
1. Seleccione **[!UICONTROL Adobe CQ DAM Expiry Notification]**. De forma predeterminada, está seleccionado Programador **[!UICONTROL basado en]** tiempo, que programa un trabajo para comprobar en un momento específico si un recurso tiene subrecursos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

1. Para ejecutar el trabajo periódicamente, desactive el campo Regla **[!UICONTROL de programador basado en]** tiempo y modifique el tiempo en segundos en el campo Programador **** periódico. Por ejemplo, la expresión de ejemplo &#39;0 0 &amp;ast; &amp;ast; ?&#39; activa el trabajo a las 00 horas.
1. Seleccione **[!UICONTROL enviar correo electrónico]** para recibir correos electrónicos cuando caduque un recurso.

   >[!NOTE]
   >
   >Solo el creador de recursos (la persona que carga un recurso concreto en Recursos AEM) recibe un correo electrónico cuando caduca el recurso. Consulte cómo configurar las notificaciones por correo electrónico para obtener más información sobre la configuración de las notificaciones por correo electrónico en todo el nivel de AEM.

1. En el campo Notificación **[!UICONTROL previa en segundos]** , especifique el tiempo en segundos antes de que caduque un recurso cuando desee recibir una notificación con respecto a la caducidad. Si es un administrador o el creador de recursos, recibirá un mensaje antes de que caduque el recurso, en el que se le notificará que el recurso está a punto de caducar después de la hora especificada.

   Una vez caducado el recurso, recibirá otra notificación que confirma la caducidad. Además, los recursos caducados se desactivan.

1. Haga clic en **[!UICONTROL Guardar]**.

## Estados de activos {#asset-states}

La consola Recursos de Recursos de Recursos Adobe Experience Manager (AEM) puede mostrar varios estados para los recursos. Según el estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario de Recursos, seleccione un recurso.

1. Tap/click the **[!UICONTROL Publish]** icon from the toolbar. Si no puede ver el icono **Publicar** en la barra de herramientas, toque o haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque el icono **[!UICONTROL Publicar]** .

1. Elija **[!UICONTROL Publicar]** en el menú y, a continuación, cierre el cuadro de diálogo de confirmación.
1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

1. En la interfaz de usuario de Recursos, seleccione un recurso y toque o haga clic en el icono **[!UICONTROL Propiedades]** para mostrar la página de detalles del recurso.

1. En la ficha Avanzado, y defina una fecha de caducidad para el recurso en el campo **[!UICONTROL Caduca]** en.

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, en **[!UICONTROL Cerrar]** para mostrar la consola Recursos.
1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

1. En la consola Recursos, seleccione una carpeta y cree una tarea de revisión en la carpeta.
1. Revise y apruebe/rechace los recursos de la tarea de revisión y haga clic en **[!UICONTROL Completar]**.
1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos aprobados/rechazados se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

1. Para buscar recursos en función de su estado, toque o haga clic en el icono **[!UICONTROL Buscar]** para mostrar la barra de Omniture.

1. Pulse la tecla Intro y, a continuación, toque o haga clic en el icono de AEM para mostrar el panel Buscar.
1. En el panel Buscar, toque o haga clic en Estado **[!UICONTROL de]** publicación y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en Recursos AEM.

1. Toque o haga clic en Estado **[!UICONTROL de]** aprobación y haga clic en la opción correspondiente para buscar recursos aprobados o rechazados.

1. Para buscar recursos en función de su estado de caducidad, seleccione Estado **[!UICONTROL de]** caducidad en el panel Buscar y elija la opción adecuada.

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que hayan sido aprobados en una tarea de revisión y que aún no hayan caducado seleccionando las opciones correspondientes en las facetas de búsqueda.

## Administración de derechos digitales en Experience Manager Assets {#digital-rights-management-in-assets-1}

Esta función fuerza la aceptación del contrato de licencia antes de poder descargar un recurso con licencia desde Recursos Adobe Experience Manager (AEM).

Si selecciona un recurso protegido y hace clic en el icono **[!UICONTROL Descargar]** , se le redirigirá a una página de licencia en la que acepte el contrato de licencia. Si no acepta el contrato de licencia, se desactiva el botón **[!UICONTROL Descargar]** .

Si la selección contiene varios recursos protegidos, selecciónelos de uno en uno, acepte el contrato de licencia y continúe con la descarga del recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` apunta a la ruta de la página de CQ que contiene el contrato de licencia del recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el contrato de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licences` utilizada para almacenar licencias en versiones anteriores de AEM ya no se utiliza.
>
>Si crea o modifica páginas de licencia o las transfiere desde versiones anteriores de AEM, Adobe recomienda que almacene las páginas en `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses`.

### Descargar recursos DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desea descargar y haga clic en el icono **[!UICONTROL Descargar]** .
1. En la página Administración **[!UICONTROL de]** derechos de autor, seleccione el recurso que desee descargar de la lista.
1. En el panel Licencia, elija **[!UICONTROL Aceptar]**. Aparece una marca de graduación junto al recurso para el que acepta el contrato de licencia. Toque o haga clic en el botón **[!UICONTROL Descargar]** .

   >[!NOTE]
   >
   >El botón **[!UICONTROL Descargar]** solo se activa cuando se decide aceptar el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel izquierdo y el botón **[!UICONTROL Descargar]** está habilitado para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Descargar]** para descargar el recurso o sus representaciones.
