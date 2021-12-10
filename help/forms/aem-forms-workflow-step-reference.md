---
title: '¿Cómo asignar un flujo de trabajo a otro usuario, enviar correo electrónico, utilizar Adobe Sign en un flujo de trabajo? '
description: Los flujos de trabajo centrados en Forms le permiten crear rápidamente flujos de trabajo adaptables basados en Forms. Puede utilizar Adobe Sign para firmar documentos por correo electrónico, crear procesos empresariales basados en formularios, recuperar y enviar datos a varios orígenes de datos y enviar notificaciones por correo electrónico
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '5377'
ht-degree: 0%

---

# Flujos de trabajo AEM centrados en Forms: referencia de pasos {#forms-centric-workflow-on-osgi-step-reference}

Los modelos de flujo de trabajo se utilizan para convertir una lógica empresarial en proceso repetitivo automatizado. Un modelo le ayuda a definir y ejecutar una serie de pasos. También puede definir propiedades del modelo, como si el flujo de trabajo es transitorio o utiliza varios recursos. Puede [incluir varios pasos AEM Workflow en un modelo para lograr la lógica empresarial](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Pasos centrados en Forms {#forms-workflow-steps}

Los pasos del flujo de trabajo centrados en Forms realizan operaciones específicas de AEM Forms en un flujo de trabajo AEM. Estos pasos le permiten crear rápidamente un flujo de trabajo centrado en Forms basado en Forms adaptable en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, procesos empresariales internos y entre cortafuegos. También puede seguir los pasos del Forms Workflow para:

* Cree procesos empresariales, flujos de trabajo posteriores al envío y flujos de trabajo back-end para administrar los procesos de inscripción.

* Cree y asigne tareas a un usuario o grupo.

* Uso [!DNL Adobe Sign] en un flujo de trabajo AEM para enviar un documento para firmar.

* Genere un documento de registro bajo demanda o en envío de formulario.

* Conecte un modelo de flujo de trabajo con varias fuentes de datos para guardar y recuperar datos fácilmente.

* Utilice el paso de correo electrónico para enviar correos electrónicos de notificación y otros archivos adjuntos al finalizar una acción y al principio o al final de un flujo de trabajo.


## Asignar paso de tarea {#assign-task-step}

El paso asignar tarea crea un elemento de trabajo y lo asigna a un usuario o grupo. Junto con asignar la tarea, el componente también especifica el formulario adaptable o el PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar los datos introducidos por los usuarios y un PDF no interactivo o un formulario adaptable de solo lectura se utiliza para revisar solo los flujos de trabajo.

También puede utilizar el componente para controlar el comportamiento de la tarea. Por ejemplo, crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, especificar la ruta de los datos enviados, especificar la ruta de los datos que se van a rellenar previamente y especificar las acciones predeterminadas. El paso Asignar tarea tiene las siguientes propiedades:

* **[!UICONTROL Título]**: Título de la tarea. El título se muestra en AEM Bandeja de entrada.
* **[!UICONTROL Descripción]**: Explicación de las operaciones que se realizan en la tarea. Esta información resulta útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **[!UICONTROL Ruta de vista en miniatura]**: Ruta de la miniatura de la tarea. Si no se especifica ninguna ruta, se muestra la miniatura predeterminada de un formulario adaptable y, para el documento de registro, se muestra un icono predeterminado.
* **[!UICONTROL Etapa del flujo de trabajo]**: Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Etapas).
* **[!UICONTROL Prioridad]**: La prioridad seleccionada se muestra en la Bandeja de entrada AEM. Las opciones disponibles son Alto, Medio y Bajo. El valor predeterminado es Medio.
* **[!UICONTROL Fecha de vencimiento]**: Especifique el número de días u horas después de los cuales se marca la tarea con retraso. Si selecciona **[!UICONTROL Off]**, la tarea nunca se marca como pendiente. También puede especificar un controlador de tiempo de espera para realizar tareas específicas después de que la tarea haya caducado.

* **[!UICONTROL Días]**: Número de días antes de los cuales se completará la tarea. El número de días se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de días especificado en el campo Días, si se selecciona, se activa un controlador de tiempo de espera después de la fecha de vencimiento.
* **[!UICONTROL Horas]**: Número de horas antes de las cuales se completará la tarea. El número de horas se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de horas especificado en el campo Horas , si se selecciona, se activa un controlador de tiempo de espera después de las horas de vencimiento.
* **[!UICONTROL Tiempo de espera después de la fecha de vencimiento]**: Seleccione esta opción para habilitar el campo de selección Controlador de tiempo de espera .
* **[!UICONTROL Controlador de tiempo de espera]**: Seleccione la secuencia de comandos que se ejecutará cuando el paso asignar tarea cruce la fecha de vencimiento. Scripts colocados en el repositorio CRX en [apps]/fd/dashboard/scripts/timeoutHandler están disponibles para su selección. La ruta especificada no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla.
* **[!UICONTROL Resalte la acción y el comentario de la última tarea en Detalles de la tarea]**: Seleccione esta opción para mostrar la última acción realizada y el comentario recibido en la sección de detalles de la tarea de una tarea.
* **[!UICONTROL Tipo]**: Elija el tipo de documento que desea rellenar al iniciar el flujo de trabajo. Puede elegir un formulario adaptable, un formulario adaptable de sólo lectura, un documento PDF no interactivo. <!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->
* **[!UICONTROL Utilizar formulario adaptable]**: Especifique el método para localizar el formulario adaptable de entrada. Esta opción está disponible si selecciona Formulario adaptable o Formulario adaptable de solo lectura en la lista desplegable Tipo . Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable de tipo String para especificar la ruta.\
   Puede asociar varios Forms adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

<!-- 
* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  -->

* **[!UICONTROL Ruta de formulario adaptable]**: Especifique la ruta del formulario adaptable.<!--  or Interactive Communication.--> Puede utilizar el formulario adaptable <!-- or interactive communication --> que se envía al flujo de trabajo, disponible en una ruta absoluta, o que recupera el formulario adaptable de una ruta almacenada en una variable de tipo de datos de cadena.
* **[!UICONTROL Seleccione el PDF de entrada mediante]**: Especifique la ruta de un documento de PDF no interactivo. El campo está disponible cuando se elige un documento de PDF no interactivo en el campo Tipo. Puede seleccionar el PDF de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta absoluta o utilizando una variable del tipo Document data . Por ejemplo, [Payload_Directory]/Workflow/PDF/credit-card.pdf. La ruta no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla. Se necesita una opción Documento de registro habilitada o Forms adaptable basado en plantillas de formulario para usar la opción Ruta del PDF .
* **[!UICONTROL Para las tareas completadas, procese el formulario adaptable como]**: Cuando se marca una tarea como completada, puede procesar el formulario adaptable como un formulario adaptable de solo lectura o un documento PDF. Se necesita una opción Documento de registro activada o una Forms adaptable basada en plantillas de formulario para procesar el formulario adaptable como documento de registro.
* **[!UICONTROL Rellenado previamente]**: Los siguientes campos sirven como entradas para la tarea:

   * **[!UICONTROL Seleccione el archivo de datos de entrada mediante]**: Ruta del archivo de datos de entrada (.json, .xml, .doc o modelo de datos de formulario). Puede recuperar el archivo de datos de entrada mediante una ruta relativa a la carga útil o recuperar el archivo almacenado en una variable de tipo de datos Document, XML o JSON. Por ejemplo, el archivo contiene los datos enviados para el formulario a través de una aplicación Bandeja de entrada AEM. Una ruta de ejemplo es [Payload_Directory]/workflow/data.
   * **[!UICONTROL Seleccionar datos adjuntos de entrada mediante]**: Los archivos adjuntos disponibles en la ubicación se adjuntan al formulario asociado a la tarea. La ruta siempre es relativa a la carga útil. Una ruta de ejemplo es [Payload_Directory]/attachment/. Puede especificar archivos adjuntos colocados en relación con la carga útil o utilizar una variable de tipo de documento (Array list > Document) para especificar un archivo adjunto de entrada para el formulario adaptable

   <!-- * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. -->
   * **[!UICONTROL Asignación de atributos de solicitud]**: Utilice la sección Asignación de atributos de solicitud para definir la variable [nombre y valor del atributo de solicitud](work-with-form-data-model.md#bindargument). Recupere los detalles de la fuente de datos en función del nombre del atributo y el valor especificados en la solicitud. Puede definir un valor de atributo de solicitud utilizando un valor literal o una variable del tipo de datos String .

   <!--  The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. -->

* **[!UICONTROL Información enviada]**: Los siguientes campos sirven como ubicaciones de salida para la tarea:

   * **[!UICONTROL Guardar el archivo de datos de salida mediante]**: Guarde el archivo de datos (.json, .xml, .doc o modelo de datos de formulario). El archivo de datos contiene información enviada a través del formulario asociado. Puede guardar el archivo de datos de salida utilizando una ruta relativa a la carga útil o almacenarla en una variable de tipo de datos Document, XML o JSON. Por ejemplo, [Payload_Directory]/Workflow/data, donde los datos son un archivo.
   * **[!UICONTROL Guardar archivos adjuntos mediante]**: Guarde los datos adjuntos del formulario proporcionados en una tarea. Puede guardar los archivos adjuntos utilizando una ruta relativa a la carga útil o almacenarla en una variable de lista de matriz del tipo Document data .
   * **[!UICONTROL Guardar documento de registro usando]**: Ruta para guardar un archivo de documento de registro. Por ejemplo, [Payload_Directory]/DocumentofRecord/credit-card.pdf. Puede guardar el documento de registro mediante una ruta relativa a la carga útil o almacenarlo en una variable del tipo de datos Document . Si selecciona **[!UICONTROL Relativo a carga útil]** , el documento de registro no se genera si el campo de ruta se deja vacío. Esta opción solo está disponible si selecciona Formulario adaptable en la lista desplegable Tipo .

   <!-- * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. -->

* **[!UICONTROL Usuario asignado]** > **[!UICONTROL Asignar opciones]**: Especifique el método para asignar la tarea a un usuario. Puede asignar dinámicamente la tarea a un usuario o grupo mediante la secuencia de comandos del selector de participantes o asignar la tarea a un usuario o grupo AEM específico.
* **[!UICONTROL Selector de participante]**: La opción está disponible cuando la variable **[!UICONTROL Dinámicamente a un usuario o grupo]** está seleccionada en el campo Assign options . Puede utilizar un ECMAScript o un servicio para seleccionar dinámicamente un usuario o un grupo. Para obtener más información, consulte [Asignar dinámicamente un flujo de trabajo a los usuarios](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) y [Crear un paso de participante dinámico de Adobe Experience Manager personalizado.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **[!UICONTROL Participantes]**: El campo está disponible cuando la variable **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** está seleccionada en la **[!UICONTROL Selector de participante]** campo . El campo permite seleccionar usuarios o grupos para la opción RandomParticipantChooser .

* **[!UICONTROL Usuario asignado]**: El campo está disponible cuando la variable **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** se selecciona en la variable **[!UICONTROL Selector de participante]** campo . El campo permite seleccionar una variable de tipo String data para definir el usuario asignado.

* **[!UICONTROL Argumentos]**: El campo está disponible cuando se selecciona una secuencia de comandos que no sea RandomParticipantChoose en el campo Selector de participantes. El campo permite proporcionar una lista de un argumento separado por comas para la secuencia de comandos seleccionada en el campo Selector de participantes .

* **[!UICONTROL Usuario o grupo]**: La tarea se asigna al usuario o grupo seleccionado. La opción está disponible cuando la variable **[!UICONTROL Para una opción de usuario o grupo específica]** se selecciona en la variable **[!UICONTROL Asignar opciones]** campo . El campo enumera todos los usuarios y grupos del [!DNL workflow-users] grupo.\
   La variable **[!UICONTROL Usuario o grupo]** en el menú desplegable se enumeran los usuarios y grupos a los que el usuario que ha iniciado sesión tiene acceso. La visualización del nombre de usuario depende de si tiene permisos de acceso en la variable **[!UICONTROL usuarios]** en crx-repository para ese usuario en particular.

* **[!UICONTROL Enviar mensaje de notificación]**: Seleccione esta opción para enviar notificaciones por correo electrónico al usuario asignado. Estas notificaciones se envían cuando se asigna una tarea a un usuario o a un grupo. Puede usar la variable **[!UICONTROL Dirección de correo electrónico del destinatario]** para especificar el mecanismo para recuperar la dirección de correo electrónico.

* **[!UICONTROL Dirección de correo electrónico del destinatario]**: Puede almacenar la dirección de correo electrónico en una variable, usar un literal para especificar una dirección de correo electrónico permanente o usar la dirección de correo electrónico predeterminada del usuario asignado especificada en el perfil del usuario asignado. Puede utilizar el literal o una variable para especificar la dirección de correo electrónico de un grupo. La opción de variable es útil para recuperar y utilizar dinámicamente una dirección de correo electrónico. La variable **[!UICONTROL Usar la dirección de correo electrónico predeterminada del usuario asignado]** es solo para un único usuario asignado. En este caso, se utiliza la dirección de correo electrónico almacenada en el perfil de usuario asignado.

* **[!UICONTROL Plantilla de correo electrónico del HTML]**: Seleccione la plantilla de correo electrónico para el correo electrónico de notificación. Para editar una plantilla, modifique el archivo ubicado en /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt en el repositorio crx.
* **[!UICONTROL Permitir delegación en]**: AEM Bandeja de entrada proporciona una opción al usuario que ha iniciado sesión para delegar el flujo de trabajo asignado a otro usuario. Se le permite delegar dentro del mismo grupo o al usuario del flujo de trabajo de otro grupo. Si la tarea está asignada a un único usuario y la variable **[!UICONTROL permitir la delegación a miembros del grupo de cesionarios]** está seleccionada, no es posible delegar la tarea a otro usuario o grupo.
* **[!UICONTROL Compartir configuración]**: AEM Bandeja de entrada proporciona opciones para compartir una o todas las tareas de la bandeja de entrada con otros usuarios:
   * Cuando la variable **[!UICONTROL Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada]** está seleccionada, el usuario puede seleccionar la tarea en AEM Bandeja de entrada y compartirla con otro usuario AEM.
   * Cuando la variable **[!UICONTROL Permitir que el usuario asignado comparta a través del uso compartido de la bandeja de entrada]** está seleccionada y los usuarios comparten sus elementos de la Bandeja de entrada o permiten que otros usuarios accedan a sus elementos de la Bandeja de entrada, solo las tareas con la opción previamente mencionada se comparten con otros usuarios.
   * Cuando la variable **[!UICONTROL Permitir que el usuario asignado delegue mediante la configuración &quot;Fuera de la oficina&quot;]** está seleccionado. El usuario asignado puede activar la opción para delegar la tarea a otros usuarios junto con otras opciones fuera de la oficina. Las nuevas tareas asignadas al usuario fuera de la oficina se delegan (asignan) automáticamente a los usuarios mencionados en la configuración fuera de la oficina.

   Permite que otros usuarios elijan tareas asignadas mientras está fuera de la oficina y no puede trabajar en tareas asignadas.

* **[!UICONTROL Acciones]** > **[!UICONTROL Acciones predeterminadas]**: Las acciones Enviar, Guardar y Restablecer están disponibles de forma predeterminada. De forma predeterminada, todas las acciones predeterminadas están habilitadas.
* **[!UICONTROL Variable de ruta]**: Nombre de la variable de ruta. La variable de ruta captura las acciones personalizadas que selecciona un usuario en AEM Bandeja de entrada.
* **[!UICONTROL Rutas]**: Una tarea puede ramificarse a diferentes rutas. Cuando se selecciona en AEM Bandeja de entrada, la ruta devuelve un valor y las ramas del flujo de trabajo se basan en la ruta seleccionada. Puede almacenar rutas en una variable de matriz del tipo de datos String o seleccionar **[!UICONTROL Literal]** para agregar rutas manualmente.

* **[!UICONTROL Título de ruta]**: Especifique el título de la ruta. Se muestra en AEM Bandeja de entrada.
* **[!UICONTROL Icono de coro]**: Especifique el atributo HTML de un icono de coral. La biblioteca CorelUI de Adobe proporciona un amplio conjunto de iconos táctiles. Puede elegir y utilizar un icono para la ruta. Se muestra junto con el título en AEM Bandeja de entrada. Si almacena las rutas en una variable, las rutas utilizan un icono de coral predeterminado &quot;Etiquetas&quot;.
* **[!UICONTROL Permitir que el usuario asignado añada un comentario]**: Seleccione esta opción para activar los comentarios en la tarea. Un usuario asignado puede agregar los comentarios desde AEM Bandeja de entrada en el momento del envío de la tarea.
* **[!UICONTROL Guardar comentario en la variable]**: Guarde el comentario en una variable de tipo String data . Esta opción solo se muestra si selecciona la variable **[!UICONTROL Permitir que el usuario asignado añada un comentario]** casilla de verificación.

* **[!UICONTROL Permitir que el usuario asignado añada archivos adjuntos a la tarea]**: Seleccione esta opción para activar los archivos adjuntos en la tarea. Un usuario asignado puede añadir los archivos adjuntos desde AEM Bandeja de entrada en el momento del envío de la tarea. También puede limitar el tamaño máximo **[!UICONTROL (Tamaño máximo del archivo)]** de un archivo adjunto. El tamaño predeterminado es de 2 MB.

* **[!UICONTROL Guardar archivos adjuntos de tareas de salida mediante]**: Especifique la ubicación de la carpeta de archivos adjuntos. Puede guardar archivos adjuntos de tareas de salida utilizando una ruta relativa a la carga útil o en una variable de matriz de tipo de datos de documento. Esta opción solo se muestra si selecciona la variable **[!UICONTROL Permitir que el usuario asignado añada archivos adjuntos a la tarea]** casilla de verificación y seleccione **[!UICONTROL Formulario adaptable]**, **[!UICONTROL Formulario adaptable de solo lectura]** o **[!UICONTROL Documento de PDF no interactivo]** de la variable **[!UICONTROL Tipo]** lista desplegable en la **[!UICONTROL Formulario/Documento]** pestaña .

* **[!UICONTROL Usar metadatos personalizados]**: Seleccione esta opción para habilitar el campo de metadatos personalizado. Los metadatos personalizados se utilizan en plantillas de correo electrónico.
* **[!UICONTROL Metadatos personalizados]**: Seleccione un metadatos personalizado para las plantillas de correo electrónico. Los metadatos personalizados están disponibles en crx-repository en apps/fd/dashboard/scripts/metadataScripts. La ruta especificada no existe en el repositorio crx. Un administrador crea la ruta antes de utilizarla. También puede utilizar un servicio para los metadatos personalizados. También puede ampliar el `WorkitemUserMetadataService` para proporcionar metadatos personalizados.
* **[!UICONTROL Mostrar datos de pasos anteriores]**: Seleccione esta opción para permitir que los usuarios asignados vean los destinatarios anteriores, las acciones ya realizadas en la tarea, los comentarios añadidos a la tarea y el documento de registro de la tarea completada, si está disponible.
* **[!UICONTROL Mostrar datos de pasos siguientes]**: Seleccione esta opción para permitir que el usuario asignado actual vea la acción realizada y los comentarios añadidos a la tarea por los siguientes asignadores. También permite al usuario asignado actual ver un documento de registro de la tarea finalizada, si está disponible.
* **[!UICONTROL Visibilidad del tipo de datos]**: De forma predeterminada, un usuario asignado puede ver un documento de registro, los cesionarios, las medidas adoptadas y los comentarios que hayan añadido los cesionarios anteriores y posteriores. Utilice la opción visibility of data type para limitar el tipo de datos visibles para los usuarios asignados.

## Enviar paso de correo electrónico {#send-email-step}

Utilice el paso de correo electrónico para enviar un correo electrónico, por ejemplo un correo electrónico con un documento de registro, un vínculo de un formulario adaptable <!-- , link of an interactive communication-->o con un documento PDF adjunto. Compatibilidad con los pasos de envío por correo electrónico [correo electrónico del HTML](https://en.wikipedia.org/wiki/HTML_email). Los correos electrónicos del HTML responden y se adaptan al cliente de correo electrónico y al tamaño de pantalla de los destinatarios. Puede utilizar una plantilla de correo electrónico de HTML para definir el aspecto, el esquema de colores y el comportamiento del correo electrónico.

El paso de correo electrónico utiliza el servicio de correo de Day CQ para enviar correos electrónicos. Antes de utilizar el paso de correo electrónico, asegúrese de que el servicio de correo electrónico está configurado. De forma predeterminada, los protocolos HTTP y HTTP solo son compatibles con el correo electrónico. [Póngase en contacto con el equipo de asistencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno. La restricción ayuda a mejorar la seguridad de la plataforma.

El paso de correo electrónico tiene las siguientes propiedades:

**[!UICONTROL Título]**: El título del paso ayuda a identificar el paso en el editor de flujo de trabajo.

**[!UICONTROL Descripción]**: La explicación es útil para otros desarrolladores de procesos cuando está trabajando en un entorno de desarrollo compartido.

**[!UICONTROL Asunto del correo electrónico]**: El asunto se puede recuperar de los metadatos de un flujo de trabajo, especificarse manualmente o recuperarse del valor almacenado en una variable. Seleccione entre las siguientes opciones:

* **[!UICONTROL Literal]** Especificar manualmente un asunto.
* **[!UICONTROL Recuperar de metadatos del flujo de trabajo]** - Recupere el asunto de una propiedad de metadatos.
* **[!UICONTROL Variable]** - Recupere el asunto del valor almacenado en una variable de tipo de datos de cadena.

**[!UICONTROL Plantilla de correo electrónico del HTML]**: plantilla de HTML para el correo electrónico. Puede especificar variables en una plantilla de correo electrónico. El paso Correo electrónico extrae y muestra todas las variables incluidas en una plantilla para las entradas.

**[!UICONTROL Metadatos de las plantillas de correo electrónico]**: El valor de las variables de plantilla de correo electrónico puede ser un valor especificado por el usuario, la ruta de un recurso en el autor o en el servidor de publicación, la imagen o una propiedad de metadatos de flujo de trabajo.

* **[!UICONTROL Literal]**: Utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadatos del flujo de trabajo]**: Utilice la opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Después de seleccionar la opción , introduzca el nombre de la propiedad de metadatos en el cuadro de texto vacío debajo de la opción Metadatos del flujo de trabajo . Por ejemplo, emailAddress.

<!-- * **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. -->
* **[!UICONTROL Imagen]**: Utilice la opción para incrustar una imagen en el correo electrónico. Después de seleccionar la opción , busque y elija la imagen. La opción de imagen solo está disponible para las etiquetas de imagen (&lt;img src=&quot;*&quot; />) disponibles en la plantilla de correo electrónico.

**[!UICONTROL Dirección de correo electrónico del remitente/destinatario]**: Seleccione el **[!UICONTROL Literal]** para especificar manualmente una dirección de correo electrónico o seleccionar la opción **[!UICONTROL Recuperar de metadatos del flujo de trabajo]** para recuperar la dirección de correo electrónico de una propiedad de metadatos. También puede especificar una lista de matrices de propiedades de metadatos para el **[!UICONTROL Recuperar de metadatos del flujo de trabajo]** . Seleccione el **[!UICONTROL Variable]** para recuperar la dirección de correo electrónico del valor almacenado en una variable de tipo de datos de cadena.

* **[!UICONTROL Archivo adjunto]**: El recurso disponible en la ubicación especificada se adjunta al correo electrónico. La ruta del recurso puede ser relativa a la carga útil o a la ruta absoluta. Una ruta de ejemplo es [Payload_Directory]/attachment/.

Seleccione el **[!UICONTROL Variable]** para recuperar el archivo adjunto almacenado en una variable de tipo de datos Document, XML o JSON.

**[!UICONTROL Nombre del archivo]**: Nombre del archivo adjunto del correo electrónico. El paso Correo electrónico cambia el nombre de archivo original del archivo adjunto al nombre de archivo especificado. El nombre se puede especificar manualmente o recuperar desde una propiedad de metadatos de flujo de trabajo o una variable. Utilice la variable **[!UICONTROL Literal]** cuando sepa el valor exacto que desea especificar. Utilice la variable **[!UICONTROL Variable]** para recuperar el nombre de archivo del valor almacenado en una variable de tipo de datos de cadena. Utilice la variable **[!UICONTROL Recuperar desde metadatos de flujo de trabajo]** cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo.

## Generar paso de documento de registro {#generate-document-of-record-step}

Cuando se rellena o se envía un formulario, se puede guardar un registro del formulario, en formato impreso o en formato de documento. Este registro se denomina Documento de registro (DoR). Puede utilizar el paso Generar documento de registro para crear una versión de PDF de solo lectura o interactiva de un formulario adaptable. La versión del PDF contiene información rellenada en el formulario junto con la presentación del formulario adaptable.

El paso Documento de registro tiene las siguientes propiedades:

**[!UICONTROL Utilizar formulario adaptable]**: Especifique el método para localizar el formulario adaptable de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable del tipo de datos String para especificar la ruta en la variable **[!UICONTROL Seleccione la variable que desee resolver]** campo .\
Puede asociar varios Forms adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

**[!UICONTROL Ruta de formulario adaptable]**: Especifique la ruta del formulario adaptable. El campo está disponible al seleccionar la variable **[!UICONTROL Disponible en una ruta absoluta]** de la **[!UICONTROL Utilizar formulario adaptable]** campo .

**[!UICONTROL Seleccionar datos de entrada mediante]**: Ruta de los datos de entrada para el formulario adaptable. Puede mantener los datos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos o recuperar datos almacenados en una variable de tipo de datos Document, JSON o XML. Los datos de entrada se combinan con el formulario adaptable para crear un documento de registro.

**[!UICONTROL Seleccione la ruta de acceso de los datos adjuntos de entrada mediante]**: Ruta de los archivos adjuntos. Estos archivos adjuntos se incluyen en el Documento de registro. Puede mantener los archivos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los archivos adjuntos o recuperar los archivos adjuntos almacenados en una variable de matriz del tipo Document data .

Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntan al documento de registro. Si hay archivos disponibles en las carpetas disponibles directamente en la ruta de datos de los archivos adjuntos especificada, los archivos se incluyen en el documento de registro como archivos adjuntos. Si hay carpetas en carpetas disponibles directamente, esas carpetas se omiten.

**[!UICONTROL Guardar documento generado de registro usando las siguientes opciones]**: Especifique la ubicación para mantener un archivo de documento de registro. Puede sobrescribir la carpeta de carga útil, colocar el documento de registro en una ubicación del directorio de carga útil o almacenar el documento de registro en una variable del tipo de datos Document.

**[!UICONTROL Configuración regional]**: Especifique el idioma del documento de registro. Select **[!UICONTROL Literal]** para seleccionar la configuración regional de una lista desplegable o seleccione **[!UICONTROL Variable]** para recuperar la configuración regional del valor almacenado en una variable de tipo de datos de cadena. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

## Invocar el paso del servicio del modelo de datos de formulario {#invoke-form-data-model-service-step}

Puede usar [[!DNL AEM Forms] Integración de datos](data-integration.md) para configurar y conectarse a orígenes de datos dispares. Estas fuentes de datos pueden ser un servicio web, un servicio REST, un servicio OData y una solución CRM. [!DNL AEM Forms] La integración de datos le permite crear un Modelo de datos de formulario que incluya varios servicios para realizar operaciones de recuperación, adición y actualización de datos en la base de datos configurada. Puede usar la variable **[!UICONTROL Invocar el paso del servicio del modelo de datos]** para seleccionar un modelo de datos de formulario (FDM) y utilizar los servicios de FDM para recuperar, actualizar o agregar datos a distintos orígenes de datos.

Para explicar las entradas de los campos del paso , se utilizan como ejemplo la siguiente tabla de base de datos y el archivo JSON :

**[!UICONTROL Tabla de detalles del cliente de muestra]**

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Value<br /> </td> 
  </tr> 
  <tr> 
   <td>Nombre<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Apellidos</td> 
   <td>Rose</td> 
  </tr> 
  <tr> 
   <td>ID de cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Dirección de correo electrónico<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL Archivo JSON de muestra]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

El paso Invocar el servicio del modelo de datos de formulario tiene los campos siguientes para facilitar las operaciones del modelo de datos de formulario:

* **[!UICONTROL Título]**: Título del paso. Ayuda a identificar el paso en el editor de flujo de trabajo.
* **[!UICONTROL Descripción]**: Explicación útil para otros desarrolladores de procesos cuando está trabajando en un entorno de desarrollo compartido.

* **[!UICONTROL Ruta del modelo de datos del formulario]**: Busque y seleccione un Modelo de datos de formulario presente en el servidor.

* **[!UICONTROL Errores y validaciones]**: La opción permite capturar mensajes de error y especificar opciones de validación para los datos recuperados y enviados a fuentes de datos. Con estos cambios, se puede garantizar que los datos pasados al paso Invocar el servicio del modelo de datos de formulario se ajusten a las restricciones de datos definidas por el origen de datos. Para obtener más información, consulte [Validación automatizada de los datos de entrada](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Nivel de validación]**: Existen tres categorías de validaciones: Básico, Completo y Desactivado:

   * Completos: Todas las restricciones se validan.
   * Básico: Solo las restricciones requeridas y las que se pueden rellenar
   * OFF: No se realiza ninguna validación.

* **[!UICONTROL Finalizar flujo de trabajo en caso de error]**: Cuando una restricción no se valida, el flujo de trabajo se detiene.

* **[!UICONTROL Almacenar código de error en variable]**: Puede almacenar un código de error en un [Variable de tipo de cadena](variable-in-aem-workflows.md).

* **[!UICONTROL Mensaje de error de almacén en la variable]**: Puede almacenar un mensaje de error en un [Variable de tipo de cadena](variable-in-aem-workflows.md).

* **[!UICONTROL Detalles de error de almacén en la variable]**: Puede almacenar un detalle de error en una [Variable de tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Servicio]**: Lista de los servicios que proporciona el Modelo de datos de formulario seleccionado.
* **[!UICONTROL Entrada para servicios]** > **[!UICONTROL Proporcionar datos de entrada utilizando metadatos literales, variables o de flujo de trabajo, y un archivo JSON]**: Un servicio puede tener varios argumentos. Seleccione la opción para obtener el valor de los argumentos de servicio de una propiedad de metadatos de flujo de trabajo, un objeto JSON o una variable, o introduzca directamente el valor en el cuadro de texto proporcionado:

   * **[!UICONTROL Literal]**: Utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, srose@we.info.
   * **[!UICONTROL Variable]**: Utilice la opción para recuperar el valor almacenado en una variable.
   * **[!UICONTROL Recuperar desde metadatos de flujo de trabajo]**: Utilice la opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Por ejemplo, emailAddress.

   * **[!UICONTROL Relativo a carga útil]**: Utilice la opción para recuperar el archivo adjunto guardado en una ruta relativa a la carga útil. Seleccione la opción y especifique el nombre de la carpeta que incluye el archivo adjunto o especifique el nombre del archivo adjunto en el cuadro de texto.

      Por ejemplo, si la carpeta Relative to Payload en el repositorio CRX incluye un archivo adjunto en el `attachment\attachment-folder` ubicación, especificar `attachment\attachment-folder` en el cuadro de texto después de seleccionar la variable **[!UICONTROL Relativo a carga útil]** .

   * **[!UICONTROL Notación de puntos JSON]**: Utilice la opción cuando el valor que desea utilizar esté en un archivo JSON. Por ejemplo, insurance.customerDetails.emailAddress. La opción Anotación de puntos JSON solo está disponible si se seleccionan los campos de entrada de Mapa de la opción JSON de entrada.
   * **[!UICONTROL Asignación de campos de entrada del JSON de entrada]**: Especifique la ruta de un archivo JSON para obtener el valor de entrada de algunos argumentos de servicio del archivo JSON. La ruta del archivo JSON puede ser relativa a la carga útil, una ruta absoluta o puede seleccionar un documento JSON de entrada utilizando una variable de tipo JSON o Modelo de datos de formulario.

* **[!UICONTROL Entrada para servicios]** > **[!UICONTROL Proporcionar datos de entrada mediante una variable o un archivo JSON]**: Seleccione la opción para obtener valores para todos los argumentos de un archivo JSON guardado en una ruta absoluta, en una ruta relativa a la carga útil o en una variable.
* **[!UICONTROL Seleccione el documento JSON de entrada mediante]**: El archivo JSON que contiene valores para todos los argumentos de servicio. La ruta del archivo JSON puede ser **[!UICONTROL relativa a la carga útil]** o **[!UICONTROL ruta absoluta]**. También puede recuperar el documento JSON de entrada utilizando una variable de tipo de datos JSON o del Modelo de datos de formulario.

* **[!UICONTROL Notación de puntos JSON]**: Deje el campo en blanco para utilizar todos los objetos del archivo JSON especificado como entrada para argumentos de servicio. Para leer un objeto JSON específico del archivo JSON especificado como entrada para argumentos de servicio, especifique la notación de puntos para el objeto JSON, por ejemplo, si tiene un JSON similar al que aparece al principio de la sección, especifique insurance.customerDetails para proporcionar todos los detalles de un cliente como entrada al servicio.
* **[!UICONTROL Resultados del servicio]** > **[!UICONTROL Asignación y escritura de valores de salida en variables o metadatos]**: Seleccione la opción para guardar los valores de salida como propiedades del nodo de metadatos de instancia de flujo de trabajo en crx-repository. Especifique el nombre de la propiedad metadata y seleccione el atributo de salida de servicio correspondiente que se va a asignar con la propiedad metadata, por ejemplo, asigne el phone_number devuelto por el servicio de salida con la propiedad phone_number de los metadatos del flujo de trabajo. Del mismo modo, se puede almacenar la salida en una variable de tipo de datos Long. Al seleccionar una propiedad para la variable **[!UICONTROL Atributo de salida del servicio a asignar]** , solo se rellenan las variables capaces de almacenar datos de la propiedad seleccionada para la variable **[!UICONTROL Guarde la salida en]** .

* **[!UICONTROL Resultados del servicio]** > **[!UICONTROL Guardar resultados en una variable o un archivo JSON]**: Seleccione la opción para guardar los valores de salida en un archivo JSON en una ruta absoluta, en una ruta relativa a la carga útil o en una variable .
* **[!UICONTROL Guardar documento JSON de salida con las siguientes opciones]**: Guarde el archivo JSON de salida. La ruta del archivo JSON de salida puede ser relativa a la carga útil o a una ruta absoluta. También puede guardar el archivo JSON de salida con una variable de tipo de datos JSON o del Modelo de datos de formulario.

## Paso Firmar documento {#sign-document-step}

El paso Firmar documento le permite utilizar [!DNL Adobe Sign] para firmar documentos. Cuando utilice [!DNL Adobe Sign] Paso del flujo de trabajo para firmar un formulario adaptable, el formulario se puede pasar de un firmante a otro o se puede enviar a todos los firmantes simultáneamente, en función de la configuración del paso del flujo de trabajo. [!DNL Adobe Sign] Forms adaptable activado se envía al servidor de Experience Manager Forms solo después de que todos los firmantes hayan completado el proceso de firma.

De forma predeterminada, la variable [!DNL Adobe Sign] Scheduler Services comprueba (encuestas) la respuesta del firmante cada 24 horas. Puede [cambiar el intervalo predeterminado para su entorno](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

El paso Firmar documento tiene las siguientes propiedades:

* **[!UICONTROL Nombre del acuerdo]**: Especifique el título del acuerdo. El nombre del acuerdo forma parte del asunto y del texto del cuerpo del correo electrónico enviado a los firmantes. Puede almacenar el nombre en una variable del tipo de datos String o seleccionar **[!UICONTROL Literal]** para agregar el nombre manualmente.

* **[!UICONTROL Configuración regional]**: Especifique el idioma para las opciones de correo electrónico y verificación. Puede almacenar la configuración regional en una variable del tipo de datos String o seleccionar **[!UICONTROL Literal]** para elegir la configuración regional de la lista de opciones disponibles. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **[!UICONTROL en_US]** para inglés y **[!UICONTROL fr_FR]** para francés.

* **[!UICONTROL Configuración de Adobe Sign Cloud]**: Elija un [!DNL Adobe Sign] Configuración de nube. Si no ha configurado [!DNL Adobe Sign] para [!DNL AEM Forms], consulte [Integrar Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Seleccionar documento para firmar mediante]**: Puede elegir un documento de una ubicación relativa a la carga útil, utilizar la carga útil como documento, especificar una ruta absoluta del documento o recuperar el documento almacenado en una variable de tipo Document data .
* **[!UICONTROL Días hasta la fecha límite]**: Un documento se marca con vencimiento (fecha límite superada) después de que no haya actividad en la tarea por el número de días especificado en la variable **[!UICONTROL Días hasta la fecha límite]** campo . El número de días se cuenta después de que el documento se asigne a un usuario para su firma.
* **[!UICONTROL Frecuencia del correo electrónico recordatorio]**: Puede enviar un correo electrónico recordatorio a intervalos diarios o semanales. La semana se cuenta desde el día en que se asigna el documento a un usuario para su firma.
* **[!UICONTROL Proceso de firma]**: Puede optar por firmar un documento en orden secuencial o paralelo. En orden secuencial, un firmante recibe el documento a la vez para su firma. Una vez que el primer firmante completa la firma del documento, el documento se envía al segundo firmante, etc. En orden paralelo, varios firmantes pueden firmar un documento a la vez.
* **[!UICONTROL Dirección URL de redirección]**: Especifique una dirección URL de redirección. Una vez firmado el documento, puede redirigir al usuario asignado a una dirección URL. Normalmente, esta URL contiene un mensaje de agradecimiento o instrucciones adicionales.
* **[!UICONTROL Etapa del flujo de trabajo]**: Un flujo de trabajo puede tener varias etapas. Estas etapas se muestran en la Bandeja de entrada AEM. Puede definir estas etapas en las propiedades del modelo ( **[!UICONTROL Barra de tareas]** > **[!UICONTROL Página]** > **[!UICONTROL Propiedades de página]** > **[!UICONTROL Etapas]**).
* **[!UICONTROL Seleccionar firmantes]**: Especifique el método para elegir firmantes para el documento. Puede asignar dinámicamente el flujo de trabajo a un usuario o grupo, o agregar manualmente los detalles de un firmante.
* **[!UICONTROL Secuencia de comandos o servicio para seleccionar firmantes]**: La opción solo está disponible si la opción Dinámicamente está seleccionada en el campo Seleccionar firmantes . Puede especificar un ECMAScript o un servicio para elegir los firmantes y las opciones de verificación de un documento.
* **[!UICONTROL Detalles del firmante]**: La opción solo está disponible si la opción Manualmente está seleccionada en el campo Seleccionar firmantes . Especifique la dirección de correo electrónico y elija un mecanismo de verificación opcional. Antes de seleccionar un mecanismo de verificación de 2 pasos, asegúrese de que la opción de verificación correspondiente esté habilitada para el [!DNL Adobe Sign] cuenta. Puede utilizar una variable del tipo de datos String para definir los valores de los campos Email, Country Code y Phone Number. Los campos Código del país y Número de teléfono solo se muestran si selecciona Verificación del teléfono en la lista desplegable de verificación de 2 pasos.

<!-- ## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).

### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.

### Generate Printed Output Step {#generatePrintedOutput}

The step generates a PCL, PostScript, ZPL, IPL, TPCL, or DPL output given a form design and data file. The data file is merged with the form design and formatted for printing. The output generated by this step can be sent directly to a printer or saved as file. It is recommended that you use this step when you want to use form designs or data from an application. If your form designs or form designs are located on the network, local file system, or HTTP location, use the generatePrintedOutput operation operation.

For example, your application requires that you merge a form design with a data file. The data contains hundreds of records. In addition, it requires the output is sent to a printer that supports ZPL. The form design and your input data are located in an application. Use the generatePrintedOutput operation to merge each record with a form design and send the output to a printer that supports ZPL.

The Generate Printed Output step has the following properties:

**[!UICONTROL Input properties]**

* **[!UICONTROL Select template file using]**: Specify the path of the template file. You can select the template file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it. Moreover, you can also accept payload as the input data file.

* **[!UICONTROL Select data document using]**: Specify the path of a input data file. You can select the input data file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it.

* **[!UICONTROL Printer Format]**: A Print Format value that specifies the page description language to use, when an XDC file is not provided, to generate the output stream. If you provide a literal value, select one of these values:

  * **[!UICONTROL Custom PCL]**: Use the option to specify a custom XDC file for PCL.
  * **[!UICONTROL Custom PostScript]**: Use the option to specify a custom XDC file for PostScript.
  * **[!UICONTROL Custom ZPL]**: Use the option to specify a custom XDC file file for ZPL.
  * **[!UICONTROL Generic Color PCL (5c)]**: Use a generic color PCL (5c).
  * **[!UICONTROL Generic PostScript Level3]**: Use generic PostScript Level 3.
  * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. The zpl300.xdc is used.
  * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. The zpl600.xdc file is used.
  * **[!UICONTROL Custom IPL]**: Use the option to specify a custom XDC file for IPL.
  * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. The ipl300.xdc is used.
  * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. The ipl400.xdc file is used.
  * **[!UICONTROL Custom TPCL]**: Use the option to specify a custom XDC file for TPCL.
  * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. The tpcl305.xdc file is used.
  * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. The tpcl600.xdc file is used.
  * **[!UICONTROL Custom DPL]**: Use the option to specify a custom XDC file DPL.
  * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. The dpl300.xdc file is used.
  * **[!UICONTROL DPL406DPI]**: Use DPL 400 DPI. The dpl406.xdc is used.
  * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. The dpl600.xdc is used.

**[!UICONTROL Output Properties]**

* **[!UICONTROL Save output document using]**: Specify the location to save the output file. You can save the output file at an location  which is relative to the payload, in a variable, or specify an absolute location to save the output file. If the path does not exist in crx-repository, an administrator can create the path before using it.

**[!UICONTROL Advanced Properties]**

* **[!UICONTROL Select Content Root location using]**: Content root is a string value that specifies the URI, absolute reference, or location in the repository to retrieve relative assets used by the form design. For example, if the form design references an image relatively, such as ../myImage.gif, myImage.gif must be located at repository://. The default value is repository://, which points to the root level of the repository.

  When you pick an asset from your application, the Content Root URI path must have the correct structure. For example, if a form is picked from an application named SampleApp, and is placed at SampleApp/1.0/forms/Test.xdp, the Content Root URI must be specified as repository://administrator@password/Applications/SampleApp/1.0/forms/, or repository:/Applications/SampleApp/1.0/forms/ (when authority is null). When the Content Root URI is specified this way, the paths of all of the referenced assets in the form will be resolved against this URI.

* **[!UICONTROL Select XCI file using]**: XCI files are used to describe fonts and other properties that are used for form design elements. You can keep an XCI file relative to the payload, at an absolute path, or using a variable of Document data type.

* **[!UICONTROL Locale]**: Specifies the language used for generating the PDF document. If you provide a literal value, select a language from the list or select one of these values:
  * **[!UICONTROL To use server default]**:
    (Default) Use the Locale setting configured on the [!DNL AEM Forms] Server. The Locale setting is configured using Administration Console. (See [Designer Help](http://www.adobe.com/go/learn_aemforms_designer_65).)

  * **[!UICONTROL To use custom value]**:
    Type the Locale code in the literal box or select a string variable containing the locale code. For a complete list of supported locale codes, see http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]**: An integer value that specifies the number of copies to generate for the output. The default value is 1.

* **[!UICONTROL Duplex Printing]**:  A Pagination value that specifies whether to use two-sided or single-sided printing. Printers that support PostScript and PCL use this value.If you provide a literal value, select one of these values:
    * **[!UICONTROL Duplex Long Edge]**: Use two-sided printing and print using long-edge pagination. 
    * **[!UICONTROL Duplex Short Edge]**: Use two-sided printing and print using short-edge pagination. 
    * **[!UICONTROL Simplex]**: Use single-sided printing.-->
