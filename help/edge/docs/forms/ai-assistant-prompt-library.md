---
title: 'Forms Experience Builder: biblioteca de mensajes'
description: Colección de patrones de indicaciones probadas y ejemplos para crear formularios con la asistencia de IA en la IU para la administración de formularios, el editor de formularios adaptables y el editor universal.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 13%

---


# Forms Experience Builder: biblioteca de mensajes

Colección de patrones de mensajes reutilizables y ejemplos optimizados para Forms Experience Builder. Esta biblioteca optimizada se centra en los dos métodos de creación principales: Crear desde cero e Importar y convertir, con compatibilidad mejorada para campos inteligentes con tecnología LLM y coherencia de marca.

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa de usuarios que lo adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Los indicadores, los ejemplos y las prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de los primeros usuarios.

## Usar esta biblioteca de mensajes

Esta biblioteca proporciona patrones de solicitud reutilizables para escenarios comunes de creación de formularios. Para conocer las prácticas recomendadas completas, consulte la [Guía de introducción a Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

### Sugerencias rápidas para esta biblioteca

- **Empiece con ejemplos**: use las indicaciones proporcionadas como plantillas y adáptelas a sus necesidades
- **Dos métodos de creación**: elija los enfoques Crear desde cero o Importar y convertir
- **Sea específico**: agregue sus propios detalles a los ejemplos genéricos
- **Realizar pruebas exhaustivas**: validar siempre los resultados en el entorno específico

### Plantillas y estilos de marca

**Prepare los recursos de marca con antelación para crear formularios de forma coherente:**

- **Plantillas de marca**: prepare plantillas de formulario estandarizadas con los colores, las fuentes y los patrones de diseño de su organización
- **Directrices de estilo**: defina un estilo de campo, diseños de botón y estándares de espaciado coherentes que Forms Experience Builder pueda aplicar.
- **Biblioteca de componentes**: colabore con su equipo de desarrollo para preparar componentes de formulario reutilizables que coincidan con su identidad de marca
- **Visual Assets**: prepare logotipos, iconos y elementos de fondo para la integración de formularios

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## Ejemplos de desarrollo incremental

Estos ejemplos muestran cómo crear formularios paso a paso, empezando por lo simple y añadiendo gradualmente complejidad:

### Ejemplo 1: Creación de un formulario de contacto de forma incremental

**Paso 1 - Inicio de forma sencilla:**

    Crear un formulario de contacto básico con campos de nombre, correo electrónico y mensaje

**Paso 2 - Añadir validación:**

    Haga que los campos @name y @email sean obligatorios con la validación adecuada

**Paso 3: Mejorar la experiencia del usuario:**

    Agregar texto de marcador de posición: @name &quot;Su nombre completo&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Díganos cómo podemos ayudarle&quot;

**Paso 4 - Añadir características avanzadas:**

    Agregue un tipo de consulta desplegable con las opciones: &quot;Pregunta general&quot;, &quot;Solicitud de soporte&quot;, &quot;Consulta de ventas&quot;, &quot;Asociación&quot;

**Paso 5 - Implementar la lógica condicional:**

    /create-rule muestra @urgencyLevel lista desplegable (baja, Medium, alta) solo cuando @inquiryType es igual a &quot;Solicitud de asistencia&quot;

### Ejemplo 2: Creación incremental de un formulario de registro

**Paso 1 - Estructura básica:**

    Crear un formulario de registro de usuario con el panel de información personal

**Paso 2 - Agregar campos obligatorios:**

    Agregue campos para @firstName, @lastName, @email, @phoneNumber con la validación adecuada

**Paso 3 - Agregar lógica empresarial:**

    Crear una regla: si el @age es menor de 18 años, mostrar la sección de información para padres/tutores

**Paso 4 - Mejorar con preferencias:**

    Agregar un panel de preferencias con @newsletterSubscription, @marketingConsent, @termsAccepted

**Paso 5 - Agregar carga de archivo:**

    Incluir un campo de carga de archivo para @profilePicture con un límite de tamaño de 5 MB

## Creación y administración de formularios

**Cuándo usar:** Cuando necesite crear formularios nuevos o modificar los existentes.

**Cómo usar:** Elija uno de los dos métodos: Crear desde cero o Importar y convertir (consulte [Guía de introducción](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Mensaje de ejemplo - Creación de formulario simple:**

    Crear un formulario de comentarios de clientes con:
    - Clasificación del producto (de 1 a 5 estrellas)
    - Campo de comentarios para comentarios detallados
    - Correo electrónico del cliente (opcional)
    - Enviar a notificación por correo electrónico

**Mensaje de ejemplo - Creación de formularios complejos:**

    Crear un formulario de incorporación completo para empleados con:
    
    **Sección de información personal:**
    - Nombre completo (primero, segundo, último)
    - Fecha de nacimiento con validación de edad
    - Información de contacto (correo electrónico, teléfono, dirección)
    - Detalles de contacto de emergencia
    
    **Detalles de empleo:**
    - Selección de puesto y departamento
    - Fecha de inicio con validación de día laborable
    - Información de salario con aviso de confidencialidad
    - Estructura de informes
    
    **Carga de documento:**
    - Reanudar/cargar el CV (PDF, DOC, DOC, DOCX)
    - Documentos de verificación de identidad
    - Formularios fiscales e información bancaria
    - Contrato de trabajo firmado
    
    **Preferencias:**
    - Selección de beneficios con calculadora de costos
    - Preferencias de horario de trabajo
    - Requisitos de capacitación
    - Necesidades de equipo
    
    **Reglas de validación:**
    - Validación de formato de correo electrónico
    - Validación de formato de número de teléfono
    - Edad debe ser 18 o mayor
    - Todos los documentos requeridos deben ser subido
    - Se deben aceptar los términos y condiciones
    
    **Acciones de envío:**
    - Enviar correo electrónico de confirmación al nuevo empleado
    - Notificar al departamento de RRHH
    - Crear registro de empleado en el sistema de RRHH
    - Programar reunión de orientación

**Indicadores de administración de formularios:**

    Importe este formulario de solicitud de PDF y conviértalo en un formulario adaptable con validación mejorada
    
    Actualice el formulario de contacto existente para incluir identificadores de medios sociales y el método de contacto preferido
    
    Reorganice el formulario de registro en un asistente de tres pasos: información personal, preferencias, confirmación

## Administración y configuración de campos

**Cuándo se debe usar:** Cuándo se deben agregar, modificar o configurar los campos de formulario.

**Cómo usar:** Sea específico acerca de los tipos de campo, las reglas de validación y los requisitos de experiencia del usuario.

**Mensaje de ejemplo - Adición de campo básico:**

    Agregue un campo de entrada de texto para &quot;Nombre de la compañía&quot; con el marcador de posición &quot;Escriba el nombre de su compañía&quot;

**Mensaje de ejemplo - Configuración avanzada de campo:**

    Agregue una sección de dirección completa con:
    
    **Dirección de la calle:**
    - Línea de dirección 1 (obligatorio, máximo 100 caracteres)
    - Línea de dirección 2 (opcional, máximo 100 caracteres)
    - Ciudad (obligatorio, desplegable con ciudades comunes)
    - Estado/provincia (obligatorio, desplegable)
    - Código postal (obligatorio, validación de formato)
    - País (obligatorio, predeterminado en &quot;Estados Unidos&quot;)
    
    **Reglas de validación:**
    - El código postal debe coincidir con la selección de estado
    - 1 no puede estar vacía
    - La ciudad debe ser una ciudad válida para el estado seleccionado
    
    **Experiencia del usuario:**
    - Completar automáticamente para los campos de dirección
    - Borrar etiquetas y texto de ayuda
    - Campos de entrada compatibles con dispositivos móviles
    - Cumplimiento de la accesibilidad

**Indicadores de configuración de campo:**

    Haga que @email campo sea obligatorio con validación en tiempo real y mensaje de error personalizado
    
    Agregue un menú desplegable para @country con opciones para EE. UU., Canadá, Reino Unido, Alemania, Francia y &quot;Otros&quot;
    
    Configure @phoneNumber campo con el formato (XXX) XXX-XXXX y la validación
    
    Agregue un campo de carga de archivo para @resume con restricciones de PDF y DOC, máximo de 5 MB

## Campos inteligentes mejorados LLM

**Cuándo usar:** Cuando necesite campos con opciones previamente rellenadas que aprovechen la base de conocimiento de la IA.

**Cómo usar:** Solicitar campos que requieran conjuntos de datos completos; la inteligencia artificial puede rellenar automáticamente las opciones utilizando sus conocimientos integrados.

### Campos geográficos y de ubicación

**Aeropuertos y transporte:**

    Agregue un menú desplegable para los aeropuertos de salida con todos los aeropuertos internacionales principales
    Agregue un campo de aeropuerto de llegada con códigos IATA y nombres completos
    Cree un campo para el aeropuerto más cercano a la ubicación del usuario
    Agregue una selección de estaciones de tren para las ciudades europeas

**Regiones administrativas:**

    Agregar una lista completa de estados de EE. UU. con abreviaturas
    Crear un menú desplegable de países con códigos ISO y nombres completos
    Agregar un campo para las principales ciudades del mundo con husos horarios
    Incluir un menú desplegable de provincias y territorios canadienses
    Agregar un campo para los condados y áreas postales del Reino Unido

### Datos empresariales e industriales

**Clasificaciones de la compañía:**

    Agregue un campo para la clasificación del sector con códigos NAICS
    Cree un menú desplegable de tipos de entidades comerciales (LLC, Corporation, Partnership, etc.)
    Agregar un campo para categorías de tamaño de compañía (inicio, PYMES, empresa)
    Incluir la selección de departamentos para organizaciones grandes
    Agregar un campo para tipos de servicios profesionales

**Clasificaciones profesionales:**

    Agregue un campo para los puestos con funciones comunes en el sector
    Cree un menú desplegable de certificaciones profesionales por campo
    Incluya niveles de educación con tipos de títulos
    Agregue un campo para rangos de años de experiencia
    Cree una selección de lenguajes y marcos de trabajo de programación

### Normas y regulaciones

**Asuntos financieros y legales:**

    Agregue un campo para códigos de moneda con símbolos y tipos de cambio
    Cree un menú desplegable de tipos de identificación fiscal por país
    Incluya un campo para tipos de documentos legales
    Agregue opciones de métodos de pago con características de seguridad
    Cree una selección para instituciones bancarias por país

**Estándares técnicos:**

    Agregar un menú desplegable de tipos de formato de archivo con extensiones
    Incluir opciones de protocolo de red
    Agregar un campo para tipos y versiones de base de datos
    Crear una selección para métodos de autenticación de API

### Sanidad y medicina

**Clasificaciones médicas:**

    Agregue un campo para especialidades médicas
    Cree un menú desplegable de medicamentos comunes con nombres genéricos
    Incluya un campo para los tipos de proveedores de seguros
    Agregue una selección para las relaciones de contacto de emergencia médica
    Cree un campo para las restricciones dietéticas y las alergias

### Inteligencia de tiempo y calendario

**Campos de fecha y hora:**

    Agregue un campo para el horario laboral con administración de husos horarios
    Cree un menú desplegable de días festivos por país
    Incluya opciones de temporada con intervalos de fechas
    Agregue un campo para la reserva de salas de conferencias con disponibilidad
    Cree una selección para patrones de reuniones recurrentes

### Categorías de productos y servicios

**Clasificaciones de comercio electrónico:**

    Agregue un campo para las categorías de productos con subcategorías
    Cree un menú desplegable de métodos de envío con estimaciones de entrega
    Incluya un campo para opciones de directivas de devolución
    Agregue una selección para los niveles de prioridad de los clientes
    Cree un campo para los ciclos de facturación de suscripción

**Indicadores de campo inteligente de ejemplo:**

    &quot;Agregar un campo de aeropuerto de salida con todos los principales aeropuertos del mundo, incluidos los códigos IATA y los nombres de ciudades&quot;
    
    &quot;Crear un campo industrial completo utilizando la clasificación estándar de NAICS con subcategorías tecnológicas&quot;
    
    &quot;Incluir un menú desplegable de certificación profesional que se adapte en función del campo de trabajo seleccionado&quot;
    
    &quot;Agregar un campo de número de teléfono internacional que dé formato según el país seleccionado&quot;
    
    &quot;Crear un campo de selección universitaria con las principales instituciones organizadas por país y clasificación&quot;

## Creación de reglas y lógica empresarial

**Cuándo usar:** Cuando necesite implementar lógica condicional, reglas de validación o procesos empresariales.

**Cómo usar:** Describa claramente la lógica empresarial, especificando condiciones y acciones.

**Mensaje de ejemplo - Lógica condicional simple:**

    Cree una regla que muestre @spouseInformation panel únicamente cuando @maritalStatus igual a &quot;Casado&quot;

**Mensaje de ejemplo - Reglas comerciales complejas:**

    Implementar validación completa de solicitud de préstamo:
    
    **Validación de ingresos:**
    - Si el @annualIncome es menor que 30000:
    - Mostrar mensaje de advertencia: &quot;Los ingresos pueden ser insuficientes para el importe solicitado del préstamo&quot;
    - Requerir documentación de ingresos adicional
    - Mostrar mensaje: &quot;Puede requerirse documentación adicional&quot;
    - Si el @annualIncome es mayor que el 100000:
    - Mostrar opciones de servicios premium
    - Habilitar la casilla de verificación de procesamiento de prioridad
    
    **Validación basada en la edad:**
    - Si el @age es menor de 18:
    - Mostrar información del tutor section
    - Hacer obligatoria la carga de firma principal
    - Cambiar el texto del botón de envío a &quot;Enviar para revisión&quot;
    - Si @age 65 años o más:
    - Mostrar las opciones de descuento de categoría superior
    - Agregar la sección de preferencias de accesibilidad

**Indicaciones específicas de cada regla:**

    Cree una **regla de visibilidad** que muestre @spouseInformation panel únicamente cuando @maritalStatus igual a &quot;Casado&quot; o &quot;Asociación doméstica&quot;
    
    Agregue **divulgación progresiva** donde aparezcan preguntas adicionales basadas en respuestas anteriores. Comience con información básica y, a continuación, muestre los seguimientos relevantes
    
    Implemente **valores predeterminados inteligentes** donde la selección de @country configura automáticamente los campos relacionados. Permitir invalidación manual

## Integración y envío de datos

**Cuándo se debe usar:** cuando necesite conectar formularios a sistemas back-end, bases de datos o servicios externos.

**Cómo se usa:** comience con la configuración básica de envío y luego añada integraciones adicionales de forma incremental. Especifique el tipo de integración, los requisitos de formato de datos y las preferencias de gestión de errores.

**Indicación de ejemplo - Empiece con el envío básico:**

    Configurar el envío de formulario básico para @applicationForm:
    
    **Envío principal:**
    - Enviar datos de formulario al extremo REST: `/api/v1/applications`
    - Dar formato a los datos como JSON
    - Mostrar mensaje de éxito: &quot;La solicitud se envió correctamente&quot;
    - Mostrar mensaje de error si el envío falla: &quot;Error en el envío, inténtelo de nuevo&quot;

**Luego añada acciones secundarias de forma incremental:**

    Agregar notificación por correo electrónico a @applicationForm: enviar correo electrónico de confirmación a @email dirección con el número de referencia de la aplicación
    
    Agregar integración de CRM a @applicationForm: crear nuevo registro de cliente potencial con @firstName, @lastName, @email y establecer el estado en &quot;Nueva aplicación&quot;

**Mensaje de ejemplo - Envío multicanal estándar:**

    Configurar el envío de formularios con varios destinos de datos:
    
    **Envío principal:**
    - Enviar datos de formulario al extremo REST: `/api/v1/applications`
    - Incluir encabezado de autenticación con clave de API
    - Dar formato a los datos como JSON con objetos anidados para la dirección y el empleo
    - Controlar la respuesta correcta (201) mostrando el mensaje de agradecimiento
    
    **Acciones secundarias:**
    - Enviar correo electrónico de notificación al solicitante en la dirección @email
    - Copiar los datos de la solicitud en el sistema de seguimiento
    - Flujo de Déclencheur para el proceso de aprobación
    - Crear en el registro CRM con estado de posible cliente &quot;Nueva aplicación&quot;
    
    **Gestión de errores:**
    - Si falla el envío principal, guarde los datos localmente y vuelva a intentarlo
    - Mostrar mensaje de error descriptivo: &quot;Envío no disponible temporalmente&quot;
    - Proporcionar opción para descargar datos de formulario como copia de seguridad
    - Enviar correo electrónico de alerta al equipo de administración sobre el envío fallido
    
    **Flujo de éxito:**
    - Redirigir a la página de confirmación con número de referencia de aplicación
    - Enviar correo electrónico de confirmación con pasos siguientes
    - Mostrar cronología estimada del procesamiento

**Indicaciones específicas de la integración:**

    Conecte este formulario a **CRM system** para crear nuevos posibles clientes. Asigne @firstName a FirstName, @email a Email, establezca LeadSource en &quot;Formulario web&quot; y Status en &quot;Nuevo&quot;
    
    Configurar **déclencheur de flujo de trabajo** cuando se envíe el formulario. Pase todos los datos de formulario y el flujo de trabajo de aprobación de déclencheur con la notificación del administrador 
    
    Configure **integración de base de datos** para guardar los envíos de formularios como registros. Crear nueva carpeta para cada envío con documentos cargados

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## Referencia de comandos

### Comandos esenciales

| Comando | Mejor caso de uso | Ejemplos |
|---------|---------------|---------|
| `/create-form` | Inicio de nuevos formularios | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Añadir formularios a páginas | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Cambio de la estructura del formulario | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modificación de las propiedades de campo | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Adición del comportamiento dinámico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organización de secciones de formulario | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversión de diseños | `/add-panel from uploaded form image with field recognition` |
| `/help` | Obtención de ayuda | `/help how to implement multi-step validation?` |

### Referencias de campo

Utilice la sintaxis `@fieldName` para hacer referencia a los campos existentes en las indicaciones:

- `@email` - Campo de correo electrónico de referencia
- `@firstName` - Campo de nombre de referencia
- `@maritalStatus` - Campo de estado civil de referencia

### Tipos de componentes

**Componentes de entrada:**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**Componentes de contenedor:**

- `fieldset`, `panel`, `repeatable`, `wizard`

### Propiedades del componente

**Propiedades universales (todos los componentes):**

- **Tipo**: Tipo de componente
- **Nombre**: identificador de campo para el envío del formulario
- **Etiqueta**: texto que se muestra para el campo
- **Descripción**: texto de ayuda para el campo
- **Visible**: booleano para visibilidad inicial
- **Obligatorio**: booleano para campos obligatorios

**Propiedades del campo de entrada:**

- **Valor**: valor predeterminado/inicial
- **Marcador de posición**: texto de sugerencia para los campos de entrada
- **Mín.**: valor mínimo (para números/fechas)
- **Máx.**: valor máximo (para números/fechas)

**Propiedades de carga de archivos:**

- **Aceptar**: tipos de archivo (.pdf, .doc, .docx, .jpg, .png, etc.)
- **Múltiple**: booleano para la selección de varios archivos

**Propiedades del control de selección:**

- **Opciones**: opciones para menús desplegables (lista separada por comas)
- **Marcado**: selección predeterminada para las casillas de verificación/botones de opción

**Propiedades del contenedor:**

- **Conjunto de campos**: agrupación de campos relacionados
- **Repetible**: booleano para secciones repetibles

**Propiedades avanzadas:**

- **Expresión visible**: fórmula para la visibilidad condicional (=fórmula)
- **Expresión de valor**: fórmula para los valores calculados (=fórmula)

### Comandos de integración

**Acciones de envío:**

- Notificaciones por correo electrónico
- Envíos de API de REST
- Almacenamiento en la nube (Azure, SharePoint)
- Automatización del flujo de trabajo (Power Automate, Workfront Fusion)
- Plataformas de marketing (Marketo)
- Integraciones de CRM

### Instrucciones de sintaxis de indicador

- **Referencias de campo**: use `@fieldName` para los campos existentes
- **Comandos**: use `/command` para acciones específicas
- **Lenguaje natural**: Describa los requisitos de forma clara y específica

### Lista de comprobación de validación

Para obtener prácticas recomendadas y directrices de validación completas, consulte la [Guía de introducción a Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

*Esta biblioteca de mensajes se actualiza continuamente en función de los comentarios de los usuarios y de las nuevas funciones de Forms Experience Builder. Para obtener las últimas funciones y ejemplos, consulte la [documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es).*
