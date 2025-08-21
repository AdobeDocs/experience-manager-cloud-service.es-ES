---
title: 'Forms Experience Builder: biblioteca de mensajes'
description: Colección de patrones de solicitud probados y ejemplos para crear formularios con la asistencia de IA en la IU para la administración de formularios, el editor de formularios adaptables y el editor universal.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---


# Forms Experience Builder: biblioteca de mensajes

Colección de patrones de mensajes reutilizables y ejemplos optimizados para Forms Experience Builder. Esta biblioteca optimizada se centra en los dos métodos de creación principales: Crear desde cero e Importar y convertir, con compatibilidad mejorada para campos inteligentes con tecnología LLM y coherencia de marca.

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa de usuarios que lo adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de solicitud se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Los indicadores, los ejemplos y las prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de los primeros usuarios.

## Usar esta biblioteca de mensajes

Esta biblioteca proporciona patrones de solicitud reutilizables para escenarios comunes de creación de formularios. Para conocer las prácticas recomendadas completas, consulte la [Guía de introducción a Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

### Sugerencias rápidas para esta biblioteca

- **Empiece con ejemplos**: use las indicaciones proporcionadas como plantillas y adáptelas a sus necesidades
- **Dos métodos de creación**: elija los enfoques Crear desde cero o Importar y convertir
- **Sea específico**: agregue sus propios detalles a los ejemplos genéricos
- **Realizar pruebas exhaustivas**: validar siempre los resultados en el entorno específico

### Plantillas y estilos de marca

**Prepare los recursos de marca con antelación para crear formularios de forma coherente:**

- **Plantillas de marca**: cree plantillas de formulario estandarizadas con los colores, las fuentes y los patrones de diseño de su organización
- **Directrices de estilo**: defina un estilo de campo, diseños de botón y estándares de espaciado coherentes
- **Biblioteca de componentes**: cree componentes de formulario reutilizables que coincidan con la identidad de su marca
- **Visual Assets**: prepare logotipos, iconos y elementos de fondo para la integración de formularios

**Ejemplo de solicitud de plantilla de marca:**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**Componentes personalizados**: consulte con su equipo de desarrollo sobre el uso de componentes específicos de la organización y su compatibilidad con Forms Experience Builder antes de implementar elementos de marca personalizados.

>[!NOTE]
>
> Esta biblioteca de mensajes se ha actualizado para reflejar las funciones optimizadas de Forms Experience Builder. Algunas de las funciones avanzadas de integración y prueba que se muestran en los ejemplos pueden requerir una configuración adicional.



## Ejemplos de desarrollo incremental

Estos ejemplos muestran cómo crear formularios paso a paso, empezando por lo simple y añadiendo gradualmente complejidad:

### Ejemplo 1: Creación de un formulario de contacto de forma incremental

**Paso 1 - Inicio de forma sencilla:**

```
Create a basic contact form with name, email, and message fields
```

**Paso 2 - Añadir validación:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Paso 3: Mejorar la experiencia del usuario:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Paso 4 - Añadir características avanzadas:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Paso 5 - Implementar la lógica condicional:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Ejemplo 2: Creación incremental de un formulario de registro

**Paso 1 - Estructura básica:**

```
Create a user registration form with personal information panel
```

**Paso 2 - Agregar campos obligatorios:**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**Paso 3 - Agregar lógica empresarial:**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**Paso 4 - Mejorar con preferencias:**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**Paso 5 - Agregar carga de archivo:**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## Creación y administración de formularios

**Cuándo usar:** Cuando necesite crear formularios nuevos o modificar los existentes.

**Cómo usar:** Elija uno de los dos métodos: Crear desde cero o Importar y convertir (consulte [Guía de introducción](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Mensaje de ejemplo - Creación de formulario simple:**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**Mensaje de ejemplo - Creación de formularios complejos:**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**Indicadores de administración de formularios:**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## Administración y configuración de campos

**Cuándo se debe usar:** Cuándo se deben agregar, modificar o configurar los campos de formulario.

**Cómo usar:** Sea específico acerca de los tipos de campo, las reglas de validación y los requisitos de experiencia del usuario.

**Mensaje de ejemplo - Adición de campo básico:**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**Mensaje de ejemplo - Configuración avanzada de campo:**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**Indicadores de configuración de campo:**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## Campos inteligentes mejorados LLM

**Cuándo usar:** Cuando necesite campos con opciones previamente rellenadas que aprovechen la base de conocimiento de la IA.

**Cómo usar:** Solicitar campos que requieran conjuntos de datos completos; la inteligencia artificial puede rellenar automáticamente las opciones utilizando sus conocimientos integrados.

### Campos geográficos y de ubicación

**Aeropuertos y transporte:**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**Regiones administrativas:**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### Datos empresariales e industriales

**Clasificaciones de la compañía:**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**Clasificaciones profesionales:**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### Normas y regulaciones

**Asuntos financieros y legales:**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**Estándares técnicos:**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### Sanidad y medicina

**Clasificaciones médicas:**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### Inteligencia de tiempo y calendario

**Campos de fecha y hora:**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### Categorías de productos y servicios

**Clasificaciones de comercio electrónico:**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**Indicadores de campo inteligente de ejemplo:**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## Creación de reglas y lógica empresarial

**Cuándo usar:** Cuando necesite implementar lógica condicional, reglas de validación o procesos empresariales.

**Cómo usar:** Describa claramente la lógica empresarial, especificando condiciones y acciones.

**Mensaje de ejemplo - Lógica condicional simple:**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**Mensaje de ejemplo - Reglas comerciales complejas:**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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

**Solicitudes específicas de cada regla:**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
```

## Integración y envío de datos

**Cuándo se debe usar:** cuando necesite conectar formularios a sistemas back-end, bases de datos o servicios externos.

**Cómo se usa:** comience con la configuración básica de envío y luego añada integraciones adicionales de forma incremental. Especifique el tipo de integración, los requisitos de formato de datos y las preferencias de gestión de errores.

**Solicitud de ejemplo - Empiece con el envío básico:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Luego añada acciones secundarias de forma incremental:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Mensaje de ejemplo - Envío multicanal estándar:**

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

**Solicitudes específicas de la integración:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## Importar y convertir Forms existente

**Cuándo se debe usar:** Si ya tiene formularios, documentos o diseños para transformarlos en formularios modernos de AEM.

**Cómo usar:** Cargue el archivo de origen y describa los requisitos de conversión (consulte [Guía de importación](forms-ai-assistant-getting-started.md#2-import-and-convert)).

**Solicitud de ejemplo - Conversión de formulario PDF:**

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**Solicitudes de importación de diseño:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
```

## Optimización y capacidad de respuesta móviles

**Cuándo se debe usar:** cuando los formularios deben funcionar sin problemas en todos los tipos de dispositivos y tamaños de pantalla.

**Cómo se usa:** empiece con la optimización básica para móviles y luego mejore con características avanzadas. Haga hincapié en el enfoque &quot;mobile-first&quot; y especifique los comportamientos de punto de interrupción de forma incremental.

**Solicitud de ejemplo: comience con la optimización básica para móviles:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**A continuación, añada funciones más avanzadas:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Solicitud de ejemplo - Optimización completa centrada en &quot;Mobile-First&quot;:**

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
```

**Indicadores específicos para móviles:**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## Accesibilidad y conformidad

**Cuándo se debe usar:** Cuándo los formularios deben cumplir los estándares de accesibilidad (WCAG) o los requisitos de cumplimiento.

**Cómo se usa:** Especifique el nivel de cumplimiento requerido y las características de accesibilidad específicas que se necesitan.

**Mensaje de ejemplo - Accesibilidad básica:**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**Mensaje de ejemplo - Accesibilidad avanzada:**

```
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
```

**Indicadores específicos de accesibilidad:**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## Optimización de rendimiento

**Cuándo se deben usar:** Cuando los formularios deben cargarse rápidamente y funcionar correctamente en diversas condiciones.

**Cómo usar:** Especifique los requisitos de rendimiento y las estrategias de optimización.

**Mensaje de ejemplo - Rendimiento básico:**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**Mensaje de ejemplo - Rendimiento avanzado:**

```
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
```

**Indicadores específicos de rendimiento:**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## Pruebas y control de calidad

**Cuándo se debe usar:** Cuando los formularios necesitan pruebas exhaustivas para garantizar la fiabilidad y la satisfacción del usuario.

**Cómo usar:** Especifique escenarios de prueba, requisitos de validación y métricas de calidad.

**Mensaje de ejemplo - Prueba básica:**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**Mensaje de ejemplo - Pruebas avanzadas:**

```
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
```

**Solicitudes específicas de pruebas:**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## Resolución de problemas

Soluciones rápidas para problemas comunes del Forms Experience Builder:

| Problema | Corrección rápida |
|-------|-----------|
| El formulario no se envía | Comprobar la configuración de la acción de envío y las reglas de validación |
| Errores de validación que no se muestran | Verificar la configuración de validación de campos y la ubicación de mensajes de error |
| Problemas de diseño de Mobile | Revisar la configuración de diseño interactivo y el tamaño de los campos |
| Los campos no aparecen | Comprobación de la lógica condicional y las reglas de visibilidad |
| Errores de importación | Comprobar la compatibilidad y los límites de tamaño del formato de archivo |
| Errores de integración | Validar extremos de API y credenciales de autenticación |
| Problemas de rendimiento | Optimizar el recuento de campos y eliminar validaciones innecesarias |
| Problemas de accesibilidad | Revisar las etiquetas de campo, los atributos ARIA y el orden de tabulación |

**Indicador de modo de depuración:**

```
Enable debug mode to identify issues with form submission and field validation
```

**Mensaje de análisis de error:**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## Análisis e información avanzados

**Cuándo usar:** Cuando necesite comprender el rendimiento del formulario y el comportamiento del usuario.

**Cómo usar:** Especifique los requisitos y perspectivas de análisis necesarios.

**Mensaje de ejemplo - Análisis básico:**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**Mensaje de ejemplo - Análisis avanzado:**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Indicadores específicos de Analytics:**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## Seguridad y protección de datos

**Cuándo usar:** Cuando los formularios administran datos confidenciales y necesitan medidas de seguridad.

**Cómo usar:** Especifique los requisitos de seguridad y las medidas de protección de datos.

**Mensaje de ejemplo - Seguridad básica:**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**Mensaje de ejemplo - Seguridad avanzada:**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**Indicadores específicos de seguridad:**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

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
| `/configure-submit` | Configuración de la gestión de datos | `/configure-submit to CRM and send confirmation email` |
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
