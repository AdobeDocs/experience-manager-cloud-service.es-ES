---
title: Configurar  [!DNL Workfront for Experience Manager enhanced connector]
description: Configurar  [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: d4e1247a-342c-4bc4-83bf-4e4902468fb3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 1%

---

# Configuración de [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-configure.html) |
| AEM as a Cloud Service | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] configura el conector mejorado después de instalarlo. Para obtener instrucciones de instalación, consulte [Instalar el conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
> A partir de junio de 2022, Adobe lanzó una nueva integración nativa para conectar Workfront con Adobe Experience Manager Assets as a Cloud Service. Esta integración se ha convertido en el método requerido para conectar estas dos soluciones. Cualquier nueva implementación futura del conector mejorado (1.9.8 y posterior) para conectar Workfront con AEM Assets as a Cloud Service está bloqueada.

>[!IMPORTANT]
>
>* Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones mejoradas de instalación del conector](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configuración de suscripciones a eventos {#event-subscriptions}

Las suscripciones a eventos se usan para notificar a AEM los eventos que tienen lugar en [!DNL Adobe Workfront]. Hay tres características de [!DNL Workfront for Experience Manager enhanced connector] que necesitan suscripciones de evento para funcionar, estas son:

* Creación automática de carpetas vinculadas a proyectos.
* Sincronización de cambios en los valores de formulario personalizados de documentos de Workfront con los metadatos de recursos de AEM.
* Publicación automática de recursos en Brand Portal al finalizar el proyecto.

Para utilizar estas funciones, habilite las suscripciones a eventos.

* Edite la configuración de [!UICONTROL Workfront Tools] Cloud Services que creó en el paso 5 y seleccione la pestaña [!UICONTROL Event Subscriptions].
* Seleccione la [!UICONTROL integración personalizada de Workfront] que creó en la sección 6.
* Haga clic en [!UICONTROL Habilitar suscripciones a eventos de Workfront].

  ![Suscripción de evento](/help/assets/assets/event-subs.png)

## Configuración de carpetas vinculadas {#linked-folders}

Para suscribirse a los eventos, siga estos pasos:

1. Vaya a la pestaña **[!UICONTROL Suscripciones de eventos]** en los servicios en la nube.
1. Seleccione la integración personalizada creada en [!DNL Workfront].
1. Haga clic en **[!UICONTROL Habilitar suscripciones a eventos de Workfront]**.

### Configuración de estructura de carpetas vinculadas {#linked-folder-structure}

1. Vaya a la pestaña Carpetas vinculadas del proyecto en los servicios en la nube.
1. Ruta principal de la carpeta vinculada: seleccione una carpeta en DAM en la que desee crear las carpetas vinculadas. Si se deja vacío, el valor predeterminado será /content/dam. Asegúrese de que el esquema de metadatos de Workfront Tools y el esquema de metadatos de la carpeta de carpetas vinculadas de Workfront se hayan aplicado a la carpeta seleccionada.
1. Estructura de carpetas vinculadas: introduzca valores separados por comas. Cada valor debe ser `DE:<some-project-custom-form-field>`, Portfolio, Program, Year, Name o algún &quot;Valor de cadena literal&quot; (este último entre comillas). Actualmente está establecido en Portfolio, Programa, Año, DE: Tipo de proyecto, Nombre.
1. Configurar permisos: agregar permisos de `jcr:all permissions` a `/conf/workfront-tools/settings/cloudconfigs` para el grupo `wf-workfront-users`.
1. La casilla de verificación Generar título de carpeta vinculado en Workfront mediante los nombres de estructura de carpetas debe activarse si el título de la carpeta en Workfront debe incluir todas las carpetas de la estructura. De lo contrario, es el título de la última carpeta.
1. Subcarpetas multicampo permite especificar una lista de carpetas que deben crearse como una carpeta secundaria de la carpeta vinculada.
1. Estado del proyecto: seleccione el estado para el que se debe configurar el proyecto para crear la carpeta vinculada.
1. Crear una carpeta vinculada en proyectos con portafolio: lista de portafolios a los que debe pertenecer el proyecto para poder crear la carpeta vinculada. Deje esta lista vacía para crear la carpeta vinculada para todo el portafolio de proyectos.
1. Crear una carpeta vinculada en proyectos con un campo de formulario personalizado: Campo de formulario personalizado y su valor correspondiente que debe tener el proyecto para poder crear la carpeta vinculada. Esta configuración se ignora si se deja vacía. Seleccione `CUSTOM FORMS: Create DAM Linked Folder` para el campo y escriba `Yes` para el valor.
1. Configurar permiso: configure estos permisos, `jcr:all permissions for /conf/workfront-tools/settings/cloudconfigs` para `wf-workfront-users group`.
1. Haga clic en Habilitar la creación automática de carpetas vinculadas. Si vuelve a la pestaña Suscripciones de eventos, verá que ahora hay un evento de creación.

![configuración de carpeta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Asignación de esquema de metadatos {#metadata-schema-mapping}

### Configurar asignación de metadatos de carpeta {#folder-metadata-mapping}

La asignación de metadatos entre los proyectos de Workfront y las carpetas de AEM se define en los esquemas de metadatos de carpeta de AEM. Los esquemas de metadatos de carpeta deben crearse y configurarse como de costumbre en AEM. Workfront Tools agrega un menú desplegable de autocompletar a la pestaña Configuración de configuración de cada campo del formulario de esquema de metadatos de carpeta. Este menú desplegable de autocompletar le permite especificar a qué campo de Workfront debe asignarse cada propiedad de carpeta de AEM.

Para configurar las asignaciones, siga estos pasos:

1. Agregar permisos de `jcr:read` a `/conf/global/settings/dam/adminui-extension/foldermetadataschema` para el grupo `wf-workfront-users`.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos de carpeta]**.
1. Seleccione el formulario de esquema de metadatos de carpeta que desee editar y haga clic en Editar.
1. Seleccione el campo del formulario del esquema de metadatos de la carpeta que desea editar y seleccione la pestaña Configuración en el panel derecho.
1. En el campo [!UICONTROL Asignado desde el campo de Workfront], seleccione el nombre del campo de Workfront que desea asignar a la propiedad de carpeta de AEM seleccionada. Las opciones disponibles son:

   * Campos de formulario personalizados del proyecto
   * Campos de Información general del proyecto (ID, nombre, descripción, número de referencia, fecha planificada de finalización, propietario del proyecto, patrocinador del proyecto, Portfolio o programa)

![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configuración de la asignación de metadatos de recursos {#asset-metadata-mapping}

La asignación de metadatos entre Documentos de Adobe Workfront y Assets se define en Esquemas de metadatos de AEM. Los esquemas de metadatos deben crearse y configurarse como de costumbre en AEM. Workfront Tools agrega opciones de configuración a la pestaña Configuración de cada campo del formulario de esquema de metadatos. Estas opciones le permiten especificar a qué campo de Workfront debe asignarse cada propiedad de AEM.

Para configurar las asignaciones, siga estos pasos:

1. Vaya a **Herramientas** > **Assets** > **Esquemas de metadatos**.
1. Seleccione el formulario de esquema de metadatos que desee editar y haga clic en **Editar** o cree un esquema de metadatos desde cero.
1. Seleccione el campo del formulario de esquema de metadatos que desee editar y seleccione la pestaña **Configuración** en el panel derecho.
1. En Campo de formulario personalizado [!DNL Workfront], seleccione el nombre del campo [!DNL Workfront] que desea asignar a la propiedad de AEM seleccionada. Las opciones disponibles son:

   * Documentar campos de formulario personalizados
   * Campos de formulario personalizados del proyecto
   * Emitir campos de formulario personalizados
   * Campos de formulario personalizados de tarea
   * Campos Información general del proyecto (ID, Nombre, Descripción o Número de referencia)

1. En caso de que el campo [!DNL Workfront] seleccionado en [!UICONTROL Campo de formulario personalizado de Workfront] sea un campo de escritura anticipada de usuario de Workfront, es necesario especificar qué campo de usuario de Workfront desea asignar. Para ello, marque Obtener valor del campo de objeto al que se hace referencia en Workfront y, a continuación, especifique el nombre del [!UICONTROL Campo de formulario personalizado de usuario de Workfront] desde el que recuperar el valor que se va a asignar.

   ![configuración de asignación de metadatos](/help/assets/assets/wf-metadata-mapping-config1.png)

## Asignar propiedad {#map-property}

Este paso del flujo de trabajo permite que un usuario asigne una propiedad a un formulario personalizado [!DNL Workfront] en un proyecto, tarea, problema o documento. El artefacto [!DNL Workfront] al que afecta este paso se busca usando una ruta relativa desde la carga útil. Las propiedades que se van a asignar se controlan desde la configuración del cuadro de diálogo de pasos.

**Tipo**: este campo permite seleccionar el tipo de objeto de Workfront al que se deben asignar las propiedades.

**Propiedad de ID**: este campo permite especificar la ruta al ID del objeto de Workfront al que se deben asignar las propiedades. La ruta especificada en este campo debe ser relativa a la carga útil del flujo de trabajo.

**Asignaciones de propiedades**: este campo múltiple permite especificar las asignaciones entre las propiedades de AEM y los campos de Workfront. Cada elemento del campo múltiple especificará una asignación. Cada asignación debe tener el formato `<workfront-field>=<aem-mapped-property>`.

* El `workfront-field` puede ser

   * Campo de formulario personalizado identificado con el prefijo `DE:`.
   * Campo editable identificado por su nombre. Los nombres de campo se encuentran en [[!DNL Workfront] Explorador de API](https://experience.workfront.com/s/api-explorer).

* El(la) `aem-mapped-property` puede ser:

   * Un valor literal. Deben ir entre comillas.
   * Una propiedad de AEM. Esta referencia debe ser relativa a la carga útil del flujo de trabajo.
   * Un valor con nombre. Estos deben ir entre corchetes.
   * Una concatenación de los tres elementos anteriores. Especifíquelo usando `{+}`.
   * Una modificación de los tres elementos anteriores al rodear el valor con `{replace(<value>,"old-char","new-char")}`.

* Algunos ejemplos son:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configuración para asignar la propiedad](/help/assets/assets/wf-map-property-config.png)

## Definir estado {#set-status}

En el editor de flujo de trabajo, edite las propiedades de **[!UICONTROL Workfront - Set Status]** en la pestaña **[!UICONTROL Arguments]**.

![Editar flujo de trabajo para establecer el estado](/help/assets/assets/wf-set-status.png)

## Sincronización de comentarios {#comments-sync}

1. En [!DNL Experience Manager], acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**, seleccione la configuración y seleccione **[!UICONTROL Propiedades]**.

   ![comentarios sincronizados](/help/assets/assets/comments-sync1.png)

1. Seleccione la ficha **[!UICONTROL Suscripciones de eventos]**, haga clic en **[!UICONTROL Habilitar sincronización de comentarios]** en la opción **[!UICONTROL Enviar comentarios realizados en Workfront a AEM]**.

   ![La sincronización está habilitada](/help/assets/assets/wf-comment-sync-enabled.png)

Para probar la sincronización de comentarios de Workfront a AEM, siga estos pasos:

1. Vaya a un documento vinculado en Workfront y añada un comentario en la pestaña Actualizaciones.

   ![dejar comentario en Workfront](/help/assets/assets/comments-sync2.png)

1. Vaya al mismo documento vinculado en AEM, seleccione el documento, abra la opción [!UICONTROL Cronología] en el panel de navegación izquierdo y seleccione [!UICONTROL Comentarios]. La barra lateral izquierda muestra los comentarios sincronizados de [!DNL Workfront].

## Versiones de recursos {#asset-versions}

Para mantener el historial de versiones de los recursos en AEM, configure las versiones de los recursos en AEM.

1. En Experience Manager, accede a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Workfront Tools]** y abre la pestaña **[!UICONTROL Avanzadas]**.

1. Seleccione la opción **[!UICONTROL Almacenar recursos con el mismo nombre que las versiones del recurso existente]**. Cuando se selecciona, esta opción permite almacenar recursos cargados con el mismo nombre y en la misma ubicación que la versión del recurso existente. Si no se selecciona, se crea un nuevo recurso con un nombre diferente (por ejemplo, `asset-name.pdf` y `asset-name-1.pdf`).

1. Seleccione la opción **[!UICONTROL Actualizar metadatos del recurso al crear una nueva versión]**. Cuando se selecciona, esta opción actualiza los metadatos del recurso cada vez que se crea una nueva versión del recurso. Si no se selecciona, el recurso conservará los metadatos que tenía antes de crear la nueva versión.

![configurar versiones de recursos](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Las versiones no son compatibles con las carpetas vinculadas. Al crear una revisión [!DNL Workfront] con un documento dentro de una carpeta vinculada, se eliminan los comentarios y anotaciones de la versión anterior del recurso.

## Adjuntar formularios personalizados {#attach-custom-forms}

Este paso del flujo de trabajo permite a los usuarios adjuntar un formulario personalizado a un artefacto [!DNL Workfront]. Este paso del flujo de trabajo se puede agregar a cualquier modelo de flujo de trabajo. El artefacto [!DNL Workfront] al que afecta este paso se busca usando una ruta relativa desde la carga útil.

En el editor de flujo de trabajo de Experience Manager, edite las propiedades del paso de flujo de trabajo [!UICONTROL Workfront - Adjuntar formulario personalizado].

![formularios personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicar recursos automáticamente {#auto-publish-assets}

1. En Experience Manager, accede a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Workfront Tools]** y abre la pestaña **[!UICONTROL Avanzadas]**.

1. Seleccione **[!UICONTROL Publicar recursos automáticamente cuando se envíen desde Workfront]**. Esta opción permite la publicación automática de recursos cuando se envían de Workfront a AEM. Esta función se puede habilitar de forma condicional especificando un campo de formulario personalizado de Workfront y el valor en el que debe establecerse. Siempre que se envía un documento a AEM, si cumple la condición, el recurso se publica automáticamente.

1. Seleccione **[!UICONTROL Publicar todos los recursos del proyecto en Brand Portal al finalizar el proyecto]**. Esta opción habilita la publicación automática de recursos en [!DNL Brand Portal] cuando el estado del proyecto de Workfront al que pertenecen se cambia a `Complete`.

![configurar publicación automática](/help/assets/assets/wf-auto-publish-config.png)

## Actualizaciones de formularios personalizados de documentos de Workfront {#subscribe-workfront-doc-custom-form-updates}

Para suscribirse a los cambios en los formularios personalizados de documento [!DNL Workfront], seleccione la opción correspondiente en la pestaña **[!UICONTROL Avanzado]**. Al suscribirse a estas actualizaciones, se actualizan los campos de metadatos asignados de [!DNL Experience Manager] cuando se cambia el campo correspondiente del formulario personalizado del documento [!DNL Workfront].

![El documento de Workfront actualiza la configuración del formulario personalizado en [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
