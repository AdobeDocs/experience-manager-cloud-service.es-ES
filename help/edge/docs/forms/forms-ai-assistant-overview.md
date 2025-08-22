---
title: Forms Experience Builder
description: Elabore formularios potentes más rápido mediante fragmentos de formulario
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 2%

---


# Introducción a Forms Experience Builder

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de los primeros usuarios.

Forms Experience Builder incorpora la potencia de la inteligencia artificial a Adobe Experience Manager (AEM) Forms. Esta solución innovadora transforma la forma en que las organizaciones crean, administran y optimizan sus formularios digitales a través de interacciones en lenguajes naturales y automatización inteligente.

Basado en tecnologías web modernas y con tecnología de servicios de IA avanzados, Forms Experience Builder permite a los usuarios técnicos y no técnicos crear formularios sofisticados de calidad profesional mediante interfaces conversacionales. Tanto si es un analista empresarial que necesita un formulario de registro sencillo como si es un desarrollador que crea flujos de trabajo complejos de varios pasos, Forms Experience Builder optimiza todo el proceso de creación de formularios.

## Interfaz de conversación

Forms Experience Builder proporciona una interfaz intuitiva basada en chat que simplifica tanto la creación de formularios como la realización de una conversación:

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Capacidades principales

### Creación de formularios con tecnología de IA

**Generación de formularios en lenguaje natural**

Cree formularios completos desde cero con descripciones simples en inglés. Describa simplemente sus necesidades, como &quot;Crear un formulario de comentarios de cliente con escalas de clasificación y campos de comentarios&quot;, y Forms Experience Builder generará la estructura de formulario, los tipos de campo y las reglas de validación adecuados.

**Administración dinámica de campos**

Agregar, modificar o quitar campos de formulario mediante comandos conversacionales. La API comprende el contexto y puede sugerir de forma inteligente tipos de campo, reglas de validación y mejoras en la interfaz de usuario en función de sus necesidades.

**Optimización del diseño**

Actualizar los diseños y las configuraciones de formulario mediante lenguaje natural. Solicite cambios como &quot;Facilite el uso del formulario para dispositivos móviles&quot; o &quot;Reorganice los campos en un flujo lógico&quot;, y Forms Experience Builder aplicará los ajustes de estilo y diseño adecuados.

### Importación y conversión inteligentes

**Conversión de PDF a formulario**

Transforme documentos estáticos de PDF en formularios interactivos y dinámicos. Cargue cualquier documento de PDF y Forms Experience Builder analizará la estructura para crear un formulario digital correspondiente con los tipos de campo y la validación adecuados.

**Conversión de URL a formulario**

Convierta formularios o páginas web existentes en AEM Forms. Solo tiene que proporcionar una dirección URL, y Forms Experience Builder extrae elementos de formulario y los vuelve a crear como AEM Forms nativo con funciones mejoradas.

**Compatibilidad con archivos multiformato**

Gestionar varios tipos de archivos para la creación de formularios, incluidos PDF, imágenes, capturas de pantalla y plantillas de formulario existentes. Forms Experience Builder puede procesarlos y convertirlos en AEM Forms funcional.

### Lógica de formulario avanzada e integración

**Generación inteligente de reglas**

Cree reglas complejas de validación de formularios y lógica empresarial mediante lenguaje natural. Forms Experience Builder puede generar sofisticadas reglas de validación, dependencias de campo y lógica condicional que normalmente requerirían amplios conocimientos de codificación.

**Configuración completa de la acción de envío**

Configure los envíos de formularios para integrarlos con los sistemas empresariales existentes:

- **Integración de correo electrónico**: configure notificaciones y confirmaciones de correo electrónico automatizadas
- **Extremos de API de REST**: conectar con aplicaciones y servicios personalizados
- **Almacenamiento en la nube**: integrar con Azure Blob Storage, SharePoint y OneDrive
- **Automatización del flujo de trabajo**: Conéctese a Power Automate y Workfront Fusion
- **Plataformas de mercadotecnia**: Integración directa con Marketo para la administración de clientes potenciales
- **Flujos de trabajo de AEM**: aproveche las capacidades existentes del flujo de trabajo de AEM

**Análisis de rendimiento**

Analizar el rendimiento de la conversión de formularios y los patrones de participación del usuario. Forms Experience Builder proporciona perspectivas sobre la eficacia del formulario y sugiere optimizaciones para mejorar las tasas de finalización y la experiencia del usuario.

## Cómo funciona

Forms Experience Builder sigue un enfoque sencillo y conversacional:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## Ejemplos de casos de uso

### Formulario de solicitud de préstamo

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### Formulario de reclamación de seguro

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### Escenarios de migración y conversión

Transforme sus formularios existentes en potentes experiencias digitales con la conversión mediante IA.


#### Transformación de PDF forms a Forms digital

Transforme PDF forms con varios campos en experiencias digitales dinámicas mediante cálculos automatizados y un diseño interactivo para dispositivos móviles.

**Ventajas principales:**

- Cálculos de impuestos automatizados y dependencias de campo
- Firmas digitales e integración de archivado electrónico
- Optimización de diseño adaptable para móviles
- Reducción del 95 % de los errores de procesamiento


#### Modernización de formularios basados en XFA heredados

Puede convertir aplicaciones XFA complejas en modernos asistentes de varios pasos con validación en tiempo real y cumplimiento de la accesibilidad.

**Ventajas principales:**

- Interfaz de asistente de varios pasos optimizada
- Validación en tiempo real con ayuda contextual
- Integración de bases de datos gubernamentales
- Cumplimiento de la accesibilidad WCAG 2.1 completo


#### Convertir captura de pantalla de un formulario en un formulario digital

Puede convertir cualquier formulario en papel en una experiencia digital. AEM Forms optimiza automáticamente el diseño y crea formularios digitales listos para la integración a partir de una captura de pantalla.

**Ventajas principales:**

- Detección inteligente del tipo de campo
- Generación de diseños adaptables optimizados
- Validación mejorada más allá del papel original
- Arquitectura lista para la integración

#### Importación y mejora de formularios web existentes

Puede importar el formulario web existente y agregar validación avanzada, lógica condicional y envío multicanal a los formularios sin romper la funcionalidad existente.

**Ventajas principales:**

- Lógica y reglas de validación avanzadas
- Comportamientos y flujos de trabajo de campo condicionales
- Opciones de envío multicanal
- Análisis y seguimiento del rendimiento integrados

## Forms Experience Builder y desarrollo tradicional

| Aspecto | Creación de formularios tradicionales | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Tiempo para crear** | 2 a 3 días | 2 a 3 horas |
| **Conocimientos técnicos** | Requerido | No obligatorio |
| **Reglas de validación** | Codificación manual | Lenguaje natural |
| **Optimización móvil** | CSS/JS manual | Automático |
| **Accesibilidad** | Implementación manual | Cumplimiento de normas integrado |
| **Actualizaciones** | Cambios de código necesarios | Lenguaje natural |


## Ventajas para las organizaciones

### Creación de formularios democratizados

Habilite a los usuarios no técnicos para crear formularios sofisticados sin conocimientos de programación. Los analistas de negocio, los expertos en la materia y los creadores de contenido pueden traducir directamente sus requisitos en formularios funcionales a través de conversaciones en lenguaje natural.

### Tiempo de respuesta reducido (TTV)

Acelerar drásticamente el desarrollo de formularios de días a horas. Lo que antes requería ciclos de desarrollo extensos ahora se puede lograr en una sola sesión a través de IA conversacional, lo que permite una salida al mercado más rápida para las iniciativas digitales.

### Simplicidad de interfaz

Elimine la curva de aprendizaje con una interfaz conversacional intuitiva. Los usuarios pueden crear formularios complejos utilizando un lenguaje natural en lugar de aprender herramientas técnicas de creación de formularios, lo que reduce el tiempo de formación y aumenta la adopción.

### Ampliación de los esfuerzos de modernización

Modernice los portafolios de formularios heredados de forma eficaz. Convierta los formularios PDF, XFA y HTML existentes en experiencias digitales adaptables, al tiempo que preserva la lógica empresarial y mejora la experiencia del usuario en todo el ecosistema de formularios.

## Introducción

Para empezar a usar Forms Experience Builder, visite la [documentación de Forms Experience Builder](forms-ai-assistant-getting-started.md). Puede acceder a Forms Experience Builder a través del Editor de AEM Forms o del Editor universal, según el flujo de trabajo que prefiera.

Para organizaciones que pretenden transformar sus procesos de creación de formularios, Forms Experience Builder ofrece una solución potente e intuitiva que combina la flexibilidad de la IA conversacional con la solidez de la administración de formularios de nivel empresarial.

## Incorporación y acceso anticipado

Forms Experience Builder está disponible actualmente como parte del programa de acceso anticipado (EA). Para participar y obtener acceso, siga estos pasos:

1. Asegúrese de que está utilizando su dirección de correo electrónico de trabajo oficial asociada a su organización.
2. Envíe un correo electrónico a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso a Forms Experience Builder.
3. Incluya el nombre de su organización y cualquier detalle relevante del proyecto en su solicitud para acelerar el proceso de incorporación.

>[!NOTE]
>
> El acceso al Forms Experience Builder está limitado a los participantes aprobados en el programa de acceso anticipado. Adobe revisará su solicitud y proporcionará más instrucciones para la incorporación si reúne los requisitos.

Para obtener más información acerca del programa de acceso anticipado y sus características, consulte la [documentación de acceso anticipado de AEM Forms](/help/forms/early-access-ea-features.md).

