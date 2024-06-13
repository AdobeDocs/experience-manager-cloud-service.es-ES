---
title: Información general sobre Edge Delivery Services
description: Descubra cómo AEM as a Cloud Service puede beneficiarse del rendimiento y las puntuaciones perfectas de Lighthouse que ofrecen los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 8d5d8910a906e2adf17fa9c75f17634602c2e0b9
workflow-type: ht
source-wordcount: '862'
ht-degree: 100%

---


# Información general sobre Edge Delivery Services {#edge-delivery-services}

Con Edge Delivery Services, AEM ofrece experiencias excepcionales que fomentan la participación y las conversiones. AEM lo hace ofreciendo experiencias de alto impacto que son rápidas de crear y desarrollar. Es un conjunto de servicios que admite composición que permite un entorno de desarrollo rápido en el que los autores pueden actualizar y publicar rápidamente y en el que los nuevos sitios se inician rápidamente. De este modo, con Edge Delivery Services puede mejorar la conversión, reducir costes y proporcionar una velocidad de contenido extrema.

Mediante Edge Delivery Services, puede:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta y monitorizar continuamente el rendimiento de su sitio a través de la monitorización de usuarios reales (RUM).
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar tanto la creación en AEM como la creación basada en documentos. De este modo, puede trabajar con varias fuentes de contenido en el mismo sitio web.
* Utilice un marco de trabajo de experimentación integrado que permita la creación y ejecución rápidas de pruebas sin impacto en el rendimiento y la publicación rápida en producción de un ganador de pruebas.

## Información general {#overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Puede usar la [administración de contenido de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) y la creación basada en AEM utilizando el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) así como la [creación basada en documentos.](https://www.aem.live/docs/authoring)

En el diagrama siguiente se ilustra cómo se puede editar contenido en Microsoft Word (creación basada en documentos) y publicarlo en Edge Delivery Services. También muestra la edición basada en AEM utilizando el Editor universal.

![Arquitectura de Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Puede utilizar contenido directamente de Microsoft Word o Google Docs para que esos orígenes se conviertan en páginas del sitio web. Además, los encabezados, las listas, las imágenes y los elementos de tipo de fuente se pueden transferir desde el origen inicial al sitio web. El nuevo contenido se añade al instante sin que sea necesario un proceso de reconstrucción.

Edge Delivery Services utiliza GitHub para que pueda administrar e implementar código directamente desde su repositorio de GitHub. Por ejemplo, puede escribir contenido en Google Docs o en Microsoft Word y la funcionalidad de su sitio se puede desarrollar mediante CSS y JavaScript en GitHub. Cuando esté listo, utilice la extensión del explorador de la barra de tareas para obtener una vista previa y publicar actualizaciones de contenido.

Para más información, consulte la documentación de Edge Delivery Services:

* Para obtener más información sobre cómo empezar a utilizar Edge Delivery, consulte la [sección Versión](https://www.aem.live/docs/#build).
* Para comprender cómo crear y publicar contenido mediante Edge Delivery, consulte la [sección Publicar](https://www.aem.live/docs/authoring).
* Para comprender cómo iniciar correctamente el proyecto de su sitio web, consulte la [sección Iniciar](https://www.aem.live/docs/#launch).

## Edge Delivery Services y otros productos de Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services forman parte de Adobe Experience Manager y, como tal, dichos Edge Delivery Services y AEM Sites pueden coexistir en el mismo dominio, lo que constituye un caso de uso común para sitios web de mayor tamaño. Además, el contenido de Edge Delivery Services se puede consumir fácilmente en sus páginas de AEM Sites y viceversa.

Consulte la [Guía de introducción de desarrolladores para la creación de contenido en AEM con Edge Delivery Services](/help/edge/aem-authoring/edge-dev-getting-started.md) y aprenda a crear su propio proyecto con AEM y Edge Delivery Services.

También puede utilizar Edge Delivery Services con [Adobe Target,](https://www.aem.live/developer/target-integration) [Monitorización de usuarios reales (RUM)](https://www.aem.live/developer/rum) para diagnosticar el uso y el rendimiento de sus sitios y [Launch.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Introducción a Edge Delivery Services {#getting-started}

Es fácil empezar a utilizar Edge Delivery Services siguiendo el tutorial [Introducción: tutorial para desarrolladores.](https://www.aem.live/developer/tutorial)

## Obtención de ayuda de Adobe {#getting-help}

Adobe proporciona tres canales para ayudarle con Edge Delivery Services:

* Interactúe con los [recursos de la comunidad](#community-resources) para realizar consultas generales.
* Acceda al [canal de colaboración de productos](#collaboration-channel) para preguntas específicas.
* [Registre un ticket de asistencia](#support-ticket) para resolver problemas importantes y críticos.

### Acceder a recursos de la comunidad {#community-resources}

Adobe se compromete a ofrecerle la mejor participación de la comunidad y asistencia para Edge Delivery Services, la creación basada en AEM y en documentos.

* Participe en la [Comunidad de Experience League](https://adobe.ly/3Q6kTKl) para hacer preguntas, compartir comentarios, iniciar discusiones, buscar ayuda de expertos de Adobe y asesores/expertos de AEM, y conectarse con personas con ideas afines en tiempo real. 
* Únase a nuestro [Canal de la discordia](https://discord.gg/aem-live), una plataforma más informal para interacciones en tiempo real e intercambios de ideas rápidos.

### Cómo acceder a su canal de colaboración de productos {#collaboration-channel}

Dado el valor del canal de comunicación directa con los usuarios, todos los proyectos de AEM en el momento del lanzamiento establecerán un canal Slack para ofrecer actualizaciones críticas y rápidas, así como sistemas de informes escalados sobre la calidad de la experiencia. Recibirá una invitación de Adobe para unirse a un canal Slack específico de su organización.

Para obtener más información, consulte el documento [Uso del bot de Slack](https://www.aem.live/docs/slack) para obtener más información.

Puede interactuar con los equipos de productos de Adobe a través del canal de colaboración de productos suministrado para responder a preguntas sobre el uso del producto o las prácticas recomendadas. No hay públicos destinatarios de nivel de servicio (SLT) asociados con las conversaciones a través del canal de colaboración de productos.

### Registro de un ticket de asistencia {#support-ticket}

Si un problema de producto requiere una investigación y resolución de problemas adicionales y debe cumplir los SLT de respuesta, puede enviar un ticket de asistencia mediante Admin Console:

1. [Siga el proceso de asistencia estándar](https://experienceleague.adobe.com/?support-tab=home#support) y cree un ticket.
1. Añada **Edge Delivery** en el título del ticket.
1. En la descripción, proporcione los siguientes detalles además de la descripción del problema:

   * URL del sitio web activo. Por ejemplo: `www.mydomain.com`.
   * URL del sitio web de origen (`.hlx` URL).

## Siguientes pasos {#whats-next}

Para empezar revise [Uso de Edge Delivery Services](/help/edge/using.md).
