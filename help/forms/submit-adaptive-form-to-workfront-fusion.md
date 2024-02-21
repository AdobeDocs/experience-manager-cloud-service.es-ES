---
title: Integración de Adobe Workfront Fusion con AEM Forms Submission
description: Adobe Workfront Fusion le permite centrarse en nuevas tareas en lugar de centrarse en tareas repetitivas. Puede conectar Adobe Workfront Fusion a un formulario adaptable mediante el envío de formularios.
keywords: Enviar un formulario adaptable a Adobe Workfront Fusion, Integración de Adobe Workfront Fusion con AEM Forms Submission, Adobe Workfront Fusion con AEM Forms, Workfront Fusion con AEM Forms, Conexión de Workfront Fusion a AEM Forms, AEM Forms y Workfront Fusion, Conexión de Workfront Fusion con AEM Forms?, Conexión de Workfront Fusion a un formulario
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 8923bfbb0e46961485ff360c0135ebdde6d8cab3
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 6%

---

# Envío de un formulario adaptable a Adobe Workfront Fusion

<span class="preview"> La función está disponible en el programa de usuarios pioneros. Puede escribir a aem-forms-early-adopter-program@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta capacidad. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) automatiza el proceso de repetición de las mismas tareas, como los flujos de trabajo de aprobación de documentos, el filtrado y la ordenación por correo electrónico, lo que le permite centrarse en nuevas tareas en lugar de en las recurrentes. Adobe Workfront Fusion incluye varios escenarios. Un escenario consiste en una serie de módulos que ejecutan la transferencia de datos entre aplicaciones y servicios web. En un escenario concreto, se agregan varios pasos (módulos) para automatizar una tarea.

Por ejemplo, con Workfront Fusion puede crear un escenario para recopilar datos con formularios adaptables, procesar los datos y enviarlos a un almacén de datos para su archivo. Una vez configurado un escenario, Workfront Fusion ejecuta automáticamente las tareas cada vez que un usuario rellena un formulario, actualizando el almacén de datos sin problemas.

AEM Forms as a Cloud Service proporciona un conector OOTB para conectarse y enviar un formulario adaptable a Adobe Workfront Fusion. El envío de un formulario a Adobe Workfront Fusion puede ofrecer varias ventajas:
* Permite la transferencia perfecta de datos de los envíos de formularios a los flujos de trabajo de Workfront Fusion.
* Ayuda a automatizar varias tareas activadas por los envíos de formularios. Esto puede incluir el inicio de proyectos, la asignación de tareas a miembros específicos del equipo, el envío de notificaciones y la actualización de los estados de los proyectos, todo sin intervención manual.
* Todos los envíos de formularios capturados en Workfront Fusion proporcionan una única fuente fiable para la información relacionada con el proyecto


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## Requisitos previos para integrar AEM Forms con Adobe Workfront Fusion {#prerequisites}

Para establecer una conexión entre Workfront Fusion y AEM Forms, es necesario lo siguiente:

* Un válido [Licencia de Workfront y Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* AEM Un usuario con derecho de acceso a la aplicación [Consola de desarrollador](https://my.cloudmanager.adobe.com/) hasta [recuperar las credenciales del servicio](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).

## Integración de AEM Forms con Adobe Workfront Fusion

### 1. Crear un escenario de Workfront {#workflow-scenario}

Para crear un escenario de Workfront, realice los siguientes pasos:

1. [Creación de un escenario](#create-scenario)
1. [Agregar un vínculo web a un escenario](#add-webhook)
1. [Adición de una conexión a un vínculo web](#add-connection)

#### Creación de un escenario {#create-scenario}

Para crear un escenario:
1. Inicie sesión en su [Cuenta de Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Clic **[!UICONTROL Escenarios]** ![Icono Compartir](/help/forms/assets/Smock_ShareAndroid_18_N.svg) en el panel izquierdo.
1. Clic **[!UICONTROL Crear un nuevo escenario]** en la esquina superior derecha de la página. Aparece en pantalla una página para crear un nuevo escenario.
1. Seleccionar **[!UICONTROL Nuevo escenario]** en la esquina superior izquierda de la página y escriba un nombre adecuado para el escenario.
1. Haga clic en el signo de interrogación y asegúrese de agregar el primer módulo como **[!UICONTROL AEM Forms]**.

   ![Añadir un módulo de AEM Forms](/help/forms/assets/workfront-aemforms.png)

   El **[!UICONTROL Buscar eventos de formulario]** aparece el cuadro de diálogo.

   >[!NOTE]
   >
   > Es obligatorio añadir el primer módulo como **[!UICONTROL AEM Forms]**.

1. Seleccione el **[!UICONTROL Buscar eventos de formulario]** y aparecerá una ventana para agregar un webhook.

#### Añadir un webhook {#add-webhook}

![Añadir un webhook](/help/forms/assets/workfront-add-webhook.png)

Para agregar un webhook:

1. Clic **[!UICONTROL Añadir]** y una **[!UICONTROL Añadir un webhook]** aparece el cuadro de diálogo.
1. Especifique un nombre de webhook.

   >[!NOTE]
   >
   > AEM Se recomienda elegir cuidadosamente el nombre del webhook, ya que el nombre del webhook especificado aparece en la instancia de.

1. Clic **[!UICONTROL Añadir]** para agregar una nueva conexión. El **[!UICONTROL Crear una conexión]** aparece el cuadro de diálogo.

#### Añadir una conexión a un webhook {#add-connection}

![Añadir una conexión](/help/forms/assets/workfront-add-connection.png)

Para agregar una conexión:

1. Especifique un **[!UICONTROL Nombre de conexión]** en el **[!UICONTROL Crear una conexión]** Cuadro de diálogo.

1. Seleccionar **Entorno** y **Tipo** en la lista desplegable.

1. Introduzca el **URL de instancia**.

   >[!NOTE]
   >
   > La URL de instancia es la dirección web única que apunta a una instancia de AEM Forms específica.

   Puede recuperar la variable [credenciales de servicio de la consola de desarrollador](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es) necesario para crear una conexión.

1. Reemplazar `ims-na1.adobelogin.com` en el **Extremo de IMS** con el valor de **imsEndpoint** desde las credenciales del servicio en la consola de desarrollador.

   >[!NOTE]
   >
   > Conserve el `https://` en el **Extremo de IMS** cuadro de texto al añadir `imsEndpoint` URL.

1. Especifique los siguientes valores en la **[!UICONTROL Crear una conexión]** Cuadro de diálogo:
   * Especificar **ID de cliente** con valor de **clientId** desde las credenciales del servicio en la consola de desarrollador.
   * Especificar **Secreto del cliente** con valor de **clientSecret** desde las credenciales del servicio en la consola de desarrollador.
   * Especificar **ID de cuenta técnica**  con valor de **id** desde las credenciales del servicio en la consola de desarrollador.
   * Especificar **ID de organización**  con valor de **org** desde las credenciales del servicio en la consola de desarrollador.
   * **Meta ámbitos**  con valor de **metascopios** desde las credenciales del servicio en la consola de desarrollador.
   * **Claves privadas**  con valor de **privateKey** desde las credenciales del servicio en la consola de desarrollador.

   >[!NOTE]
   >
   >* Para **Clave privada**, eliminar `\r\n` de su valor.
   >  Por ejemplo, si el valor de la clave privada es:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, y después de quitar el `\r\n` desde la clave privada, la clave tendría el siguiente aspecto, y ambos valores aparecerían en una línea independiente:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* También tiene la opción de recuperar una clave privada o un certificado del archivo seleccionando la **Extract** botón.

1. Haga clic en **Continuar**.

   La conexión creada aparecerá en la lista desplegable de la **[!UICONTROL Conexión]** en el **[!UICONTROL Añadir un webhook]** Cuadro de diálogo.

1. Seleccione la conexión creada **[!UICONTROL Conexión]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Guardar]**.
1. Clic **[!UICONTROL OK]** y guarde los cambios para el escenario.
1. Para activar el escenario, haga clic en el botón de alternancia ENCENDIDO/APAGADO del editor de escenarios.

>[!NOTE]
>
> Si no activa el escenario de Workfront, no se detectará el envío del formulario y establecer la acción de envío en Workfront provocará un envío fallido.

### 2. Configurar la acción de envío de un formulario adaptable para Workfront Fusion

Puede configurar la acción de envío para Workfront Fusion para:
* [Nuevo Forms adaptable](#new-af-submit-action)
* [Formularios adaptables existentes](#existing-af-submit-action)

#### Configuración de la acción de envío del nuevo formulario adaptable para Workfront Fusion {#new-af-submit-action}

Para configurar la acción de envío del nuevo formulario adaptable para Workfront Fusion:

1. AEM Inicie sesión en la instancia de.
1. Ir a **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]** > **[!UICONTROL Crear]** > **[!UICONTROL Formulario adaptable]**. El **[!UICONTROL Crear formulario]** aparece el asistente.
1. Seleccione una plantilla de formulario adaptable de la **[!UICONTROL Origen]** pestaña.
1. Seleccione una temática del **[!UICONTROL Estilo]** pestaña.

   ![Acción de envío para Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Seleccione el **[!UICONTROL Invocar un escenario de Workfront Fusion]** desde el **[!UICONTROL Envío]** pestaña.
1. Seleccione el webhook creado en **[!UICONTROL Opciones]** en la pestaña **[!UICONTROL Propiedades]** ventana.

   >[!NOTE]
   >
   > El nombre del webhook del escenario de Workfront aparece en la **Opciones** lista desplegable.

1. Haga clic en **[!UICONTROL Crear]**.
1. Especifique el nombre del nuevo formulario adaptable y haga clic en **[!UICONTROL Crear]**.

#### Configurar la acción de envío de un formulario adaptable existente para Workfront Fusion {#existing-af-submit-action}

Para configurar la acción de envío de un formulario adaptable existente para Workfront Fusion:

1. AEM Inicie sesión en la instancia de.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un formulario adaptable y ábralo en modo de edición.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.

   ![Acción de envío para Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Abra la pestaña **[!UICONTROL Envío]**.
1. Seleccione el **[!UICONTROL Acción de envío]** as **[!UICONTROL Invocar un escenario de Workfront Fusion]**
1. Seleccionar **[!UICONTROL Escenario de Workfront Fusion]** en la lista desplegable.
1. Haga clic en **[!UICONTROL Listo]**.

## Prácticas recomendadas {#best-practices}

* AEM Se recomienda elegir el nombre del webhook con cuidado, ya que no hay forma de obtener el nombre del escenario en la instancia de. En caso de que cambie el nombre del gancho web en el futuro, esto no se reflejará en la lista desplegable de acción de envío de AEM Forms.
* Un escenario puede tener varios vínculos de gancho web, pero a la vez solo hay un vínculo activo. Se recomienda eliminar el webhook no vinculado, de modo que no aparezca en la lista desplegable de acciones de envío de AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Artículos relacionados

{{af-submit-action}}