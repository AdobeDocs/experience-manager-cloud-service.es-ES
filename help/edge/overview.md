---
title: Información general sobre Edge Delivery Services
description: Descubra cómo AEM as a Cloud Service puede beneficiarse del rendimiento y las puntuaciones perfectas de Lighthouse que ofrecen los Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 03a1aa93-d2e6-4175-9cf3-c7ae25c0d24e
role: Admin, Architect, Developer
source-git-commit: fa50e661d05a5083be3605a8c6e26450357f4aec
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 93%

---


# Información general sobre Edge Delivery Services {#edge-delivery-services}

Con Edge Delivery Services, AEM ofrece experiencias excepcionales que fomentan la participación y las conversiones. AEM lo hace ofreciendo experiencias de alto impacto que son rápidas de crear y desarrollar. Es un conjunto de servicios que admite composición que permite un entorno de desarrollo rápido en el que los autores pueden actualizar y publicar rápidamente y en el que los nuevos sitios se inician rápidamente. De este modo, con Edge Delivery Services puede mejorar la conversión, reducir costes y proporcionar una velocidad de contenido extrema.

Mediante Edge Delivery Services, puede:

* Crear sitios rápidos con una puntuación de Lighthouse perfecta y monitorizar continuamente el rendimiento de su sitio a través de la monitorización de usuarios reales (RUM).
* Aumentar la eficacia de la creación desacoplando las fuentes de contenido. De forma predeterminada, puede utilizar tanto la creación WYSIWYG como la creación basada en documentos. De este modo, puede trabajar con varias fuentes de contenido en el mismo sitio web.
* Utilice un marco de trabajo de experimentación integrado que permita la creación y ejecución rápidas de pruebas sin impacto en el rendimiento y la publicación rápida en producción de un ganador de pruebas.

## Reacción ágil a las necesidades empresariales {#agile-reaction}

Como reconocido líder del sector desde hace mucho, Adobe sabe lo importante que es poder crear y publicar con rapidez contenido nuevo y significativo para sus clientes. El mercado ha dejado claros los desafíos comunes para escalar la creación de contenido, entre los que se incluyen:

1. **La demanda de contenido sigue creciendo.**
   * Es necesario desbloquear nuevos autores de contenido para satisfacer esta demanda.
   * El proceso de creación de contenido debe escalarse de forma eficaz en toda la empresa.
   * Los autores deben poder reaccionar de manera rápida a los cambios de tendencias.
1. **Se necesita contenido omnicanal.**
   * El control del diseño es necesario, con independencia de la entrega de contenido.
   * Es necesario facultar a los autores para que cambien de forma directa el diseño del contenido.
1. **Aumenta la presión para aumentar el ROI en el contenido.**
   * Los propios autores necesitan la capacidad de optimizar el contenido que crean.

Estas tendencias han demostrado ser coherentes en todo el sector. Sin embargo, los requisitos individuales varían de forma inevitable de un proyecto a otro. El objetivo de cualquier proyecto de Edge Delivery Services es encontrar la solución que funcione para sus usuarios.

1. **Céntrese en el valor, en lugar de en las características.**: determine el flujo de trabajo más optimizado para asistir a los autores, en lugar de perderse en el amplio conjunto de funciones de AEM.
1. **Aproveche la flexibilidad de AEM.**: no es necesario usar las características de AEM en vacío. Utilice las funciones que necesite en cada caso de uso.
1. **Aproveche los conocimientos de su autor.**: involucre a autores de contenido real en el proyecto desde el principio para asegurarse de ofrecerles lo que necesitan implementando funciones que tienen sentido.

Al centrarse en el valor para los autores, su proyecto de Edge Delivery Services puede satisfacer las modernas exigencias del sector a las que se enfrentan los creadores y proporcionar contenido de manera rápida para agradar a sus clientes.

## Herramientas flexibles para los creadores de contenido {#overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Puede usar la [administración de contenido de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/getting-started/concepts.html?lang=es) y la creación WYSIWYG utilizando el [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md), así como la [creación basada en documentos](https://www.aem.live/docs/authoring).

En el diagrama siguiente se ilustra cómo se puede editar contenido en Microsoft Word (creación basada en documentos) y publicarlo en Edge Delivery Services. También muestra la edición WYSIWYG utilizando el Editor universal.

![Arquitectura de Edge Delivery](assets/AEM-with-EDS-publishing-simple2.png)

Edge Delivery Services utiliza GitHub para que pueda administrar e implementar código directamente desde su repositorio de GitHub. El nuevo contenido se añade al instante sin que sea necesario un proceso de reconstrucción.

### Creación basada en documentos {#document-based}

Con la creación basada en documentos, puede utilizar contenido directamente de Microsoft Word o Google Docs para que esos orígenes se conviertan en páginas del sitio web. Los encabezados, las listas, las imágenes y los elementos de tipo de fuente se pueden transferir desde el origen inicial al sitio web.

* Con la creación basada en documentos, cualquier experto en marketing puede crear contenido de manera rápida mediante herramientas conocidas (Microsoft Word, Google Docs, etc.).
* La creación de contenido se optimiza al permitir la creación, revisión y publicación directa dentro de los documentos de origen.
* Dado que se emplean herramientas conocidas, no se requiere ninguna incorporación para los autores de contenido, lo que aumenta su velocidad.
* La funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub.

![Creación basada en documentos](assets/document-based-authoring.png)

Para obtener más información, consulte la documentación sobre creación basada en documentos:

* Para obtener más información sobre cómo empezar a utilizar Edge Delivery, consulte la [sección Versión](https://www.aem.live/docs/#build).
* Para comprender cómo crear y publicar contenido mediante Edge Delivery, consulte la [sección Publicar](https://www.aem.live/docs/authoring).
* Para comprender cómo iniciar correctamente el proyecto de su sitio web, consulte la [sección Iniciar](https://www.aem.live/docs/#launch).

### Creación WYSIWYG {#wysiwyg-authoring}

La creación de lo que se ve es lo que se obtiene (WYSIWYG, por sus siglas en inglés) aprovecha el Editor universal, una solución personalizable e integral para editar contenido en directo y en contexto con una vista previa muy visual.

* Con la creación WYSIWYG, puede aumentar la eficacia del autor, ya sea sin encabezado o con encabezado.
* Puede aprovechar las completas funcionalidades de gestión de contenido de AEM, incluidas las de flujo de trabajo y control de la gestión de contenido.
* Aproveche numerosos puntos de extensión para admitir sus propios procesos e integraciones.
* La funcionalidad del sitio se puede desarrollar mediante CSS y JavaScript en GitHub.

![Creación WYSIWYG](assets/wysiwyg-authoring.png)

Más información en la documentación sobre creación WYSIWYG:

* Para obtener información general del editor universal y de la creación WYSIWYG, consulte el documento [Creación de contenido WYSIWYG para Edge Delivery Services.](/help/edge/wysiwyg-authoring/authoring.md)
* Para obtener información general para desarrolladores, consulte el documento [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)

### Decisión de un método de creación {#authoring-method}

La flexibilidad de AEM garantiza que se cubran sus necesidades de creación. Adobe puede ayudarle a determinar qué método (o métodos) se adapta mejor a sus necesidades.

* Incluya siempre a los autores de contenido en la decisión.
* Se pueden implementar varios métodos de creación.
* Siempre puede cambiar el método de creación con posterioridad.
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

Si un problema de producto necesita una investigación y una solución de problemas adicionales y debe cumplir los SLT de respuesta, puede enviar un ticket de asistencia.

Para registrar un ticket de asistencia, primero debe registrar el sitio de Edge Delivery en Cloud Manager. Se recomienda registrar su sitio web con Cloud Manager para todos los usuarios de AEM as a Cloud Service, y [esto ofrece una serie de ventajas.](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) Consulte [la documentación de Cloud Manager](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) para obtener más información si aún no ha registrado el sitio.

Una vez registrado el sitio web con Cloud Manager, siga este proceso con el Admin Console para enviar un ticket de asistencia:

1. [Siga el proceso de asistencia estándar](https://experienceleague.adobe.com/?support-tab=home#support) y cree un ticket.
1. Añada **Edge Delivery** en el título del ticket.
1. En la descripción, proporcione los siguientes detalles además de la descripción del problema:

   * URL del sitio web activo. Por ejemplo: `www.mydomain.com`.
   * URL del sitio web de origen (`.hlx` URL).

## Siguientes pasos {#whats-next}

Para empezar revise [Uso de Edge Delivery Services](/help/edge/using.md).
