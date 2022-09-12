---
title: Flujo de trabajo centrado en Forms en OSGi
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Uso [!DNL AEM Forms] Flujo de trabajo para automatizar y construir rápidamente revisiones y aprobaciones, para iniciar document services
seo-description: Use [!DNL AEM Forms] Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# Flujo de trabajo centrado en Forms en OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

Las empresas recopilan datos de cientos y miles de formularios, varios sistemas back-end y fuentes de datos en línea o sin conexión. También tienen un conjunto dinámico de usuarios para tomar decisiones sobre los datos, lo que implica procesos de revisión y aprobación iterativos.

Junto con los flujos de trabajo de revisión y aprobación para audiencias internas y externas, las grandes organizaciones y empresas tienen tareas repetitivas. Por ejemplo, convertir un documento PDF a otro formato. Cuando se realizan manualmente, estas tareas tardan mucho tiempo y recursos. Las empresas también tienen requisitos legales para firmar digitalmente un documento y archivar datos de formulario para su uso posterior en formatos predefinidos.

## Introducción al flujo de trabajo centrado en Forms en OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puede utilizar AEM Flujos de trabajo para crear rápidamente flujos de trabajo adaptables basados en Forms. Estos flujos de trabajo se pueden utilizar para revisiones y aprobaciones, flujos de procesos empresariales, para iniciar document services, integrarse con el flujo de trabajo de firmas de Adobe Sign y operaciones similares. Por ejemplo, el procesamiento de la aplicación de tarjeta de crédito, el empleado deja los flujos de trabajo de aprobación y guarda un formulario como documento de PDF. Además, estos flujos de trabajo se pueden utilizar dentro de una organización o entre cortafuegos de red.

Con el flujo de trabajo centrado en Forms en OSGi, puede crear e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la capacidad de administración de procesos completa en la pila JEE. El desarrollo y la administración de flujos de trabajo utilizan las funciones conocidas AEM Workflow y AEM Inbox . Los flujos de trabajo forman la base de la automatización de los procesos del negocio en el mundo real que abarcan múltiples sistemas de software, redes, departamentos e incluso organizaciones.

Una vez configurados, estos flujos de trabajo se pueden activar manualmente para completar un proceso definido o ejecutarse programáticamente cuando los usuarios envían un formulario <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

Flujo de trabajo centrado en Forms en OSGi se amplía [Bandeja de entrada AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) y proporciona componentes adicionales (pasos) para AEM editor de flujo de trabajo para agregar compatibilidad con [!DNL AEM Forms]Flujos de trabajo centrados en . <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

Todo [!DNL AEM Forms] los pasos del flujo de trabajo admiten el uso de variables. Las variables permiten realizar pasos en el flujo de trabajo para guardar y pasar metadatos por varios pasos durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. También puede crear colecciones de variables (matriz) para almacenar varias instancias de datos relacionados con el mismo tipo. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en función del valor que contiene o para almacenar información que se necesite más adelante en un proceso. Para obtener más información sobre el uso de variables en estos componentes (pasos) de flujo de trabajo centrados en Forms, consulte [Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos](aem-forms-workflow-step-reference.md). Para obtener información sobre la creación y administración de variables, consulte [Variables en flujos de trabajo AEM](variable-in-aem-workflows.md).

En el diagrama siguiente se describe el procedimiento de extremo a extremo para crear, ejecutar y supervisar un flujo de trabajo centrado en Forms en OSGi.

![introducción a aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de comenzar {#before-you-start}

* Un flujo de trabajo es una representación de un proceso empresarial real. Mantenga su proceso de negocio real y lista de los participantes del proceso de negocio preparados. Además, mantenga el material colateral (Forms adaptable, Documentos del PDF, etc.) listo antes de empezar a crear un flujo de trabajo.
* Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM y ayudan a informar sobre el progreso del flujo de trabajo. Divida el proceso empresarial en etapas lógicas.
* Puede configurar el paso asignar tarea de AEM Flujos de trabajo para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Entonces, [habilitar notificaciones por correo electrónico](#configure-email-service).
* Un flujo de trabajo también puede utilizar el signo de Adobe para las firmas digitales. Si planea utilizar Adobe Sign en un flujo de trabajo, la variable [configurar Adobe Sign para [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) antes de utilizarla en un flujo de trabajo.

## Creación de un modelo de flujo de trabajo {#create-a-workflow-model}

Un modelo de flujo de trabajo consiste en la lógica y el flujo de un proceso empresarial. Se compone de una serie de pasos. Estos pasos son componentes AEM. Puede ampliar los pasos del flujo de trabajo con parámetros y secuencias de comandos para proporcionar más funcionalidad y control, según sea necesario. [!DNL AEM Forms] proporciona algunos pasos además de AEM pasos disponibles de forma predeterminada. Para obtener una lista detallada de AEM y [!DNL AEM Forms] pasos, consulte [Referencia de pasos del flujo de trabajo AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) y [Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos](aem-forms-workflow.md).

AEM proporciona una interfaz de usuario intuitiva para crear un modelo de flujo de trabajo siguiendo los pasos del flujo de trabajo proporcionados. Para obtener instrucciones paso a paso sobre la creación de un modelo de flujo de trabajo, consulte [Creación de modelos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows). El siguiente ejemplo proporciona instrucciones paso a paso para crear un modelo de flujo de trabajo para un flujo de trabajo de aprobación y revisión:

>[!NOTE]
>
>Debe ser miembro del grupo de editor de flujo de trabajo para crear o editar un modelo de flujo de trabajo.

### Creación de un modelo para un flujo de trabajo de aprobación y revisión {#create-a-model-for-an-approval-and-review-workflow}

El flujo de trabajo de aprobación y revisión corresponde a las tareas que requieren la intervención humana para tomar decisiones. En el siguiente ejemplo se crea un modelo de flujo de trabajo para una aplicación de préstamo hipotecario que debe rellenar un agente bancario de la oficina principal. Una vez completada la solicitud, se envía para su aprobación. Posteriormente, la solicitud aprobada se envía al solicitante para que la firme utilizando Adobe Sign.

El ejemplo está disponible como paquete adjunto a continuación. Importe e instale el ejemplo mediante el administrador de paquetes. También puede realizar los siguientes pasos para crear manualmente el modelo de flujo de trabajo para la aplicación:

En el ejemplo se crea un modelo de flujo de trabajo con una aplicación hipotecaria que se rellenará con un agente bancario de la oficina principal. Una vez completada, la solicitud se envía para su aprobación. Posteriormente, la aplicación aprobada se envía al cliente para que la firme mediante Adobe Sign. Puede importar e instalar el ejemplo mediante el administrador de paquetes.

[Obtener archivo](assets/example-mortgage-loan-application.zip)

1. Abra la consola Modelos de flujo de trabajo . La dirección URL predeterminada es `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Select **Crear**, luego **Crear modelo**. Aparecerá el cuadro de diálogo Agregar modelo de flujo de trabajo.
1. Introduzca la variable **Título** y **Nombre** (opcional). Por ejemplo, una aplicación hipotecaria. Puntee **Listo**.
1. Seleccione el modelo de flujo de trabajo recién creado y pulse **Editar**. Ahora, puede agregar pasos de flujo de trabajo para crear lógica empresarial. La primera vez que se crea un modelo de flujo de trabajo, contiene:

   * Los pasos: Inicio de flujo y Fin de flujo. Estos pasos representan el principio y el final del flujo de trabajo. Estos pasos son obligatorios y no se pueden editar ni eliminar.
   * Un ejemplo de paso de participante denominado Paso 1. Este paso está configurado para asignar un elemento de trabajo al usuario administrador. Elimine este paso.

1. Habilitar las notificaciones por correo electrónico. Puede configurar el flujo de trabajo centrado en Forms en OSGi para enviar notificaciones por correo electrónico a los usuarios o a los usuarios asignados. Realice las siguientes configuraciones para habilitar las notificaciones por correo electrónico:

   1. Vaya a AEM administrador de configuración en `https://[server]:[port]/system/console/configMgr`.
   1. Abra el **[!UICONTROL Day CQ Mail Service]** configuración. Especifique un valor para la variable **[!UICONTROL Nombre de host del servidor SMTP]**, **[!UICONTROL puerto del servidor SMTP,]** y **[!UICONTROL Dirección &quot;De&quot;]** campos. Haga clic en **[!UICONTROL Guardar]**.
   1. Abra el **[!UICONTROL Externalizador de vínculos de CQ de día]** configuración. En el **[!UICONTROL Dominios]** especifique el nombre de host/dirección IP real y el número de puerto para las instancias locales, de autor y de publicación. Haga clic en **[!UICONTROL Guardar]**.

1. Cree etapas de flujo de trabajo. Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM y en el progreso del informe del flujo de trabajo.

   Para definir un escenario, pulse el botón ![info-círculo](assets/info-circle.png) para abrir las propiedades del modelo de flujo de trabajo, abra **Etapas** , añada etapas para el modelo de flujo de trabajo y pulse **Guardar y cerrar**. Para la aplicación hipoteca de ejemplo, cree etapas: solicitud de préstamo, estado de solicitud de préstamo, documentos a firmar y documento de préstamo firmado.

1. Arrastre y suelte la **Asignar tarea** pasa el explorador al modelo de flujo de trabajo. Hacerlo el primer paso del modelo.

   El componente Asignar tarea asigna la tarea, creada por el flujo de trabajo, a un usuario o grupo. Junto con asignar la tarea, puede utilizar el componente para especificar un formulario adaptable o un PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar los datos introducidos por los usuarios y un PDF no interactivo o un formulario adaptable de solo lectura se utiliza para revisar solo los flujos de trabajo.

   También puede utilizar el paso para controlar el comportamiento de la tarea. Por ejemplo, al crear un documento de registro automático, asigne la tarea a un usuario o grupo específico, la ruta de los datos enviados, la ruta de los datos que se van a rellenar previamente y las acciones predeterminadas. Para obtener información detallada sobre las opciones del paso asignar tarea, consulte [Flujo de trabajo centrado en Forms en OSGi: referencia de los pasos](aem-forms-workflow.md) documento.

   ![workflow-editor](assets/workflow-editor.png)

   Para el ejemplo de la aplicación hipoteca, configure el paso asignar tarea para utilizar un Formulario adaptable de solo lectura y mostrar el Documento del PDF una vez que se haya completado la tarea. Además, seleccione el grupo de usuarios autorizado para aprobar la solicitud de préstamo. En el **Acciones** , desactive la **Submit** . Cree un **actionTaken** del tipo de datos String y especifique la variable como **Variable de ruta**. Por ejemplo, actionTaken. Además, añada las rutas Aprobar y Rechazar . Las rutas se muestran como acciones independientes (botones) en AEM Bandeja de entrada. El flujo de trabajo selecciona una rama en función de la acción (botón) que toca un usuario.

   Puede importar el paquete de ejemplo, disponible para descargar al principio de la sección, para el conjunto completo de valores de todos los campos del paso asignar tarea configurado por ejemplo aplicación de hipoteca.

1. Arrastre y suelte el componente OR Split desde el navegador de pasos al modelo de flujo de trabajo. La división OR crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

   Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

   Utilice el editor de expresiones para crear expresiones de enrutamiento para las ramas 1 y 2. Estas expresiones de enrutamiento ayudan a elegir una rama basada en la acción del usuario en AEM Bandeja de entrada.

   **Expresión de enrutamiento para la rama 1**

   Cuando el usuario toca **Aprobar** en AEM bandeja de entrada, se activa la rama 1.

   ![Ejemplo de división OR](assets/orsplit_branch1_active_new.png)

   **Expresión de enrutamiento para la rama 2**

   Cuando el usuario toca **Rechazar** en AEM bandeja de entrada, se activa la rama 2.

   ![Ejemplo de división OR](assets/orsplit_branch2_active_new.png)

   Para obtener información sobre la creación de expresiones de enrutamiento mediante variables, consulte [Variables en [!DNL AEM Forms] flujos de trabajo](variable-in-aem-workflows.md).

1. Añada otros pasos del flujo de trabajo para crear la lógica empresarial.

   Para el ejemplo de hipoteca, añada un documento de registro generado, dos pasos de asignación de tareas y un paso de documento de signo a la rama 1 del modelo, como se muestra en la imagen siguiente. Un paso de tarea de asignación es mostrar y enviar **documentos de préstamo que se firmarán al solicitante** y otro componente de tarea de asignación es **para mostrar documentos firmados**. Además, añada un componente de tarea de asignación a la rama 2. Se activa cuando un usuario pulsa Rechazar en AEM bandeja de entrada.

   Para el conjunto completo de valores de todos los campos de los pasos de tarea de asignación, el paso Documento de registro y el paso de documento de firma configurado para, por ejemplo, la aplicación hipoteca, importe el paquete de ejemplo, disponible para su descarga en el inicio de esta sección.

   El modelo de flujo de trabajo está listo. Puede iniciar el flujo de trabajo mediante varios métodos. Para obtener más información, consulte [Iniciar un flujo de trabajo centrado en Forms en OSGi](#launch).

   ![workflow-editor-hipoteca](assets/workflow-editor-mortgage.png)

## Crear una aplicación de flujo de trabajo centrada en Forms {#create-a-forms-centric-workflow-application}

La aplicación es el formulario adaptable asociado al flujo de trabajo. Cuando una aplicación se envía a través de la bandeja de entrada, inicia el flujo de trabajo asociado. Para que un flujo de trabajo de Forms esté disponible como aplicación en AEM Bandeja de entrada y [!DNL AEM Forms] Para crear una aplicación de flujo de trabajo, haga lo siguiente:

>[!NOTE]
>
>Debe ser miembro del grupo fd-administrator para poder crear y administrar aplicaciones de flujo de trabajo.

1. En la instancia de autor de AEM, vaya a ![herramientas-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Administrar aplicación de flujo de trabajo]** y toques **[!UICONTROL Crear]**.
1. En la ventana Crear aplicación de flujo de trabajo , introduzca entradas para los campos siguientes y pulse **Crear**. Se crea una nueva aplicación que aparece en la pantalla Aplicaciones de flujo de trabajo .

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>El título está visible en AEM Bandeja de entrada y ayuda a los usuarios a elegir una aplicación. Manténgalo descriptivo. Por ejemplo, la aplicación de apertura de cuentas de guardado.<br /> </td>
  </tr>
  <tr>
   <td>Nombre </td>
   <td>Especifique el nombre de la aplicación. Todos los caracteres que no sean alfabetos, números, guiones y guiones bajos se sustituyen por guiones. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>La descripción está visible en AEM Bandeja de entrada. Proporcione información detallada sobre la aplicación en los campos de descripción. Por ejemplo, Finalidad de la aplicación.<br /> </td>
  </tr>
  <tr>
   <td>Formulario adaptable</td>
   <td><p>Especifique la ruta de un formulario adaptable. Cuando un usuario inicia una aplicación, se muestra el formulario adaptable especificado.</p> <p><strong>Nota</strong>: Las aplicaciones de flujo de trabajo no admiten formularios ni documentos de PDF que tengan más de una página o que requieran desplazamiento en Apple iPad. Cuando se abre una aplicación en Apple iPad y el formulario adaptable o el documento del PDF es más largo que una página, se pierden los campos y el contenido del formulario de la segunda página.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acceso</td>
   <td><p>Seleccione un grupo. La aplicación solo está visible en AEM Bandeja de entrada para los miembros del grupo seleccionado. La opción de grupo de acceso hace que todos los grupos de la variable [!DNL workflow-users] grupo disponible para selección. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servicio de rellenado previo</td>
   <td>Seleccione un <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servicio prefill</a> para el formulario adaptable.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de flujo de trabajo</td>
   <td>Seleccione un <a href="aem-forms-workflow.md#create-a-workflow-model">modelo de flujo de trabajo</a> para la aplicación. Un modelo de flujo de trabajo consiste en la lógica y el flujo del proceso empresarial. </td>
  </tr>
  <tr>
   <td>Ruta del archivo de datos</td>
   <td>Especifique la ruta del archivo de datos en el repositorio crx. La ruta es relativa a la carga útil del formulario adaptable y contiene el nombre del archivo de datos. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Ruta de archivos adjuntos</td>
   <td>Especifique la ruta de la carpeta de archivos adjuntos en el repositorio crx. La ruta de acceso de datos adjuntos es relativa a la ubicación de carga útil. Por ejemplo, [carga útil]/data.xml. </td>
  </tr>
  <tr>
   <td>Documento de ruta de registro</td>
   <td>Especifique la ruta del archivo Document of Record en el repositorio crx. La ruta es relativa a la ubicación de carga útil del formulario adaptable. Incluya siempre el nombre completo del archivo, incluida la extensión, si corresponde. Por ejemplo, [carga útil]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar un flujo de trabajo centrado en Forms en OSGi {#launch}

Puede iniciar o déclencheur un flujo de trabajo centrado en Forms mediante:

* [Envío de una aplicación desde AEM bandeja de entrada](#inbox)
* [Envío de una aplicación desde [!DNL AEM Forms] Aplicación](#afa)

* [Envío de un formulario adaptable](#af)
* [Uso de la carpeta vigilada](#watched)

* [Envío de una comunicación interactiva o una carta](#letter)

### Envío de una aplicación desde AEM bandeja de entrada {#inbox}

La aplicación de flujo de trabajo que ha creado está disponible como una aplicación en la bandeja de entrada. Usuarios que son miembros de [!DNL workflow-users] puede rellenar y enviar la aplicación que déclencheur el flujo de trabajo asociado. Para obtener información sobre el uso de AEM Bandeja de entrada para enviar aplicaciones y administrar tareas, consulte [Administrar aplicaciones y tareas de Forms en AEM bandeja de entrada](manage-applications-inbox.md).

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and allows you to make changes to the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### Envío de un formulario adaptable {#af}

Puede configurar las acciones de envío de un formulario adaptable para iniciar un flujo de trabajo al enviar el formulario adaptable. Forms adaptable proporciona la variable **Invocar un flujo de trabajo AEM** Enviar acción para iniciar un flujo de trabajo al enviar un formulario adaptable. Para obtener información detallada sobre la acción de envío, consulte [Configuración de la acción de envío](configuring-submit-actions.md). Para enviar un formulario adaptable a través de la variable [!DNL AEM Forms] aplicación, habilite Sincronizar con [!DNL AEM Forms] Aplicación en las propiedades del formulario adaptable.

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Tap **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Tap **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### Purgar instancias de flujo de trabajo {#purge-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujo de trabajo, por lo que puede depurar con regularidad las instancias de flujo de trabajo completadas o en ejecución desde el repositorio. Para obtener información detallada, consulte [Depuración regular de instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=es) depuración de instancias de flujo de trabajo
