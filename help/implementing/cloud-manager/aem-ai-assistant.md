---
title: Asistente de IA en Adobe Experience Manager (Beta)
description: Utilice el Asistente de IA para encontrar respuestas y solucionar problemas de las soluciones disponibles en Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 71041c9e4d4afe964f549f193daf8ec72bd97a41
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 1%

---

# Asistente de IA en Adobe Experience Manager {#aem-home}

El asistente de IA de AEM (Adobe Experience Manager) ofrece una interfaz conversacional diseñada para agilizar la búsqueda de respuestas a sus consultas relacionadas con Adobe Experience Manager. Le ayuda a obtener respuestas instantáneas a sus preguntas relacionadas con el producto AEM (*disponible para todos los usuarios*) y a automatizar la creación de vales de soporte técnico (*disponible para los administradores de soporte técnico*).

Durante la versión beta privada, el AEM AI Assistant es compatible con AEM as a Cloud Service, e incluye las siguientes soluciones:

* Sites
* Assets
* Dynamic Media
* Edge Delivery Services
* Cloud Manager
* Formularios

Está directamente incrustado en AEM y es accesible desde AEM Experience Hub, Cloud Manager y la interfaz de usuario del autor.

El siguiente vídeo de 3 minutos y 39 segundos ofrece una guía paso a paso del asistente de IA de AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

>[!IMPORTANT]
>Asegúrese de haber revisado y enviado el acuerdo de usuario para que Adobe pueda habilitar la función Asistente de IA y pueda probarlo y participar en el programa beta privado.
>
>Si tiene alguna pregunta, envíe un correo electrónico a [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

## Ámbito {#scope}

El ámbito actual del asistente de IA de AEM se centra en abordar las preguntas de conocimiento del producto para Adobe Experience Manager as a Cloud Service. Este ámbito incluye una compatibilidad completa con áreas clave, como Sites, Assets, Forms, Edge Delivery Services y Cloud Manager.

* **Superficies**: disponible en AEM Experience Hub, IU de creación y Cloud Manager.
* **Capacidades**: conocimiento del producto y primera parada para solucionar problemas y obtener instrucciones, creación automatizada de vales de soporte y búsqueda.
* **Value**: ahorra tiempo, acelera el aprendizaje y el tiempo de obtención de valor, reduce la necesidad de crear vales de soporte de forma manual y mejora la eficacia en la creación de vales de soporte.

## Privacidad, seguridad y gobernanza{#privacy-security-governance}

El asistente de IA de AEM está diseñado con un fuerte énfasis en la privacidad, la seguridad y la gobernanza.

Este artículo describe las funciones centradas en la confianza que puede esperar del asistente de IA de AEM:

* AEM AI Assistant no utiliza datos personales, ni siquiera para fines de formación.
* El asistente de IA de AEM no tiene acceso a los datos del consumidor.
* Se requiere permiso explícito para interactuar con el AEM AI Assistant.
* Las preguntas proporcionadas por el usuario (preguntas, consultas, etc.) no se comparten con otros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Conozca AEM AI Assistant para obtener información sobre el producto y crear vales de soporte automatizado {#ai-prod-insights}

El conocimiento del producto engloba conceptos y temas derivados de la documentación de Adobe Experience League. Estas preguntas se pueden clasificar en los siguientes subgrupos:


| Conocimiento del producto | Disponible para todos los usuarios<br>Ejemplos |
| :--- | :--- |
| Aprendizaje puntual | <ul><li>¿Qué es el editor universal?</li><li>¿Cómo se crea un programa en Cloud Manager?</li></ul> |
| Abrir detección | <ul><li>¿Cómo se utiliza el editor universal?</li><li>¿Hay alguna manera de copiar contenido de un entorno a otro?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué no puedo acceder al editor universal?</li><li>¿Por qué falla mi canalización?</li></ul> |
| **Creación de ticket de asistencia** | **Disponible solo para administradores de soporte técnico &#x200B;**<br>**Ejemplos** |
| Creación automatizada de tickets de asistencia que captura el historial y el contexto de chat del asistente de IA | <ul><li>Crea un ticket de asistencia para mí.</li></ul> |
| Recuperar el estado del ticket de asistencia | <ul><li>Muéstrame todos los boletos de soporte que he abierto.</li><li>Muéstrame el estado del ticket &quot;E-----------&quot;</li></ul> |

{style="table-layout:auto"}


## Cómo crear preguntas efectivas {#ai-craft-questions}

Para recibir las respuestas más precisas del asistente de IA de AEM, es importante expresar sus preguntas con claridad y contexto. Utilice las siguientes sugerencias para asegurarse de que las consultas son claras y están bien estructuradas:

* Indique claramente su tarea o pregunta de forma concisa.
* Evite utilizar palabras ambiguas o sintaxis demasiado compleja para mejorar la comprensión.
* Incluya un contexto relevante sobre su tarea o pregunta, ya que este método ayuda al asistente de IA de AEM a proporcionar respuestas más precisas y relevantes.
Por ejemplo, en el mensaje, ayuda asignar un nombre a la solución de AEM en la que está trabajando: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager o Forms.

### Ejemplos de preguntas no admitidas {#ai-unsupported-questions}

| Área | Ejemplos |
| --- | --- |
| Perspectivas operativas | <ul><li>¿Cuántos entornos de desarrollo existen en mi inquilino?</li><li>¿Quién inició la última canalización de producción?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué falla mi canalización de producción?</li></ul> |
| Tarea y automatización | <ul><li>Configure una canalización de calidad de código desde una rama de desarrollo para mí.</li></ul> |


## Uso del asistente de AEM AI {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AEM AI Assistant access through Admin Console 

To use the AEM AI Assistant, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AEM AI Assistant in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AEM AI Assistant of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Iniciar o restablecer una conversación

Puede restablecer el Ayudante de IA de AEM e iniciar una nueva conversación cuando desee cambiar de tema. Esta capacidad es especialmente útil para solucionar problemas de consultas que fallan o proporcionan información incorrecta.

![Botón Iniciar conversación](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Para iniciar o restablecer una conversación:**

1. En el Asistente de IA de AEM, haga clic en ![Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Para informar al Asistente de IA de AEM de un nuevo tema o de un cambio en el tema, haz clic en **Iniciar nueva conversación**.

### Uso de detectabilidad

El Asistente de IA de AEM incluye una función de detección que le ayudará a explorar los temas y las categorías admitidos.

![Icono de bombilla de luz ideal](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Para usar la detección:**

1. Cerca de la esquina superior derecha del Ayudante de IA de AEM, haz clic en ![Icono de aprendizaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Seleccione una categoría para ver una lista de peticiones de datos relacionadas.
1. Elija un mensaje para comprender mejor los tipos de preguntas que puede responder el Asistente de IA de AEM.

### Proporcione comentarios sobre el asistente de AEM AI

Sus datos ayudan a mejorar el asistente de IA de AEM para obtener un mejor rendimiento y precisión.

Comparta sus comentarios sobre su experiencia con AEM AI Assistant a través de las siguientes opciones:

![Iconos de pulgar arriba, pulgar abajo y marca](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Icono | Descripción |
| --- | --- |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Haga clic en para indicar qué ha salido bien y compartir comentarios positivos. |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Haga clic en para proporcionar sugerencias de mejora. Añada comentarios específicos sobre su experiencia, que se revisan diariamente. |
| ![Icono de marca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Haga clic en para informar de sus problemas o proporcionar comentarios detallados acerca de su interacción con el asistente de IA de AEM. |

## Preguntas frecuentes sobre AEM AI Assistant {#ai-faq}

A continuación encontrará respuestas a algunas preguntas comunes sobre el asistente de IA:

* **¿La información proporcionada por el Asistente de IA de AEM está en tiempo real?**\
  No. El asistente de IA obtiene su contenido de la documentación de Adobe Experience League. Las actualizaciones del contenido pueden tardar un poco en reflejarse en sus respuestas.
* **¿Qué aplicaciones de Adobe es compatible con el Asistente de IA de AEM?**\
  Actualmente, el asistente de IA admite consultas de conocimientos de productos en AEM as a Cloud Service, incluidos Sites, Assets, Dynamic Media, Cloud Manager y Forms.
* **¿Cuáles son las capacidades del Asistente de IA de AEM?**\
  AEM AI Assistant está diseñado para responder a consultas relacionadas con el conocimiento del producto Adobe.
* **¿El Asistente de IA de AEM usa información personal para los datos de formación?**\
  No. AEM AI Assistant no utiliza información personal con fines formativos. Evite compartir información personal sobre usted u otros, incluidos nombres o detalles de contacto, con el asistente de IA de AEM.


## Asistente de IA de AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Además del asistente general de AEM AI para obtener conocimientos del producto, AEM ofrece un asistente especializado de **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. Este asistente mejorado puede ayudarle a crear y configurar formularios de forma activa mediante mensajes en lenguaje natural y responder preguntas específicas a los formularios.

### Capacidades clave

El asistente de AEM Forms AI proporciona lo siguiente:

* **Creación de formularios**: cree nuevos formularios desde cero con descripciones en lenguaje natural.
* **Importación de diseños**: Convierte diseños existentes (PDF, Figma, imágenes) en AEM Forms funcional.
* **Configuración de formulario**: agregue campos, paneles, reglas de validación y lógica condicional.
* **Administración de diseños**: organice la estructura del formulario y optimícela para diferentes dispositivos.
* **Configuración de integración**: configure los envíos de formularios y la administración de datos.
* **Conocimiento del producto**: responda preguntas sobre las características de AEM Forms y las prácticas recomendadas.

### Dónde acceder

El asistente de AEM Forms AI está disponible en los siguientes entornos:

* **Editor universal**: para formularios Edge Delivery Services con capacidades de edición visual.
* **Editor de Forms adaptable**: Para obtener información detallada sobre la configuración del formulario y las características avanzadas.
* **IU de administración de Forms**: para tareas de administración y creación de formularios de alto nivel.

### Introducción

>[!NOTE]
>
> El AEM Forms AI Assistant (Forms Experience Builder) está disponible en el programa beta privado. Envíe un correo electrónico desde su dirección de trabajo a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso.

Para obtener más información sobre el uso del Asistente de IA de AEM Forms, consulte la [documentación del Asistente de IA de AEM Forms](/help/edge/docs/forms/forms-ai-assistant.md).

### Casos de uso de ejemplo

* **&quot;Crear un formulario de comentarios de cliente con campos de nombre, correo electrónico, clasificación y comentarios&quot;**
* **&quot;Convertir este formulario de aplicación de PDF cargado en un formulario adaptable digital&quot;**
* **&quot;Agregar lógica condicional para mostrar la información del cónyuge solamente cuando el estado civil es &#39;Casado&#39;&quot;**
* **&quot;Configurar este formulario para enviar datos al sistema de administración de relaciones con los clientes&quot;**

Este asistente de IA de AEM Forms especializado representa la siguiente evolución en la creación de formularios, combinando la potencia de la IA con las sólidas capacidades de formularios de AEM para optimizar el flujo de trabajo de creación de formularios.
