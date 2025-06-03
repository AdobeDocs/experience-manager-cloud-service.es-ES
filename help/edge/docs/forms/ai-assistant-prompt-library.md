---
title: 'Asistente de IA de AEM Forms: biblioteca de mensajes'
description: Recopilación de patrones de mensajes probados y ejemplos para la creación de formularios con asistencia de IA en la IU de administración de Forms, el editor de Forms adaptable y el editor universal.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# Asistente de IA de AEM Forms: biblioteca de mensajes

Colección de patrones de mensajes reutilizables y ejemplos para escenarios comunes de creación de formularios. Considere estas plantillas como plantillas que puede adaptar a sus necesidades específicas. Cada sección cubre un caso de uso particular con instrucciones sobre cuándo utilizarlo y ejemplos comprobados.

>[!NOTE]
>
> El asistente de IA para AEM Forms está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a mailto:aem-forms-ea@adobe.com para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de mensajes se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Los indicadores, los ejemplos y las prácticas recomendadas pueden cambiar a medida que el asistente de IA para AEM Forms sigue evolucionando durante el programa de adopción temprana.

## Prácticas recomendadas para obtener resultados óptimos

Para sacar el máximo partido al Asistente de IA, tenga en cuenta estos consejos:

### Inicio sencillo, compilación incremental

Comience con comandos más pequeños y específicos (por ejemplo, &quot;Agregar una entrada de texto para &quot;Nombre&quot;) en lugar de solicitudes de varios pasos demasiado complejas inicialmente. Este método ayuda a garantizar la precisión y facilita la resolución de problemas si algo no funciona como se espera.

**Ejemplo de inicio simple:**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**Luego Genere Incrementalmente:**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### Uso de terminología de AEM Forms

Utilice términos como &quot;panel&quot;, &quot;campo de entrada de texto&quot;, &quot;grupo de casillas de verificación&quot;, &quot;acción de envío&quot;, &quot;regla&quot;, etc., para que el asistente los entienda mejor. Esto garantiza que la API interprete sus solicitudes correctamente en el contexto de AEM Forms.

**Términos preferidos:**

- &quot;campo de entrada de texto&quot; en lugar de &quot;cuadro de texto&quot;
- &quot;checkbox group&quot; en lugar de &quot;checkboxes&quot;
- &quot;desplegable&quot; en lugar de &quot;seleccionar lista&quot;
- &quot;panel&quot; en lugar de &quot;sección&quot; o &quot;contenedor&quot;
- &quot;acción de envío&quot; en lugar de &quot;envío de formulario&quot;
- &quot;rule&quot; en lugar de &quot;logic&quot; o &quot;condition&quot;

### Campos de referencia claramente

Al configurar los campos existentes, utilice la notación @fieldName (por ejemplo, &quot;Hacer @firstName obligatorio&quot;). Esto ayuda a la IA a identificar exactamente a qué campo se hace referencia, especialmente en formularios complejos con muchos campos.

**Ejemplos:**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### Revisar siempre los planes

Revise siempre los planes cuidadosamente para ver los cambios propuestos por el asistente en el Editor universal antes de hacer clic en &quot;Aplicar&quot;. La API le mostrará lo que planea hacer: dedique un momento a verificar que coincida con sus expectativas.

### Validar manualmente

Una vez que el asistente haya realizado los cambios, obtenga siempre una vista previa del formulario y pruébelo para asegurarse de que se comporta y tiene el aspecto esperado. La IA es una herramienta potente, pero la validación final es clave para garantizar la calidad.

**Lista de comprobación de validación:**

- Probar la funcionalidad del formulario en el modo de vista previa
- Verificar que la lógica condicional funcione correctamente
- Compruebe la capacidad de respuesta móvil
- Probar el envío del formulario
- Validar funciones de accesibilidad

### Iterar y refinar

Si la primera solicitud no arroja el resultado exacto, intente reformular o desglosar la solicitud en pasos más pequeños. La IA aprende del contexto, por lo que proporcionar detalles más específicos a menudo mejora los resultados.

**Ejemplo de iteración:**

1. Primer intento: &quot;Hacer que el formulario sea compatible con dispositivos móviles&quot;
2. Refinado: &quot;Optimizar el diseño del formulario para pantallas móviles de menos de 768 píxeles con diseño de una sola columna y destinos táctiles más grandes&quot;

### Proporcionar comentarios

Utilice el mecanismo de comentarios integrado para ayudar al asistente a aprender y mejorar. Sus comentarios ayudan a mejorar la IA para todos.


## Ejemplos de desarrollo incremental

Estos ejemplos muestran cómo crear formularios paso a paso, empezando por lo simple y agregando complejidad gradualmente:

### Ejemplo 1: Creación de un formulario de contacto de forma incremental

**Paso 1 - Inicio sencillo:**

```
Create a basic contact form with name, email, and message fields
```

**Paso 2 - Agregar validación:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Paso 3: Mejorar la experiencia del usuario:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Paso 4 - Agregar características avanzadas:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Paso 5 - Implementar lógica condicional:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Ejemplo 2: Creación de un formulario de registro incremental

**Paso 1 - Estructura básica:**

```
Create a user registration form with personal information panel
```

**Paso 2 - Agregar campos principales:**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**Paso 3 - Agregar validación:**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**Paso 4 - Agregar información de la cuenta:**

```
Create a new panel "Account Information" with @username and @password fields
```

**Paso 5 - Mejorar la seguridad:**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**Paso 6 - Agregar preferencias:**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

Este enfoque incremental le ayuda a:

- Detectar problemas antes de que se agraven
- Pruebe cada función a fondo
- Realizar ajustes según los comentarios del usuario
- Mantener un mejor control sobre el proceso de desarrollo

## Iniciar nuevo Forms

**Cuándo se debe usar:** Al principio de cualquier proyecto de formulario. Este mensaje ayuda a la IA a comprender sus necesidades y a crear la estructura de base.

**Cómo usar:** Comience con la estructura básica y los requisitos principales. Especifique el tipo de formulario, la audiencia de destino y el propósito principal. Agregue complejidad en las peticiones de datos posteriores.

**Mensaje de ejemplo - Inicio sencillo:**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**Luego Genere Incrementalmente:**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**Indicadores de inicio simples alternativos:**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## Estructura y diseño del formulario

**Cuándo se debe usar:** Cuando se necesita organizar formularios complejos o mejorar la experiencia del usuario mediante un mejor diseño.

**Cómo usar:** Céntrese en el recorrido del usuario y en la agrupación lógica de la información. Especifique las preferencias de diseño y los patrones de navegación.

**Mensaje de ejemplo - Estructura de formulario de varios pasos:**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**Indicadores de optimización de diseño:**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## Administración y validación de campos

**Cuándo usar:** Cuando necesite agregar, modificar o mejorar campos de formulario con reglas y comportamientos de validación específicos.

**Cómo usar:** Sea específico acerca de los tipos de campo, los requisitos de validación y las expectativas de la experiencia del usuario. Hacer referencia a campos existentes mediante sintaxis @fieldName.

**Mensaje de ejemplo - Mejora de campo:**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**Indicadores específicos de campo:**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## Lógica y reglas condicionales

**Cuándo se debe usar:** Cuando se necesita un comportamiento de formulario dinámico basado en la entrada del usuario o en reglas empresariales.

**Cómo usar:** Defina claramente las condiciones y las acciones resultantes. Utilice referencias de campo y operadores lógicos específicos.

**Mensaje de ejemplo - Lógica condicional compleja:**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**Indicadores específicos de reglas:**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## Integración y envío de datos

**Cuándo usar:** Cuando necesite conectar formularios a sistemas backend, bases de datos o servicios externos.

**Cómo usar:** Comience con la configuración básica de envío y luego agregue integraciones adicionales de forma incremental. Especifique el tipo de integración, los requisitos de formato de datos y las preferencias de gestión de errores.

**Mensaje de ejemplo: Comience con el envío básico:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Luego Agregue Acciones Secundarias Incrementalmente:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Mensaje de ejemplo - Envío multicanal avanzado:**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**Indicadores específicos de la integración:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## Diseño, importación y conversión

**Cuándo se debe usar:** Si ya tiene diseños de formulario (PDF, Figma e imágenes) que necesitan convertirse en formularios AEM funcionales.

**Cómo se usa:** Proporcione un contexto claro sobre el diseño de origen y especifique las modificaciones o mejoras necesarias.

**Mensaje de ejemplo - Conversión de formulario PDF:**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**Indicadores de importación de diseño:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## Optimización y capacidad de respuesta móviles

**Cuándo se debe usar:** Cuando los formularios deben funcionar sin problemas en todos los tipos de dispositivos y tamaños de pantalla.

**Cómo usar:** Empiece con la optimización básica para móviles y luego mejore con características avanzadas. Enfatice el enfoque &quot;mobile-first&quot; y especifique los comportamientos de punto de interrupción de forma incremental.

**Mensaje de ejemplo: Comience con la optimización móvil básica:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**A Continuación, Agregue Funciones Móviles Avanzadas:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Mensaje De Ejemplo - Optimización Completa De Mobile-First:**

```
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

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**Indicadores simples específicos para móviles:**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## Accesibilidad y conformidad

**Cuándo se debe usar:** Cuándo los formularios deben cumplir los requisitos de cumplimiento o los estándares de accesibilidad (WCAG 2.1 AA).

**Cómo usar:** Especifique los requisitos de accesibilidad y los estándares de cumplimiento que deben cumplirse.

**Mensaje de ejemplo - Implementación de accesibilidad:**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**Indicadores específicos de cumplimiento:**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## Pruebas y calidad de Assurance

**Cuándo se debe usar:** Cuando se necesita validar la funcionalidad del formulario, la experiencia del usuario y el rendimiento técnico.

**Cómo se usa:** Especifique los escenarios de prueba, los casos extremos y los criterios de calidad que deben verificarse.

**Mensaje de ejemplo - Prueba de formulario completa:**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**Indicadores Específicos De Pruebas:**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## Funciones e integraciones avanzadas

**Cuándo se debe usar:** Cuando se necesitan capacidades de formulario sofisticadas, como asistencia de IA, flujos de trabajo avanzados o integraciones complejas.

**Cómo usar:** Defina claramente los requisitos avanzados de funcionalidad e integración.

**Mensaje de ejemplo - Formulario mejorado con IA:**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**Indicadores de integración avanzada:**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## Solución de problemas y optimización

**Cuándo usar:** Cuando los formularios tienen problemas de rendimiento, problemas de experiencia del usuario o dificultades técnicas.

**Cómo usar:** Describa claramente el problema específico y el resultado deseado.

**Mensaje de ejemplo - Optimización de rendimiento:**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**Indicadores de solución de problemas:**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## Prácticas recomendadas específicas del entorno

### IU de administración de Forms

**Cuándo usar:** para tareas de administración y creación de formularios de alto nivel.

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### Editor de Forms adaptable

**Cuándo se debe usar:** Para obtener información detallada sobre la configuración de formularios y la creación de reglas complejas.

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### Editor universal

**Cuándo se debe usar:** para formularios Edge Delivery Services con edición visual.

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## Guía rápida de referencia de comandos

| Comando | Mejor caso de uso | Ejemplos |
|---------|---------------|---------|
| `/create-form` | Iniciar nuevos formularios | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Agregar formularios a páginas | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Cambiar la estructura del formulario | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modificación de propiedades del campo | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Adición del comportamiento dinámico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organización de secciones de formulario | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversión de diseños | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | Configuración de la gestión de datos | `/configure-submit to CRM and send confirmation email` |
| `/help` | Obtención de ayuda | `/help how to implement multi-step validation?` |

## Referencia de propiedades de componentes compatibles

### Propiedades universales (todos los componentes)

- **Tipo**: Tipo de componente (texto, correo electrónico, número, teléfono, fecha, casilla de verificación, radio, lista desplegable, archivo, etc.)
- **Nombre**: identificador de campo para el envío del formulario
- **Etiqueta**: mostrar texto para el campo
- **Descripción**: texto de ayuda para el campo
- **Visible**: booleano para visibilidad inicial
- **Obligatorio**: booleano para campos obligatorios

### Propiedades del campo de entrada

- **Valor**: Valor predeterminado/inicial
- **Marcador de posición**: texto de sugerencia para los campos de entrada
- **Mín.**: Valor mínimo (para números/fechas)
- **Máximo**: Valor máximo (para números/fechas)

### Propiedades de carga de archivos

- **Aceptar**: Tipos de archivo (.pdf, .doc, .docx, .jpg, .png, etc.)
- **Múltiple**: booleano para selección de varios archivos

### Propiedades del control de selección

- **Opciones**: opciones para desplegables (lista separada por comas)
- **Comprobado**: selección predeterminada para casillas de verificación/radio

### Propiedades del contenedor

- **Conjunto de campos**: Agrupando campos relacionados
- **Repetible**: booleano para secciones repetibles

### Propiedades avanzadas

- **Expresión visible**: Fórmula para visibilidad condicional (=formula)
- **Expresión de valor**: Fórmula para valores calculados (=fórmula)

## Resumen de prácticas recomendadas

### Directrices técnicas

- **Use solo propiedades compatibles** con la especificación oficial del componente de AEM Forms
- **Siga la sintaxis correcta** para las referencias (@fieldName) y expresiones de campo (=formula)
- **Realizar pruebas de forma incremental** después de cada cambio para detectar los problemas con antelación
- **Planifique la accesibilidad** desde el principio, no como una idea tardía
- **Considera a los usuarios móviles** en cada decisión de diseño
- **Documentar reglas complejas** para el mantenimiento futuro y la colaboración en equipo

### Enfoque estratégico

- **Empiece con las necesidades de los usuarios**. Céntrese en lo que los usuarios necesitan lograr, no solo en las características técnicas
- **Diseñar para finalizar**: minimiza la fricción y la carga cognitiva en el diseño de formularios
- **Planificar el flujo de datos** antes de tiempo: considere cómo se procesarán, almacenarán y utilizarán los datos
- **Generar para escala**: diseñe formularios que puedan gestionar el volumen de usuario y el crecimiento de datos esperados
- **Implementar mejora progresiva**: Asegúrese de que la funcionalidad básica funcione y agregue características avanzadas

### Problemas comunes que se deben evitar

- **Solicitudes iniciales excesivamente complejas**: divida las tareas grandes en pasos más pequeños y manejables
- **Usando propiedades no admitidas** que no se encuentran en la especificación de AEM Forms
- **Ignorando la experiencia móvil** hasta tarde en el proceso de desarrollo
- **Omitiendo prueba de usuario** con escenarios reales y casos puntuales
- **Suponiendo que la IA comprende el contexto** sin proporcionar instrucciones claras y específicas
- **Olvidando la accesibilidad** y los requisitos de cumplimiento
- **No se validan los cambios** antes de pasar al siguiente paso

### Enfoque de Assurance de calidad

1. **Vista previa con frecuencia**: compruebe su trabajo en el modo de vista previa después de cada cambio significativo
2. **Casos periféricos de prueba**: pruebe entradas inusuales, texto largo y caracteres especiales
3. **Validar en todos los dispositivos**: realice pruebas en dispositivos móviles, tabletas y de escritorio
4. **Comprobar accesibilidad** - Comprobar la compatibilidad del lector de pantalla y la navegación mediante el teclado
5. **Prueba de rendimiento** - Asegúrate de que los formularios se carguen rápidamente y respondan sin problemas
6. **Pruebas de aceptación de usuarios** - Haga que usuarios reales prueben el formulario antes de la implementación


*Esta biblioteca de mensajes se actualiza continuamente en función de los comentarios de los usuarios y las nuevas capacidades del Asistente de IA. Para obtener las últimas funciones y ejemplos, consulte la [documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es).*
