---
title: Trabajo de actualización de contenido
description: Descubra qué es el trabajo de actualización de contenido de Brand Experience Agent y qué puede hacer por usted.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: a3b00916c0d949fe9fac50bc0c3056b0a1b05358
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---


# Trabajo de actualización de contenido {#content-update}

El trabajo de actualización de contenido de [Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md) automatiza la producción de contenido para acelerar las tareas diarias de Adobe Experience Manager (AEM) as a Cloud Service y Edge Delivery Services.

## Información general {#overview}

El trabajo de actualización de contenido actualiza el contenido existente, incluidos los fragmentos de contenido, las páginas, los formularios y los recursos. El trabajo puede realizar acciones como actualizar, quitar, reemplazar o agregar elementos de contenido para mantener las experiencias precisas y actuales. Las entradas pueden ser descripciones en lenguaje natural y, cuando se utilizan con PDF de Jira y capturas de pantalla, pueden proporcionar entradas a.

El trabajo de actualización de contenido transforma los detalles que proporciona, ya sea a través del lenguaje natural o de imágenes, en actualizaciones de contenido en la página. Debe proporcionar la dirección URL de una página que necesita actualizarse, junto con los detalles de lo que necesita actualizarse, y la aptitud del agente para completar su tarea. Cuando se usa con Adobe Experience Manager (AEM) as a Cloud Service, el trabajo crea un nuevo [launch](/help/sites-cloud/authoring/launches/overview.md) para que pueda revisar las actualizaciones antes de aplicar. Cuando se usa con la creación de documentos, el trabajo crea una nueva [versión](https://experienceleague.adobe.com/es/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#).

## Capacidades {#capabilities}

Puede acceder a la aptitud de actualización de contenido desde:

* [El asistente de IA](#ai-assistant)
* [Jira](#jira)

## Asistente de IA {#ai-assistant}

Puede acceder al trabajo en AEM mediante el asistente de IA.

Abra el Asistente de IA de [`experience.adobe.com`,](https://experience.adobe.com) y comience a interactuar especificando el mensaje en lenguaje natural mediante el campo `Ask AI Assistant anything`:

![Trabajo de actualización de contenido](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Configuración de la URL de publicación {#configuring-the-publish-url}

Para utilizar una URL de publicación (pública), se debe realizar una configuración única:

* Requisitos previos:

   * Para realizar la configuración, el usuario debe tener derechos de administrador del sistema o del producto.

* Configuración:

   1. Invoque la aptitud Actualización de contenido solicitando una actualización de contenido para la URL.
   1. El asistente le guiará a través de la configuración y le hará varias preguntas.
   1. Una vez finalizada, la dirección URL de publicación se configura y se puede utilizar.

Por ejemplo:

![aptitud para la actualización de contenido: configurar URL de publicación](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### Indicadores {#prompts}

Para iniciar actualizaciones de contenido, puede dar una amplia gama de mensajes en lenguaje natural. Debe especificar la URL pública (publicación) o la URL del entorno de creación de la página que desea actualizar. Algunos de los verbos admitidos, pero no todos; reemplazar, actualizar, quitar, cambiar, revisar, modificar, ajustar y eliminar.

>[!NOTE]
>
>Las cargas de archivos se pueden usar al interactuar con [Jira](#jira), pero no son compatibles con el Asistente de IA.

### Indicadores de ejemplo {#sample-prompts}

Los indicadores de ejemplo incluyen:

* en `<your-publish-URL>` actualizar &quot;Su café perfecto está a cuatro preguntas!&quot; a &quot;Tu café, a tu manera!&quot;
* en `<your-author-env-URL>` reemplazar la imagen de &quot;holdingcup.png&quot; a &quot;stairhead.png&quot;
* en `<your-publish-URL>` cambiar &quot;Realizar nuestra prueba de café&quot; por una versión más atractiva&quot;
* en `<your-author-env-URL>` eliminar la sección &quot;Recompensas no reclamadas es un regalo perdido&quot;

## Jira {#jira}

El uso del trabajo de actualización de contenido con Jira le permite crear un ticket con instrucciones que automatizan sus ediciones.

### Crear un ticket {#create-a-ticket}

Crea un ticket Jira (de cualquier tipo). Se necesitan dos detalles esenciales en el campo **Descripción** de su ticket:

1. La dirección URL pública de la página que debe editar.

1. Los cambios necesarios.

   El trabajo admite la siguiente gama de formatos para describir los cambios:

   * Lenguaje natural en la descripción del ticket
      * por ejemplo, &quot;Cambiar el titular de X a Y&quot;
   * PDF anotado adjunto
      * por ejemplo, cree un PDF de su página y añada anotaciones que detallen lo que desea cambiar
   * Comentarios en PDF adjunto
      * por ejemplo, cree un PDF de su página y agregue comentarios que detallen lo que desea cambiar
   * Captura de pantalla anotada adjunta
      * por ejemplo, realice una captura de pantalla de parte de la página y añada anotaciones que detallen lo que desea cambiar
   * Archivo de Microsoft Word adjunto, que contiene cambios de lenguaje natural

### Invocar el trabajo desde la incidencia {#invoke-the-job-from-your-ticket}

Para utilizar el trabajo, añada un comentario a su ticket. En el comentario, mencione el trabajo con el símbolo `@`, junto con las instrucciones.

Por ejemplo:

* `@aemagent@adobe.com process this ticket`

### Cómo interactúa el trabajo {#how-the-agent-interacts}

Después de emitir un comando al trabajo, este responde con comentarios en el Jira. Los comentarios detallan el progreso del trabajo y las acciones realizadas.

En el caso de un comando `process` para almacenar en déclencheur las actualizaciones, las respuestas pueden seguir la secuencia:

* El comentario inicial confirma que el trabajo se ha iniciado.

* Una vez finalizada la tarea, el trabajo responde con otro comentario que contiene detalles de las acciones realizadas.
   * Las actualizaciones de contenido realizadas por el trabajo no son destructivas, lo que significa que se realizan en una instancia de vista previa.
   * El comentario contiene enlaces a las actualizaciones, para que pueda revisar y publicar según sea necesario, o asignar el Jira a quien sea responsable.

* La siguiente imagen muestra un ejemplo de Jira que almacena en déclencheur el comando `process` para el trabajo de actualización de contenido:

  ![Ejemplo de uso de Jira en el trabajo de actualización de contenido de Brand Experience Agent](assets/content-update-jira-example.png)

## Activación {#activation}

Puede explorar los agentes de AEM a través de [Playground](https://www.aem.live/developer/aem-playground), o conectarse con su CSM o TAM para discutir el acceso a través del SKU de Agentic.

## Limitaciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* Las cargas de archivos se pueden usar al interactuar con [Jira](#jira), pero no se admiten al interactuar con el [Ayudante de IA.](#ai-assistant)
