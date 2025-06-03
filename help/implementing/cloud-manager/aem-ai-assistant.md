---
title: Asistente de IA en Adobe Experience Manager (Beta limitado)
description: Utilice el Asistente de IA en Adobe Experience Manager para encontrar respuestas, solucionar problemas y explorar Sites, Assets, Forms y Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
exl-id: 6cdf7f65-7112-420a-90c1-564f0ef8ceaf
source-git-commit: 2db966405b5326d735083a66b2625d6d973ad7db
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Acerca del asistente de IA en Adobe Experience Manager {#aem-home}

El asistente de IA de AEM (Adobe Experience Manager) ofrece una interfaz conversacional diseñada para agilizar la búsqueda de respuestas a sus consultas relacionadas con Adobe Experience Manager. Le ayuda a acceder a los conocimientos del producto, solucionar problemas y explorar la información disponible en Experience League. Durante el programa limitado de Beta, el asistente de IA es compatible con Adobe Experience Manager as a Cloud Service, incluidos Sites, Assets, Forms y Cloud Manager.

>[!IMPORTANT]
>Asegúrese de haber revisado y enviado el acuerdo de usuario para que Adobe pueda habilitar la función Asistente de IA y así poder probarlo y participar en el programa de Beta.
>
>Si tiene alguna pregunta, envíe un correo electrónico a [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

## Privacidad, seguridad y gobernanza

El asistente de IA de AEM está diseñado con un fuerte énfasis en la privacidad, la seguridad y la gobernanza.

Este artículo describe las funciones centradas en la confianza que puede esperar del asistente de IA:

* AI Assistant no utiliza datos personales, ni siquiera con fines formativos.
* El asistente de IA no tiene acceso a los datos del consumidor.
* Se requiere permiso explícito para interactuar con el Ayudante de IA.
* Las preguntas proporcionadas por el usuario (preguntas, consultas, etc.) no se comparten con otros clientes.


## Conozca al asistente de IA para conocer el producto {#ai-prod-insights}

El conocimiento del producto engloba conceptos y temas derivados de la documentación de Adobe Experience League. Estas preguntas se pueden clasificar en los siguientes subgrupos:

| Conocimiento del producto | Ejemplos |
| --- | --- |
| Aprendizaje puntual | <ul><li>¿Qué es el editor universal?</li><li>¿Cómo se crea un programa en Cloud Manager?</li></ul> |
| Abrir detección | <ul><li>¿Cómo se utiliza el editor universal?</li><li>¿Hay alguna manera de copiar contenido de un entorno a otro?</li></ul> |
| Solución de problemas | <ul><li>¿Por qué no puedo acceder al editor universal?</li><li>¿Por qué falla mi canalización?</li></ul> |

El ámbito actual del asistente de IA se centra en abordar las preguntas de conocimiento del producto para Adobe Experience Manager as a Cloud Service. Este ámbito incluye una compatibilidad completa con áreas clave, como Sites, Assets, Forms y Cloud Manager.

## Asistente de IA para AEM Forms (Forms Experience Builder) {#ai-forms-builder}

Además del Asistente general de IA para obtener conocimientos del producto, AEM ofrece un **[Asistente de IA especializado para AEM Forms (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. Este asistente mejorado puede ayudarle a crear y configurar formularios de forma activa mediante mensajes en lenguaje natural y responder preguntas específicas a los formularios.

### Capacidades clave

El asistente de IA para AEM Forms proporciona lo siguiente:

* **Creación de formularios**: cree nuevos formularios desde cero con descripciones en lenguaje natural
* **Importación de diseños**: Convierta diseños existentes (PDF, Figma, imágenes) en formularios AEM funcionales
* **Configuración de formulario**: agregue campos, paneles, reglas de validación y lógica condicional
* **Administración de diseños**: organice la estructura del formulario y optimícela para diferentes dispositivos
* **Configuración de integración**: configure los envíos de formularios y la administración de datos
* **Conocimiento del producto**: responda preguntas sobre las características de AEM Forms y las prácticas recomendadas

### Dónde acceder

El asistente de IA para AEM Forms está disponible en:

* **Editor universal**: para formularios Edge Delivery Services con capacidades de edición visual
* **Editor de Forms adaptable**: Para obtener información detallada sobre la configuración del formulario y las características avanzadas
* **IU de administración de Forms**: para tareas de administración y creación de formularios de alto nivel

### Introducción

>[!NOTE]
>
> El asistente de IA para AEM Forms (Forms Experience Builder) está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso.

Para obtener más información sobre el uso del Asistente de IA para AEM Forms, incluidos ejemplos detallados y prácticas recomendadas, consulte la [documentación del Asistente de IA para AEM Forms](/help/edge/docs/forms/forms-ai-assistant.md).

### Casos de uso de ejemplo

* **&quot;Crear un formulario de comentarios de cliente con campos de nombre, correo electrónico, clasificación y comentarios&quot;**
* **&quot;Convertir este formulario de aplicación de PDF cargado en un formulario adaptable digital&quot;**
* **&quot;Agregar lógica condicional para mostrar la información del cónyuge solamente cuando el estado civil es &#39;Casado&#39;&quot;**
* **&quot;Configurar este formulario para enviar datos a nuestro sistema CRM&quot;**

Este asistente de IA de Forms especializado representa la siguiente evolución en la creación de formularios, combinando la potencia de la IA con las sólidas capacidades de formularios de AEM para optimizar el flujo de trabajo de creación de formularios.

## Cómo crear preguntas efectivas {#ai-craft-questions}

Para recibir las respuestas más precisas del asistente de IA, es importante expresar sus preguntas con claridad y contexto. Utilice las siguientes sugerencias para asegurarse de que las consultas son claras y están bien estructuradas:

* Indique claramente su tarea o pregunta de forma concisa.
* Evite utilizar palabras ambiguas o sintaxis demasiado compleja para mejorar la comprensión.
* Incluya un contexto relevante sobre su tarea o pregunta, ya que este enfoque ayuda al asistente de IA a proporcionar respuestas más precisas y relevantes.

### Ejemplos de preguntas no admitidas {#ai-unsupported-questions}

| Área | Ejemplos |
| --- | --- |
| Perspectivas operativas | <ul><li>¿Cuántos entornos de desarrollo existen en mi inquilino?</li><li>¿Quién inició la última canalización de producción?</li></ul> |
| Solución de problemas | <ul><li>¿Por qué falla mi canalización de producción?</li></ul> |
| Tarea y automatización | <ul><li>Configure una canalización de calidad de código desde una rama de desarrollo para mí.</li></ul> |


## Utilizar el asistente de IA {#ai-use}


### Iniciar o restablecer una conversación

Puede restablecer el Ayudante de IA e iniciar una nueva conversación cuando desee cambiar de tema. Esta capacidad es especialmente útil para solucionar problemas de consultas que fallan o proporcionan información incorrecta.

![Botón Iniciar conversación](/help/implementing/cloud-manager/assets/ai-assistant-start-conversation.png)

**Para iniciar o restablecer una conversación:**

1. En el Asistente de IA, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Para informar al Ayudante de IA de un nuevo tema o de un cambio en el tema, haz clic en **Iniciar nueva conversación**.

### Uso de detectabilidad

El Asistente de IA incluye una función de detección que le ayudará a explorar los temas y las categorías admitidos.

![Icono de bombilla de luz ideal](/help/implementing/cloud-manager/assets/ai-assistant-idea.png)

**Para usar la detección:**

1. Cerca de la esquina superior derecha del Ayudante de IA, haz clic en ![Icono de aprendizaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).
1. Seleccione una categoría para ver una lista de peticiones de datos relacionadas.
1. Elija un mensaje para comprender mejor los tipos de preguntas que el Ayudante de IA puede responder.

### Proporcionar comentarios sobre el asistente de IA

Sus datos ayudan a mejorar el asistente de IA para obtener un mejor rendimiento y precisión.

Comparta sus comentarios sobre su experiencia con AI Assistant mediante las siguientes opciones:

![Iconos de pulgar arriba, pulgar abajo y marca](/help/implementing/cloud-manager/assets/ai-assistant-feedback.png)

| Icono | Descripción |
| --- | --- |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Haga clic en para indicar qué ha salido bien y compartir comentarios positivos. |
| ![Icono de esquema en miniatura](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Haga clic en para proporcionar sugerencias de mejora. Añada comentarios específicos sobre su experiencia, que se revisan diariamente. |
| ![Icono de marca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Haga clic en para informar de sus problemas o proporcionar comentarios detallados acerca de su interacción con el asistente de IA. |

## Preguntas frecuentes sobre el asistente de IA {#ai-faq}

A continuación encontrará respuestas a algunas preguntas comunes sobre el asistente de IA:

* **¿La información proporcionada por el Asistente de IA es en tiempo real?**\
  No. El asistente de IA obtiene su contenido de la documentación de Adobe Experience League. Las actualizaciones del contenido pueden tardar un poco en reflejarse en sus respuestas.
* **¿Qué aplicaciones de Adobe admite el Asistente de IA?**\
  Actualmente, el asistente de IA admite AEM as a Cloud Service, incluidos Sites, Assets, Forms y Cloud Manager, específicamente para consultas de conocimiento de productos.
* **¿Cuáles son las capacidades del Asistente de IA?**\
  El asistente de IA está diseñado para responder a consultas relacionadas con el conocimiento del producto de Adobe.
* **¿El Asistente de IA usa información personal para los datos de entrenamiento?**\
  No. AI Assistant no utiliza información personal con fines formativos. Evite compartir información personal sobre usted u otros, incluidos nombres o detalles de contacto, con el asistente de IA.
