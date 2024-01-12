---
title: AEM Edge Delivery Services de y
description: Descubra cómo AEM as a Cloud Service puede beneficiarse del rendimiento y las puntuaciones perfectas de Lighthouse que ofrecen los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: 9d26a4835dc331f2ff8b741a4c14847ead611874
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 43%

---


# AEM Edge Delivery Services de y {#aem-edge}

Con Edge Delivery Services, AEM ofrece experiencias excepcionales que fomentan la participación y las conversiones. AEM lo hace ofreciendo experiencias de alto impacto que son rápidas de crear y desarrollar. Es un conjunto de servicios que admite composición que permite un entorno de desarrollo rápido en el que los autores pueden actualizar y publicar rápidamente y en el que los nuevos sitios se inician rápidamente. De este modo, con Edge Delivery Services puede mejorar la conversión, reducir costes y proporcionar una velocidad de contenido extrema.

Con los Edge Delivery Services, puede:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta y monitorizar continuamente el rendimiento de su sitio a través de la monitorización real del usuario (RUM).
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar tanto la creación en AEM como la creación basada en documentos. De este modo, puede trabajar con varias fuentes de contenido en el mismo sitio web.
* Utilice un marco de trabajo de experimentación integrado que permita la creación y ejecución rápidas de pruebas sin impacto en el rendimiento y la publicación rápida en producción de un ganador de pruebas.

## Resumen de Edge Delivery Services {#edge-overview}

El diagrama siguiente ilustra cómo se puede editar contenido en Microsoft Word (edición basada en documentos) y publicarlo en Edge Delivery Services. AEM También muestra el método de publicación de la mediante el Editor universal.

![Arquitectura de Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Los servicios de entrega perimetral son un conjunto de servicios componibles que permiten un alto grado de flexibilidad en la forma en que se crea contenido en el sitio web. Como se mencionó anteriormente, puede utilizar ambos [AEM administración de contenido de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) con [Creación del editor universal](/help/implementing/universal-editor/introduction.md) así como [creación basada en documentos.](https://www.aem.live/docs/authoring)

Por ejemplo, puede utilizar contenido directamente desde Microsoft Word o Google Docs. Esto significa que los documentos de esas fuentes pueden convertirse en páginas de su sitio web. Además, los encabezados, las listas, las imágenes y los elementos de tipo de fuente se pueden transferir desde el origen inicial al sitio web. El nuevo contenido se añade instantáneamente sin un proceso de reconstrucción.

Los Edge Delivery Services utilizan GitHub para que los clientes puedan administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir contenido en Google Docs o en Microsoft Word, y la funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub. Cuando esté listo, puede utilizar la extensión del explorador de la barra de tareas para obtener una vista previa y publicar actualizaciones de contenido.

Para obtener más información, consulte la documentación de Edge Delivery Services:

* Para obtener más información sobre cómo empezar a utilizar la entrega perimetral, consulte [Sección Build.](https://www.aem.live/docs/#build)
* Para comprender cómo crear y publicar contenido mediante Edge Delivery, consulte [Publicar sección.](https://www.aem.live/docs/authoring)
* Para comprender cómo iniciar correctamente el proyecto de sitio web, consulte la [Sección Launch.](https://www.aem.live/docs/#launch)

## Edge Delivery Services y otros productos de Adobe Experience Cloud {#edge-other-products}

Los Edge Delivery Services forman parte de Adobe Experience Manager y, como tales, los Edge Delivery Services AEM y los sitios de pueden coexistir en el mismo dominio. Este es un caso de uso común en sitios web más grandes. Además, el contenido de los Edge Delivery Services se puede consumir fácilmente en sus páginas de AEM Sites y a la inversa.

También puede utilizar Edge Delivery Services con Adobe Target, Analytics y Launch.

## Obtención de acceso a Edge Delivery Services {#getting-access}

Es fácil empezar a usar Edge Delivery Services. Empiece siguiendo los pasos de [Introducción: tutorial para desarrolladores.](https://www.aem.live/developer/tutorial)

## Obtención de ayuda de Adobe {#adobe-gethelp}

Puede interactuar con los equipos de productos de Adobe a través del canal de colaboración de productos suministrado (consulte a continuación para obtener los detalles de acceso) para responder a preguntas sobre el uso del producto o las prácticas recomendadas. No hay ningún destinatario de nivel de servicio (SLT, Service Level Targets) asociado a las conversaciones a través del canal de colaboración de productos. Si un problema de producto necesita más investigación y solución de problemas, y debe cumplir con los SLT de respuesta, puede enviar un ticket de asistencia después de la [proceso de soporte.](https://experienceleague.adobe.com/?support-tab=home&amp;lang=es#support)

Adobe proporciona tres canales para ayudarle con Edge Delivery Services:

* Interactúe con los recursos de la comunidad para realizar consultas generales
* Acceda al canal de colaboración de productos para preguntas específicas
* Registre un ticket de asistencia para resolver problemas importantes y críticos

### Acceder a recursos de la comunidad {#community-resource}

El Adobe se compromete a empoderarle con la mejor participación de la comunidad y apoyo para Edge Delivery Services y la creación basada en documentos.

* Participar en [Comunidad de Experience League](https://adobe.ly/3Q6kTKl) para hacer preguntas, compartir comentarios, iniciar discusiones, buscar ayuda de expertos en Adobe AEM y asesores/campistas, y conectarse con personas con ideas afines en tiempo real.
* Únase a nuestros [Canal de discordia,](https://discord.gg/aem-live) una plataforma más informal para interacciones en tiempo real e intercambios de ideas rápidos.

### Cómo acceder a su canal de colaboración de productos {#collab-channel}

AEM Dado el valor del canal de comunicación directa con los clientes, todos los clientes en el momento de la presentación de, establecerán un canal Slack para la velocidad, las actualizaciones críticas y la creación de informes a escala sobre la calidad de la experiencia. Recibirá una invitación del Adobe para unirse a un canal de Slack específico de su organización.

Para obtener más información, consulte el documento [Uso del bot de Slack](https://www.aem.live/docs/slack) para obtener más información.

### Registro de un ticket de asistencia {#support-ticket}

Pasos para registrar un ticket de asistencia a través de Admin Console:

1. [Siguiendo el proceso de soporte estándar,](https://experienceleague.adobe.com/?support-tab=home&amp;lang=es#support) cree un ticket.
1. Añada **Edge Delivery** en el título del ticket.
1. En la descripción, proporcione los siguientes detalles:

   * URL del sitio web activo. Por ejemplo: `www.mydomain.com`.
   * URL del sitio web de origen (`.hlx` URL).

## Siguientes pasos {#whats-next}

Introducción a la revisión [Uso de Edge Delivery Services](/help/edge/using.md).
