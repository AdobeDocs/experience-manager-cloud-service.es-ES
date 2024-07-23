---
title: Información general sobre Edge Delivery Services
description: Descubra cómo AEM as a Cloud Service puede beneficiarse del rendimiento y las puntuaciones perfectas de Lighthouse que ofrecen los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: 6c7e704dff97e8549664618f879863c3ca0f8f86
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 55%

---


# Información general sobre Edge Delivery Services {#edge-delivery-services}

Con Edge Delivery Services, AEM ofrece experiencias excepcionales que fomentan la participación y las conversiones. AEM lo hace ofreciendo experiencias de alto impacto que son rápidas de crear y desarrollar. Es un conjunto de servicios que admite composición que permite un entorno de desarrollo rápido en el que los autores pueden actualizar y publicar rápidamente y en el que los nuevos sitios se inician rápidamente. De este modo, con Edge Delivery Services puede mejorar la conversión, reducir costes y proporcionar una velocidad de contenido extrema.

Mediante Edge Delivery Services, puede:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta y monitorizar continuamente el rendimiento de su sitio a través de la monitorización de usuarios reales (RUM).
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar la creación WYSIWYG y basada en documentos. De este modo, puede trabajar con varias fuentes de contenido en el mismo sitio web.
* Utilice un marco de trabajo de experimentación integrado que permita la creación y ejecución rápidas de pruebas sin impacto en el rendimiento y la publicación rápida en producción de un ganador de pruebas.

## Reacción ágil a las necesidades empresariales {#agile-reaction}

Como reconocido líder del sector desde hace mucho tiempo, Adobe sabe lo importante que es poder crear y publicar rápidamente contenido nuevo y significativo para sus clientes. El mercado ha dejado en claro los desafíos comunes para escalar la creación de contenido, entre los que se incluyen:

1. **La demanda de contenido sigue creciendo.**
   * Es necesario desbloquear nuevos autores de contenido para satisfacer esta demanda.
   * El proceso de creación de contenido debe escalarse de forma eficaz en todo el negocio.
   * Los autores deben poder reaccionar rápidamente ante los cambios de tendencias.
1. **Se necesita contenido omnicanal.**
   * Se necesita el control del diseño, independientemente de la entrega de contenido.
   * Es necesario facultar a los autores para que cambien directamente el diseño del contenido.
1. **Aumenta la presión para aumentar el retorno de la inversión en el contenido.**
   * Los propios autores necesitan la capacidad de optimizar el contenido que crean.

Estas tendencias han demostrado ser coherentes en toda la industria. Sin embargo, los requisitos individuales inevitablemente varían de un proyecto a otro. El objetivo de cualquier proyecto de Edge Delivery Services es encontrar la solución que mejor se adapte a sus necesidades.

1. **Céntrese en el valor en lugar de las características.AEM**: determine el flujo de trabajo más optimizado para servir a los autores en lugar de perderse en el conjunto de características expansivas de la aplicación en el que se va a.
1. AEM **Aproveche la flexibilidad de la.AEM**: no es necesario usar las características de la en un vacío. Utilice las funciones que necesite por caso de uso.
1. **Aproveche la experiencia de su autor.**: involucre a autores de contenido real en el proyecto desde el principio para asegurarse de que entrega el valor que necesitan implementando las funciones que tienen sentido.

Al centrarse en el valor para sus autores, su proyecto de Edge Delivery Services puede satisfacer las exigencias modernas del sector a las que se enfrentan sus creadores de contenido y proporcionar contenido rápidamente para deleitar a sus clientes.

## Herramientas flexibles de creación para los creadores de contenido {#overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Puede usar la [administración de contenido de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) y la creación WYSIWYG utilizando el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md), así como la [creación basada en documentos](https://www.aem.live/docs/authoring).

En el diagrama siguiente se ilustra cómo se puede editar contenido en Microsoft Word (creación basada en documentos) y publicarlo en Edge Delivery Services. También muestra la edición WYSIWYG utilizando el Editor universal.

![Arquitectura de Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services utiliza GitHub para que pueda administrar e implementar código directamente desde su repositorio de GitHub. El nuevo contenido se añade instantáneamente sin un proceso de reconstrucción.

### Creación basada en documentos {#document-based}

Con la creación basada en documentos, puede utilizar contenido directamente de Microsoft Word o Google Docs para que esas fuentes se conviertan en páginas del sitio web. Encabezados, listas, imágenes, elementos de fuente se pueden transferir desde la fuente inicial al sitio web.

* Con la creación basada en documentos, todos los expertos en marketing pueden crear contenido rápidamente con herramientas de creación conocidas (Microsoft Word, Google Docs, etc.).
* La creación de contenido se optimiza al permitir la creación, revisión y publicación directamente dentro de los documentos de origen.
* Dado que se utilizan herramientas conocidas, se requiere la incorporación cero para los autores de contenido, lo que aumenta la velocidad de contenido.
* La funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub.

![Creación basada en documentos](assets/document-based-authoring.png)

Para obtener más información, consulte la documentación de creación basada en documentos:

* Para obtener más información sobre cómo empezar a utilizar Edge Delivery, consulte la [sección Versión](https://www.aem.live/docs/#build).
* Para comprender cómo crear y publicar contenido mediante Edge Delivery, consulte la [sección Publicar](https://www.aem.live/docs/authoring).
* Para comprender cómo iniciar correctamente el proyecto de su sitio web, consulte la [sección Iniciar](https://www.aem.live/docs/#launch).

### Creación WYSIWYG {#wysiwyg-authoring}

La creación de elementos que se ven es lo que se obtiene (WYSIWYG) aprovecha el Editor universal, un lugar personalizable y de ventanilla única para editar contenido en directo y en contexto con una previsualización visual.

* Con la creación WYSIWYG, puede aumentar la eficacia del autor, ya sea sin encabezado o con encabezado.
* AEM Puede aprovechar las ventajas de las funcionalidades completas de gestión de contenido, incluidas las de flujo de trabajo y control de la gestión de contenido.
* Aproveche numerosos puntos de extensión para admitir sus propios procesos e integraciones.
* La funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub.

![Creación de WYSIWYG](assets/wysiwyg-authoring.png)

Más información en la documentación de creación de WYSIWYG:

* Para obtener una descripción general del editor universal y de la creación WYSIWYG, consulte el documento [Creación de contenido WYSIWYG para Edge Delivery Services.](/help/edge/wysiwyg-authoring/authoring.md)
* Para obtener información general para desarrolladores, consulte el documento [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### Decidir el método de creación {#authoring-method}

AEM La flexibilidad de la garantiza que se cubran sus necesidades de creación. El Adobe puede ayudarle a determinar qué método (o métodos) se adapta mejor a sus necesidades.

* Incluya siempre a los autores de contenido en la decisión.
* Se pueden implementar varios métodos de creación.
* Siempre puede cambiar el método de creación después de los hechos.
* No debe decidir antes de la implementación, sino como parte de la implementación.

Consulte el documento [Elección de un método de creación](authoring-methods.md) para obtener más información.

## Edge Delivery Services y otros productos de Adobe Experience Cloud {#edge-other-products}

Edge Delivery Services forman parte de Adobe Experience Manager y, como tal, dichos Edge Delivery Services y AEM Sites pueden coexistir en el mismo dominio, lo que constituye un caso de uso común para sitios web de mayor tamaño. Además, el contenido de Edge Delivery Services se puede consumir fácilmente en sus páginas de AEM Sites y viceversa.

Consulte la [Guía de introducción del desarrollador para WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) y aprenda a crear su propio proyecto con AEM y Edge Delivery Services.

También puede utilizar Edge Delivery Services con [Adobe Target,](https://www.aem.live/developer/target-integration) [Monitorización de usuarios reales (RUM)](https://www.aem.live/developer/rum) para diagnosticar el uso y el rendimiento de sus sitios y [Launch.](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

## Introducción a Edge Delivery Services {#getting-started}

Es fácil empezar a utilizar Edge Delivery Services siguiendo el tutorial [Introducción: tutorial para desarrolladores.](https://www.aem.live/developer/tutorial)

## Obtención de ayuda de Adobe {#getting-help}

Adobe proporciona tres canales para ayudarle con Edge Delivery Services:

* Interactúe con los [recursos de la comunidad](#community-resources) para realizar consultas generales.
* Acceda al [canal de colaboración de productos](#collaboration-channel) para preguntas específicas.
* [Registre un ticket de asistencia](#support-ticket) para resolver problemas importantes y críticos.

### Acceder a recursos de la comunidad {#community-resources}

Adobe se compromete a ofrecerle la mejor participación de la comunidad y asistencia para Edge Delivery Services, la creación WYSIWYG y la creación basada en documentos.

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
