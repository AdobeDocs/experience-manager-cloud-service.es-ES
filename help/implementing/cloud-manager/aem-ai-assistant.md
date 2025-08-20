---
title: Asistente de IA en AEM
description: Utilice el Asistente de IA para encontrar respuestas y solucionar problemas de las soluciones disponibles en Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive"
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 99f4e5731d5631981986a783534c820ad8f7088a
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# Asistente de IA en AEM {#aem-home}

El asistente de IA de AEM (Adobe Experience Manager) ofrece una interfaz conversacional diseñada para agilizar la búsqueda de respuestas a sus consultas relacionadas con Adobe Experience Manager. Le ayuda a obtener respuestas instantáneas a sus preguntas relacionadas con el producto AEM (*disponible para todos los usuarios*) y a automatizar la creación de vales de soporte técnico (*disponible para los administradores de soporte técnico*).

El asistente de IA es compatible con AEM as a Cloud Service, e incluye las siguientes soluciones:

* Página de información general de Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


Está directamente incrustado en AEM y es accesible desde AEM Experience Hub, Cloud Manager y la interfaz de usuario del autor.

El siguiente vídeo de 3 minutos y 39 segundos ofrece una guía paso a paso del asistente de IA en AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

## Cómo obtener acceso al asistente de IA en AEM{#get-access}

1. [Los clientes deben firmar el controlador de IA general con Adobe](https://fieldreadiness-adobe.highspot.com/items/665f831c9f831b011aeda057#1).

   GenAI Rider es un acuerdo legal entre un cliente y Adobe, requerido para utilizar la mayoría de las capacidades de IA y agénticas. Póngase en contacto con el Servicio de atención al cliente de Adobe para obtener más información.

1. El administrador de AEM configura el asistente de IA para su uso en la organización. Consulte [Configuración del asistente de IA en AEM](/help/implementing/cloud-manager/aem-ai-assistant-admin.md).

<!--
>[!IMPORTANT]
>Be sure you have reviewed and submitted the user agreement so Adobe can enable the AI Assistant feature for you to test out and participate in the private beta program.
>
>For any questions, send an email to [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) from your email address associated with your Adobe ID. -->

## Ámbito {#scope}

El ámbito actual del asistente de IA de AEM se centra en abordar las preguntas de conocimiento del producto para AEMr as a Cloud Service. Este ámbito incluye un amplio soporte para áreas clave. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Superficies**: disponible en AEM Experience Hub, IU de creación y Cloud Manager.
* **Capacidades**: conocimiento del producto y primera parada para solucionar problemas y obtener instrucciones, creación automatizada de vales de soporte y búsqueda.
* **Value**: ahorra tiempo, acelera el aprendizaje y el tiempo de obtención de valor, reduce la necesidad de crear vales de soporte de forma manual y mejora la eficacia en la creación de vales de soporte.

## Privacidad, seguridad y gobernanza{#privacy-security-governance}

El asistente de IA de AEM está diseñado con un fuerte énfasis en la privacidad, la seguridad y la gobernanza.

Este artículo describe las funciones centradas en la confianza que puede esperar del asistente de IA de AEM:

* AI Assistant no utiliza datos personales en AEM, ni siquiera para fines de formación.
* El asistente de IA de AEM no tiene acceso a los datos de los consumidores.
* Se requiere permiso explícito para interactuar con el asistente de IA en AEM.
* Las preguntas proporcionadas por el usuario (preguntas, consultas, etc.) no se comparten con otros clientes.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Conozca el asistente de IA de AEM para obtener información sobre el producto y crear vales de soporte automatizado {#ai-prod-insights}

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

Para recibir las respuestas más precisas del asistente de IA en AEM, es importante expresar sus preguntas con claridad y contexto. Utilice las siguientes sugerencias para asegurarse de que las consultas son claras y están bien estructuradas:

* Indique claramente su tarea o pregunta de forma concisa.
* Evite utilizar palabras ambiguas o sintaxis demasiado compleja para mejorar la comprensión.
* Incluya un contexto relevante sobre su tarea o pregunta, ya que este enfoque ayuda al asistente de IA en AEM a proporcionar respuestas más precisas y relevantes.
Por ejemplo, en el mensaje, ayuda asignar un nombre a la solución de AEM en la que está trabajando: Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager o Forms.

### Ejemplos de preguntas no admitidas {#ai-unsupported-questions}

| Área | Ejemplos |
| --- | --- |
| Perspectivas operativas | <ul><li>¿Cuántos entornos de desarrollo existen en mi inquilino?</li><li>¿Quién inició la última canalización de producción?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué falla mi canalización de producción?</li></ul> |
| Tarea y automatización | <ul><li>Configure una canalización de calidad de código desde una rama de desarrollo para mí.</li></ul> |


## Uso del asistente de IA en AEM {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use the AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Iniciar o restablecer un asistente de IA en una conversación de AEM

Puede restablecer el asistente de IA en AEM e iniciar una nueva conversación cuando desee cambiar de tema. Esta capacidad es especialmente útil para solucionar problemas de consultas que fallan o proporcionan información incorrecta.

![Botón Iniciar conversación](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Para iniciar o restablecer una conversación:**

1. En el Asistente de IA de AEM, haga clic en ![Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Para informar al Asistente de inteligencia artificial de un nuevo tema o de un cambio en el tema, haz clic en **Iniciar nueva conversación**.

### Uso de detectabilidad

El asistente de IA de AEM incluye una función de detección que le ayudará a explorar los temas y las categorías admitidos.

![Icono de bombilla de luz ideal](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Para usar la detección:**

1. Cerca de la esquina superior derecha del Ayudante de IA, haz clic en ![Icono de aprendizaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Seleccione una categoría para ver una lista de peticiones de datos relacionadas.
1. Elija un mensaje para comprender mejor los tipos de preguntas que puede responder el Asistente de IA en AEM.

### Proporcionar comentarios sobre el asistente de IA en AEM

Sus datos ayudan a mejorar el asistente de IA en AEM para obtener un mejor rendimiento y precisión.

Comparta sus comentarios sobre su experiencia con el AI Assistant de AEM mediante las siguientes opciones:

![Iconos de pulgar arriba, pulgar abajo y marca](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Icono | Descripción |
| --- | --- |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Haga clic en para indicar qué ha salido bien y compartir comentarios positivos. |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Haga clic en para proporcionar sugerencias de mejora. Añada comentarios específicos sobre su experiencia, que se revisan diariamente. |
| ![Icono de marca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Haga clic en para informar sobre problemas o proporcionar comentarios detallados acerca de su interacción con el asistente de IA en AEM. |

## Preguntas frecuentes sobre el asistente de IA en AEM {#ai-faq}

A continuación encontrará respuestas a algunas preguntas comunes sobre el asistente de IA:

* **¿La información proporcionada por el Asistente de IA en AEM es en tiempo real?**\
  No. El asistente de IA obtiene su contenido de la documentación de Adobe Experience League. Las actualizaciones del contenido pueden tardar un poco en reflejarse en sus respuestas.
* **¿Qué aplicaciones de Adobe admite el Asistente de IA en AEM?**\
  Actualmente, el asistente de IA admite consultas de conocimientos de productos en AEM as a Cloud Service, incluidos Sites, Assets, Dynamic Media, Cloud Manager y Forms.
* **¿Cuáles son las capacidades del Asistente de IA en AEM?**\
  El asistente de IA de AEM está diseñado para responder a consultas relacionadas con el conocimiento del producto de Adobe.
* **¿El asistente de IA de AEM utiliza información personal para los datos de formación?**\
  No. El asistente de IA de AEM no utiliza información personal con fines de formación. Evite compartir información personal sobre usted u otros, incluidos nombres o detalles de contacto, con el asistente de IA de AEM.

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
