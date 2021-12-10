---
title: Administrar aplicaciones y tareas de Forms en AEM bandeja de entrada
seo-title: Manage Forms applications and tasks in AEM Inbox
description: AEM Bandeja de entrada le permite iniciar flujos de trabajo centrados en Forms enviando aplicaciones y administrando tareas.
seo-description: AEM Inbox allows you to launch Forms-centric workflows through submitting applications and manage tasks.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 2%

---


# Administrar aplicaciones y tareas de Forms en AEM bandeja de entrada{#manage-forms-applications-and-tasks-in-aem-inbox}

Una de las muchas maneras de iniciar o déclencheur un flujo de trabajo centrado en Forms es a través de las aplicaciones en AEM Bandeja de entrada. Debe crear una aplicación de flujo de trabajo para que un flujo de trabajo de Forms esté disponible como aplicación en la Bandeja de entrada. Para obtener más información sobre la aplicación de flujo de trabajo y otras formas de iniciar flujos de trabajo de Forms, consulte [Iniciar un flujo de trabajo centrado en Forms en OSGi](aem-forms-workflow.md#launch).

Además, AEM Bandeja de entrada consolida las notificaciones y tareas de varios componentes de AEM, incluidos los flujos de trabajo de Forms. Cuando se activa un flujo de trabajo de formularios que contiene un paso Asignar tarea , la aplicación asociada aparece como una tarea en la bandeja de entrada del usuario asignado. Si el usuario asignado es un grupo, la tarea aparece en la Bandeja de entrada de todos los miembros del grupo hasta que un individuo solicite o delegue la tarea.

La interfaz de usuario de la Bandeja de entrada proporciona vistas de lista y calendario para ver las tareas. También puede configurar la configuración de vista. Puede filtrar tareas en función de varios parámetros. Para obtener más información sobre la vista y los filtros, consulte [Su bandeja de entrada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#inbox-in-the-header).

En resumen, la Bandeja de entrada permite crear una nueva aplicación y administrar las tareas asignadas.

>[!NOTE]
>
>Debe ser miembro de [!DNL workflow-users] para poder utilizar AEM Bandeja de entrada.

## Crear aplicación {#create-application}

1. Vaya a AEM bandeja de entrada en https://&#39;[server]:[puerto]&#39;/aem/inbox.
1. En la interfaz de usuario de la bandeja de entrada, pulse **[!UICONTROL Crear > Aplicación]**. Aparece la página Seleccionar aplicación .
1. Seleccione una aplicación y haga clic en **[!UICONTROL Crear]**. Se abre el formulario adaptable asociado a la aplicación. Rellene la información del formulario adaptable y pulse **[!UICONTROL Submit]**. Inicia el flujo de trabajo asociado y crea una tarea en la bandeja de entrada del usuario asignado.

## Administrar tareas {#manage-tasks}

Cuando un flujo de trabajo de Forms déclencheur y usted es un usuario asignado o parte del grupo de usuarios asignados, aparece una tarea en la bandeja de entrada. Puede ver los detalles de las tareas y realizar las acciones disponibles en la tarea desde la bandeja de entrada.

### Reclamar o delegar tareas {#claim-or-delegate-tasks}

Las tareas asignadas a un grupo aparecen en la bandeja de entrada de todos los miembros del grupo. Cualquier miembro del grupo puede reclamar esa tarea o delegarla a otro miembro del grupo. Para ello:

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea aparecen en la parte superior.

   ![select-task](assets/select-task.png)

1. Realice una de las acciones siguientes:

   * Para delegar la tarea, pulse **[!UICONTROL Delegar]**. Se abre el cuadro de diálogo Delegar elemento. Seleccione un usuario, opcionalmente añada un comentario y pulse **[!UICONTROL OK]**.

   ![delegate](assets/delegate.png)

   * Para reclamar la tarea, pulse **[!UICONTROL Apertura]**. Se abrirá el cuadro de diálogo Asignar a sí mismo. Toque **[!UICONTROL Continuar]** para reclamar la tarea. La tarea reclamada aparece con usted como el usuario asignado en su Bandeja de entrada.

   ![presentar](assets/claim.png)

### Ver detalles y realizar acciones en tareas {#view-details-and-perform-actions-on-tasks}

Al abrir una tarea, puede ver los detalles de la tarea y realizar las acciones disponibles. Las acciones disponibles para una tarea se definen en el paso Assign task del flujo de trabajo de Forms asociado.

1. Toque para seleccionar la miniatura de la tarea. Las opciones para abrir o delegar la tarea seleccionada aparecen en la parte superior.
1. Toque **Apertura** para ver los detalles de la tarea y realizar acciones. Se abre la vista de tareas detallada. En esta vista, puede ver los detalles de la tarea y realizar acciones en ella.

   >[!NOTE]
   >
   >Si una tarea está asignada a un grupo, debe reclamarla para poder abrirla en vista detallada.

![task-details](assets/task-details.png)

La vista de tareas detallada consta de las siguientes secciones:

* Detalles de la tarea
* Formulario 
* Detalles de flujo de trabajo
* Barra de herramientas Acciones

#### Detalles de la tarea {#task-details}

La sección Detalles de la tarea muestra información sobre la tarea. La información mostrada depende de los ajustes de configuración de la variable [Asignar paso de tarea](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) en el flujo de trabajo. El ejemplo anterior muestra la descripción, el estado, la fecha de inicio y el flujo de trabajo utilizado para la tarea. También permite adjuntar un archivo a la tarea.

#### Formulario  {#form}

La ficha Formulario del área de contenido principal muestra los archivos adjuntos de formulario y de nivel de campo enviados, si los hay.

#### Detalles de flujo de trabajo {#workflow-details}

La pestaña Detalles del flujo de trabajo de la parte superior muestra el progreso de la tarea a través de varias etapas del flujo de trabajo. Muestra las etapas completadas, actuales y pendientes de la tarea. Las etapas de un flujo de trabajo se definen en la variable [Asignar paso de tarea](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) del flujo de trabajo asociado.

Además, la pestaña muestra el historial de tareas para cada fase completada en el flujo de trabajo. Puede tocar **[!UICONTROL Ver detalles]** para una fase completada para conocer los detalles de dicha fase. Muestra comentarios, archivos adjuntos de formularios y tareas, estado, fechas de inicio y finalización, etc., sobre la tarea.

![workflow-details](assets/workflow-details.png)

#### Barra de herramientas Acciones {#actions-toolbar}

La barra de herramientas Acciones muestra todas las opciones disponibles para la tarea. Mientras que Guardar, Restablecer y Delegar son acciones predeterminadas, otras acciones disponibles se configuran en [Asignar paso de tarea](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem). En el ejemplo anterior, Aprobar y Rechazar están configurados en el flujo de trabajo.

A medida que realiza una acción sobre la tarea, esta continúa en el flujo de trabajo.

### Ver tareas completadas {#view-completed-tasks}

AEM bandeja de entrada solo muestra tareas activas. Las tareas completadas no aparecen en la lista. Sin embargo, puede utilizar los filtros de la bandeja de entrada para filtrar las tareas según varios parámetros, como el tipo de tarea, el estado, las fechas de inicio y finalización, etc. Para ver las tareas completadas:

1. En AEM bandeja de entrada, pulse ![alternar panel lateral1](assets/toggle-side-panel1.png) para abrir el selector de filtros.
1. Toque **[!UICONTROL Estado de la tarea]** acordeón y seleccione **[!UICONTROL Completar]**. Se mostrarán todas las tareas completadas.

   ![filter](assets/filter.png)

1. Toque para seleccionar una tarea y haga clic en **[!UICONTROL Apertura]**.

La tarea se abre para mostrar el documento o el formulario adaptable asociado a la tarea. En el caso del formulario adaptable, la tarea muestra el formulario adaptable de sólo lectura o su documento de registro PDF, tal y como se ha configurado en la ficha Formulario/documento de la [Paso Asignar flujo de trabajo de tarea](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem).

La sección de detalles de la tarea muestra información como acción realizada, estado de la tarea, fecha de inicio y fecha de finalización.

![complete-task](assets/completed-task.png)

La variable **[!UICONTROL Detalles del flujo de trabajo]** muestra cada paso del flujo de trabajo. Toque **[!UICONTROL Ver detalles]** para obtener información detallada.

![complete-task-workflow](assets/completed-task-workflow.png)

## Solución de problemas {#troubleshooting-workflows}

### No se pueden ver los elementos relacionados con AEM flujo de trabajo en AEM bandeja de entrada {#unable-to-see-aem-worklow-items}

El propietario de un modelo de flujo de trabajo no puede ver elementos relacionados con AEM flujo de trabajo en AEM bandeja de entrada. Para resolver el problema, agregue los siguientes índices a su repositorio de AEM y reconstruya el índice.

1. Utilice uno de los siguientes métodos para añadir índices:

   * Cree los siguientes nodos en CRX DE en `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` con las propiedades respectivas especificadas en la siguiente tabla:

      | Nodo | Propiedad | Tipo |
      |---|---|---|
      | sharedWith | sharedWith | CADENA |
      | bloqueado | bloqueado | BOOLEANO |
      | return | return | BOOLEANO |
      | allowInboxSharing | allowInboxSharing | BOOLEANO |
      | allowExplicitSharing | allowExplicitSharing | BOOLEANO |


   * Implemente los índices a través de un paquete AEM. Puede usar un [Tipo de archivo AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) para crear un paquete de AEM implementable. Utilice el siguiente código de ejemplo para agregar índices a un proyecto de tipo de archivo AEM:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Crear un índice de propiedades y establecerlo en true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=en#the-property-index).

1. Después de configurar índices en CRX DE o implementar mediante un paquete, [volver a indexar el repositorio](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

