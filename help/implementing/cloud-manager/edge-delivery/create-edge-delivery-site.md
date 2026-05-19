---
title: Creación del primer sitio de Edge Delivery con un clic
description: Aprenda a crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: 9cf3ab69adf8819d9f5496bf826c63f7cf01d554
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 56%

---


# Creación del primer sitio de Edge Delivery con un clic{#about-one-click-edge-delivery-site}

Crear su primer sitio de Edge Delivery con un clic se ha diseñado para ayudarle a automatizar la incorporación y la implementación de sitios de Edge Delivery en Cloud Manager. Simplifica enormemente el proceso, ya que solo tiene que hacer clic en un botón. Con un solo clic se aprovisiona la infraestructura necesaria, se integra con GitHub para el control de versiones y se configura el almacenamiento de documentos y recursos en Google Drive.

Esta automatización ayuda a reducir el esfuerzo manual necesario para configurar el sitio inicial. Garantiza flujos de trabajo y escalabilidad fluidos y mejora el rendimiento de sus equipos en lo que respecta a la administración de contenido en el extremo.

>[!IMPORTANT]
>
>El aprovisionamiento de sitios Edge Delivery con un solo clic está optimizado para sitios de prueba de concepto y prototipos rápidos. Para las cargas de trabajo de producción, Adobe recomienda migrar el sitio a una organización de Edge Delivery Services dedicada.

<!--
 Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on)
-->

## Creación de un sitio de Edge Delivery en Cloud Manager con un solo clic {#one-click-edge-delivery-site}

Para crear un sitio de Adobe Edge Delivery con un solo clic, su organización debe tener una licencia de Edge Delivery Services disponible. Esta licencia forma parte de Adobe Experience Manager (AEM) y es necesaria para crear Edge Delivery Services en Cloud Manager.

En cuanto a los permisos, debe ser miembro de la función Propietario del negocio o tener los permisos adecuados para añadir o editar programas en Cloud Manager. Este nivel de acceso le permite administrar la integración de Edge Delivery Services en sus programas.

Consulte también [Introducción a Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Para crear un sitio de Edge Delivery en Cloud Manager con un solo clic:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
   1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
   1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
   1. Seleccione una organización.
1. En la consola **Mis programas**, haga clic en un programa.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú de la izquierda, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la página de Edge Delivery, en el cuadro de diálogo **Lista de tareas pendientes de Edge Delivery**, en el cuadro de grupo **Agregar sitio de Edge Delivery**, haga clic en **Crear sitio ahora**.
1. En el cuadro de diálogo **Crear sitio de Edge Delivery**, en el campo de texto **Nombre del proyecto**, escriba el nombre del sitio.
1. En **Opciones de creación**, seleccione una de las siguientes opciones:
   * **Creación de documentos**: Cree contenido en Google Drive o SharePoint. Esta opción es la predeterminada y no requiere un entorno de AEM.
   * **Creación en AEM**: Cree contenido en AEM con el editor universal. Si elige esta opción, en **Seleccionar plantilla**, seleccione una plantilla inicial para el sitio de Edge Delivery.

   ![Cuadro de diálogo Crear sitio de Edge Delivery con la opción Creación de AEM seleccionada.](/help/implementing/cloud-manager/edge-delivery/assets/eds-create-aem-authoring.png)

1. En la lista desplegable **Entornos de creación**, seleccione un entorno de AEM para utilizarlo en la creación. Este entorno ya debe existir en su programa. Solo se requiere el nivel de Author; no se necesita un nivel de publicación cuando Edge Delivery gestiona la entrega. Consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

1. Haga clic en **Crear sitio ahora**.

   Aparece un mensaje cerca de la parte superior central de la pantalla que le informa de que se ha iniciado el aprovisionamiento del sitio de Edge Delivery.

   Cuando Cloud Manager completa el aprovisionamiento y la validación del sitio, aparece **Nombre del sitio** (el nombre del proyecto que escribió anteriormente) en el cuadro de lista **Sitios de Edge Delivery** de la página de Edge Delivery. También aparece un punto verde a la izquierda de la columna de estado **Verified**.

Ver también [Publicar contenido de AEM Author en Edge Delivery](#publish-from-aem-author).

### Exploración de un sitio de Edge Delivery creado con un clic {#explore-one-click-ed-site}

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú de la izquierda, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la página Edge Delivery, realice una de las siguientes acciones:

   | Qué explorar | Etapas |
   | --- | --- |
   | Repositorio de GitHub de un sitio | <ul><li>En el cuadro de lista **Sitios de Edge Delivery**, en el encabezado de la columna **Repositorio**, haga clic en la URL del sitio que acaba de crear.<br>Es posible que deba iniciar sesión en GitHub con su nombre de usuario o dirección de correo electrónico y su contraseña.</li> |
   | Publicar un sitio | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![Icono de verificación de publicación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publicar sitio** en el menú desplegable.<br>Aparece un mensaje que le informa de que la publicación del sitio se inició correctamente.</li></ul> |
   | Previsualización de un sitio publicado | <ul><li>En el cuadro de lista **Sitios de Edge Delivery**, en el encabezado de la columna **Nombre del sitio**, haga clic en la URL del sitio que acaba de crear y publicar.<br>En la barra de direcciones URL del explorador, tenga en cuenta que la URL del sitio termina con `.page`, lo que indica que está viendo una vista previa del sitio.</li><li>Para ver el sitio activo, cambie manualmente `.page` a `.live` en la barra de direcciones URL.</li></ul> |
   | Conceder a los usuarios acceso al repositorio de contenido en Google Drive | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![icono de adición de usuarios](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Obtener acceso al repositorio de contenido** en el menú desplegable.</li><li>En el cuadro de diálogo **`Add collaborators to your site`**, escriba la dirección de correo electrónico de un colaborador y haga clic en ![Icono de marca de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga añadiendo correos electrónicos de colaboradores, según sea necesario.</li><li>Cuando termine, haga clic en **Añadir colaborador**.</li><li>Para compartir el vínculo con sus colaboradores de contenido, en el cuadro de diálogo **Colaboración añadida correctamente**, haga clic en **Aceptar**.</li><li>En el cuadro de diálogo Colaboración añadida correctamente, haga clic en ![icono Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar el vínculo y compartirlo con sus colaboradores.<br>Antes de compartir el vínculo, confirme que los colaboradores han iniciado sesión con la dirección de correo electrónico asociada a sus respectivas cuentas de IMS. Si sus cuentas de correo electrónico de IMS no están disponibles, deberán utilizar la dirección de correo electrónico añadida como colaborador. De este modo, los colaboradores podrán acceder al vínculo y ver el contenido que se va a editar o actualizar en Google Drive.</li><li>Cuando termine de editar, haga clic en **Publicar sitio** en Cloud Manager, tal como se ha descrito anteriormente.<br>O bien, obtenga una vista previa de los cambios realizados, tal como se ha descrito anteriormente.</li></ul> |
   | Conceder a los usuarios acceso al repositorio base en GitHub | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![icono de código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Obtener acceso al repositorio base** en el menú desplegable.</li><li>En el cuadro de diálogo **Acceder al repositorio base del sitio**, escriba el nombre de usuario de GitHub de un colaborador y, a continuación, haga clic en ![icono de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga añadiendo nombres de usuario de GitHub, según sea necesario.</li><li>Cuando termine, haga clic en **Añadir colaborador**.</li>Los usuarios deben conceder acceso al nombre de usuario de su propio GitHub para ver el repositorio. |

## Publicación de contenido de AEM Author en Edge Delivery {#publish-from-aem-author}

Esta funcionalidad solo está disponible para sitios de Edge Delivery creados con la opción AEM Authoring.

Una vez creado el sitio de Edge Delivery y **verificado** en Cloud Manager, podrá crear y publicar contenido con el Editor universal de AEM.

**Para tener acceso al Editor universal desde Cloud Manager:**

1. En la ficha Edge Delivery, en la lista Sitios de Edge Delivery, busque el sitio.

   ![Publicar contenido de AEM Author en Edge Delivery](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. Haga clic en el vínculo **Source de contenido** en la fila del sitio. El vínculo abre la página Editor universal de AEM, desde la cual puede crear y editar contenido para el sitio.

**Para publicar contenido:**

* **De Cloud Manager** -

   1. En la ficha **Publicar entrega** de la página **Información general**, en la tarjeta **Entornos**, haga clic en el icono ![Información o Información](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) resaltado.

   1. En la ventana emergente informativa, seleccione **Haga clic para activar** y habilitar el aprovisionamiento del nivel de publicación en la interfaz de usuario de Cloud Manager.

      ![Haga clic para activar el aprovisionamiento del nivel de publicación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

   1. En el cuadro de diálogo Activar nivel de publicación, haga clic en **Activar**.

      ![Activar cuadro de diálogo Publicar nivel](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

      Una vez activado, el nivel de publicación se aprovisiona automáticamente. Como alternativa, el nivel de publicación se puede aprovisionar automáticamente si el autor intenta publicar contenido directamente desde la interfaz de usuario de AEM.

      Una vez que el nivel de publicación se ha activado y aprovisionado correctamente, el vínculo **Haga clic para activar** se atenúa o no está disponible.

* **De AEM Author**: en la interfaz de creación de AEM, haga clic en **Publicación rápida** para publicar contenido directamente en el sitio de Edge Delivery. El nivel de publicación no es necesario para esta operación cuando Edge Delivery administra la entrega.

Después de la publicación, obtiene una vista previa del contenido en la dirección URL `.page` del sitio o visualícelo en directo en la dirección URL `.live`.—>

