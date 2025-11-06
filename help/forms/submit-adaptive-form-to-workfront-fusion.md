---
title: Integración de Adobe Workfront Fusion con el envío de AEM Forms
description: Adobe Workfront Fusion le permite centrarse en nuevas tareas en lugar de centrarse en tareas repetitivas. Puede conectar Adobe Workfront Fusion a un formulario adaptable mediante el envío de formularios.
keywords: Envío de un formulario adaptable a Adobe Workfront Fusion, Integración de Adobe Workfront Fusion con el envío de AEM Forms, Adobe Workfront Fusion con AEM Forms, Workfront Fusion con AEM Forms, Conexión de Workfront Fusion a AEM Forms, AEM Forms y Workfront Fusion, ¿Cómo conectar Workfront Fusion con AEM Forms?, Conexión de Workfront Fusion a un formulario
topic-tags: author, developer
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 100%

---

# Enviar un formulario adaptable a Adobe Workfront Fusion

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html?lang=es) automatiza el proceso de repetición de las mismas tareas, como los flujos de trabajo de aprobación de documentos, el filtrado y la ordenación por correo electrónico, lo que le permite centrarse en nuevas tareas en lugar de en las recurrentes. Adobe Workfront Fusion incluye varios escenarios. Un escenario consiste en una serie de módulos que ejecutan la transferencia de datos entre aplicaciones y servicios web. En un escenario concreto, se añaden varios pasos (módulos) para automatizar una tarea.

Por ejemplo, con Workfront Fusion puede crear un escenario para recopilar datos con formularios adaptables, procesar los datos y enviarlos a un almacén de datos para su archivo. Una vez configurado un escenario, Workfront Fusion ejecuta automáticamente las tareas cada vez que se rellena un formulario, actualizando el almacén de datos sin problemas.

AEM Forms as a Cloud Service proporciona un conector predeterminado para conectarse y enviar un formulario adaptable a Adobe Workfront Fusion. El envío de un formulario a Adobe Workfront Fusion puede ofrecer varias ventajas:

* Permitía la transferencia perfecta de datos de los envíos de formularios a los flujos de trabajo de Workfront Fusion.
* Ayuda a automatizar varias tareas activadas por los envíos de formularios. Esto puede incluir el inicio de proyectos, la asignación de tareas a integrantes del equipo específicos, el envío de notificaciones y la actualización de los estados de los proyectos, todo sin intervención manual.
* Todos los envíos de formularios capturados en Workfront Fusion proporcionan una única fuente fiable para la información relacionada con el proyecto


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

<span> Este vídeo solo es aplicable a los componentes principales. Para componentes del editor universal o de base, consulte el artículo.</span>

## Requisitos previos para integrar AEM Forms con Adobe Workfront Fusion {#prerequisites}

Para establecer una conexión entre Workfront Fusion y AEM Forms, es necesario lo siguiente:

* Una [licencia de Workfront y Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html?lang=es) válida.
* Un usuario de AEM con derecho de acceso a la aplicación [Consola de desarrollo](https://my.cloudmanager.adobe.com/) para [recuperar las credenciales del servicio](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).

## Integración de AEM Forms con Adobe Workfront Fusion

### &#x200B;1. Crear un escenario de Workfront {#workflow-scenario}

Para crear un escenario de Workfront, realice los siguientes pasos:

1. [Crear un escenario](#create-scenario)
1. [Añadir un vínculo web a un escenario](#add-webhook)
1. [Añadir una conexión a un vínculo web](#add-connection)

#### Crear un escenario {#create-scenario}

Para crear un escenario:

1. Inicie sesión en su [cuenta de Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Haga clic en **[!UICONTROL Escenarios]** ![icono Compartir](/help/forms/assets/Smock_ShareAndroid_18_N.svg) en el panel izquierdo.
1. Haga clic en **[!UICONTROL Crear un nuevo escenario]** en la esquina superior derecha de la página. Aparece en pantalla una página para crear un nuevo escenario.
1. Seleccione **[!UICONTROL Nuevo escenario]** en la esquina superior izquierda de la página y escriba un nombre adecuado para el escenario.
1. Haga clic en el signo de interrogación y asegúrese de añadir el primer módulo como **[!UICONTROL AEM Forms]**.

   ![Añadir un módulo de AEM Forms](/help/forms/assets/workfront-aemforms.png)

   Aparece el cuadro de diálogo **[!UICONTROL Buscar eventos de formulario]**.

   >[!NOTE]
   >
   > Es obligatorio añadir el primer módulo como **[!UICONTROL AEM Forms]**.

1. Seleccione el cuadro de diálogo **[!UICONTROL Buscar eventos de formulario]** y aparecerá una ventana para añadir un webhook.

#### Añadir un webhook {#add-webhook}

![Añadir un webhook](/help/forms/assets/workfront-add-webhook.png)

Para añadir un webhook:

1. Haga clic en **[!UICONTROL Añadir]** y aparecerá un cuadro de diálogo **[!UICONTROL Añadir un webhook]**.
1. Especifique un nombre de webhook.

   >[!NOTE]
   >
   > Se recomienda elegir cuidadosamente el nombre del webhook, ya que el nombre del webhook especificado aparece en la instancia de AEM.

1. Haga clic en **[!UICONTROL Añadir]** para añadir una nueva conexión. Aparece el cuadro de diálogo **[!UICONTROL Crear una conexión]**.

>[!NOTE]
>
> Asegúrese de que la cuenta técnica sea miembro del grupo **usuarios de formularios**; de lo contrario, se producirá un error al añadir un webhook.

#### Añadir una conexión a un webhook {#add-connection}

![Añadir una conexión](/help/forms/assets/workfront-add-connection.png)

Para añadir una conexión, haga lo siguiente:

1. Especifique un **[!UICONTROL Nombre de conexión]** en el cuadro de diálogo **[!UICONTROL Crear una conexión]**.

1. Seleccione **Entorno** y **Tipo** en la lista desplegable.

1. Introduzca la **URL de instancia**.

   >[!NOTE]
   >
   > La URL de instancia es la dirección web única que apunta a una instancia de AEM Forms específica.

   Puede recuperar las [credenciales de servicio de Developer console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es) necesarias para crear una conexión.

1. Reemplazar `ims-na1.adobelogin.com` en el **Punto final de IMS** con el valor de **imsEndpoint** desde las credenciales del servicio en la Developer console.

   >[!NOTE]
   >
   > Conserve el `https://` en el cuadro de texto **Punto final de IMS** al añadir la URL `imsEndpoint`.

1. Especifique los siguientes valores en el cuadro de diálogo **[!UICONTROL Crear una conexión]**:
   * Especifique **ID de cliente** con valor de **clientId** en las credenciales del servicio en Developer console.
   * Especifique **Secreto del cliente** con valor de **clientSecret** en las credenciales del servicio en Developer console.
   * Especifique **ID de cuenta técnica** con valor de **id** en las credenciales del servicio en Developer console.
   * Especifique **ID de organización** con valor de **org** en las credenciales del servicio en Developer console.
   * **Meta ámbitos** con valor de **metascopios** en las credenciales del servicio en Developer console.
   * **Claves privadas** con valor de **privateKey** en las credenciales del servicio en Developer console.

   >[!NOTE]
   >
   >* Para **Clave privada**, quitar `\r\n` de su valor.
   >  Por ejemplo, si el valor de la clave privada es:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, y después de quitar el `\r\n` desde la clave privada, la clave tendría el siguiente aspecto, y ambos valores aparecerían en una línea independiente:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* También tiene la opción de recuperar una clave privada o un certificado del archivo seleccionando el botón **Extraer**.

1. Haga clic en **Continuar**.

   La conexión creada aparecerá en la lista desplegable de la **[!UICONTROL Conexión]** en el cuadro de diálogo **[!UICONTROL Añadir un webhook]**.

1. Seleccione la conexión creada **[!UICONTROL Conexión]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL OK]** y guarde los cambios para el escenario.
1. Para activar el escenario, haga clic en el botón de alternancia ON/OFF del editor de escenarios.

>[!NOTE]
>
> Si no activa el escenario de Workfront, no se detectará el envío del formulario y establecer la acción de envío en Workfront provocará un envío fallido.

### &#x200B;2. Configurar la acción de envío de un formulario adaptable para Workfront Fusion

>[!BEGINTABS]

>[!TAB Componente base]

Para configurar la acción de envío de un formulario adaptable basado en componentes de base para Workfront Fusion:

1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Invocar un escenario de WorkFront Fusion]**.
   ![Acción de envío para Workfront Fusion](/help/forms/assets/workfront-fusion-fc.png)

1. Seleccione **[!UICONTROL Escenario de Workfront Fusion]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Listo]**.


>[!TAB Componente principal]

Para configurar la acción de envío de un formulario adaptable basado en componentes principales para Workfront Fusion:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Invocar un escenario de WorkFront Fusion]**.

   ![Acción de envío para Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)
1. Seleccione **[!UICONTROL Escenario de Workfront Fusion]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Listo]**.

>[!TAB Editor universal]

Para configurar la acción de envío de un formulario adaptable creado con el editor universal:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.
Aparece el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades del formulario** en la interfaz del editor universal, habilite la extensión **Editar propiedades del formulario** en Extension Manager.
   > * Consulte el artículo [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar las extensiones del editor universal.

1. Haga clic en la pestaña **Envío** y seleccione la acción de envío **[!UICONTROL Invocar un escenario de WorkFront Fusion]**.

   ![Acción de envío para Workfront Fusion](/help/forms/assets/workfront-fusion-ue.png)

1. Seleccione **[!UICONTROL Escenario de Workfront Fusion]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

>[!ENDTABS]

## Prácticas recomendadas {#best-practices}

* Se recomienda elegir cuidadosamente el nombre del webhook, ya que no hay forma de obtener el nombre del escenario en la instancia de AEM. En caso de que cambie el nombre de webhook en el futuro, no se reflejará en la lista desplegable de acción de envío de AEM Forms.
* Un escenario puede tener varios vínculos de webhook, pero a la vez solo hay un vínculo de webhook activo. Se recomienda eliminar el webhook no vinculado, de modo que no aparezca en la lista desplegable de acciones de envío de AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Artículos relacionados

{{af-submit-action}}