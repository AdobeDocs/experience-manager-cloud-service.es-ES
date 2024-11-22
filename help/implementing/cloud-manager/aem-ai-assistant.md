---
title: Asistente de IA en Adobe Experience Manager (Beta limitado)
description: Utilice el Asistente de IA en Adobe Experience Manager para encontrar respuestas, solucionar problemas y explorar Sites, Assets, Forms y Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
hidefromtoc: true
source-git-commit: e454581a2e6f2b8184a54d6550daec60e58bbc6c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# Acerca del asistente de IA en Adobe Experience Manager {#aem-home}

AEM El asistente de inteligencia artificial en el servicio de información (Adobe Experience Manager, por sus siglas en inglés) ofrece una interfaz conversacional diseñada para optimizar la búsqueda de respuestas a sus consultas relacionadas con Adobe Experience Manager. Le ayuda a acceder al conocimiento del producto, solucionar problemas y explorar la información disponible en Experience League. Durante el programa limitado de Beta, el asistente de IA es compatible con Adobe Experience Manager as a Cloud Service, incluidos Sites, Assets, Forms y Cloud Manager.

>[!IMPORTANT]
>Asegúrese de haber revisado y enviado el acuerdo de usuario para que el Adobe pueda habilitar la función Asistente de IA y poder probarlo y participar en el programa de Beta.
>
>Si tiene alguna pregunta, envíe un correo electrónico a [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

## Privacidad, seguridad y gobernanza

AEM El asistente de IA en el servicio de inteligencia artificial (AI) en el servicio de información está diseñado con un fuerte énfasis en la privacidad, la seguridad y la gobernanza.

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



