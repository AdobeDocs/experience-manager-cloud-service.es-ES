---
title: Introducción a AEM Forms as a Cloud Service
description: Descubra las funcionalidades de AEM Forms para crear formularios adaptables, automatizar flujos de trabajo y administrar documentos digitales. Plataforma completa para procesos empresariales impulsados por formularios.
landing-page-description: Aprenda a utilizar AEM Forms as a Cloud Service para crear formularios adaptables, procesar documentos y automatizar flujos de trabajo empresariales.
keywords: AEM Forms, formularios adaptables, generador de formularios, formularios digitales, automatización del flujo de trabajo, servicios de documentos, modelo de datos de formulario
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
exl-id: 50d7ce19-7d76-4ea1-a54c-8ca0e5379982
source-git-commit: eca09e1bf2ba4466f54e915e01218cc89cf5b116
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# Introducción a AEM Forms as a Cloud Service {#introduction}



Adobe Experience Manager Forms as a Cloud Service ofrece una plataforma completa para crear, administrar y optimizar experiencias de formularios digitales. Las organizaciones utilizan AEM Forms para digitalizar procesos basados en papel, crear formularios web adaptables, automatizar flujos de trabajo de documentos y ofrecer comunicaciones personalizadas a escala.

La plataforma combina las capacidades de creación de formularios con servicios back-end sólidos, lo que le permite crear de todo, desde formularios de contacto simples hasta aplicaciones empresariales complejas de varios pasos. Con la arquitectura nativa de la nube, obtiene actualizaciones automáticas, escalado elástico y seguridad de nivel empresarial sin administrar la infraestructura.

Esta guía presenta las funciones principales organizadas en torno al ciclo de vida completo del formulario, desde el diseño inicial hasta la optimización continua.

## Novedades de AEM Forms. {#whats-new}

**Últimos elementos destacados de la versión:**

- **Componente de entrada de fecha y hora**: entrada de usuario mejorada con interfaz de calendario y reloj para una selección precisa de fecha y hora
- **Seguridad mejorada de carga de archivos**: validación automática y comprobación de tipo de contenido para evitar formatos de archivo no compatibles
- **Gestión de errores mejorada**: Mejor depuración con códigos de error específicos para las acciones de envío personalizadas
- **Mejoras en el documento de registro**: opción para excluir los campos ocultos para la generación de documentos más limpios

**Características previas al lanzamiento:**

- **Compatibilidad con formato AFP**: funciones de impresión de nivel empresarial con API de comunicación
- **Mejoras en el editor de reglas**: compatibilidad con JavaScript moderno, variables dinámicas y reglas de panel según el contexto
- **Métodos de validación mejorados**: validación a nivel de formulario, campo y panel con flexibilidad mejorada

[Ver → notas de la versión completas](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Programa de acceso anticipado {#early-access}

Obtenga acceso exclusivo a las innovaciones de vanguardia de AEM Forms antes de que estén disponibles de forma general.

**Características actuales de acceso anticipado:**

- **Asistente de IA de AEM Forms**: IA generativa para la creación automatizada de formularios, la generación de paneles y las recomendaciones de optimización
- **Componente de firma manuscrita**: captura de firma directa dentro de los formularios mediante el mouse, el lápiz o la pantalla táctil
- **Integración directa de API**: conéctese a las API en el editor de reglas sin requerir la configuración del modelo de datos de formulario
- **Optimización de Forms**: sugerencias de análisis de rendimiento con tecnología de IA y mejora de la tasa de conversión

**Únase al programa:**
Sea uno de los primeros en acceder a las innovaciones y ayudar a dar forma al futuro de AEM Forms.

[Solicitar acceso →](mailto:aem-forms-ea@adobe.com) | [Más información →](/help/forms/early-access-ea-features.md)


## Funciones principales {#core-capabilities}

AEM Forms es compatible con el recorrido completo de formularios digitales, desde la creación inicial hasta la optimización continua. Cada fase se basa en la anterior, lo que crea una plataforma completa para los procesos empresariales impulsados por formularios.

**Recorrido de flujo de trabajo de AEM Forms:**

    CREAR → GOBERNAR → PUBLICAR → CAPTURAR → PROCESO → INTEGRAR → RASTREAR → ARCHIVO → MEJORAR
    ↓        ↓        ↓         ↓         ↓         ↓          ↓       ↓        ↓
    Diseño   Revisar   Implementar   Recopilar   Handle   Connect   Almacén de monitor   Optimizar
    ↑                                                                              ↓
    ←←←←←←←←←←←←←←← bucle de mejora continua ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←

### Crear: diseño y desarrollo de formularios {#create}

Cree formularios adaptables utilizando varios métodos de creación adaptados a diferentes necesidades y requisitos técnicos.

**Generador de formularios visuales**
Diseñe formularios adaptables mediante interfaces de arrastrar y soltar usando [componentes principales](/help/forms/creating-adaptive-form-core-components.md), [componentes de base](/help/forms/creating-adaptive-form.md) o [Edge Delivery Services](/help/edge/docs/forms/overview.md). El editor visual proporciona comentarios inmediatos y mantiene un marcado semántico limpio que funciona en todos los dispositivos y tecnologías de asistencia.

**Creación basada en documentos**
Cree formularios con herramientas conocidas como Microsoft Excel mediante [Edge Delivery Services](/help/edge/docs/forms/overview.md). Este enfoque permite a los autores de contenido crear formularios de alto rendimiento sin experiencia técnica, a la vez que logran puntuaciones excepcionales de Google Lighthouse.

**Plantillas y temas**
Acelere la creación de formularios utilizando [plantillas](/help/forms/template-editor-core-components.md) prediseñadas que definen la estructura y el contenido inicial. Aplique una personalización de marca coherente con [themes](/help/forms/using-themes-in-core-components.md) que controlan el estilo visual en varios formularios, lo que garantiza la coherencia del diseño y reduce el tiempo de desarrollo.

**Integraciones de datos**
Conectar formularios a sistemas back-end durante la fase de diseño. El [Modelo de datos de formulario](/help/forms/create-form-data-models.md) proporciona una interfaz unificada para varias fuentes de datos, lo que permite [la población previa](/help/forms/prepopulate-adaptive-form-fields.md), [las reglas de validación](/help/forms/rule-editor-core-components.md) y un flujo de datos fluido entre los formularios y los sistemas empresariales.

**Validaciones y lógica condicional**
Implemente [lógica condicional](/help/forms/rule-editor-core-components.md), divulgación progresiva y validación adaptativa para guiar a los usuarios a través de procesos complejos. [La funcionalidad de guardar y reanudar](/help/forms/save-core-component-based-form-as-draft.md) permite a los usuarios completar formularios en varias sesiones.

**HTML5 Forms**
Procesar formularios basados en XFA como [formularios HTML5](/help/forms/introductionhtml5.md) para dispositivos móviles y exploradores heredados. HTML5 Forms proporciona una experiencia móvil nativa sin complementos mientras mantiene la lógica y validación del formulario de las plantillas XDP originales.

**Comunicaciones interactivas**
Cree comunicaciones centradas en el documento como extractos, facturas y avisos con un editor visual. [Comunicaciones interactivas](/help/forms/interactive-communication/create-interactive-communication.md) combinan contenido estático con datos dinámicos para generar comunicaciones personalizadas entre los canales impreso y digital.

### Gobernar: revisión y cumplimiento {#govern}

Establezca procesos de supervisión y aprobación para garantizar que los formularios cumplan las normas organizativas y los requisitos regulatorios.

**Aprobaciones basadas en flujos de trabajo**
Dirija los diseños de formulario a través de procesos de revisión de varios pasos con asignaciones basadas en roles. Las partes interesadas pueden [revisar](/help/forms/create-reviews-forms.md), [comentar](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) y aprobar formularios antes de la publicación, manteniendo el control de calidad y la supervisión del cumplimiento mediante [flujos de trabajo de AEM](/help/forms/aem-forms-workflow.md).

**Administración de versiones**
Realice un seguimiento de las versiones de los formularios y mantenga los seguimientos de auditoría para el cumplimiento normativo. El control de versiones integrado [versioning](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) garantiza que se puedan revertir los cambios, comparar las iteraciones y mantener los registros históricos para las auditorías de cumplimiento.

**Control de acceso y permisos**
Defina permisos granulares para la creación, edición y publicación de formularios. [El acceso basado en roles](/help/forms/forms-groups-privileges-tasks.md) garantiza que solo los usuarios autorizados puedan modificar los formularios, manteniendo al mismo tiempo la separación de tareas para los procesos empresariales confidenciales.

### Publicación: distribución multicanal {#publish}

Implemente formularios en varios canales y puntos de contacto para llegar a los usuarios independientemente de dónde se encuentren.

**Publicación omnicanal**
Publicar formularios en [AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md), páginas web independientes, aplicaciones móviles o [incrustar en sistemas de terceros](/help/forms/embed-adaptive-form-core-components-external-web-page.md). La publicación de una sola fuente garantiza la coherencia al adaptarse a diferentes requisitos de canal.

**Localización y Personalization**
Envíe formularios en varios idiomas utilizando [flujos de trabajo de traducción de AEM](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md), con compatibilidad para [idiomas de izquierda a derecha y de derecha a izquierda](/help/forms/right-left-languages.md). Integre con Adobe Target para personalizar las experiencias de los formularios en función de segmentos de usuarios, comportamientos o datos contextuales.

**Optimización del rendimiento**
Aproveche Edge Delivery Services para una carga de formularios increíblemente rápida y un rendimiento de SEO óptimo. Las redes de entrega de contenido garantizan la accesibilidad global con una latencia mínima.

**Portal de Forms**
Cree repositorios de formularios centralizados en los que los usuarios puedan detectar, acceder y administrar formularios. El [Portal de Forms](/help/forms/configure-forms-portal.md) proporciona funciones de búsqueda, categorización de formularios, administración de borradores y seguimiento de envíos en una interfaz unificada para mejorar la experiencia del usuario.

### Capture: experiencia del usuario y recopilación de datos {#capture}

Optimice la experiencia de cumplimentación de formularios para maximizar las tasas de finalización y la calidad de los datos.

**Diseño interactivo**
Forms se adapta automáticamente a diferentes tamaños de pantalla y métodos de entrada. Los controles táctiles, la navegación mediante el teclado y la compatibilidad con lectores de pantalla garantizan la [accesibilidad](/help/forms/creating-accessible-adaptive-forms.md) en todos los tipos de usuarios.

**Firmas digitales**
Integre [Adobe Sign](/help/forms/working-with-adobe-sign.md) para firmas electrónicas legalmente vinculantes dentro de la experiencia del formulario. Los usuarios pueden firmar documentos sin salir del formulario, lo que optimiza los procesos de aprobación y reduce el abandono.

**Acciones de envío**
Configure [acciones de envío](/help/forms/configure-submit-actions-core-components.md) para definir qué sucede cuando los usuarios completan y envían formularios. Dirija los datos al correo electrónico, las bases de datos, los flujos de trabajo o los sistemas externos, al tiempo que proporciona comentarios y confirmación inmediatos a los usuarios.

### Proceso: Gestión y enrutamiento de envíos {#process}

Administre los envíos de formularios con capacidades sólidas de procesamiento, validación y enrutamiento.

**Validación y procesamiento de datos**
Garantice la integridad de los datos mediante reglas de procesamiento automatizadas y validación del lado del servidor. Transforme, valide y enrute los datos enviados al generar recibos, confirmaciones o materiales de seguimiento para los usuarios.

**API de comunicación**
Genere, manipule y proteja documentos mediante programación a través de [API RESTful](/help/forms/aem-forms-cloud-service-communications-introduction.md). Cree archivos PDF, formatos listos para imprimir, combine documentos, aplique firmas digitales y procese [operaciones por lotes](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) de gran volumen para flujos de trabajo de documentos a escala empresarial.

**Documento de registro**
Generar automáticamente registros PDF de envíos de formularios para la conformidad y la confirmación de los usuarios. [Documento de registro](/help/forms/generate-document-of-record-core-components.md) crea versiones imprimibles y con formato de formularios completados con datos enviados, proporcionando documentación oficial para transacciones y requisitos regulatorios.

**Orquestación de flujo de trabajo**
Almacene en déclencheur procesos empresariales complejos basados en envíos de formularios. Dirija los datos a través de cadenas de aprobación, asigne tareas a usuarios específicos y automatice operaciones rutinarias mientras mantiene las pistas de auditoría.

**Gestión y recuperación de errores**
Los mecanismos de reintentos integrados y el procesamiento de reserva garantizan que no se pierdan los envíos. El registro completo ayuda a solucionar problemas y a mantener los acuerdos de nivel de servicio.

### Integrar: conectividad back-end {#integrate}

Conecte los formularios a los sistemas empresariales existentes y a las fuentes de datos para obtener un flujo de información fluido.

**Conectores pregenerados**
Integración nativa con las soluciones [Salesforce](/help/forms/configure-salesforce.md), [Microsoft Dynamics](/help/forms/configure-msdynamics.md), [SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md) y Adobe Experience Cloud. Los conectores creados previamente reducen el tiempo de desarrollo y garantizan una sincronización de datos fiable.

**Integración de API RESTful**
Conéctese a cualquier servicio accesible en la web a través de las API RESTful mediante [acciones de envío](/help/forms/configure-submit-action-restpoint.md) o [integración de datos](/help/forms/data-integration.md). El modelo de datos de formulario abstrae la complejidad de la integración y proporciona una interfaz coherente independientemente de la arquitectura del sistema subyacente.

**Intercambio de datos en tiempo real**
Habilitar el flujo de datos bidireccional entre formularios y sistemas empresariales. Rellene previamente formularios de registros existentes, valide con datos activos y actualice varios sistemas simultáneamente al enviar mediante la [integración de datos](/help/forms/data-integration.md) completa.

### Seguimiento: Análisis y monitorización del rendimiento {#track}

Comprenda el rendimiento del formulario y el comportamiento del usuario a través de análisis y monitorización completos.

**Análisis de formularios**
Rastree las tasas de finalización, los patrones de abandono y las interacciones a nivel de campo mediante la [integración de Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md). Identifique los puntos de fricción, mida los canales de conversión y comprenda el comportamiento del usuario en diferentes segmentos.

**Supervisión del rendimiento**
Monitorice los tiempos de carga de los formularios, las tasas de éxito de los envíos y el rendimiento del sistema. Los paneles en tiempo real proporcionan perspectivas sobre el estado técnico y las métricas de experiencia del usuario.

**Business Intelligence**
Generar informes sobre el uso del formulario, los volúmenes de envío y la eficacia del proceso. Analytics informa sobre la planificación de la capacidad, la optimización de la experiencia del usuario y las mejoras de los procesos empresariales.

**Informes de transacciones**
Monitorice el uso de la API, los volúmenes de generación de documentos y las [transacciones facturables](/help/forms/transaction-reports-billable-apis.md) en su implementación de AEM Forms. Realice un seguimiento de los patrones de consumo, optimice la asignación de recursos y mantenga el cumplimiento de los requisitos de licencias basados en el uso.

### Archivo: Administración de documentos y cumplimiento {#archive}

Almacene y administre de forma segura los envíos de formularios y los documentos generados para la retención y el cumplimiento a largo plazo.

**Almacenamiento de documentos**
Almacene los documentos generados y los envíos de formularios en el sistema de administración de recursos digitales de AEM o integre repositorios de documentos externos como [SharePoint](/help/forms/configure-submit-action-sharepoint.md), [OneDrive](/help/forms/configure-submit-action-onedrive.md) o [Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md).

**Cumplimiento y retención**
Implementar políticas de retención de datos que cumplan con los requisitos regulatorios, incluidos el RGPD, la CCPA y la HIPAA. [Procesos de archivo automatizados](/help/forms/aem-forms-cloud-service-communications-batch-processing.md) garantizan que los documentos se conserven durante los períodos necesarios y se eliminen de forma segura cuando corresponda.

**Control de acceso y seguridad**
Aplique cifrado, firmas digitales y [controles de acceso basados en roles](/help/forms/forms-groups-privileges-tasks.md) a los documentos archivados. Las pistas de auditoría rastrean el acceso a los documentos y las modificaciones para la creación de informes de cumplimiento y la supervisión de la seguridad.

### Mejorar: optimización {#improve}

Optimice continuamente el rendimiento del formulario y la experiencia del usuario a través de perspectivas y pruebas basadas en datos.

**Integración de pruebas A/B**
Utilice Adobe Target para probar diferentes diseños de formulario, disposiciones de campos y flujos de usuarios. El análisis estadístico ayuda a identificar los enfoques más efectivos para diferentes segmentos de usuarios y casos de uso.

**Optimización Impulsada Por Analytics**
Analice los datos de comportamiento del usuario para identificar oportunidades de mejora. [Vea y comprenda los informes de análisis](/help/forms/view-understand-aem-forms-analytics-reports.md) para la asignación de calor, el análisis de interacción de campos y el reconocimiento de patrones de abandono a fin de informar las mejoras de diseño iterativo.

**Mejora iterativa**
Implemente procesos de mejora continua basados en los comentarios de los usuarios, las métricas de rendimiento y los requisitos empresariales. Las capacidades de [control de versiones](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md) y reversión permiten una experimentación segura y una iteración rápida.

## Introducción {#getting-started}

El enfoque que adopte depende de sus necesidades inmediatas y objetivos a largo plazo.

### Inicio rápido: Forms simple {#quick-start}

Elija su método de creación preferido en función de sus conocimientos técnicos y sus requisitos de rendimiento:

**Generación de formularios visuales:**

1. **[Crear formularios adaptables con componentes principales](/help/forms/creating-adaptive-form-core-components.md)** para formularios modernos y adaptables
2. **[Configurar acciones de envío](/help/forms/configure-submit-actions-core-components.md)** para administrar los datos del formulario
3. **[Incrustar formularios en AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)** o compartirlos mediante vínculos directos

**Creación basada en documentos:**

1. **[Generar formularios con Excel](/help/edge/docs/forms/create-forms.md)** con Edge Delivery Services para formularios de alto rendimiento
2. **[Publicar en Edge Delivery](/help/edge/docs/forms/publish-forms.md)** para obtener velocidades de carga y SEO óptimas

**Compatibilidad con formularios heredados:**

- **[HTML5 Forms](/help/forms/introductionhtml5.md)** para la representación de formularios XFA optimizados para dispositivos móviles

### Implementación avanzada: procesos empresariales {#advanced-implementation}

Para requisitos complejos que implican varios sistemas, generación de documentos y flujos de trabajo de aprobación:

**Integración de datos y flujos de trabajo:**

1. **[Configurar modelos de datos de formulario](/help/forms/create-form-data-models.md)** para conectar sistemas backend
2. **[Diseñar procesos de flujo de trabajo](/help/forms/aem-forms-workflow.md)** para su aprobación y enrutamiento
3. **[Configurar análisis](/help/forms/integrate-aem-forms-with-adobe-analytics.md)** para medir el rendimiento

**Servicios y comunicaciones de documentos:**

1. **[Implementar API de comunicación](/help/forms/aem-forms-cloud-service-communications-introduction.md)** para la generación automatizada de documentos
2. **[Crear comunicaciones interactivas](/help/forms/interactive-communication/create-interactive-communication.md)** para avisos e instrucciones personalizadas
3. **[Configurar el portal de Forms](/help/forms/configure-forms-portal.md)** para la administración centralizada de formularios

### Implementación empresarial: escala y administración {#enterprise-deployment}

Para implementaciones en toda la organización que requieran gobernanza, conformidad y supervisión:

**Arquitectura y administración:**

1. **[Revisar patrones de arquitectura](/help/forms/aem-forms-cloud-service-architecture.md)** para una implementación escalable
2. **[Configurar la administración de usuarios](/help/forms/forms-groups-privileges-tasks.md)** y los controles de acceso
3. **[Configurar flujos de trabajo de desarrollo](/help/forms/setup-local-development-environment.md)** para la colaboración en equipo

**Migración y supervisión:**

1. **[Planificar estrategias de migración](/help/forms/migrate-to-forms-as-a-cloud-service.md)** desde sistemas existentes
2. **[Implementar la supervisión de transacciones](/help/forms/transaction-reports-billable-apis.md)** para el seguimiento de uso y el cumplimiento normativo

<details>
<summary><strong>❓ preguntas más frecuentes</strong></summary>

**¿Qué es un generador de formularios?**
Un generador de formularios es una herramienta que le permite crear formularios digitales sin codificación. Puede diseñar formularios utilizando interfaces de arrastrar y soltar, agregar campos como cuadros de texto y listas desplegables, y publicarlos en línea para recopilar datos de los usuarios.

**¿Cómo se crea un formulario en línea?**
Con AEM Forms, puede crear formularios adaptables mediante componentes principales a través de un editor visual de arrastrar y soltar, crear formularios de alto rendimiento con Edge Delivery Services o utilizar componentes de base para flujos de trabajo establecidos. Para empezar, seleccione una plantilla, añada campos de formulario, configure conexiones de datos y publique en varios canales.

**¿Qué es un buen formulario en línea?**
Los buenos formularios en línea responden a las necesidades de los dispositivos móviles, se cargan rápidamente, tienen etiquetas claras, utilizan el orden lógico de los campos, incluyen validación para evitar errores y proporcionan comentarios inmediatos a los usuarios tras el envío.

**¿Puedo integrar formularios con otros sistemas empresariales?**
Sí, los creadores de formularios modernos ofrecen amplias funciones de integración. Puede conectar formularios a sistemas CRM, plataformas de marketing por correo electrónico, bases de datos, almacenamiento en la nube y herramientas de automatización de flujos de trabajo para optimizar los procesos empresariales.

**¿Los formularios en línea son seguros?**
Los creadores de formularios profesionales incluyen funciones de seguridad de nivel empresarial como cifrado de datos, transmisión de datos segura, controles de acceso y cumplimiento de regulaciones como RGPD, HIPAA y CCPA para proteger la información confidencial.

**¿Cómo puedo agregar firmas electrónicas a mis formularios?**
Las firmas digitales se pueden integrar directamente en formularios utilizando Adobe Sign u otros proveedores de firma electrónica. Esto permite a los usuarios firmar documentos dentro de la experiencia del formulario, eliminando la necesidad de flujos de trabajo de firma independientes y reduciendo el abandono del formulario.

**¿Pueden los formularios generar documentos de PDF automáticamente?**
Sí, las plataformas de formulario modernas pueden generar automáticamente confirmaciones, documentos de registro o confirmaciones de PDF cuando se envían los formularios. Esto es esencial para el cumplimiento, el mantenimiento de registros y la confirmación inmediata a los usuarios.

**¿Cómo realizo un seguimiento del rendimiento y el análisis del formulario?**
El análisis de formularios le ayuda a comprender las tasas de finalización, los patrones de abandono y el comportamiento del usuario. La integración con plataformas de análisis como Adobe Analytics proporciona perspectivas sobre los campos que causan fricción y la forma de optimizar las tasas de conversión.

**¿Qué es la automatización del flujo de trabajo del formulario?**
La automatización del flujo de trabajo de formularios enruta los envíos a través de procesos de aprobación, asigna tareas a los integrantes del equipo y déclencheur acciones en otros sistemas empresariales. Esto elimina el procesamiento manual y garantiza un manejo coherente de los datos del formulario.

**¿Cómo puedo hacer que los formularios sean accesibles para los usuarios con discapacidades?**
[Los formularios accesibles](/help/forms/creating-accessible-adaptive-forms.md) incluyen etiquetado adecuado, navegación mediante el teclado, compatibilidad con lectores de pantalla y cumplimiento con las directrices WCAG. Esto garantiza que todos los usuarios puedan completar formularios independientemente de sus capacidades o tecnologías de asistencia.

**¿Cuánto cuestan los creadores de formularios?**
Los precios de AEM Forms as a Cloud Service dependen de sus requisitos específicos, volumen de uso y necesidades de funciones. Para obtener información detallada sobre los precios y discutir una solución adaptada a su organización, póngase en contacto con el departamento de ventas de Adobe o con su representante de Adobe.

</details>

## Próximos pasos {#next-steps}

Explore las capacidades que coinciden con sus prioridades actuales:

- **[Cree su primer formulario](/help/forms/creating-adaptive-form-core-components.md)** para experimentar el entorno de creación
- **[Revisar opciones de arquitectura](/help/forms/aem-forms-cloud-service-architecture.md)** para la planificación de la implementación
- **[Configure su entorno de desarrollo](/help/forms/setup-local-development-environment.md)** para la colaboración en equipo
- **[Explorar opciones de integración](/help/forms/data-integration.md)** para conectar sistemas existentes

Para obtener instrucciones de implementación completas, piense en Adobe Professional Services para acelerar la implementación y garantizar las prácticas recomendadas desde el principio.
