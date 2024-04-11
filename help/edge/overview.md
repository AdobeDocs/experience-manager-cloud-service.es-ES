---
title: Información general de Edge Delivery Services
description: Descubra cómo AEM as a Cloud Service puede beneficiarse del rendimiento y las puntuaciones perfectas de Lighthouse que ofrecen los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
source-git-commit: bf6d0ff2f4aebb6620be46704072743578b096d2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 48%

---


# Información general de Edge Delivery Services {#edge-delivery-services}

Con Edge Delivery Services, AEM ofrece experiencias excepcionales que fomentan la participación y las conversiones. AEM lo hace ofreciendo experiencias de alto impacto que son rápidas de crear y desarrollar. Es un conjunto de servicios que admite composición que permite un entorno de desarrollo rápido en el que los autores pueden actualizar y publicar rápidamente y en el que los nuevos sitios se inician rápidamente. De este modo, con Edge Delivery Services puede mejorar la conversión, reducir costes y proporcionar una velocidad de contenido extrema.

Mediante Edge Delivery Services, puede:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta y monitorizar continuamente el rendimiento de su sitio a través de la monitorización real del usuario (RUM).
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar tanto la creación en AEM como la creación basada en documentos. De este modo, puede trabajar con varias fuentes de contenido en el mismo sitio web.
* Utilice un marco de trabajo de experimentación integrado que permita la creación y ejecución rápidas de pruebas sin impacto en el rendimiento y la publicación rápida en producción de un ganador de pruebas.

## Información general {#overview}

Edge Delivery Services es un conjunto de servicios componibles que permiten un alto grado de flexibilidad en la forma en que se crea contenido en el sitio web. Puede usar ambos [AEM administración de contenido de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) AEM y creación basada en el uso de la variable de entorno [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) así como [creación basada en documentos.](https://www.aem.live/docs/authoring)

El diagrama siguiente ilustra cómo se puede editar contenido en Microsoft Word (creación basada en documentos) y publicarlo en Edge Delivery Services. AEM También muestra la edición basada en el uso de la mediante el editor universal.

![Arquitectura de Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Puede utilizar contenido directamente de Microsoft Word o Google Docs para que esas fuentes se conviertan en páginas del sitio web. Además, los encabezados, las listas, las imágenes y los elementos de tipo de fuente se pueden transferir desde el origen inicial al sitio web. El nuevo contenido se añade al instante sin que sea necesario un proceso de reconstrucción.

Los Edge Delivery Services utilizan GitHub para que pueda administrar e implementar código directamente desde el repositorio de GitHub. Por ejemplo, escribe contenido en Google Docs o Microsoft Word y la funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub. Cuando esté listo, utilice la extensión del explorador Sidekick para obtener una vista previa y publicar actualizaciones de contenido.

Para más información, consulte la documentación de Edge Delivery Services:

* Para obtener más información sobre cómo empezar a utilizar Edge Delivery, consulte la [sección Versión](https://www.aem.live/docs/#build).
* Para comprender cómo crear y publicar contenido mediante Edge Delivery, consulte la [sección Publicar](https://www.aem.live/docs/authoring).
* Para comprender cómo iniciar correctamente el proyecto de su sitio web, consulte la [sección Iniciar](https://www.aem.live/docs/#launch).

## Edge Delivery Services y otros productos de Adobe Experience Cloud {#edge-other-products}

Los Edge Delivery Services forman parte de Adobe Experience Manager y, como tales, los Edge Delivery Services AEM y los sitios de la pueden coexistir en el mismo dominio, lo que es un caso de uso común para los sitios web más grandes. Además, las páginas de AEM Sites pueden consumir fácilmente contenido de los Edge Delivery Services y viceversa.

Consulte la [Guía de introducción de desarrolladores para la creación de contenido en AEM con Edge Delivery Services](/help/edge/aem-authoring/edge-dev-getting-started.md) y aprenda a crear su propio proyecto con AEM y Edge Delivery Services.

También puede utilizar Edge Delivery Services con [Adobe Target,](https://www.aem.live/developer/target-integration) [Monitorización de usuarios reales (RUM)](https://www.aem.live/developer/rum) para diagnosticar el uso y el rendimiento de sus sitios, y [Lanzamiento.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Introducción a Edge Delivery Services {#getting-started}

Es fácil empezar a utilizar Edge Delivery Services siguiendo las [Introducción: tutorial para desarrolladores.](https://www.aem.live/developer/tutorial)

## Obtención de ayuda de Adobe {#getting-help}

Adobe proporciona tres canales para ayudarle con Edge Delivery Services:

* Interactúe con [recursos comunitarios](#community-resources) para consultas generales.
* Acceda a su [canal de colaboración de productos](#collaboration-channel) para preguntas específicas.
* [Registrar un ticket de asistencia](#support-ticket) para resolver problemas importantes y críticos.

### Acceder a recursos de la comunidad {#community-resources}

Adobe se compromete a proporcionarle la mejor participación de la comunidad y el mejor apoyo para la creación basada en Edge Delivery Services AEM, basada en la experiencia y basada en documentos.

* Participe en la [Comunidad de Experience League](https://adobe.ly/3Q6kTKl) para hacer preguntas, compartir comentarios, iniciar discusiones, buscar ayuda de expertos de Adobe y asesores/expertos de AEM, y conectarse con personas con ideas afines en tiempo real. 
* Únase a nuestro [Canal de la discordia](https://discord.gg/aem-live), una plataforma más informal para interacciones en tiempo real e intercambios de ideas rápidos.

### Cómo acceder a su canal de colaboración de productos {#collaboration-channel}

AEM Dado el valor del canal de comunicación directa con los usuarios, todos los proyectos de en el momento del lanzamiento establecerán un canal Slack para la velocidad, las actualizaciones críticas y la creación de informes a escala sobre la calidad de la experiencia. Recibirá una invitación de Adobe para unirse a un canal Slack específico de su organización.

Para obtener más información, consulte el documento [Uso del bot de Slack](https://www.aem.live/docs/slack) para obtener más información.

Puede interactuar con los equipos de productos de Adobe a través del canal de colaboración de productos aprovisionado para responder a preguntas sobre el uso del producto o las prácticas recomendadas. No hay ningún destinatario de nivel de servicio (SLT) asociado a las conversaciones a través del canal de colaboración de productos.

### Registro de un ticket de asistencia {#support-ticket}

Si un problema de producto necesita más investigación y solución de problemas y debe cumplir los SLT de respuesta, puede enviar un ticket de asistencia siguiendo este proceso con el Admin Console:

1. [Siguiendo el proceso de soporte estándar,](https://experienceleague.adobe.com/?support-tab=home#support) y cree un ticket.
1. Añada **Edge Delivery** en el título del ticket.
1. En la descripción, proporcione los siguientes detalles además de la descripción del problema:

   * URL del sitio web activo. Por ejemplo: `www.mydomain.com`.
   * URL del sitio web de origen (`.hlx` URL).

## Siguientes pasos {#whats-next}

Introducción a la revisión [Uso de Edge Delivery Services.](/help/edge/using.md)
