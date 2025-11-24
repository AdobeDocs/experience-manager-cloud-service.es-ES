---
title: Habilidad de actualización de contenido
description: Descubra cuál es la aptitud de actualización de contenido del agente de producción de experiencia y qué puede hacer por usted.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---


# Habilidad de actualización de contenido {#content-update}

La habilidad de actualización de contenido de Experience Production Agent automatiza la producción de contenido para acelerar las tareas diarias de Adobe Experience Manager (AEM) as a Cloud Service y Edge Delivery Services.

La aptitud para la actualización de contenido actualiza el contenido existente en CMS, incluidos los fragmentos de contenido, las páginas, los formularios y los recursos. El agente puede realizar acciones como actualizar, quitar, reemplazar o agregar elementos de contenido para mantener las experiencias precisas y actualizadas. Las entradas pueden ser descripciones en lenguaje natural y, cuando se utilizan con PDF de Jira y capturas de pantalla, pueden proporcionar entradas a.

## Información general {#overview}

La aptitud para actualizar contenido transforma los detalles que proporciona, ya sea a través del lenguaje natural o de imágenes, en actualizaciones de contenido en la página. Debe proporcionar la dirección URL de una página que necesita actualizarse, junto con los detalles de lo que necesita actualizarse, y la aptitud del agente para completar su tarea.

## Capacidades {#capabilities}

Puede acceder a la aptitud de actualización de contenido desde:

* [Asistente de IA](#ai-assistant)

* [Jira](#jira)

## Asistente de IA {#ai-assistant}

Puede acceder a los agentes empresariales de AEM a través del asistente de IA.

Abra el Asistente de IA desde experience.adobe.com y empiece a interactuar especificando el mensaje en lenguaje natural utilizando el campo `Ask AI Assistant anything`:

![Agente de detección de acceso](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

### Indicadores de ejemplo {#sample-prompts}

Para iniciar actualizaciones de contenido, puede dar una amplia gama de mensajes en lenguaje natural. También debe especificar la dirección URL pública de la página que desea actualizar. Por ejemplo:

* Modifique la siguiente página https://www.your-url.com/sale Actualice el encabezado del héroe principal a &quot;Black Friday Mega Sale - Hasta 70% Off&quot;, Cambie el temporizador de cuenta atrás para mostrar &quot;Termina en 48 horas&quot;, elimine &quot;Regístrese para recibir actualizaciones&quot;, cambie todos los botones &quot;Comprar ahora&quot; a &quot;Agarrarse a la oferta&quot;

* https://www.your-url.com/laptops/your-laptop-model Actualizar el texto del banner a "Ahorre 300 USD solo hoy", Actualizar el precio de 1.299 USD a 999 USD, Eliminar el banner de la opción de financiación

* https://www.your-url.com/your-sneaker Actualizar el estado de las existencias de "Bajo stock" a "Nuevo en stock - Cantidades limitadas", Cambiar el selector de tamaño para resaltar los tamaños disponibles en verde, Quitar el distintivo "Próximamente"

* https://www.your-url.com/your-sneaker Actualice las imágenes de producto para mostrar nuevos colores

>[!NOTE]
>
>Las cargas de archivos se pueden usar al interactuar con [Jira](#jira), pero no son compatibles con el Asistente de IA.

## Jira {#jira}

El uso de la habilidad de actualización de contenido con Jira le permite crear un ticket con instrucciones que automatizan sus ediciones.

### Crear un ticket {#create-a-ticket}

Crea un ticket Jira (de cualquier tipo).

Se necesitan dos detalles esenciales en el campo **Descripción** de su ticket:

1. La dirección URL pública de la página que debe editar.

1. Los cambios necesarios.

   Actualmente, la aptitud admite la siguiente gama de formatos para describir sus cambios:

   * Lenguaje natural en la descripción del ticket
      * por ejemplo, &quot;Cambiar el titular de X a Y&quot;
   * PDF anotado adjunto
      * por ejemplo, cree un PDF de su página y añada anotaciones que detallen lo que desea cambiar
   * Comentarios en PDF adjunto
      * por ejemplo, cree un PDF de su página y agregue comentarios que detallen lo que desea cambiar
   * Captura de pantalla anotada adjunta
      * por ejemplo, realice una captura de pantalla de parte de la página y añada anotaciones que detallen lo que desea cambiar
   * Archivo de Microsoft Word adjunto, que contiene cambios de lenguaje natural

### Invoque al agente desde su ticket {#invoke-the-agent-from-your-ticket}

Para usar el agente, agregue un comentario a su ticket. En el comentario, mencione el agente con el símbolo `@`, junto con el comando que debe ejecutar; por ejemplo:

* `@aemagent@adobe.com process`

Actualmente, el agente entiende los comandos:

* `process` - procesar la solicitud
* `cancel` - cancelar una solicitud de procesamiento
* `retry` - volver a procesar una solicitud
* `feedback` - aplicar comentarios a una generación anterior
* `reprocess` - volver a procesar la solicitud original

### Interacción del agente {#how-the-agent-interacts}

Después de emitir un comando al agente, este responde con comentarios en el Jira. Los comentarios detallan el progreso del agente y las acciones realizadas.

En el caso de un comando `process` para almacenar en déclencheur las actualizaciones, las respuestas pueden seguir la secuencia:

* El comentario inicial confirma que el agente se ha iniciado.

* Una vez completada la tarea. el agente responde con otro comentario que contiene detalles de las acciones realizadas.
   * Las actualizaciones de contenido realizadas por el agente no son destructivas, lo que significa que se realizan en una instancia de previsualización.
   * El comentario contiene enlaces a las actualizaciones, para que pueda revisar y publicar según sea necesario, o asignar el Jira a quien sea responsable.

* La siguiente imagen muestra un ejemplo de Jira que almacena en déclencheur el comando `process` para la aptitud de actualización de contenido:

  ![Ejemplo de Jira con la habilidad de actualización de contenido del agente de producción de experiencia](assets/content-update-jira-example.png)

## Activación {#activation}

Para activar y obtener acceso al agente de producción de Experience, debe ponerse en contacto con Adobe. Para empezar, puede ponerse en contacto con:

* `experience-production-agent@adobe.com`
* o póngase en contacto con el equipo de su cuenta

Para acelerar el proceso, es útil proporcionar la siguiente información:

* Para AEM as a Cloud Service
   * Debe proporcionar lo siguiente:
      * Id. de organización
      * `product_id`
      * `profile_id`

   * Estos valores se pueden encontrar siguiendo los pasos siguientes:
      * El administrador debe visitar <https://adminconsole.adobe.com/>
      * Seleccionar **Adobe Experience Manager as a Cloud Service**
      * Seleccione la instancia de AEM adecuada
      * Seleccione el perfil que permite operaciones de lectura y escritura para el contenido en cuestión
      * Obtener la dirección URL del explorador
      * Extraiga `product_id` y `profile_id` de la dirección URL.
Por ejemplo, <https://adminconsole.adobe.com/products/profiles/users>

* Creación de documentos de Edge Delivery
   * Proporcione a su equipo de Adobe la siguiente información:
      * Dominios relevantes
      * Información relevante de Github:
         * Org
         * Repositorio
         * Rama

## Limitaciones {#limitations}

Actualmente, las limitaciones del actualizador de contenido son:

* Las cargas de archivos se pueden usar al interactuar con [Jira](#jira), pero no se admiten al interactuar con el [Ayudante de IA](#ai-assistant).
