---
title: ¿Qué pasos de flujo de trabajo están disponibles en Cloud Service de AEM Forms para crear un flujo de trabajo o para la automatización de procesos empresariales (BPM)?
description: Los flujos de trabajo centrados en Forms le permiten crear rápidamente flujos de trabajo basados en formularios adaptables. Puede utilizar Adobe Sign para firmar documentos por correo electrónico, crear procesos empresariales basados en formularios, recuperar y enviar datos a varias fuentes de datos y enviar notificaciones por correo electrónico
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: Uso de flujos de trabajo de AEM, uso de los pasos Asignar tarea, paso Convertir en PDF/A, paso Generar documento de registro, uso de flujos de trabajo, paso Firmar documento, paso Generar salida impresa, paso Generar salida de PDF no interactiva
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: ht
source-wordcount: '7370'
ht-degree: 100%

---


# Uso de flujos de trabajo de AEM centrados en Forms: referencia de pasos para automatizar los procesos empresariales {#forms-centric-workflow-on-osgi-step-reference}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Se utilizan los modelos de flujo de trabajo. Un modelo le ayuda a definir y ejecutar una serie de pasos. También puede definir propiedades del modelo, como si el flujo de trabajo es transitorio o utiliza varios recursos. Puede [incluir varios pasos del flujo de trabajo AEM en un modelo para lograr establecer una lógica empresarial](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es#extending-aem).

## Pasos centrados en Forms {#forms-workflow-steps}

Los pasos del flujo de trabajo centrados en AEM Forms realizan operaciones específicas en un flujo de trabajo AEM. Estos pasos le permiten crear rápidamente formularios adaptables basados en flujos de trabajo centrados en Forms en OSGi. Estos flujos de trabajo se pueden utilizar para desarrollar flujos de trabajo básicos de revisión y aprobación, y procesos empresariales internos y a través del firewall. También puede seguir los pasos de Forms Workflow para:

* Crear procesos empresariales, flujos de trabajo posteriores al envío y flujos de trabajo back-end para administrar los procesos de inscripción.

* Crear y asignar tareas a un usuario o grupo.

* Usar [!DNL Adobe Sign] en un flujo de trabajo AEM para enviar un documento que se debe firmar.

* Generar un documento de registro bajo demanda o en envío de formulario.

* Conectar un modelo de flujo de trabajo con varias fuentes de datos para guardar y recuperar datos fácilmente.

* Utilizar el paso de correo electrónico para enviar correos electrónicos de notificación y otros archivos adjuntos al finalizar una acción y al principio o al final de un flujo de trabajo.

>[!NOTE]
>
>Si el modelo de flujo de trabajo está marcado para un almacenamiento externo, para todos los pasos del flujo de Forms Workflow, puede seleccionar solo la opción de variable para almacenar o recuperar archivos de datos y archivos adjuntos.

## Paso de tarea de asignación {#assign-task-step}

El paso para asignar una tarea crea un elemento de trabajo y lo asigna a un usuario o grupo. Junto con asignar la tarea, el componente también especifica el formulario adaptable o el PDF no interactivo para la tarea. El formulario adaptable es necesario para aceptar los datos que han introducido los usuarios y un PDF no interactivo o un formulario adaptable de solo lectura solo se utiliza para revisar los flujos de trabajo.

También puede utilizar el componente para controlar el comportamiento de la tarea. Por ejemplo, crear un documento de registro automático, asignar la tarea a un usuario o grupo específico, especificar la ruta de los datos enviados, especificar la ruta de los datos que se van a rellenar previamente y especificar las acciones predeterminadas. El paso para asignar una tarea tiene las siguientes propiedades:

* **[!UICONTROL Título]**: título de la tarea. El título se muestra en la bandeja de entrada AEM.
* **[!UICONTROL Descripción]**: explicación de las operaciones que se realizan en la tarea. Esta información resulta útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

* **[!UICONTROL Ruta de vista en miniatura]**: ruta de la miniatura de la tarea. Si no se especifica ninguna ruta, se muestra la miniatura predeterminada de un formulario adaptable y, para el documento de registro, se muestra un icono predeterminado.
* **[!UICONTROL Fase del flujo de trabajo]**: un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM. Puede definir estas fases en las propiedades del modelo (Barra de tareas > Página > Propiedades de la página > Fases).
* **[!UICONTROL Prioridad]**: la prioridad seleccionada se muestra en la bandeja de entrada AEM. Las opciones disponibles son Alta, Media y Baja. El valor predeterminado es Media.
* **[!UICONTROL Fecha de vencimiento]**: especifique el número de días u horas después de los cuales se marca la tarea con retraso. Si selecciona **[!UICONTROL No]**, la tarea nunca se marca como con retraso. También puede especificar un controlador de tiempo de espera para realizar tareas específicas después de que la tarea haya llegado a la fecha de vencimiento.

* **[!UICONTROL Días]**: número de días antes de los cuales se completará la tarea. El número de días se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de días especificado en el campo Días, si se selecciona, se activa un controlador de tiempo de espera después de la fecha de vencimiento.
* **[!UICONTROL Horas]**: número de horas antes de las cuales se completará la tarea. El número de horas se cuenta después de que la tarea se asigne a un usuario. Si una tarea no está completa y sobrepasa el número de horas especificado en el campo Horas, si se selecciona, se activa un controlador de tiempo de espera después de las horas de vencimiento.
* **[!UICONTROL Tiempo de espera después de la fecha de vencimiento]**: seleccione esta opción para habilitar el campo de selección Controlador de tiempo de espera.
* **[!UICONTROL Controlador de tiempo de espera]**: seleccione la secuencia de comandos que se ejecutará cuando el paso para asignar tarea sobrepase la fecha de vencimiento. Scripts colocados en el repositorio CRX en [apps]/fd/dashboard/scripts/timeoutHandler están disponibles para su selección. La ruta especificada no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla.
* **[!UICONTROL Resaltar la acción y el comentario de la última tarea en Detalles de la tarea]**: seleccione esta opción para mostrar la última acción realizada y el comentario recibido en la sección de detalles de una tarea.
* **[!UICONTROL Tipo]**: elija el tipo de documento que desea rellenar al iniciar el flujo de trabajo. Puede elegir un formulario adaptable, un formulario adaptable de solo lectura o un documento PDF no interactivo.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Utilizar formulario adaptable]**: especifique el método para localizar el formulario adaptable de entrada. Esta opción está disponible si selecciona Formulario adaptable o Formulario adaptable de solo lectura en la lista desplegable Tipo. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta de acceso absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable de tipo cadena para especificar la ruta.\
  Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Ruta de formulario adaptable]**: especifique la ruta del formulario adaptable. Puede utilizar el formulario adaptable que se envía al flujo de trabajo, que está disponible en una ruta de acceso absoluta, o recuperar el formulario adaptable de una ruta almacenada en una variable de tipo de datos de cadena.
* **[!UICONTROL Seleccionar el PDF de entrada mediante]**: especifique la ruta de un documento de PDF no interactivo. El campo está disponible cuando se elige un documento PDF no interactivo en el campo Tipo. Puede seleccionar el PDF de entrada utilizando la ruta relativa a la carga útil, guardada en una ruta de acceso absoluta o utilizando una variable con un tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/PDF/credit-card.pdf. La ruta no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla. Se necesita habilitar una opción de documento de registro o formulario adaptable basado en plantillas de formulario para usar la opción Ruta del PDF.
* **[!UICONTROL Para las tareas completadas, procese el formulario adaptable como]**: cuando se marca una tarea como completada, puede procesar el formulario adaptable como un formulario adaptable de solo lectura o un documento PDF. Se necesita habilitar una opción de documento de registro o formulario adaptable basado en plantillas de formulario para procesar el formulario adaptable como documento de registro.
* **[!UICONTROL Rellenado previamente]**: los siguientes campos sirven como entradas para la tarea:

   * **[!UICONTROL Seleccionar el archivo de datos de entrada mediante]**: ruta del archivo de datos de entrada (.json, .xml, .doc o modelo de datos de formulario (FDM)). Puede recuperar el archivo de datos de entrada mediante una ruta relativa a la carga útil o recuperar el archivo almacenado en una variable con un tipo de datos Doc, XML o JSON. Por ejemplo, el archivo contiene los datos enviados para el formulario a través de una aplicación de bandeja de entrada AEM. Una ruta de ejemplo es [Payload_Directory]/workflow/data.
   * **[!UICONTROL Seleccionar datos adjuntos de entrada mediante]**: los archivos adjuntos disponibles en la ubicación se adjuntan al formulario asociado a la tarea. La ruta puede ser relativa a la carga útil o recuperar el archivo adjunto almacenado en una variable de tipo Doc. Una ruta de ejemplo es [Payload_Directory]/attachments/. Puede especificar archivos adjuntos colocados en relación con la carga útil o utilizar una variable de tipo Doc (Lista de matriz > Documento) para especificar un archivo adjunto de entrada para el formulario adaptable.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Asignación de atributos de solicitud]**: utilice la sección Asignación de atributos de solicitud para definir [el nombre y el valor del atributo de solicitud](work-with-form-data-model.md#bindargument). Recupere los detalles de la fuente de datos en función del nombre del atributo y el valor especificados en la solicitud. Puede definir un valor de atributo de solicitud utilizando un valor literal o una variable de tipo de datos de cadena.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Información enviada]**: los siguientes campos sirven como ubicaciones de salida para la tarea:

   * **[!UICONTROL Guardado del archivo de datos de salida]**: guarde el archivo de datos (.json, .xml, .doc o modelo de datos de formulario). El archivo de datos contiene información enviada a través del formulario asociado. Puede guardar el archivo de datos de salida utilizando una ruta relativa a la carga útil o almacenarla en una variable con un tipo de datos Doc, XML o JSON. Por ejemplo, [Payload_Directory]/Workflow/data, donde los datos son un archivo.
   * **[!UICONTROL Guardar archivos adjuntos mediante]**: guarde los datos adjuntos del formulario proporcionados en una tarea. Puede guardar los archivos adjuntos utilizando una ruta relativa a la carga útil o almacenarla en una variable de lista de matriz con un tipo de datos Doc.
   * **[!UICONTROL Guardar documento de registro mediante]**: ruta para guardar un archivo de documento de registro. Por ejemplo, [Payload_Directory]/DocumentofRecord/credit-card.pdf. Puede guardar el documento de registro mediante una ruta relativa a la carga útil o almacenarlo en una variable con un tipo de datos Doc. Si selecciona la opción **[!UICONTROL Relativo a la carga útil]**, el documento de registro no se genera si el campo de ruta se deja vacío. Esta opción solo está disponible si selecciona Formulario adaptable en la lista desplegable Tipo.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Usuario asignado]** > **[!UICONTROL Asignar opciones]**: especifique el método para asignar la tarea a un usuario. Puede asignar dinámicamente la tarea a un usuario o grupo mediante el script del selector de participantes o asignar la tarea a un usuario o grupo AEM específico.
* **[!UICONTROL Selector de participantes]**: la opción está disponible cuando la variable **[!UICONTROL Dinámicamente a un usuario o grupo]** está seleccionada en el campo Asignar opciones. Puede utilizar un ECMAScript o un servicio para seleccionar dinámicamente un usuario o un grupo. Para obtener más información, consulte [Crear un paso de participante dinámico de Adobe Experience Manager personalizado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es&CID=RedirectAEMCommunityKautuk).

* **[!UICONTROL Participantes]**: el campo está disponible cuando la opción **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** está seleccionada en el campo **[!UICONTROL Selector de participantes]**. El campo permite seleccionar usuarios o grupos para la opción RandomParticipantChooser.

* **[!UICONTROL Usuario asignado]**: el campo está disponible cuando la variable **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** está seleccionada en el campo **[!UICONTROL Selector de participantes]**. El campo permite seleccionar una variable de tipo de datos de cadena para definir el usuario asignado.

* **[!UICONTROL Argumentos]**: el campo está disponible cuando se selecciona un script que no sea RandomParticipantChoose en el campo Selector de participantes. El campo permite proporcionar una lista de un argumento separado por comas para la secuencia de comandos seleccionada en el campo Selector de participantes. 

* **[!UICONTROL Usuario o grupo]**: la tarea se asigna al usuario o grupo seleccionado. La opción está disponible cuando la variable **[!UICONTROL Para una opción de usuario o grupo específica]** está seleccionada en el campo **[!UICONTROL Asignar opciones]**. El campo enumera todos los usuarios y grupos del grupo [!DNL workflow-users].\
  La lista **[!UICONTROL Usuario o grupo]** en el menú desplegable enumera los usuarios y grupos a los que el usuario que ha iniciado sesión tiene acceso. La visualización del nombre de usuario depende de si tiene permisos de acceso en el nodo **[!UICONTROL usuarios]** en el repositorio CRX para ese usuario en particular.

* **[!UICONTROL Enviar correo electrónico de notificación]**: seleccione esta opción para enviar notificaciones por correo electrónico al usuario asignado. Estas notificaciones se envían cuando se asigna una tarea a un usuario o a un grupo. Puede usar la variable **[!UICONTROL Dirección de correo electrónico del destinatario]** para especificar el mecanismo para recuperar la dirección de correo electrónico.

* **[!UICONTROL Dirección de correo electrónico del destinatario]**: puede almacenar la dirección de correo electrónico en una variable, usar un valor literal para especificar una dirección de correo electrónico permanente o usar la dirección de correo electrónico predeterminada del usuario asignado especificada en el perfil de este. Puede utilizar el valor literal o una variable para especificar la dirección de correo electrónico de un grupo. La opción de variable es útil para recuperar y utilizar dinámicamente una dirección de correo electrónico. La variable **[!UICONTROL Usar la dirección de correo electrónico predeterminada del usuario asignado]** es solo para un único usuario asignado. En este caso, se utiliza la dirección de correo electrónico almacenada en el perfil del usuario asignado.

* **[!UICONTROL Plantilla de correo electrónico HTML]**: seleccione la plantilla de correo electrónico para el correo electrónico de notificación. Para editar una plantilla, modifique el archivo ubicado en /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt en el repositorio CRX.
* **[!UICONTROL Permitir delegación en]**: la bandeja de entrada AEM proporciona una opción al usuario que ha iniciado sesión para delegar el flujo de trabajo asignado a otro usuario. Se le permite delegar dentro del mismo grupo o al usuario del flujo de trabajo de otro grupo. Si la tarea está asignada a un único usuario y la opción **[!UICONTROL Permitir la delegación a los miembros del grupo de asignados]** está seleccionada, no es posible delegar la tarea a otro usuario o grupo.
* **[!UICONTROL Compartir configuración]**: la bandeja de entrada AEM proporciona opciones para compartir una o todas las tareas de la bandeja de entrada con otros usuarios:
   * Cuando la variable **[!UICONTROL Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada]** está seleccionada, el usuario puede seleccionar la tarea en la bandeja de entrada AEM y compartirla con otro usuario de AEM.
   * Cuando la opción **[!UICONTROL Permitir que el usuario asignado comparta a través del uso compartido de la bandeja de entrada]** está seleccionada y los usuarios comparten sus elementos de la bandeja de entrada o permiten que otros usuarios accedan a sus elementos de la bandeja de entrada, solo las tareas con la opción previamente mencionada habilitada se comparten con otros usuarios.
   * Cuando la opción de configuración **[!UICONTROL Permitir que el usuario asignado delegue mediante la configuración ‘Fuera de la oficina’]** está seleccionada. El usuario asignado puede activar la opción para delegar la tarea a otros usuarios junto con otras opciones fuera de la oficina. Las nuevas tareas asignadas al usuario fuera de la oficina se delegan (asignan) automáticamente a los usuarios mencionados en la configuración fuera de la oficina.

  Permite que otros usuarios elijan tareas asignadas mientras está fuera de la oficina y no puede trabajar en tareas asignadas.

* **[!UICONTROL Acciones]** > **[!UICONTROL Acciones predeterminadas]**: las acciones Enviar, Guardar y Restablecer están disponibles por defecto. De forma predeterminada, todas estas acciones están habilitadas.
* **[!UICONTROL Variable de ruta]**: nombre de la variable de ruta. La variable de ruta captura las acciones personalizadas que selecciona un usuario en la bandeja de entrada AEM.
* **[!UICONTROL Rutas]**: una tarea puede ramificarse a diferentes rutas. Cuando se selecciona en la bandeja de entrada AEM, la ruta devuelve un valor y las ramas del flujo de trabajo se basan en la ruta seleccionada. Puede almacenar rutas en una variable de matriz de tipo de datos de cadena o seleccionar **[!UICONTROL Literal]** para agregar rutas manualmente.

* **[!UICONTROL Título de ruta]**: especifique el título de la ruta. Se muestra en la bandeja de entrada AEM.
* **[!UICONTROL Icono coral]**: especifique el atributo HTML de un icono coral. La biblioteca CorelUI de Adobe proporciona un amplio conjunto de iconos táctiles. Puede elegir y utilizar un icono para la ruta. Se muestra junto con el título en la bandeja de entrada AEM. Si almacena las rutas en una variable, las rutas utilizan un icono coral predeterminado de &#39;Etiquetas&#39;.
* **[!UICONTROL Permitir que el usuario asignado añada un comentario]**: seleccione esta opción para habilitar los comentarios en la tarea. Un usuario asignado puede agregar los comentarios desde la bandeja de entrada AEM en el momento del envío de la tarea.
* **[!UICONTROL Guardar comentario en la variable]**: guarde el comentario en una variable de tipo de datos de cadena. Esta opción solo se muestra si selecciona la casilla de verificación **[!UICONTROL Permitir que el usuario asignado añada un comentario]**.

* **[!UICONTROL Permitir que el usuario asignado añada archivos adjuntos a la tarea]**: seleccione esta opción para activar los archivos adjuntos en la tarea. Un usuario asignado puede agregar los archivos adjuntos desde la bandeja de entrada AEM en el momento del envío de la tarea. También puede limitar el tamaño máximo **[!UICONTROL (Tamaño máximo del archivo)]** de un archivo adjunto. El tamaño predeterminado es de 2 MB.

* **[!UICONTROL Guardar archivos adjuntos de tareas de salida mediante]**: especifique la ubicación de la carpeta de archivos adjuntos. Puede guardar archivos adjuntos de tareas de salida utilizando una ruta relativa a la carga útil o en una variable de matriz de tipos de datos de documento. Esta opción solo se muestra si selecciona la casilla de verificación **[!UICONTROL Permitir que el usuario asignado añada archivos adjuntos a la tarea]** y selecciona **[!UICONTROL Formulario adaptable]**, **[!UICONTROL Formulario adaptable de solo lectura]** o **[!UICONTROL Documento PDF no interactivo]** de la lista desplegable **[!UICONTROL Tipo]** en la pestaña **[!UICONTROL Formulario/Documento]**.

* **[!UICONTROL Usar metadatos personalizados]**: seleccione esta opción para habilitar el campo de metadatos personalizado. Los metadatos personalizados se utilizan en plantillas de correo electrónico.
* **[!UICONTROL Metadatos personalizados]**: seleccione metadatos personalizado para las plantillas de correo electrónico. Los metadatos personalizados están disponibles en el repositorio CRX en apps/fd/dashboard/scripts/metadataScripts. La ruta especificada no existe en el repositorio CRX. Un administrador crea la ruta antes de utilizarla. También puede utilizar un servicio para los metadatos personalizados. También puede ampliar la interfaz de `WorkitemUserMetadataService` para proporcionar metadatos personalizados.
* **[!UICONTROL Mostrar datos de pasos anteriores]**: seleccione esta opción para permitir que los usuarios asignados vean los destinatarios anteriores, las acciones ya realizadas en la tarea, los comentarios añadidos a la tarea y el documento de registro de la tarea completada, si está disponible.
* **[!UICONTROL Mostrar datos de pasos siguientes]**: seleccione esta opción para permitir que el usuario asignado actual vea la acción realizada y los comentarios añadidos a la tarea por los siguientes usuarios asignados. También permite al usuario asignado actual ver un documento de registro de la tarea finalizada, si está disponible.
* **[!UICONTROL Visibilidad del tipo de datos]**: de forma predeterminada, un usuario asignado puede ver un documento de registro, los usuarios asignados, las medidas adoptadas y los comentarios que hayan añadido los usuarios asignados anteriores y posteriores. Utilice la opción del tipo de visibilidad de datos para limitar el tipo de datos visibles para los usuarios asignados.

>[!NOTE]
>
>Las opciones para guardar el paso Asignar tarea como borrador y para recuperar su historial se desactivan al configurar un modelo de flujo de trabajo de AEM para el almacenamiento de datos externo. Además, en la bandeja de entrada, la opción para guardar está desactivada.

## Paso para convertir a PDF/A {#convert-pdfa}

PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, al incrustar las fuentes y descomprimir el archivo. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Puede usar el paso ***Convertir a PDF/A*** en un flujo de trabajo AEM para convertir los documentos de su PDF a formato PDF/A.

El paso para convertir a PDF/A tiene las siguientes propiedades:

**[!UICONTROL Documento de entrada]**: el documento de entrada puede ser relativo a la carga útil, tener una ruta de acceso absoluta, puede proporcionarse como carga útil o almacenarse en una variable de tipo de datos de Documento.

**[!UICONTROL Opciones de conversión]**: con esta propiedad, se especifica la configuración para convertir documentos de PDF a documentos de PDF/A. Hay varias opciones disponibles en esta pestaña:
* **[!UICONTROL Cumplimiento]**: especifica el estándar que debe cumplir el documento PDF/A de salida. Admite diferentes estándares de PDF, como PDF/A-1b, PDF/A-2b o PDF/A-3b.
* **[!UICONTROL Nivel de resultado]**: especifica el nivel de resultado como Superado/No superado, Resumen o Detallado, para la salida de conversión.
* **[!UICONTROL Espacio de color]**: especifica el espacio de color predefinido como S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED o SWOP, que se puede utilizar para archivos PDF/A de salida.
* **[!UICONTROL Contenido opcional]**: permita que objetos gráficos específicos o anotaciones estén visibles en un documento PDF/A de salida, solo cuando se cumpla un conjunto especificado de criterios.

**[!UICONTROL Documentos de salida]**: especifica la ubicación para guardar el archivo de salida. El archivo de salida puede guardarse en una ubicación relativa a la carga útil, sobrescribir la carga útil, si esta es un archivo, o en una variable de tipo de datos de documento.


## Paso para enviar correo electrónico {#send-email-step}

Utilice este paso para enviar un correo electrónico, por ejemplo un correo electrónico con un documento de registro, un vínculo <!-- , link of an interactive communication--> de formulario adaptable o con un documento PDF adjunto. Este paso es compatible con el [correo electrónico HTML](https://es.wikipedia.org/wiki/Correo_HTML). Los correos electrónicos HTML responden y se adaptan al cliente de correo electrónico y al tamaño de pantalla de los destinatarios. Puede utilizar una plantilla de correo electrónico HTML para definir el aspecto, el esquema de colores y el comportamiento del correo electrónico.

El paso de correo electrónico utiliza el servicio de correo de Day CQ para enviar correos electrónicos. Antes de utilizar el paso de correo electrónico, asegúrese de que el servicio de correo electrónico está configurado. De forma predeterminada, el correo electrónico admite los protocolos HTTP y HTTPs. [Póngase en contacto con el equipo de soporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno. La restricción ayuda a mejorar la seguridad de la plataforma.

El paso de correo electrónico tiene las siguientes propiedades:

**[!UICONTROL Título]**: el título ayuda a identificar el paso en el editor de flujo de trabajo.

**[!UICONTROL Descripción]**: la explicación es útil para otros desarrolladores de procesos cuando trabaja en un entorno de desarrollo compartido.

**[!UICONTROL Asunto del correo electrónico]**: el asunto se puede recuperar de los metadatos de un flujo de trabajo, especificarse manualmente o recuperarse del valor almacenado en una variable. Seleccione entre las siguientes opciones:

* **[!UICONTROL Literal]**. Especificar manualmente un asunto.
* **[!UICONTROL Recuperar a partir de metadatos del flujo de trabajo]**. Recupere el asunto de una propiedad de metadatos.
* **[!UICONTROL Variable]**. Recupere el asunto del valor almacenado en una variable de tipo de datos de cadena.

**[!UICONTROL Plantilla de correo electrónico HTML]**. Plantilla HTML para el correo electrónico. Puede especificar variables en una plantilla de correo electrónico. El paso de correo electrónico extrae y muestra todas las variables incluidas en una plantilla para las entradas.

**[!UICONTROL Metadatos de las plantillas de correo electrónico]**: el valor de las variables de plantilla de correo electrónico puede ser un valor especificado por el usuario, la ruta de un recurso de parte del autor o en el servidor de publicación, una imagen o una propiedad de metadatos de flujo de trabajo.

* **[!UICONTROL Literal]**: utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadatos del flujo de trabajo]**: utilice la opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Después de seleccionar la opción, indique el nombre de la propiedad de metadatos en el cuadro de texto vacío debajo de la opción Metadatos del flujo de trabajo. Por ejemplo, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Imagen]**: utilice la opción para incrustar una imagen en el correo electrónico. Después de seleccionar la opción, busque y elija la imagen. La opción de imagen solo está disponible para las etiquetas de imagen (&lt;img src=&quot;&#42;&quot;/>) en la plantilla de correo electrónico.

**[!UICONTROL Dirección de correo electrónico del remitente/destinatario]**: seleccione la opción **[!UICONTROL Literal]** para especificar manualmente una dirección de correo electrónico o seleccione la opción **[!UICONTROL Recuperar a partir de metadatos del flujo de trabajo]** para recuperar la dirección de correo electrónico de una propiedad de metadatos. También puede especificar una lista de matrices de propiedades de metadatos para la opción **[!UICONTROL Recuperar a partir de metadatos del flujo de trabajo]**. Seleccione la opción **[!UICONTROL Variable]** para recuperar la dirección de correo electrónico a partir valor almacenado en una variable de tipo de datos de cadena.

* **[!UICONTROL Archivo adjunto]**: el recurso disponible en la ubicación especificada se adjunta al correo electrónico. La ruta del recurso puede ser relativa a la carga útil o a la ruta de acceso absoluta. Una ruta de ejemplo es [Payload_Directory]/attachments/.

Seleccione la opción **[!UICONTROL Variable]** para recuperar el archivo adjunto almacenado en una variable con un tipo de datos Doc, XML o JSON.

**[!UICONTROL Nombre del archivo]**: nombre del archivo adjunto del correo electrónico. El paso de correo electrónico cambia el nombre de archivo original del archivo adjunto al nombre de archivo especificado. El nombre se puede especificar manualmente o recuperar a partir de una propiedad de metadatos de flujo de trabajo o una variable. Utilice la opción **[!UICONTROL Literal]** cuando sepa el valor exacto que desea especificar. Utilice la opción **[!UICONTROL Variable]** para recuperar el nombre de archivo del valor almacenado en una variable de tipo de datos de cadena. Utilice la variable **[!UICONTROL Recuperar a partir de metadatos de flujo de trabajo]** cuando el valor que se va a utilizar se guarde en una propiedad de metadatos de flujo de trabajo.

## Paso para generar documentos de registro {#generate-document-of-record-step}

Cuando se rellena o se envía un formulario, se puede guardar un registro del formulario, en formato impreso o en formato de documento. Este registro se denomina Documento de registro (DoR). Puede utilizar el paso Generar documento de registro para crear una versión PDF de solo lectura o interactiva de un formulario adaptable. La versión en PDF contiene información rellenada en el formulario junto con la presentación del formulario adaptable.

El paso Documento de registro tiene las siguientes propiedades:

**[!UICONTROL Utilizar formulario adaptable]**: especifique el método para localizar el formulario adaptable de entrada. Puede utilizar el formulario adaptable enviado al flujo de trabajo, disponible en una ruta de acceso absoluta o disponible en una ruta de acceso de una variable. Puede utilizar una variable del tipo de datos de cadena para especificar la ruta en el campo **[!UICONTROL Seleccionar variable que resolver]**.\
Puede asociar varios formularios adaptables a un flujo de trabajo. Como resultado, se puede especificar un formulario adaptable en tiempo de ejecución mediante los métodos de entrada disponibles.

**[!UICONTROL Ruta de formulario adaptable]**: especifique la ruta del formulario adaptable. El campo está disponible al seleccionar la variable **[!UICONTROL Disponible en una ruta de acceso absoluta]** del campo **[!UICONTROL Utilizar formulario adaptable]**.

**[!UICONTROL Seleccionar datos de entrada mediante]**: ruta de los datos de entrada para el formulario adaptable. Puede mantener los datos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los datos o recuperar datos almacenados en una variable con un tipo de datos Doc, JSON o XML. Los datos de entrada se combinan con el formulario adaptable para crear un documento de registro.

**[!UICONTROL Seleccionar ruta de acceso de los datos adjuntos de entrada mediante]**: ruta de los archivos adjuntos. Estos archivos adjuntos se incluyen en el documento de registro. Puede mantener los archivos adjuntos en una ubicación relativa a la carga útil, especificar una ruta absoluta de los archivos adjuntos o recuperar los archivos adjuntos almacenados en una variable de matriz con un tipo de datos Doc.

Si especifica la ruta de una carpeta, por ejemplo, los archivos adjuntos, todos los archivos disponibles directamente en la carpeta se adjuntan al documento de registro. Si hay archivos disponibles en las carpetas accesibles directamente en la ruta de datos de los archivos adjuntos especificada, los archivos se incluyen en el documento de registro como archivos adjuntos. Si hay carpetas en carpetas accesibles directamente, esas carpetas se omiten.

**[!UICONTROL Guardar documento de registro generado mediante las siguientes opciones]**: especifique la ubicación para mantener un archivo de documento de registro. Puede sobrescribir la carpeta de carga útil, colocar el documento de registro en una ubicación del directorio de carga útil o almacenar el documento de registro en una variable de tipo de datos de Documento.

**[!UICONTROL Configuración regional]**: especifique el idioma del documento de registro. Seleccione **[!UICONTROL Literal]** para elegir la configuración regional de una lista desplegable o seleccione **[!UICONTROL Variable]** para recuperar la configuración regional a partir del valor almacenado en una variable de tipo de datos de cadena. Definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **en_US** para inglés y **fr_FR** para francés.

## Paso para invocar DDX {#invokeddx}

Document Description XML (DDX) es un lenguaje declarativo de marcado cuyos elementos representan componentes básicos de documentos. Estos componentes básicos incluyen documentos PDF y XDP, y otros elementos como comentarios, marcadores y texto con estilo. DDX define un conjunto de operaciones que se pueden aplicar en uno o varios documentos de entrada para generar uno o más documentos de salida. Se puede utilizar un solo DDX con una amplia gama de documentos de origen. Puede usar el ***paso para invocar DDX*** en un flujo de trabajo AEM para realizar varias operaciones, como Ensamblaje y Desensamblaje de documentos, crear y modificar Acrobat y XFA Forms, y otras que se describen en [Documentación de referencia DDX](https://helpx.adobe.com/content/dam/help/es/experience-manager/forms-cloud-service/ddxRef.pdf).

El paso Invocar DDX tiene las siguientes propiedades:

**[!UICONTROL Documentos de entrada]**: se utiliza para establecer las propiedades de un documento de entrada. Hay varias opciones disponibles en esta pestaña:
* **[!UICONTROL Especificar DDX mediante]**: especifica el documento de entrada que puede ser relativo a la carga útil, tener una ruta de acceso absoluta, puede proporcionarse como carga útil o almacenarse en una variable con un tipo de datos tipo Doc.
* **[!UICONTROL Crear Mapa de Carga útil]**: agregue todos los documentos de la carpeta de carga útil al Mapa del documento de entrada para la API de invocación en el Ensamblador. El nombre de nodo de cada documento se utiliza como clave en el mapa.
* **[!UICONTROL Mapa del documento de entrada]**: la opción se usa para agregar varias entradas mediante el botón **[!UICONTROL AGREGAR]**. Cada entrada representa la clave del documento en el mapa y el origen del documento.

**[!UICONTROL Opciones de entorno]**: esta opción se utiliza para definir la configuración de procesamiento de la API de invocación. Hay varias opciones disponibles en esta pestaña:
* **[!UICONTROL Validar solo]**: comprueba la validez del documento DDX de entrada.
* **[!UICONTROL Finalizar al producirse un error]**: valor booleano que indica si el servicio de API de invocación falla, en caso de error o no. De forma predeterminada, su valor se establece en False.
* **[!UICONTROL Primer número Bates]**: especifica el número, que incrementa de forma automática. Este número de aumento automático se muestra en cada página consecutiva de forma automática.
* **[!UICONTROL Estilo predeterminado]**: define el estilo predeterminado del archivo de salida.

>[!NOTE]
>
>Las opciones de entorno se mantienen sincronizadas con las API de HTTP.

**[!UICONTROL Documentos de salida]**: especifica la ubicación para guardar el archivo de salida. Hay varias opciones disponibles en esta pestaña:
* **[!UICONTROL Guardar salida en carga útil]**: guarda los documentos de salida en la carpeta de carga útil o sobrescribe la carga útil, en caso de que esta sea un archivo.
* **[!UICONTROL Mapa del documento de salida]**: especifica la ubicación para guardar cada archivo de documento explícitamente, añadiendo una entrada por documento. Cada entrada representa el documento y la ubicación donde guardarlo. Si hay varios documentos de salida, se utiliza esta opción.

## Paso para invocar el servicio de modelo de datos de formulario (FDM) {#invoke-form-data-model-service-step}

Puede usar la integración de datos de [[!DNL AEM Forms] ](data-integration.md) para configurar y conectarse a fuentes de datos dispares. Estas fuentes de datos pueden ser un servicio web, un servicio REST, un servicio OData y una solución CRM. La integración de datos de [!DNL AEM Forms] le permite crear un modelo de datos de formulario (FDM) que incluya varios servicios para realizar operaciones de recuperación, adición y actualización de datos en la base de datos configurada. Puede usar el **[!UICONTROL paso para invocar el servicio de modelo de datos]** para seleccionar un modelo de datos de formulario (FDM) y utilizar los servicios de FDM para recuperar, actualizar o agregar datos a distintos orígenes de datos.

Para explicar las entradas de los campos del paso, se utilizan como ejemplo la siguiente tabla de base de datos y el archivo JSON:

**[!UICONTROL Tabla de detalles del cliente de muestra]**

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Valor<br /> </td> 
  </tr> 
  <tr> 
   <td>FirstName<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>LastName</td> 
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

El paso para invocar el servicio de modelo de datos de formulario (FDM) tiene los campos siguientes para facilitar las operaciones del modelo de datos de formulario (FDM):

* **[!UICONTROL Título]**: el título del paso. Ayuda a identificar los pasos en el editor de flujo de trabajo.
* **[!UICONTROL Descripción]**: la explicación es útil para otros desarrolladores de procesos cuando trabajan en un entorno de desarrollo compartido.

* **[!UICONTROL Ruta del modelo de datos de formulario]**: examine y seleccione un modelo de datos de formulario del servidor.

* **[!UICONTROL Errores y validaciones]**: la opción permite capturar mensajes de error y especificar las opciones de validación para los datos recuperados y enviados a fuentes de datos. Con estos cambios, se puede garantizar que los datos transferidos al paso para invocar el servicio de modelo de datos de formulario (FDM) se ajusten a las restricciones de datos definidas por la fuente de datos. Para obtener más información, consulte [Validación automatizada de los datos de entrada](work-with-form-data-model.md#automated-validation-of-input-data).

* **[!UICONTROL Nivel de validación]**: existen tres categorías de validaciones: Básico, Completo y Desactivado:

   * Completo: todas las restricciones se validan.
   * Básico: solo las restricciones requeridas y las que se pueden rellenar.
   * Desactivado: no se realiza ninguna validación.

* **[!UICONTROL Finalizar flujo de trabajo en caso de error]**: cuando una restricción no se valida, el flujo de trabajo se detiene.

* **[!UICONTROL Almacenar código de error en variable]**: puede almacenar un código de error en una [variable de tipo cadena](variable-in-aem-workflows.md).

* **[!UICONTROL Almacenar mensaje de error en variable]**: puede almacenar un mensaje de error en una [variable de tipo cadena](variable-in-aem-workflows.md).

* **[!UICONTROL Almacenar detalles de error en variable]**: puede almacenar detalles de error en una [variable de tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Servicio]**: lista de los servicios que proporciona el modelo de datos de formulario (FDM) seleccionado.
* **[!UICONTROL Entrada para servicios]** > **[!UICONTROL Proporcionar datos de entrada utilizando metadatos literales, variables o de flujo de trabajo, y un archivo JSON]**: un servicio puede tener varios argumentos. Seleccione la opción para obtener el valor de los argumentos de servicio de una propiedad de metadatos de flujo de trabajo, un objeto JSON o una variable, o indique directamente el valor en el cuadro de texto proporcionado:

   * **[!UICONTROL Literal]**: utilice la opción cuando conozca el valor exacto que desea especificar. Por ejemplo, srose@we.info.
   * **[!UICONTROL Variable]**: utilice la opción para recuperar el valor almacenado en una variable.
   * **[!UICONTROL Recuperar a partir de metadatos de flujo de trabajo]**: utilice la opción cuando el valor que desea utilizar se guarde en una propiedad de metadatos de flujo de trabajo. Por ejemplo, emailAddress.

   * **[!UICONTROL Relativo a la carga útil]**: utilice la opción para recuperar el archivo adjunto guardado en una ruta relativa a la carga útil. Seleccione la opción y especifique el nombre de la carpeta que incluye el archivo adjunto o especifique el nombre del archivo adjunto en el cuadro de texto.

     Por ejemplo, si la carpeta Relativo a la carga útil en el repositorio CRX incluye un archivo adjunto en la ubicación `attachment\attachment-folder`, especifique `attachment\attachment-folder` en el cuadro de texto después de seleccionar la variable **[!UICONTROL Relativo a la carga útil]**.

   * **[!UICONTROL Notación de puntos JSON]**: utilice la opción cuando el valor que desea utilizar esté en un archivo JSON. Por ejemplo, insurance.customerDetails.emailAddress. La opción de notación de puntos JSON solo está disponible si se selecciona la opción Asignar campos de entrada desde la entrada JSON.
   * **[!UICONTROL Asignar campos de entrada desde la entrada JSON]**: especifique la ruta de un archivo JSON para obtener el valor de entrada de algunos argumentos de servicio del archivo JSON. La ruta del archivo JSON puede ser relativa a la carga útil, una ruta de acceso absoluta o puede seleccionar un documento JSON de entrada mediante una variable de tipo JSON o un modelo de datos de formulario (FDM).

* **[!UICONTROL Entrada para servicios]** > **[!UICONTROL Proporcionar datos de entrada mediante una variable o un archivo JSON]**: seleccione la opción para obtener valores para todos los argumentos de un archivo JSON guardado en una ruta de acceso absoluta, en una ruta relativa a la carga útil o en una variable.
* **[!UICONTROL Seleccionar el documento JSON de entrada mediante:]** el archivo JSON que contiene valores para todos los argumentos de servicio. La ruta del archivo JSON puede ser **[!UICONTROL relativa a la carga útil]** o una **[!UICONTROL ruta de acceso absoluta]**. También puede recuperar el documento JSON de entrada mediante una variable de tipo de datos JSON o un modelo de datos de formulario (FDM).

* **[!UICONTROL Notación de puntos JSON]**: deje el campo en blanco para utilizar todos los objetos del archivo JSON especificado como entrada para argumentos de servicio. Para leer un objeto JSON específico del archivo JSON especificado como entrada para los argumentos del servicio, especifique la notación de puntos para el objeto JSON. Por ejemplo: si tiene un archivo JSON similar al listado al principio de la sección, especifique insurance.customerDetails para proporcionar todos los detalles de un cliente como entrada al servicio.
* **[!UICONTROL Resultados del servicio]** > **[!UICONTROL Asignación y escritura de valores de salida en variables o metadatos]**: seleccione la opción para guardar los valores de salida como propiedades del nodo de metadatos de instancia de flujo de trabajo en el repositorio CRX. Especifique el nombre de la propiedad de metadatos y seleccione el atributo de salida del servicio correspondiente que se va a asignar con la propiedad de metadatos. Por ejemplo: asigne el número de teléfono devuelto por el servicio de salida con la propiedad phone_number (número de teléfono) de los metadatos del flujo de trabajo. Del mismo modo, se puede almacenar la salida en una variable de tipo de datos de registro. Al seleccionar una propiedad para la opción **[!UICONTROL Atributo de salida del servicio que se va a asignar]**, solo se rellenan las variables capaces de almacenar datos de la propiedad seleccionada para la opción **[!UICONTROL Guardar salida en]**.

* **[!UICONTROL Resultados del servicio]** > **[!UICONTROL Guardar resultados en una variable o un archivo JSON]**: seleccione la opción para guardar los valores de salida en un archivo JSON en una ruta de acceso absoluta, en una ruta relativa a la carga útil o en una variable.
* **[!UICONTROL Guardar documento JSON de salida con las siguientes opciones]**: guarde el archivo JSON de salida. La ruta del archivo JSON de salida puede ser relativa a la carga útil o a una ruta de acceso absoluta. También puede guardar el archivo JSON de salida con una variable de tipo de datos JSON o un modelo de datos de formulario (FDM).



## Paso para firmar el documento {#sign-document-step}

El paso Firmar documento le permite utilizar [!DNL Adobe Sign] para firmar documentos. Cuando utilice el paso del flujo de trabajo de [!DNL Adobe Sign] para firmar un formulario adaptable, el formulario se puede pasar de un firmante a otro o se puede enviar a todos los firmantes simultáneamente, en función de la configuración del paso del flujo de trabajo. Los formularios adaptables habilitados para [!DNL Adobe Sign] se envían al servidor de Experience Manager Forms solo después de que todos los firmantes completen el proceso de firma.

De forma predeterminada, el servicio del planificador de [!DNL Adobe Sign] comprueba (sondea) la respuesta del destinatario cada 24 horas. Puede [cambiar el intervalo predeterminado para su entorno](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

El paso Firmar documento tiene las siguientes propiedades:

* **[!UICONTROL Nombre del acuerdo]**: especifique el título del acuerdo. El nombre del acuerdo forma parte del asunto y del texto del cuerpo del correo electrónico enviado a los firmantes. Puede almacenar el nombre en una variable de tipo de datos de cadena o seleccionar **[!UICONTROL Literal]** para agregar el nombre manualmente.

* **[!UICONTROL Configuración regional]**: especifique el idioma para las opciones de correo electrónico y verificación. Puede almacenar la configuración regional en una variable de tipo de datos de cadena o seleccionar **[!UICONTROL Literal]** para elegir la configuración regional de la lista de opciones disponibles. Debe definir el código de configuración regional mientras almacena el valor de la configuración regional en una variable. Por ejemplo, especifique **[!UICONTROL en_US]** para inglés y **[!UICONTROL fr_FR]** para francés.

* **[!UICONTROL Configuración de Adobe Sign Cloud]**: elija una configuración de [!DNL Adobe Sign] Cloud. Si no ha configurado [!DNL Adobe Sign] para [!DNL AEM Forms], consulte [Integrar Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Seleccionar documento para firmar mediante]**: puede elegir un documento de una ubicación relativa a la carga útil, utilizar la carga útil como documento, especificar una ruta de acceso absoluta del documento o recuperar el documento almacenado en una variable de tipo de datos de Documento.
* **[!UICONTROL Días hasta la fecha límite]**: un documento se marca con vencimiento (fecha límite superada) después de que no haya actividad en la tarea por el número de días especificado en el campo **[!UICONTROL Días hasta la fecha límite]**. El número de días se cuenta después de que la documentación se asigna a un usuario para su firma.
* **[!UICONTROL Frecuencia del correo electrónico de recordatorio]**: puede enviar un correo electrónico de recordatorio a intervalos diarios o semanales. La semana se cuenta desde el día en que se asigna la documentación a un usuario para su firma.
* **[!UICONTROL Proceso de firma]**: puede optar por firmar un documento en orden secuencial o paralelo. En orden secuencial, un solo firmante a la vez recibe el documento para su firma. Una vez que el primer firmante completa la firma del documento, el documento se envía al segundo firmante, y así sucesivamente. En orden paralelo, varios firmantes pueden firmar un documento a la vez.
* **[!UICONTROL URL de redireccionamiento]**: especifique una URL de redireccionamiento. Una vez firmado el documento, puede redirigir al usuario asignado a una dirección URL. Normalmente, esta URL contiene un mensaje de agradecimiento o instrucciones adicionales.
* **[!UICONTROL Fase del flujo de trabajo]**: un flujo de trabajo puede tener varias fases. Estas fases se muestran en la bandeja de entrada AEM. Puede definir estas fases en las propiedades del modelo (**[!UICONTROL Barra de tareas]** > **[!UICONTROL Página]** > **[!UICONTROL Propiedades de página]** > **[!UICONTROL Fases]**).
* **[!UICONTROL Seleccionar firmantes]**: especifique el método para elegir firmantes para el documento. Puede asignar dinámicamente el flujo de trabajo a un usuario o grupo, o agregar manualmente los detalles de un firmante. Al seleccionar Manualmente en el menú desplegable, se agregan detalles del destinatario como Correo electrónico, Función y Método de autenticación.

  >[!NOTE]
  >
  >* En la sección Función, puede especificar la función de destinatario como Firmante, Aprobador, Aceptante, Destinatario certificado, Rellenador de formulario y Delegador.
  >* Si selecciona Delegador en la opción Función, el Delegado puede asignar la tarea de firma a otro destinatario.
  >* Si ha configurado un método de autenticación para [!DNL Adobe Sign], en función de su configuración, seleccionará un método de autenticación, como autenticación basada en el teléfono, autenticación basada en la identidad social, autenticación basada en el conocimiento o autenticación basada en la identidad oficial.

* **[!UICONTROL Script o servicio para seleccionar firmantes]**: la opción solo está disponible si la opción Dinámicamente está seleccionada en el campo Seleccionar firmantes. Puede especificar un ECMAScript o un servicio para elegir los firmantes y las opciones de verificación de un documento.
* **[!UICONTROL Detalles del destinatario]**: la opción solo está disponible si la opción Manualmente está seleccionada en el campo Seleccionar firmantes. Especifique la dirección de correo electrónico y elija un mecanismo de verificación opcional. Antes de seleccionar un mecanismo de verificación de 2 pasos, asegúrese de que la opción de verificación correspondiente esté habilitada para la cuenta de [!DNL Adobe Sign]. Puede utilizar una variable del tipo de datos de cadena para definir los valores de los campos Correo electrónico, Código de país y Número de teléfono. Los campos código de país y número de teléfono solo se mostrarán si selecciona Verificación por teléfono de la lista desplegable verificación en dos pasos.
* **[!UICONTROL Documento firmado]**: puede guardar el estado del documento firmado en Variable. Para añadir una pista de auditoría de firma electrónica para una mayor seguridad y legalidad al documento firmado, puede seleccionar Incluir informe de auditoría. Puede guardar el documento firmado mediante la carpeta Variable o Carga útil.

  >[!NOTE]
  >
  > El informe de auditoría se añade a la última página del documento firmado.

<!--
## Document Services steps {#document-services-steps}

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
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## Paso Generar una salida impresa {#generatePrintedOutput}

El paso genera una salida PCL, PostScript, ZPL, IPL, TPCL o DPL a partir de un diseño de formulario y un archivo de datos. El archivo de datos se combina con el diseño de formulario y se le aplica un formato para imprimirlo. La salida generada por este paso se puede enviar directamente a una impresora o guardarse como archivo. Se recomienda utilizar este paso cuando desee utilizar diseños de formulario o datos de una aplicación. Si los diseños de formulario se encuentran en la red, el sistema local de archivos o la ubicación HTTP, utilice la operación generatePrintedOutput.

Por ejemplo, la aplicación requiere que combine un diseño de formulario con un archivo de datos. Los datos contienen cientos de registros. Además, requiere que la salida se envíe a una impresora compatible con ZPL. El diseño de formulario y los datos de entrada se encuentran en una aplicación. Utilice la operación generatePrintedOutput para combinar cada registro con un diseño de formulario y enviar la salida a una impresora compatible con ZPL.

El paso Generar salida impresa tiene las siguientes propiedades:

**[!UICONTROL Propiedades de entrada]**

* **[!UICONTROL Seleccionar el archivo de plantilla mediante:]** especifica la ruta del archivo de la plantilla. Puede seleccionar la plantilla mediante la ruta relativa a la carga útil, guardada en una ruta absoluta o mediante una variable de tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla. Además, también puede aceptar la carga útil como archivo de datos de entrada.

* **[!UICONTROL Seleccionar documento de datos mediante]**: especificar la ruta de un archivo de datos de entrada. Puede seleccionar los datos de entrada mediante la ruta relativa a la carga útil, guardada en una ruta absoluta o mediante una variable de tipo de datos Doc. Por ejemplo, [Payload_Directory]/Workflow/data.xml. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

* **[!UICONTROL Formato de impresora]**: valor del formato de impresión que especifica el idioma de descripción de la página que se utilizará, cuando no se proporcione un archivo XDC, para generar el flujo de salida. Si proporciona un valor literal, seleccione uno de estos valores:

   * **[!UICONTROL PCL de color]**: utilice la opción para especificar un archivo XDC para PCL.
   * **[!UICONTROL PostScript genérico]**: utilice la opción para especificar un archivo XDC genérico para PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: utilice ZPL 300 DPI. Se utiliza zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: utilice ZPL 600 DPI. Se utiliza el archivo zpl600.xdc.
   * **[!UICONTROL IPL 300 DPI]**: utilice IPL 300 DPI. Se utiliza ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: utilice IPL 400 DPI. Se utiliza el archivo ipl400.xdc.
   * **[!UICONTROL TPCL 600 DPI]**: utilice TPCL 600 DPI. Se utiliza el archivo tpcl600.xdc.
   * **[!UICONTROL PostScript sin formato]**: utilice la opción para especificar un archivo XDC de texto sin formato para PostScript.
   * **[!UICONTROL DPL300DPI]**: utilice DPL 300 DPI. Se utiliza el dpl300.xdc.
   * **[!UICONTROL DPL400DPI]**: utilice DPL 400 DPI. Se utiliza el dpl400.xdc.
   * **[!UICONTROL DPL600DPI]**: utilice DPL 600 DPI. Se utiliza el dpl600.xdc.
   * **[!UICONTROL HP_PCL_5e]**: utilice la opción para admitir varios dispositivos Canon.


**[!UICONTROL Propiedades de salida]**

* **[!UICONTROL Guardar documento de salida mediante]**: especifica la ubicación para guardar el archivo de salida. Puede guardar el archivo de salida en una ubicación relativa a la carga útil, en una variable o especificar una ubicación absoluta para guardar el archivo de salida. Si la ruta no existe en el repositorio crx, un administrador puede crear la ruta antes de utilizarla.

**[!UICONTROL Propiedades avanzadas]**

* **[!UICONTROL Seleccionar la ubicación raíz del contenido mediante]**: la raíz del contenido es un valor de cadena que especifica el URI, la referencia absoluta o la ubicación en el repositorio para recuperar los recursos relativos que utiliza el diseño de formulario. Por ejemplo, si el diseño de formulario hace referencia a una imagen de forma relativa, como `../myImage.gif`, `myImage.gif` debe estar en `repository://`. El valor predeterminado es `repository://`, que apunta al nivel raíz del repositorio.

  Cuando elige un recurso de la aplicación, la ruta del URI raíz del contenido debe tener la estructura correcta. Por ejemplo, si se selecciona un formulario de una aplicación denominada SampleApp y se coloca en `SampleApp/1.0/forms/Test.xdp`, el URI de raíz de contenido debe especificarse como `repository://administrator@password/Applications/SampleApp/1.0/forms/` o `repository:/Applications/SampleApp/1.0/forms/` (cuando la autoridad sea nula). Cuando se especifica el URI de la raíz de contenido de esta forma, las rutas de todos los recursos a los que se hace referencia en el formulario se resuelven en relación con este URI.

* **[!UICONTROL Seleccionar el archivo XCI mediante]**: los archivos XCI se utilizan para describir fuentes y otras propiedades que se utilizan para elementos de diseño de formulario. Puede mantener un archivo XCI relativo a la carga útil, en una ruta absoluta o mediante una variable del tipo de datos Document.

* **[!UICONTROL Configuración regional]**: especifica el idioma que se utiliza para generar el documento PDF. Si proporciona un valor literal, seleccione un idioma de la lista o seleccione uno de estos valores:
   * **[!UICONTROL Para usar el servidor predeterminado]**: (Predeterminado) Use la configuración regional configurada en el servidor de [!DNL AEM Forms]. La configuración regional se configura con la consola de administración. (Consulte [Ayuda de Designer](https://helpx.adobe.com/content/dam/help/es/experience-manager/6-5/forms/pdf/using-designer.pdf)).

   * **[!UICONTROL Para utilizar un valor personalizado]**: escriba el código de configuración regional en el cuadro literal o seleccione una variable de cadena que contenga el código de configuración regional. Para obtener una lista completa de los códigos de configuración regional admitidos, consulte https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copias]**: valor entero que especifica el número de copias que se generarán para la salida. El valor predeterminado es 1.

* **[!UICONTROL Impresión a doble cara]**: valor de Paginación que especifica si se utiliza la impresión a doble o a una sola cara. Las impresoras compatibles con PostScript y PCL utilizan este valor. Si proporciona un valor literal, seleccione uno de estos valores:
   * **[!UICONTROL Borde largo a doble cara]**: utiliza la impresión a doble cara y la impresión mediante paginación de borde largo.
   * **[!UICONTROL Borde corto a doble cara]**: utiliza la impresión a doble cara y la impresión mediante paginación de borde corto.
   * **[!UICONTROL Simple]**: utiliza la impresión a una sola cara.

## Generar etapa de Salida PDF no interactiva {#generatePDFdocuments}

1. Arrastre el flujo de trabajo Generar salida PDF no interactiva a la pestaña Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, los documentos de salida y los parámetros adicionales, y haga clic en **[!UICONTROL Aceptar]**.

### Documentos de entrada {#input-documents-3}

* **Archivo de plantilla**: especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* **Documento de datos**: especifica la ubicación del XML de datos que debe combinarse con la plantilla.

### Documento de salida {#output-document}

**Documento de salida**: especifica el nombre del formulario PDF generado.

### Parámetros adicionales {#additional-parameters-1}

* **Raíz de contenido**: especifica la ruta de la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* **Configuración regional**: especifica la configuración regional predeterminada para el formulario PDF generado.
* **Versión de Acrobat**: especifica la versión de Acrobat de destino del formulario PDF generado.
* **PDF linearizado**: especifica si se debe optimizar el PDF generado para la visualización web.
* **PDF etiquetado**: especifica si se debe hacer accesible el PDF generado.
* **Documento XCI**: especifica la ruta del archivo XCI.

## Ver también {#see-also}

* [Variables en flujos de trabajo de AEM centrados en Forms](/help/forms/variable-in-aem-workflows.md)
* [Configuración del ajuste Fuera de la oficina](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->