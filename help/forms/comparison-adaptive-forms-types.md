---
title: Componentes principales de Forms adaptable frente a Edge Delivery Services Forms frente a componentes básicos
description: 'Comparación técnica de los enfoques de creación de AEM Forms: componentes principales, Edge Delivery Services Forms y componentes de base. Arquitectura, renderización, funciones y casos de uso.'
keywords: comparación de formularios adaptables, componentes principales, componentes de base, formularios de servicios de envío de Edge, comparación de formularios AEM, comparación de Forms Builder
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 9%

---


# Adaptive Forms: componentes principales frente a Edge Delivery Services Forms frente a componentes básicos

Adobe Experience Manager (AEM) Forms proporciona tres enfoques distintos para crear experiencias de captura de datos: Forms adaptable basado en componentes principales, Edge Delivery Services Forms y Forms adaptable basado en componentes de base. Cada enfoque tiene una arquitectura, un modelo de renderización y un caso de uso de destinatario diferentes. Este artículo proporciona una comparación técnica para ayudar a los arquitectos de soluciones, desarrolladores y clientes de AEM a seleccionar el enfoque adecuado para sus requisitos.

## Información general

Los tres tipos de formulario tienen el propósito de capturar los datos del usuario e integrarlos con sistemas back-end. Sin embargo, difieren en su arquitectura subyacente, dónde se procesan los formularios, cómo se entregan y qué capacidades admiten.

| Enfoque | Estado | Caso de uso principal |
|----------|--------|------------------|
| **Componentes principales** | Recomendado para formularios nuevos | Formularios modernos y escalables que requieren la creación de AEM con opciones de publicación flexibles |
| **Edge Delivery Services Forms** | Recomendado para sitios críticos para el rendimiento | Formularios de alto rendimiento entregados desde el perímetro con implementación rápida |
| **Componentes de base** | Modo de mantenimiento | Formularios existentes que requieren compatibilidad con funciones heredadas |

## Forms adaptable basado en componentes principales

### Definición

Los componentes principales de Forms adaptables son un conjunto de 30 componentes de código abierto compatibles con BEM creados sobre la base de los componentes principales de WCM de Adobe Experience Manager. Representan el enfoque recomendado por Adobe para crear un nuevo Forms adaptable, proporcionando una arquitectura moderna, un rendimiento mejorado y una generación automática de formularios sin encabezado.

### Arquitectura

Los componentes principales utilizan una arquitectura de componentes modular y estandarizada:

- **Base de componentes**: creada en los componentes principales de WCM de AEM
- **Metodología de estilo**: Convenciones CSS de BEM (modificador de elemento de bloque)
- **Almacenamiento de contenido**: Repositorio JCR con nodos de contenido estructurado
- **Procesamiento**: Procesamiento del lado del servidor en AEM con procesamiento opcional sin encabezado del lado del cliente
- **Source**: de código abierto (disponible en [GitHub](https://github.com/adobe/aem-core-forms-components))

### Modelo de procesamiento

Los componentes principales admiten varios modelos de renderización:

1. **Procesamiento del lado del servidor (SSR)**: Forms procesa en el servidor de AEM y envía HTML completo al explorador
2. **Procesamiento sin encabezado**: Forms expone las representaciones JSON a través de API para el procesamiento del lado del cliente en React, Angular u otros módulos
3. **Procesamiento híbrido**: combinación de procesamiento de cliente y servidor para un rendimiento óptimo

### Opciones de publicación

- Instancias de publicación de AEM
- Edge Delivery Services (cuando está configurado)
- API sin encabezado para aplicaciones de front-end personalizadas

### Funciones principales

| Categoría | Capacidades |
|----------|-------------|
| **Componentes** | 30 componentes estandarizados, incluidos Cuadro de texto, Cuadro numérico, Selector de fecha, Lista desplegable, Grupo de casillas de verificación, Botón de opción, Archivo adjunto, Asistente, Acordeón, Pestañas horizontales/verticales |
| **Modelos de formulario** | Esquema JSON (v4 y 2020-12), modelo de datos de formulario (FDM), plantillas XDP/XFA (limitadas) |
| **Motor de reglas** | Editor de reglas visual con lógica condicional, validación, invocación de servicio, funciones personalizadas |
| **Acciones de envío** | Extremo REST, Correo electrónico, Flujo de trabajo de AEM, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion, Modelo de datos de formulario |
| **Relleno previo** | Servicio de prerrellenado del modelo de datos de formulario, servicios de prerrellenado personalizados |
| **CAPTCHA** | reCAPTCHA, hCaptcha, Torniquete |
| **Documento de registro** | Generación de PDF con plantillas personalizadas o OOTB |
| **Accesibilidad** | Compatible con WCAG, etiquetas ARIA, navegación mediante el teclado, compatibilidad con lectores de pantalla |
| **Localización** | Compatibilidad multilingüe mediante el flujo de trabajo de traducción de AEM |
| **Creación de versiones** | Versiones de contenido heredadas de AEM Sites |

### Requisitos previos

- **AEM Forms as a Cloud Service**: los componentes principales están habilitados de manera predeterminada
- **AEM 6.5 Forms**: Requiere la habilitación mediante el tipo de archivo de AEM
- **Permisos de usuario**: el usuario debe estar en el grupo `forms-users`
- **Plantilla**: se requiere la plantilla de formulario adaptable (componente principal)
- **Tema**: Tema de lienzo (OOTB) o tema personalizado

### Limitaciones

- **Restricciones de esquema JSON**: tipo nulo, tipos de unión (cualquiera), construcciones OneOf/AnyOf/AllOf/NOT no compatibles
- **Lagunas de componentes**: bloque de Adobe Sign, firma manuscrita, gráfico, opción de imagen no disponible (disponible en componentes de base)
- **Funciones personalizadas**: no se admiten funciones de generador, asincrónicas/de espera, métodos de clase
- **Firmas digitales**: no disponible de forma nativa (a diferencia de los componentes de base)

### Cuándo usarlas

**Recomendado para:**

- Nuevos proyectos de desarrollo de formularios
- Organizaciones que requieren una arquitectura moderna y sostenible
- Proyectos que requieren una publicación flexible (AEM + Edge Delivery + Sin encabezado)
- Aplicaciones de front-end personalizadas (React, Angular) mediante API sin encabezado
- Proyectos que priorizan el rendimiento y la accesibilidad
- Requisitos de entrega omnicanal (web, móvil, quioscos)

**No recomendado para:**

- Forms que requiere integración con Adobe Sign (utilizar componentes de base)
- Formularios simples en los que el rendimiento de Edge Delivery Services es crítico
- Formularios basados en componentes de base existentes (se mantienen en Foundation a menos que se migre)

## Formularios de Edge Delivery Services

### Definición

Edge Delivery Services (EDS) Forms es un conjunto de servicios componibles para crear y entregar formularios a través de Adobe Experience Manager Edge Delivery Services. Permiten un desarrollo rápido de formularios con un rendimiento excepcional a través de una entrega basada en Edge, un procesamiento del lado del cliente y varios métodos de creación.

### Arquitectura

EDS Forms utiliza una arquitectura desacoplada y con un diseño Edge-First:

- **Fuentes de contenido**: Microsoft SharePoint, Google Drive (basado en documentos) o Universal Editor (WYSIWYG)
- **Repositorio de código**: GitHub
- **Entrega de contenido**: CDN de Edge Delivery Services
- **Procesamiento**: Procesamiento del lado del cliente mediante JavaScript de vainilla
- **Bloque de formularios**: el bloque de Forms adaptable procesa las definiciones de formularios y genera HTML

### Modelo de procesamiento

EDS Forms utiliza exclusivamente el procesamiento en el lado del cliente:

1. La definición del formulario almacenada como JSON (convertida desde una hoja de cálculo o creada en el Editor universal)
2. JSON obtenido del perímetro: `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. Procesos JSON de JavaScript de bloque de Forms adaptable
4. Estructura de HTML generada dinámicamente en el explorador
5. CSS aplicado para el estilo

**Patrón de estructura de HTML:**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### Métodos de creación

EDS Forms admite dos métodos de creación:

#### Editor universal (WYSIWYG)

- Interfaz visual de arrastrar y soltar
- Previsualización en tiempo real con simulación de dispositivo
- Editor de reglas avanzado para lógica condicional
- Integración del modelo de datos de formulario (FDM)
- Integración de flujos de trabajo de AEM
- Compatibilidad con componentes personalizados
- Creación basada en plantillas

#### Creación basada en documentos

- Creación de hojas de Microsoft Excel o Google
- Definición de formulario basado en hoja de cálculo
- Publicación instantánea (los cambios se reflejan inmediatamente)
- Adecuado para formularios de complejidad simples a moderados

### Opciones de envío

**Servicio de envío de Forms (FSS):**

- Enviar a hojas de Google
- Enviar a Microsoft Excel (OneDrive/SharePoint)
- Notificaciones por correo electrónico

**Acciones de envío de publicación de AEM:**

- Extremo REST
- servicios de correo de AEM
- Modelo de datos de formulario
- Flujo de trabajo AEM
- SharePoint/OneDrive
- Azure Blob Storage
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### Funciones principales

| Categoría | Capacidades |
|----------|-------------|
| **Componentes** | Todos los tipos de entrada de HTML5, Grupos de casillas de verificación, Grupos de radio, Lista desplegable, Paneles, Secciones repetibles, Archivo adjunto, Acordeón, Asistente, Modal |
| **Validación** | Validación de nivel de campo (obligatorio, mínimo/máximo, motivo), mensajes de validación personalizados |
| **Reglas** | Visibilidad condicional, expresiones de valor, reglas impulsadas por evento |
| **Integraciones** | Adobe Sign, Salesforce, Microsoft Dynamics, pruebas A/B |
| **Seguridad** | reCAPTCHA Enterprise, Captcha, configuración CORS |
| **Análisis** | Adobe Experience Platform Web SDK, vistas de formulario y seguimiento de envío |

### Requisitos previos

**Para la creación basada en documentos:**

- Cuenta de GitHub
- Cuenta de Google Drive o Microsoft SharePoint
- Nodo/npm para desarrollo local
- Proyecto de AEM con bloque de Forms adaptable configurado
- Compartir carpeta con `forms@adobe.com` (editar permisos)

**Para el editor universal:**

- Instancia de AEM Forms as a Cloud Service
- Proyecto de Edge Delivery Services configurado
- Permisos necesarios para los destinos

**Para el envío de publicación de AEM:**

- URL de instancia de AEM Cloud Service configurada
- Configuración del filtro de referente OSGi
- Configuración de CORS para dominios de sitio de Edge Delivery

### Limitaciones

**Creación basada en documentos:**

- Nomenclatura de hoja restringida a `helix-default` y `shared-aem`
- Más adecuado para formularios de baja complejidad
- Funcionalidades de reglas limitadas
- Sin flujos de trabajo de AEM (sin envío de publicación de AEM)
- Sin integración con el modelo de datos de formulario

**Editor universal:**

- Importaciones estáticas/dinámicas no admitidas en funciones personalizadas
- Los fragmentos de formulario solo se pueden editar de forma independiente
- Funcionalidad de incrustación de formularios en desarrollo

**Información general:**

- `shared-aem` hojas no deben contener PII (accesible públicamente)
- Requiere la configuración de CORS para envíos de origen cruzado
- El filtro de referente OSGi es necesario para los envíos de publicación de AEM

### Cuándo usarlas

**Recomendado para:**

- Sitios web críticos para el rendimiento que requieren puntuaciones altas en Lighthouse
- Sitios que ya utilizan Edge Delivery Services
- Desarrollo e implementación rápidos de formularios
- Captura de datos de complejidad simple a moderada
- Equipos que prefieren la creación basada en hojas de cálculo (basada en documentos)
- Proyectos que requieren un tiempo de comercialización rápido

**No recomendado para:**

- Forms que requiere un procesamiento exhaustivo del lado del servidor
- Integración profunda con sistemas heredados sin API de REST
- Requisitos de formulario sin conexión
- Organizaciones que requieren marcos de JavaScript específicos (React, Angular) con control total

## Forms adaptable basado en componentes de base

### Definición

Los componentes de base representan el enfoque clásico de creación de AEM Forms. Son los componentes originales de Adaptive Forms que han estado disponibles en AEM Forms durante muchos años. Aunque sigue siendo compatible, Adobe recomienda los componentes de base principalmente para mantener los formularios existentes en lugar de crear nuevos.

### Arquitectura

Los componentes de base utilizan la arquitectura tradicional de AEM:

- **Modelo de contenido**: componente WCM `cq:Page` con estructura de contenido JCR
- **Estructura raíz**: `guideContainer` (raíz) → `rootPanel` → `items` (campos de formulario)
- **Procesamiento**: Procesamiento del lado del servidor con JavaScript del lado del cliente
- **Expresiones SOM**: modelo de objetos de scripts para hacer referencia a objetos de formulario

### Modelo de procesamiento

Los componentes de base utilizan el procesamiento del lado del servidor:

1. Contenido de formulario almacenado en el repositorio JCR
2. El servidor de AEM procesa la estructura del formulario
3. HTML completo procesado y enviado al explorador
4. JavaScript del lado del cliente gestiona la interactividad y la validación

### Funciones principales

| Categoría | Capacidades |
|----------|-------------|
| **Componentes** | Más de 40 componentes, incluidos todos los equivalentes de componentes principales, además de: bloque de Adobe Sign, gráfico, firma manuscrita, opción de imagen, paso de resumen, lista de archivos adjuntos |
| **Modelos de formulario** | Modelo de datos de formulario (FDM), plantillas XDP/XFA, esquema XML (XSD), esquema JSON |
| **Motor de reglas** | Editor visual + editor de código (para el grupo de usuarios avanzados de formularios) |
| **Firmas digitales** | Integración de Adobe Sign, firma manuscrita |
| **Acciones de envío** | Varias acciones OOTB similares a los componentes principales |

### Componentes exclusivos de base

Los siguientes componentes solo están **disponibles** en los componentes de base:

- Bloque de Adobe Sign
- Gráfico
- Lista de archivos adjuntos
- Marcador de nota al pie
- Opción de imagen
- Firma manuscrita
- Paso de resumen
- Turnstile Captcha

### Requisitos previos

- AEM Forms as a Cloud Service o AEM 6.5 Forms
- Plantilla de formulario adaptable (base)
- Usuario en el grupo `forms-users`

### Limitaciones

- **Publicación**: Solo AEM (sin API de Edge Delivery Services o sin encabezado)
- **Rendimiento**: Rendimiento estándar (no optimizado para puntuaciones de Lighthouse)
- **Arquitectura**: arquitectura heredada sin compatibilidad con BEM
- **Abrir Source**: no es de código abierto
- **Desarrollo futuro**: modo de mantenimiento; las nuevas características se agregaron principalmente a los componentes principales

### Cuándo usarlas

**Recomendado para:**

- Mantener formularios existentes basados en Foundation
- Forms que requiere la integración de Adobe Sign o Firma manuscrita
- Flujos de trabajo dependientes de funciones de base establecidas
- Proyectos con requisitos de publicación solo para AEM
- Forms que requiere componentes exclusivos de base (gráfico, opción de imagen)

**No recomendado para:**

- Desarrollo de nuevos formularios (utilice componentes principales)
- Proyectos que requieren la publicación en Edge Delivery Services
- API de formulario sin encabezado
- Implementaciones críticas para el rendimiento
- Proyectos que priorizan la arquitectura preparada para el futuro

## Tabla de comparación

| Parámetro | Componentes principales | Formularios de Edge Delivery Services | Componentes de base |
|-----------|-----------------|-----------------------------|-----------------------|
| **Estado** | Recomendado para formularios nuevos | Recomendado para sitios de alto rendimiento | Modo de mantenimiento |
| **Arquitectura** | Modular, compatible con BEM | Primero Edge, disociado | WCM tradicional |
| **Procesando** | Lado del servidor + sin encabezado | Solo del lado del cliente | Del lado del servidor |
| **Publicación** | AEM + Edge Delivery + API sin encabezado | Edge Delivery Services solo | Solo AEM |
| **Creación** | Editor de AEM Forms | Editor universal para hojas de cálculo | Editor de AEM Forms |
| **Rendimiento** | Bueno (mejorado con respecto a Base) | Excelente (puntuaciones altas de Lighthouse) | Estándar |
| **Recuento de componentes** | 30 | Más de 20 (todos los tipos de entrada de HTML5) | 40+ |
| **Abrir Source** | Sí (GitHub) | Sí | No |
| **Modelo de datos de formulario** | ✅ | ✅ (solo editor universal) | ✅ |
| **Esquema JSON** | ✅ | Limitado | ✅ |
| **Compatibilidad con XDP/XFA** | Limitado | ❌ | ✅ |
| **Esquema XML** | ❌ | ❌ | ✅ |
| **Motor de reglas** | Editor visual avanzado | Avanzado (editor universal) / Limitado (basado en documentos) | Visual avanzada + editor de código |
| **Firmas digitales** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | Mediante integración | ✅ (bloque nativo) |
| **Documento de registro** | ✅ | ✅ | ✅ |
| **Opciones de CAPTCHA** | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise, Chcaptcha | reCAPTCHA, hCaptcha, Torniquete |
| **Flujo de trabajo de AEM** | ✅ | ✅ (a través de AEM Publish) | ✅ |
| **API sin encabezado** | ✅ (automático) | ❌ | ❌ |
| **Accesibilidad** | Compatible con WCAG | Compatible con WCAG | Básica |
| **Velocidad de implementación** | Basado en canalizaciones | Instantáneo (confirmar en vivo) | Basado en canalizaciones |
| **Estilo** | BEM CSS, temas | CSS, temas de nivel de proyecto | CSS, temas |
| **Creación de versiones** | ✅ (heredado de Sites) | Basado en Git | ✅ |
| **Localización** | Flujo de trabajo de traducción de AEM | Flujo de trabajo manual/de AEM Sites | Flujo de trabajo de traducción de AEM |

## Matriz de decisión

| Requisito | Enfoque recomendado |
|-------------|---------------------|
| Nuevo desarrollo de formularios | Componentes principales |
| Mantenimiento de formularios existentes | Componentes de base (hasta la migración) |
| Rendimiento crítico (puntuaciones altas de Lighthouse) | Formularios de Edge Delivery Services |
| Entrega sin encabezado/omnicanal | Componentes principales |
| Integración de Adobe Sign | Componentes de base |
| Creación basada en hoja de cálculo | Edge Delivery Services (basado en documentos) |
| Creación de Visual WYSIWYG con entrega perimetral | Edge Delivery Services (editor universal) |
| Integraciones empresariales complejas | Componentes principales o de base |
| Creación rápida de prototipos | Edge Delivery Services (basado en documentos) |
| Compatibilidad con plantillas XFA/XDP | Componentes de base |
| Front-end personalizado de React/Angular | Componentes principales (API sin encabezado) |

## Consideraciones de migración

### Componentes básicos a Componentes principales.

- **Herramienta**: Herramientas de modernización de AEM (Utilidad de conversión de Forms)
- **Esfuerzo**: de moderado a alto según la complejidad del formulario
- **Consideraciones**:
   - Las reglas requieren recreación manual
   - Los componentes exclusivos de Foundation (bloque de Adobe Sign, firma manuscrita, gráfico) se eliminan durante la migración
   - La configuración de traducción no se transfiere
   - Las funciones personalizadas requieren reescritura

### Tradicional para Edge Delivery Services

- **Enfoque**: Reconstruir formularios con el Editor universal o la creación basada en documentos
- **Esfuerzo**: alto para formularios complejos y bajo para formularios simples
- **Ventajas**: mejora significativa del rendimiento, experiencia de desarrollo moderna

## Lagunas y ambigüedades de la documentación

Las siguientes áreas tienen documentación incompleta o ambigua:

1. **Compatibilidad con XDP/XFA de componentes principales**: la documentación indica compatibilidad &quot;limitada&quot;, pero no especifica limitaciones exactas
2. **Incrustación de formularios Edge Delivery Services**: marcado como &quot;Próximamente&quot; en la documentación; estado actual no es claro
3. **Futuro de componentes de base**: no hay una cronología de obsolescencia explícita; se describe como &quot;modo de mantenimiento&quot;
4. **Cobertura de API sin encabezado**: No se ha documentado la paridad exacta de características entre los formularios procesados por el servidor y los formularios sin encabezado
5. **Parámetros de rendimiento**: no se proporcionaron comparaciones de puntuación específicas de Lighthouse entre los enfoques

## Recursos relacionados

- [Creación de un formulario adaptable (componentes principales)](/help/forms/creating-adaptive-form-core-components.md)
- [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
- [Información general sobre Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)
- [Introducción al editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [Tutorial de creación basada en documentos](/help/edge/docs/forms/tutorial.md)
- [Herramienta de utilidad de migración](/help/forms/migration-utility-tool-for-af-core-components.md)
- [Componentes principales de AEM Forms en GitHub](https://github.com/adobe/aem-core-forms-components)
