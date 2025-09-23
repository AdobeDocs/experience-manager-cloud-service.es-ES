---
title: 'AEM Forms as a Cloud Service: Plataforma de formularios digitales'
description: Cree, integre y optimice formularios digitales con componentes modulares. Elija entre formularios adaptables, conectores de datos, automatización del flujo de trabajo, análisis y herramientas de administración para crear experiencias de formulario potentes.
landing-page-description: Plataforma de formulario digital modular con componentes independientes para la creación de formularios, la integración de datos, la automatización de procesos, el análisis y la gobernanza.
keywords: AEM Forms, formularios digitales, generador de formularios, formularios adaptables, integración de formularios, automatización del flujo de trabajo, análisis de formularios, servicios de documentos
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
index: false
source-git-commit: 51d9fed937ea5f12544ed476974d2812843fb457
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 1%

---


# AEM Forms as a Cloud Service {#aem-forms-platform}

Cree, integre y optimice formularios digitales con componentes modulares. AEM Forms proporciona productos independientes que trabajan juntos o por separado para crear experiencias de formulario potentes para cualquier necesidad empresarial.

Elija los componentes que necesita, desde la creación sencilla de formularios hasta los flujos de trabajo de documentos complejos, la integración de datos y el análisis avanzado.

## Novedades {#whats-new}

**Últimos elementos destacados de la versión:**

- **Componente de entrada de fecha y hora**: entrada de usuario mejorada con la interfaz de calendario y reloj
- **Seguridad mejorada de carga de archivos**: validación automática y comprobación de tipo de contenido
- **Gestión de errores mejorada**: Mejor depuración con códigos de error específicos para las acciones de envío personalizadas
- **Mejoras en el documento de registro**: opción para excluir los campos ocultos para la generación de documentos más limpios

**Características previas al lanzamiento:**

- **Compatibilidad con formato AFP**: funciones de impresión de nivel empresarial con API de comunicación
- **Mejoras en el editor de reglas**: compatibilidad con JavaScript moderno y variables dinámicas
- **Métodos de validación mejorados**: mejoras en la validación a nivel de formulario, campo y panel

[Ver → notas de la versión completas](/help/release-notes/release-notes-cloud/release-notes-current.md#forms)

## Programa de acceso anticipado {#early-access}

Obtenga acceso exclusivo a las innovaciones más avanzadas de AEM Forms:

- **🤖AEM Forms AI Assistant**: IA generativa para la creación y optimización automatizadas de formularios
- **✍️componente de firma manuscrita** - Captura de firma directa dentro de los formularios
- **🔗integración de API directa**: conéctese a las API sin configurar el modelo de datos de formulario
- **📊Optimización de Forms**: análisis de rendimiento con tecnología de IA y mejoras de conversión

[Solicitar acceso →](mailto:aem-forms-ea@adobe.com) | [Más información →](/help/forms/early-access-ea-features.md)

## 📋 Creación y creación de formularios {#form-creation}

Cree formularios utilizando el método de creación que mejor se adapte a sus necesidades y requisitos técnicos.

### Forms de componentes principales {#core-components}

| **Forms de componente principal** |
|---|
| Creación de formularios moderna y adaptable con los últimos estándares web. Cree formularios adaptables que funcionen automáticamente en todos los dispositivos y produzcan formularios sin encabezado para una entrega basada en API. |
| **Lo que hace:** Generador de formularios de arrastrar y soltar visual con componentes modernos, diseño interactivo automático y características de accesibilidad integradas. |
| **Cuándo se deben usar:** Proyectos nuevos, experiencias web modernas, entrega de formularios sin encabezado, diseño con prioridad móvil. |
| ✅ Diseño interactivo ✅ Cumplimiento de accesibilidad ✅ Funciones sin encabezado ✅ Componentes modernos de la interfaz de usuario |
| [Introducción a los componentes principales →](/help/forms/creating-adaptive-form-core-components.md) |

### Forms de componentes de base {#foundation-components}

| **Forms de componente de base** |
|---|
| Método de creación de formularios establecido para proyectos existentes e integraciones heredadas. Componentes probados con amplias opciones de personalización. |
| **Lo que hace:** Creación tradicional de formularios adaptables con una biblioteca de componentes completa y amplias capacidades de personalización. |
| **Cuándo usar:** proyectos existentes, integración de sistemas heredados, requisitos de personalización específicos, flujos de trabajo establecidos. |
| ✅ Biblioteca de componentes extensa ✅ Personalización profunda ✅ Compatibilidad heredada ✅ Estabilidad comprobada |
| [Introducción a los componentes de base →](/help/forms/creating-adaptive-form.md) |

### Edge Delivery Forms {#edge-delivery}

| **Edge Delivery Forms** |
|---|
| Creación de formularios de alto rendimiento con herramientas conocidas como Microsoft Excel. Alcanza velocidades de carga excepcionales y rendimiento SEO. |
| **Lo que hace:** Cree formularios utilizando hojas de cálculo de Excel y publique en una red de entrega perimetral de alto rendimiento con puntuaciones óptimas de Google Lighthouse. |
| **Cuándo usar:** aplicaciones críticas para el rendimiento, proyectos centrados en SEO, creación de formularios basada en el autor de contenido y entrega de contenido global. |
| ⚡ Creación basada en Excel ⚡ Carga ultrarrápida de ⚡ SEO óptimo ⚡ Entrega de CDN global |
| [Introducción a Edge Delivery →](/help/edge/docs/forms/overview.md) |

### Formularios HTML5 {#html5-forms}

| **Formularios HTML5** |
|---|
| Procesar formularios basados en XFA como HTML5 para dispositivos móviles y exploradores heredados. Mantenga la lógica del formulario mientras proporciona una experiencia móvil nativa. |
| **Lo que hace:** Convertir plantillas de formulario XFA a formularios HTML5 con experiencia móvil nativa y compatibilidad entre exploradores. |
| **Cuándo usar:** modernización de formularios XFA, optimización móvil, compatibilidad con exploradores heredados, inversiones en XDP existentes. |
| 📱 Compatibilidad de XFA 📱 Optimización móvil 📱 Compatibilidad entre exploradores 📱 Sin requisitos de complemento |
| [Introducción a HTML5 Forms →](/help/forms/introductionhtml5.md) |

### Comunicaciones interactivas {#interactive-communications}

| **Comunicaciones interactivas** |
|---|
| Cree comunicaciones centradas en el documento como extractos, facturas y avisos mediante un editor visual con integración dinámica de datos. |
| **Lo que hace:** Diseñe comunicaciones personalizadas que combinen contenido estático con datos dinámicos para canales impresos y digitales. |
| **Cuándo usar:** extractos de clientes, facturas, avisos, comunicaciones personalizadas y flujos de trabajo con gran cantidad de documentos. |
| 📄 Diseño de documento visual 📄 Integración dinámica de datos 📄 Salida multicanal 📄 Personalization |
| [Introducción a las comunicaciones interactivas →](/help/forms/introduction-to-interactive-communication.md) |

## Integración y datos de 🔗 {#data-integration}

Conecte los formularios a sistemas back-end y fuentes de datos para un flujo de información fluido y un intercambio de datos en tiempo real.

### Modelo de datos de formulario {#form-data-model}

| **Modelo de datos de formulario** |
|---|
| Interfaz unificada para varias fuentes de datos con capacidades de rellenado previo, validación y envío. Complejidad de la integración abstracta tras un modelo coherente. |
| **Lo que hace:** Cree una capa de datos unificada que conecte formularios a varios sistemas back-end con una interfaz y una administración de flujo de datos coherentes. |
| **Cuándo se debe usar:** Integración de varias fuentes de datos, relaciones de datos complejas, requisitos previos a la población, validación con datos activos. |
| 🔄 Integración de varios orígenes 🔄 Modelado de datos 🔄 Precapado 🔄 Reglas de validación 🔄 Interfaz unificada |
| [Introducción al modelo de datos de formulario →](/help/forms/create-form-data-models.md) |

### Conectores RESTful {#restful-connectors}

| **Conectores RESTful** |
|---|
| Integración directa con cualquier servicio accesible desde la web a través de las API de RESTful. Conéctese a API y servicios web personalizados. |
| **Lo que hace:** Habilite las llamadas API directas desde formularios mediante acciones de envío o la integración de datos para la conectividad en tiempo real con los servicios web. |
| **Cuándo se debe usar:** Integración de API personalizada, conectividad de servicio web, intercambio de datos en tiempo real, integración de servicio de terceros. |
| 🌐 llamadas API directas 🌐 Conectividad en tiempo real 🌐 Integración flexible 🌐 Soporte de servicio personalizado |
| [Configurar puntos finales REST →](/help/forms/configure-submit-action-restpoint.md) \| [Configuración de integración de datos →](/help/forms/data-integration.md) |

### Conector de Salesforce {#salesforce-connector}

| **Conector de Salesforce** |
|---|
| Integración nativa con Salesforce CRM para la administración de posibles clientes, la sincronización de datos de clientes y la automatización de los procesos de ventas. |
| **Lo que hace:** Conector generado previamente para Salesforce con sincronización de datos de formulario, creación de posibles clientes y administración de registros de clientes. |
| **Cuándo se debe usar:** Integración de Salesforce CRM, formularios de generación de clientes potenciales, administración de datos de clientes, automatización de procesos de ventas. |
| 🏢 Conector generado previamente 🏢 Administración de clientes potenciales 🏢 Sincronización de datos 🏢 Automatización de ventas |
| [Configurar la integración de Salesforce →](/help/forms/configure-salesforce.md) |

### Conector de Microsoft Dynamics {#dynamics-connector}

| **Conector de Microsoft Dynamics** |
|---|
| Integración empresarial con Microsoft Dynamics para la conectividad de ERP y CRM con compatibilidad completa con los procesos empresariales. |
| **Lo que hace:** Conectar formularios a Microsoft Dynamics para la administración de clientes, la integración de procesos empresariales y el flujo de datos empresariales. |
| **Cuándo se debe usar:** Integración de Microsoft Dynamics, flujos de trabajo empresariales, administración de clientes, automatización de procesos empresariales. |
| 🏭 Conectividad empresarial 🏭 Integración de procesos empresariales 🏭 Administración de clientes 🏭 Sincronización de datos |
| [Configurar integración de Dynamics →](/help/forms/configure-msdynamics.md) |

### Conector de SharePoint {#sharepoint-connector}

| **Conector de SharePoint** |
|---|
| Integración de la administración de documentos con SharePoint para el almacenamiento de archivos, la colaboración y la automatización del flujo de trabajo de documentos. |
| **Qué hace:** Almacena envíos de formularios y documentos generados en SharePoint con funciones automatizadas de colaboración y administración de documentos. |
| **Cuándo se debe usar:** Administración de documentos, colaboración en equipo, almacenamiento de archivos, flujos de trabajo basados en SharePoint. |
| 📁 Almacenamiento de documentos 📁 Funciones de Collaboration 📁 Flujos de trabajo automatizados 📁 Integración de SharePoint |
| [Configurar la integración de SharePoint →](/help/forms/connect-forms-to-sharepoint-document-library.md) |

## Proceso y flujo de trabajo {#process-workflow}

Automatice los procesos empresariales, las aprobaciones y la generación de documentos con funciones completas de flujo de trabajo y procesamiento.

### Flujos de trabajo de AEM {#aem-workflows}

Automatización de procesos empresariales con aprobaciones de varios pasos, asignaciones de tareas y orquestación de procesos para flujos de trabajo complejos impulsados por formularios.

**Lo que hace:** Cree procesos empresariales automatizados con cadenas de aprobación, enrutamiento de tareas y supervisión de procesos para los envíos de formularios.

**Cuándo usar:** procesos de aprobación, automatización empresarial, administración de tareas, flujos de trabajo complejos, orquestación de procesos.

**Características principales:** Automatización de procesos, cadenas de aprobación, enrutamiento de tareas, supervisión de procesos, reglas empresariales.

[Introducción a AEM Workflows →](/help/forms/aem-forms-workflow.md)

### Integración con Adobe Sign {#adobe-sign}

Flujos de trabajo de firma electrónica con firmas digitales jurídicamente vinculantes integradas directamente en experiencias de formulario para procesos de firma fluidos.

**Lo que hace:** Habilitar firmas digitales en formularios con capacidades de firma electrónica legalmente vinculantes y flujos de trabajo de firma automatizada.

**Cuándo se debe usar:** Firma de contrato, documentos legales, flujos de trabajo de aprobación, requisitos de cumplimiento, automatización de firma.

**Características principales:** firmas electrónicas legales, flujos de trabajo de firmas, compatibilidad con el cumplimiento, procesos automatizados.

[Configuración de Adobe Sign →](/help/forms/working-with-adobe-sign.md)

### Acciones de envío {#submit-actions}

Administración del envío de formularios con varias opciones de procesamiento, incluidos correo electrónico, almacenamiento de bases de datos, déclencheur de flujo de trabajo y procesamiento personalizado.

**Lo que hace:** Defina lo que sucede cuando los usuarios envían formularios: enrute los datos a correo electrónico, bases de datos, flujos de trabajo o sistemas externos.

**Cuándo se debe usar:** Procesamiento de envío de formularios, enrutamiento de datos, sistemas de notificación y déclencheur de integración.

**Características principales:** Varias opciones de envío, enrutamiento de datos, sistemas de notificación y déclencheur de integración.

[Configuración de acciones de envío →](/help/forms/configure-submit-actions-core-components.md)

### API de comunicación {#communication-apis}

Generación, manipulación y seguridad de documentos mediante programación con API RESTful para la automatización y el procesamiento de documentos de gran volumen.

**Lo que hace:** Generar, manipular y proteger documentos mediante programación con API para la creación de PDF, el ensamblado de documentos y el procesamiento por lotes.

**Cuándo se debe usar:** Automatización de documentos, procesamiento de gran volumen, generación mediante programación, ensamblado de documentos, operaciones por lotes.

**Características principales:** Generación de documentos, procesamiento por lotes, control programático, seguridad de documentos, automatización de API.

[Introducción a las API de comunicación →](/help/forms/aem-forms-cloud-service-communications-introduction.md)

## Analytics y optimización {#analytics-optimization}

Monitorice el rendimiento del formulario, comprenda el comportamiento del usuario y optimice las tasas de conversión con capacidades completas de análisis y prueba.

### Integración de Adobe Analytics {#adobe-analytics}

Realizar un seguimiento del rendimiento del formulario con análisis detallados de las tasas de finalización, los patrones de abandono y el comportamiento del usuario para la optimización basada en datos.

**Qué hace:** Rastree las interacciones de formularios, las tasas de finalización, los análisis de nivel de campo y los patrones de comportamiento del usuario con sistemas de informes completos.

**Cuándo se debe usar:** Supervisión del rendimiento, optimización de la conversión, análisis del comportamiento del usuario y mejoras basadas en datos.

**Características principales:** Seguimiento del rendimiento, análisis del comportamiento del usuario, métricas de conversión e informes detallados.

[Configuración del → de integración de Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

### Informes de transacciones {#transaction-reports}

Monitorización del uso y transparencia de la facturación con informes detallados sobre las llamadas a la API, la generación de documentos y las transacciones facturables en toda la implementación.

**Lo que hace:** Supervisar el uso de la API, los volúmenes de generación de documentos y las transacciones facturables con informes de consumo detallados y seguimiento de costos.

**Cuándo se debe usar:** Supervisión del uso, seguimiento de costos, planificación de la capacidad, informes de cumplimiento normativo, optimización de recursos.

**Características principales:** Seguimiento del uso, supervisión de costos, planificación de la capacidad, informes de conformidad.

[Ver informes de transacciones →](/help/forms/transaction-reports-billable-apis.md)

### Integración de pruebas A/B {#ab-testing}

Optimización de formularios mediante la prueba de diferentes diseños, disposiciones de campos y flujos de usuarios con análisis estadístico para la mejora de la conversión.

**Lo que hace:** Pruebe diferentes variaciones de formularios para identificar los enfoques más efectivos para diferentes segmentos de usuarios y casos de uso.

**Cuándo se debe usar:** Optimización de la conversión, pruebas de la experiencia del usuario, mejora del rendimiento, decisiones de diseño basadas en datos.

**Características principales:** Pruebas de formularios, análisis estadístico, optimización de conversión y comparación de rendimiento.

[Obtenga información sobre los → de optimización de formularios](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Administración y administración {#management-governance}

Administración centralizada de formularios, control de acceso de usuarios y funciones de gobernanza para implementaciones de formularios a escala empresarial.

### Portal de Forms {#forms-portal}

Repositorio de formularios centralizado con capacidades de búsqueda, categorización de formularios, administración de borradores y seguimiento de envíos en una interfaz unificada.

**Lo que hace:** Cree repositorios de formularios centralizados en los que los usuarios puedan detectar, acceder, administrar borradores y realizar un seguimiento de los envíos mediante búsquedas y clasificaciones.

**Cuándo usar:** La detección de formularios, la administración centralizada, el autoservicio de usuarios, la administración de borradores y el seguimiento de envíos.

**Características principales:** Detección de formularios, funciones de búsqueda, administración de borradores, seguimiento de envíos, interfaz de usuario.

[Configuración del → del portal de Forms](/help/forms/configure-forms-portal.md)

### Administración de usuarios {#user-management}

Control de acceso basado en funciones con permisos granulares para la creación, edición, publicación y administración de formularios en toda la organización.

**Lo que hace:** Defina funciones de usuario y permisos para diferentes aspectos de la administración de formularios con control de acceso granular y seguridad.

**Cuándo se debe usar:** Control de acceso, administración de seguridad, definición de rol, administración de permisos, administración de la organización.

**Características principales:** Acceso basado en roles, administración de permisos, control de seguridad, administración de la organización.

[Configurar → de administración de usuarios](/help/forms/forms-groups-privileges-tasks.md)

### Control de versión {#version-control}

Administración del ciclo vital de los formularios con seguimiento de versiones, historial de cambios, funciones de reversión y pistas de auditoría para el cumplimiento y la gobernanza.

**Lo que hace:** Realizar un seguimiento de las versiones de los formularios, mantener el historial de cambios, habilitar reversiones y proporcionar seguimientos de auditoría para los requisitos de cumplimiento y control.

**Cuándo se debe usar:** Administración de cambios, requisitos de cumplimiento, pistas de auditoría, seguimiento de versiones, procesos de control.

**Características principales:** Seguimiento de versiones, historial de cambios, funciones de reversión, pistas de auditoría y compatibilidad.

[Más información sobre las versiones →](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## Introducción por producto {#getting-started}

Elija su punto de partida en función de sus necesidades inmediatas y requisitos técnicos.

### Inicio rápido de creación de formularios {#form-creation-start}

**Para proyectos modernos:** Empiece con [Forms de componentes principales](/help/forms/creating-adaptive-form-core-components.md)

**Para obtener un alto rendimiento:** Comience con [Edge Delivery Forms](/help/edge/docs/forms/overview.md)

**Para proyectos existentes:** Comience con [Forms de componente de base](/help/forms/creating-adaptive-form.md)

**Para la modernización XFA:** Empiece con [HTML5 Forms](/help/forms/introductionhtml5.md)

**Para comunicaciones de documentos:** Comience con [comunicaciones interactivas](/help/forms/introduction-to-interactive-communication.md)

### Inicio rápido de integración de datos {#integration-start}

**Para varios orígenes de datos:** Comience con [Modelo de datos de formulario](/help/forms/create-form-data-models.md)

**Para Salesforce CRM:** Comience con [Conector de Salesforce](/help/forms/configure-salesforce.md)

**Para Microsoft Dynamics:** Comience con [Conector de Dynamics](/help/forms/configure-msdynamics.md)

**Para las API personalizadas:** Comience con [Conectores RESTful](/help/forms/configure-submit-action-restpoint.md)

**Para el almacenamiento de documentos:** Comience con [Conector de SharePoint](/help/forms/connect-forms-to-sharepoint-document-library.md)

### Inicio rápido de automatización de procesos {#workflow-start}

**Para procesos de aprobación:** Comience con [Flujos de trabajo de AEM](/help/forms/aem-forms-workflow.md)

**Para firmas electrónicas:** Comience con [Integración de Adobe Sign](/help/forms/working-with-adobe-sign.md)

**Para administrar el envío:** Comience con [Acciones de envío](/help/forms/configure-submit-actions-core-components.md)

**Para la generación de documentos:** Comience con [API de comunicación](/help/forms/aem-forms-cloud-service-communications-introduction.md)

### Inicio rápido de Analytics {#analytics-start}

**Para el seguimiento del rendimiento:** Comience con [Integración de Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)

**Para la supervisión de uso:** Comience con [Informes de transacciones](/help/forms/transaction-reports-billable-apis.md)

**Para obtener información de optimización:** Comience con [Informes de Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

### Inicio rápido de administración {#management-start}

**Para la detección de formularios:** Comience con [Portal de Forms](/help/forms/configure-forms-portal.md)

**Para el control de acceso:** Comience con [Administración de usuarios](/help/forms/forms-groups-privileges-tasks.md)

**Para el seguimiento de cambios:** Comience con [Control de versiones](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)

## Arquitectura e implementación {#architecture}

Para obtener instrucciones de implementación completas:

- **[Revisar patrones de arquitectura](/help/forms/aem-forms-cloud-service-architecture.md)** para una implementación escalable
- **[Configurar el entorno de desarrollo](/help/forms/setup-local-development-environment.md)** para la colaboración en equipo
- **[Planificar estrategias de migración](/help/forms/migrate-to-forms-as-a-cloud-service.md)** desde sistemas existentes

## Asistencia y recursos {#support}

- **Centro de ayuda**: obtenga asistencia para la implementación y solución de problemas
- **Foros de la comunidad**: conéctese con otros usuarios y expertos de AEM Forms
- **Servicios profesionales**: asesoría de Adobe para implementaciones empresariales
- **Formación y certificación**: desarrolle su experiencia en las funciones de AEM Forms

*Elija los componentes que necesita para crear experiencias de formulario eficaces. Cada producto funciona de forma independiente o se combina con otros para crear soluciones completas para sus necesidades empresariales.*
