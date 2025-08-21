---
title: Introducción a Forms Experience Builder
description: Aprenda a utilizar Forms Experience Builder para crear y administrar formularios con divulgación progresiva para todos los tipos de usuarios
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: da429952-ccc0-4579-a243-8bddeb73a0fb
source-git-commit: 8be2b09200af58c701721b3e8537ea5e6cc3e4a2
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 15%

---

# Introducción a Forms Experience Builder

>[!NOTE]
>
> La funcionalidad Forms Experience Builder está disponible en **programa de adopción anticipada**. Si está interesado, envíe un mensaje de correo electrónico rápido desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso a la funcionalidad.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de los primeros usuarios.

Esta guía completa le ayuda a empezar a crear y administrar formularios mediante la tecnología de IA conversacional. Tanto si es un principiante que busca crear su primer formulario como si es un usuario avanzado que busca aprovechar las sofisticadas funciones, encontrará información detallada y ejemplos prácticos para guiar a su recorrido a través de las funcionalidades de Forms Experience Builder.

## Requisitos previos y configuración

### &#x200B;1. Solicitar acceso

Si no tiene acceso al Forms Experience Builder:

1. **Solicitar acceso**: envía un correo electrónico a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) desde tu correo electrónico de trabajo
2. **Incluir información**: Nombre de organización y detalles de proyecto
3. **Esperar aprobación**: Adobe revisará y proporcionará instrucciones de incorporación

### &#x200B;2. Compruebe que Forms está activado

Antes de usar Forms Experience Builder, asegúrate de que [AEM Forms está habilitado para tu entorno](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurar el entorno


* **Para Edge Delivery Services (EDS):**

   * [Configuración del entorno para Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [Crear un nuevo formulario con la plantilla de Edge Delivery Forms](/help/edge/docs/forms/universal-editor/create-forms.md)

* **Para formularios basados en componentes principales:**

   * En la instancia de Adobe Experience Manager, acceda a Forms > Forms y documentos
   * [Crear una nueva página con la plantilla de componentes principales](/help/forms/creating-adaptive-form-core-components.md)

## Inicio rápido

### Acceso a Forms Experience Builder

**Editor universal**

* Abra la página EDS en el editor universal
* Busque el icono de Forms Experience Builder en el panel izquierdo
* Haga clic para abrir la interfaz de conversación

**Editor de formularios adaptables**

* Vaya a AEM > Forms > Forms y documentos
* Cree o abra un formulario basado en componentes principales para editarlo
* Haga clic en el icono de Forms Experience Builder en la barra de herramientas del editor

### Su primer formulario

Pruebe esta sencilla conversación para empezar:

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### Comandos esenciales

| Símbolo | Función | Usos |
|--------|---------|------------|
| `/` | Acciones rápidas y métodos abreviados | Escriba `/create` para la creación de formularios, `/help` para obtener asistencia |
| `@` | Hacer referencia a campos de formulario existentes | Escriba `@fieldName` para modificar campos específicos (por ejemplo, `@email`) |
| Texto sin formato | Conversación natural | Describa lo que desea: &quot;Añadir un campo de número de teléfono requerido&quot; |

### Sugerencias para alcanzar el éxito

* **Sea específico**: &quot;Agregar un campo de correo electrónico requerido con validación&quot; funciona mejor que &quot;agregar correo electrónico&quot;
* **Hacer referencia a campos existentes**: usar `@fieldName` al modificar formularios
* **Pedir ayuda**: escriba `/help` seguido de su pregunta
* **Iterar**: realice un cambio a la vez para obtener mejores resultados

## Funciones principales

### Dos formas de crear Forms

#### &#x200B;1. Crear desde cero

Describa los requisitos de los formularios en lenguaje natural y Forms Experience Builder generará la estructura completa del formulario:

**Ejemplos:**

* &quot;Crear un formulario de solicitud de préstamo con información personal, detalles financieros y cargas de documentos&quot;
* &quot;Cree un formulario de comentarios de clientes con clasificaciones, comentarios y categorías de productos&quot;
* &quot;Necesito un formulario de registro de varios pasos para una conferencia con procesamiento de pagos&quot;

#### &#x200B;2. Importar y convertir

Transforme formularios y documentos existentes en experiencias modernas e interactivas:

**Fuentes compatibles:**

* **PDF forms**: cargar PDF estáticos → formularios digitales interactivos con validación
* **Capturas de pantalla/Imágenes**: Foto de formularios en papel → versiones digitales funcionales
* **HTML Forms**: formularios web básicos → AEM Forms mejorado con características avanzadas
* **XFA Forms**: formularios Adobe heredados → formularios adaptables modernos
* **URL**: formularios web existentes → AEM Forms nativo con UX mejorado

**Cómo importar:**

1. Haga clic en el icono de datos adjuntos en la interfaz de Forms Experience Builder
2. Cargue el archivo (PDF, imagen, diseño Figma, etc.)
3. Describa sus necesidades:
   * &quot;Convertir este formulario de PDF a una versión digital&quot;
   * &quot;Crear un formulario que coincida con este diseño de captura de pantalla&quot;
   * &quot;Construir este formulario a partir de mi diseño Figma&quot;

**Tipos de archivo compatibles:**

* **Imágenes** (PNG, JPG, GIF): diseños de formulario, maquetas de interfaz de usuario, formularios escaneados
* **Archivos de PDF**: Formularios, especificaciones y documentos existentes
* **Archivos Figma**: Diseñe prototipos y directrices de marca
* **Archivos de diseño**: Referencias visuales, guías de estilo

### Interacciones clave

#### Incorporación de elementos de formulario

**Incorporaciones básicas:**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**Especificaciones detalladas:**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### Creación de un comportamiento dinámico

**Lógica simple:**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**Reglas empresariales complejas:**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### Diseño de formularios

**Cambios en el diseño:**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**Mejoras en el diseño:**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### Configuración de integración

Forms Experience Builder puede configurar varios extremos de envío para conectar los formularios con sistemas y servicios externos:

| Tipo de integración | Comando de instalación | Caso práctico |
|------------------|---------------|----------|
| **Correo electrónico** | &quot;Enviar formulario al correo electrónico&quot; | Notificaciones y confirmaciones para envíos de formularios |
| **API DE REST** | &quot;Enviar al punto final REST&quot; | Aplicaciones personalizadas y sistemas de terceros |
| **Almacenamiento en la nube** | &quot;Guardar en Azure/SharePoint&quot; | Almacenamiento de documentos y administración de archivos |
| **Flujo de trabajo** | &quot;Conectarse a Power Automate&quot; | Automatización y aprobaciones de procesos empresariales |
| **Marketing** | &quot;Integración con Marketo&quot; | Administración de posibles clientes y automatización de marketing |

**Ejemplos de integración avanzada:**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## Operaciones de formulario avanzadas


### Creación de reglas complejas

Cree una lógica empresarial y de validación sofisticada que responda a las interacciones del usuario y garantice la integridad de los datos:

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### Creación de formularios de varios pasos

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### Tipos de campo avanzados

* Carga de archivos con restricciones de validación y tamaño para la administración de documentos
* Selector de fechas con restricciones y reglas de negocio para la programación
* Lista desplegable con opciones dinámicas que cambian según las selecciones de los usuarios
* Botones de opción con lógica condicional para árboles de decisión complejos


### Conversión de PDF a formulario

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### Conversión de URL a formulario

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### Análisis de rendimiento

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### Personalización avanzada

#### Reglas de validación personalizadas

* Dependencias de campo que crean un comportamiento de formulario dinámico basado en las entradas del usuario
* Lógica condicional compleja que adapta la experiencia del formulario a las necesidades del usuario
* Mensajes de error personalizados que proporcionan una guía clara a los usuarios
* Validación entre campos que garantiza la coherencia de los datos en varias entradas

#### Optimización de diseño

* Capacidad de respuesta móvil que garantiza que los formularios funcionen sin problemas en todos los dispositivos
* Cumplimiento de la accesibilidad que hace que los formularios sean utilizables por personas con discapacidades
* Mejoras en el diseño visual que mejoran la participación del usuario y las tasas de finalización
* Mejoras en la experiencia del usuario que reducen la fricción y mejoran la satisfacción

#### Flujos de trabajo de integración

* Procesos de aprobación de varios pasos que enrutan los envíos de formularios a través de flujos de trabajo empresariales
* Transformación de datos que convierte los datos del formulario en formatos requeridos por sistemas externos
* Lógica empresarial personalizada que aplica reglas y cálculos específicos a los envíos de formularios
* Tratamiento de errores avanzado que proporciona una recuperación correcta de los problemas del sistema

## Referencia de comandos

### Comandos esenciales

| Símbolo | Función | Usos |
|--------|---------|------------|
| `/` | Acciones rápidas y métodos abreviados | Escriba `/create` para la creación de formularios, `/help` para obtener asistencia |
| `@` | Hacer referencia a campos de formulario existentes | Escriba `@fieldName` para modificar campos específicos (por ejemplo, `@email`) |
| Texto sin formato | Conversación natural | Describa lo que desea: &quot;Añadir un campo de número de teléfono requerido&quot; |

### Comandos de barra diagonal

| Comando | Contexto | Uso de ejemplo |
|---------|---------|---------------|
| `/create-form` | Todos los entornos | `/create-form customer survey` |
| `/add-form` | Editor universal | `/add-form contact form` |
| `/update-layout` | Editor de formulario | `/update-layout wizard with 3 steps` |
| `/update-field` | Editor de formulario | `/update-field @email to be required` |
| `/create-rule` | Editor de formulario | `/create-rule show @spouse if married` |
| `/create-panel` | Editor de formulario | `/create-panel Personal Information` |
| `/configure-submit` | Editor de formulario | `/configure-submit to email support` |
| `/help` | Todos los entornos | `/help multi-step forms` |

### Referencias de campo

Use `@fieldName` para hacer referencia a los campos existentes:

* `@firstName`, `@lastName` * Campos de nombre
* `@email`, `@phoneNumber` * Campos de contacto
* `@address`, `@city`, `@zipCode` * Campos de dirección
* `@dateOfBirth`, `@startDate` * Campos de fecha

### Tipos de componentes

Utilice estos términos al describir elementos de formulario:

* `text input` * Campo de texto de una sola línea
* `text area` * Campo de texto multilínea
* `dropdown` * Seleccionar lista con opciones
* `checkbox` * Una sola casilla de verificación
* `checkbox group` * Varias casillas de verificación
* `radio group` * Grupo de botones de opción
* `date picker` * Campo de selección de fecha
* `file upload` * Campo de datos adjuntos del archivo
* `panel` * Contenedor para agrupar campos

### Comandos de integración

| Servicio | Comando de lenguaje natural | Requisitos  |
|---------|--------------------------|--------------|
| Correo electrónico | &quot;Enviar envíos a [correo electrónico]&quot; | Dirección de correo electrónico válida |
| API DE REST | &quot;Enviar al extremo REST [URL]&quot; | Credenciales y extremo de API |
| Almacenamiento de Azure | &quot;Guardar archivos en Azure Storage&quot; | Configuración de cuenta de almacenamiento |
| SharePoint | &quot;Almacenar en SharePoint [sitio]&quot; | Acceso al sitio de SharePoint |
| Power Automate | &quot;Flujo de Déclencheur Power Automate&quot; | Configuración de flujo |
| Marketo | &quot;Añadir posibles clientes a Marketo&quot; | Credenciales de API de Marketo |

### Sugerencias

1. **Usar lenguaje natural**: la IA comprende las solicitudes complejas y puede interpretar los requisitos detallados
2. **Sea específico**: Las descripciones detalladas generan mejores resultados y una generación de formularios más precisa
3. **Iterar**: perfeccione los formularios a través de la conversación para lograr la experiencia de usuario perfecta
4. **Aproveche el contexto**: Haga referencia a los elementos de formulario existentes para aprovechar lo que ya tiene
5. **Realizar pruebas exhaustivas**: valide todos los escenarios de usuario para asegurarse de que los formularios funcionan según lo esperado

## Ayuda y aprendizaje del producto

Forms Experience Builder también puede enseñarle sobre las funciones de AEM Forms:

### Formule preguntas como:

* &quot;¿Cómo se crea un formulario de varios pasos?&quot;
* &quot;¿Cuál es la diferencia entre paneles y secciones?&quot;
* &quot;¿Cómo se configuran las notificaciones por correo electrónico?&quot;
* &quot;¿Cuáles son las prácticas recomendadas para los formularios fáciles de usar en dispositivos móviles?&quot;
* &quot;¿Cómo se aplican las temáticas a los formularios?&quot;

### Obtenga ayuda sobre:

* Conceptos y terminología de AEM Forms
* Instrucciones paso a paso para funciones complejas
* Prácticas recomendadas y consideraciones
* Solución de problemas comunes

## Prácticas recomendadas

### Diseño de formulario

* **Simplifique**: Comience con campos esenciales y agregue complejidad solo cuando sea necesario para evitar abrumar a los usuarios
* **Use etiquetas claras**: haga que los propósitos de los campos sean obvios con etiquetas descriptivas que guíen a los usuarios a través del formulario
* **Proporcionar texto de ayuda**: guíe a los usuarios a través de campos complejos con ayuda contextual y ejemplos
* **Realizar pruebas exhaustivas**: valide todas las rutas de usuario para asegurarse de que los formularios funcionan correctamente en todos los escenarios

### Experiencia del usuario

* **Divulgación progresiva**: mostrar campos relevantes basados en el contexto para reducir la carga cognitiva y mejorar las tasas de finalización
* **Borrar navegación**: Ayude a los usuarios a comprender dónde se encuentran en el formulario y qué pasos quedan por realizar
* **Diseño interactivo**: compruebe que los formularios funcionan en todos los dispositivos y tamaños de pantalla para lograr la máxima accesibilidad
* **Accesibilidad**: siga las directrices de WCAG para que las personas con discapacidades puedan utilizar los formularios

### Rendimiento

* **Optimizar recuento de campos**: solo pida la información necesaria para reducir el abandono de formularios y mejorar las tasas de finalización
* **Use la validación apropiada**: Evite errores antes del envío para proporcionar comentarios y orientación inmediatos
* **Tasas de finalización de pruebas**: supervise y mejore la efectividad de los formularios mediante análisis y comentarios de los usuarios
* **Actualizaciones regulares**: mantenga los formularios al día con las necesidades de la empresa y las expectativas de los usuarios para obtener un rendimiento óptimo

### Coherencia de marca

* **Crear plantillas de marca**: prepare plantillas de formulario con marca con los colores, las fuentes y el estilo de su organización antes de comenzar a crear formularios
* **Definir estándares de estilo**: establezca estilos de botón, diseños de campo y directrices de espaciado coherentes a los que se pueda hacer referencia en las solicitudes
* **Usar recursos de marca**: prepare logotipos, códigos de color y directrices de marca para facilitar la referencia al crear formularios
* **Biblioteca de plantillas**: genere una colección de plantillas de formulario de marca para casos de uso comunes (contacto, registro, comentarios)
* **Instrucciones de estilo**: Incluir instrucciones específicas de la marca: &quot;Usar azul de la compañía (#1234AB) para botones y fuentes corporativas Helvetica&quot;

### Sugerencias para obtener mejores resultados

**Inicio sencillo, compilación**

* Empiece con solicitudes básicas: &quot;Crear un formulario de contacto&quot;
* Añada detalles gradualmente: &quot;Añadir validación al campo de correo electrónico&quot;
* Pruebe y perfeccione: &quot;Hacer que el campo de teléfono sea opcional&quot;

**Sea Específico Cuando Sea Necesario**

* En lugar de: &quot;Hacer que se vea bien&quot;
* Pruebe: &quot;Utilizar colores profesionales y una tipografía limpia&quot;

**Usar lenguaje natural**

* En lugar de: &quot;Añadir componente de entrada de texto&quot;
* Pruebe: &quot;Añadir un campo para el nombre&quot;

**Elementos existentes de referencia**

* Use `@fieldName` para los campos existentes: &quot;Hacer que @email sea obligatorio&quot;
* Sea específico sobre los nombres de campo: &quot;Actualizar el campo @phoneNumber&quot;

**Desglosar solicitudes complejas**

* En lugar de una solicitud grande, pruebe con varias más pequeñas
* Cree su formulario paso a paso
* Pruebe cada cambio antes de pasar al siguiente

## Resolución de problemas

| Problema | Corrección rápida |
|-------|-----------|
| **La interfaz no se carga** | Actualice el explorador, compruebe la conexión a Internet |
| **Los comandos no funcionan** | `/help` o use lenguaje natural en su lugar |
| **@fieldName no reconocido** | Revise la ortografía, asegúrese de que el campo exista primero |
| **Error al cargar el archivo** | Utilice PDF/JPG/PNG con menos de 10 MB |
| **El formulario tiene un aspecto incorrecto** | Sea más específico: &quot;Hacerlo compatible con dispositivos móviles&quot; |
| **Error de integración** | Verificar las credenciales y los permisos de API |

**¿Aún necesita ayuda?** escriba `/help` seguido de su pregunta específica o comuníquese con el administrador del sistema.

Para obtener soporte adicional, consulte la [Biblioteca de mensajes de Forms Experience Builder](/help/edge/docs/forms/ai-assistant-prompt-library.md) principal o póngase en contacto con el administrador del sistema para obtener asistencia técnica.
