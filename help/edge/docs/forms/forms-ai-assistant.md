---
title: Asistente de IA para AEM Forms (Forms Experience Builder)
description: Elabore formularios potentes más rápido mediante fragmentos de formulario
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 2%

---

# Asistente de IA para AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funcionalidad Asistente de IA para AEM Forms (Forms Experience Builder) está disponible en el programa de usuarios pioneros. Si está interesado, envíe un correo electrónico rápido desde su dirección de trabajo a mailto:aem-forms-ea@adobe.com para solicitar acceso a la funcionalidad.


El asistente de IA para AEM Forms (Forms Experience Builder) mejora la experiencia de creación al optimizar las tareas comunes de creación de formularios mediante peticiones de datos en lenguaje natural. Disponible en Forms Manager, el editor de Forms adaptable y el editor universal, le permite crear de forma más inteligente y rápida mediante la compatibilidad de acciones de creación y configuración. Esta guía le ayudará a empezar y a aprovechar al máximo sus capacidades.

## Introducción

Antes de profundizar, vamos a cubrir los conceptos básicos del acceso y la interacción con el asistente de IA.

### Acceso al asistente de IA

Puede acceder al asistente de IA desde tres ubicaciones diferentes en AEM Forms:

1. **Administrador de Forms**
   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono para abrir el panel Asistente de IA

   ![Icono de asistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **Editor de Forms adaptable**
   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Seleccione y abra un formulario para editarlo
   - Haga clic en el icono Ayudante de IA de la interfaz del editor

   ![Icono de asistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **Editor universal**

   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono Ayudante de IA de la interfaz del editor

El asistente de IA adapta su funcionalidad en función de su ubicación y tarea actuales, lo que proporciona una asistencia relevante para cada contexto.

### Cómo interactuar:

- Simplemente escriba su solicitud en lenguaje natural.
- Use `/` para ver una lista de comandos disponibles o acciones rápidas.
- Hacer referencia a campos de formulario específicos mediante `@fieldName` (por ejemplo, `@firstName`, `@emailAddress`) cuando desee que el asistente configure o actualice ese campo en particular.


### Inicio rápido

Póngase en marcha rápidamente viendo nuestro vídeo introductorio:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


Este vídeo explica cómo iniciar el asistente en todos los entornos, la interacción básica y una descripción general de sus funciones.

## Referencia de comandos del asistente de IA

| Comando | Descripción | Función | Contexto de uso | Ejemplos | Funciones principales |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | Iniciar un formulario nuevo en Forms Manager o Forms Editor | Inicia la creación de un formulario completamente nuevo desde cero | Forms Manager, editor de Forms adaptable | /create-form encuesta de comentarios de clientes | Proporciona opciones para la estructura de formularios y crea el formulario |
| /add-form | Agregar un nuevo formulario en el editor universal | Agrega un nuevo bloque de formulario o componente dentro del Editor universal | Editor universal para Edge Delivery Services | /add-form formulario de contacto con nombre y correo electrónico | Inserta bloques de formulario y funciona con la edición basada en bloques |
| /update-layout | Cambiar el diseño del formulario a acordeón, basado en pestañas, asistente o diseño adaptable de una sola página | Modifica el diseño estructural general y el patrón de navegación | Todos los entornos de edición | /update-layout asistente con 3 pasos | Acordeón, pestañas, asistente, opciones adaptables de una sola página |
| /update-field | Modificar propiedades y configuración de campos de formulario existentes | Cambia atributos de campo como etiquetas, validación, formato y comportamiento | Todos los entornos de edición | /update-field @email ser necesario con la validación | Etiquetas, reglas de validación, tipos de campo, valores predeterminados, visibilidad |
| /create-rule | Crear un comportamiento dinámico y una lógica condicional para los formularios | Implementa lógica empresarial, cálculos e interacciones condicionales | Todos los entornos de edición | /create-rule mostrar @spouseName si @maritalStatus es igual a &quot;Married&quot; | Visibilidad condicional, cálculos, validación, configuración de valores |
| /create-panel | Crear un nuevo panel (contenedor para agrupar campos relacionados) | Agrega contenedores estructurales para organizar los campos de formulario de forma lógica | Todos los entornos de edición | /create-panel Información personal con nombre, correo electrónico, teléfono | Agrupación de campos, títulos, opciones de diseño, secciones contraíbles |
| /add-panel | Conversión de una imagen en el panel del formulario en el editor universal | Utiliza IA para analizar las imágenes cargadas y convertirlas en paneles de formularios estructurados | Editor universal | /add-panel desde la imagen de formulario cargada | Reconocimiento de imágenes, conversión de visual a funcional, preservación de diseños |
| /configure-submit | Configurar acciones de envío de formularios y administración de datos | Define lo que sucede cuando los usuarios envían el formulario completado | Todos los entornos de edición | /configure-submit para enviar correo electrónico a `support@company.com` | Correo electrónico, API de REST, flujos de trabajo, hojas de cálculo, bases de datos, Power Automate |
| /help | Acceso a asistencia y documentación dentro del asistente de IA | Proporciona ayuda contextual, instrucciones y respuestas acerca de AEM Forms | Todos los entornos de edición | /help ¿cómo se crean formularios de varios pasos? | Explicaciones de funciones, guías, prácticas recomendadas, solución de problemas |

### Categorías de comandos

| Categoría | Comandos | Casos de uso principales |
|----------|----------|-------------------|
| Creación de formularios | /create-form, /add-form | Iniciar formularios nuevos, agregar bloques de formulario |
| Estructura y diseño | /update-layout, /create-panel, /add-panel | Organizar la estructura del formulario, diseño visual |
| Administración de campos | /update-field | Configuración de elementos de formulario individuales |
| Lógica y reglas | /create-rule | Adición del comportamiento dinámico y la validación |
| Envío | /configure-submit | Configuración de gestión de datos y flujos de trabajo |
| Soporte | /help | Obtención de asistencia y documentación |

### Directrices de sintaxis

| Elemento | Formato | Ejemplos | Notas |
|---------|--------|---------|-------|
| Comandos | /command-name | /create-form | Iniciar siempre con barra diagonal |
| Referencias de campo | @fieldName | @email, @firstName | Utilice el símbolo @ para los campos existentes |
| Lenguaje natural | Comando + descripción | /create-rule mostrar campo si condición | Combinación de comandos con texto descriptivo |
| Múltiples acciones | Separar comandos | /create-panel y luego /update-layout | Aplicar un comando a la vez |


### Funciones específicas del entorno

| Entorno | Comandos disponibles | Características especiales |
|-------------|-------------------|------------------|
| Administrador de Forms | /create-form, /help | Creación y administración a nivel de formulario |
| Editor de Forms adaptable y editor universal | Todos los comandos | Conjunto completo de funciones, configuración detallada |



### Sintaxis de referencia de campo (elementos contextuales)

Usar `@fieldName` para hacer referencia a campos existentes:

- `@firstName` - Campo de nombre
- `@email` - Campo de correo electrónico
- `@phoneNumber` - Campo de número de teléfono
- `@dateOfBirth` - Campo de fecha de nacimiento

### Tipos de componentes

Esta lista cubre tipos de componentes comunes. La IA puede reconocer variaciones o tipos más especializados, pero el uso de estos términos precisos proporciona los mejores resultados:

- `text input` - Campo de texto de una sola línea
- `text area` - Campo de texto multilínea
- `dropdown` - Seleccionar lista
- `checkbox` - Una casilla de verificación
- `checkbox group` - Varias casillas de verificación
- `radio group` - Grupo de botones de opción
- `date picker` - Selección de fecha
- `file upload` - Archivo adjunto
- `panel`: contenedor para agrupar campos


## Capacidades principales y ejemplos de mensajes ampliados

El asistente de IA comprende una amplia gama de comandos. Aquí hay algunos ejemplos para ilustrar su poder. Recuerde utilizar términos precisos para componentes como &quot;panel&quot;, &quot;entrada de texto&quot;, &quot;casilla de verificación&quot;, etc.

| Categoría de función | Descripción | Indicadores de ejemplo |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Creación de formularios** | Inicie un nuevo formulario desde cero o en función de una descripción. | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` |
| **Importar diseño** | Convierta un diseño existente (imagen, Figma, PDF) en un formulario de AEM. | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` |
| **Agregando Componentes Y Paneles** | Agregue varios campos de formulario y contenedores estructurales (paneles). | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` |
| **Ajustes de diseño** | Modifique la estructura y el aspecto del diseño del formulario. | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` |
| **Creación y lógica de reglas** | Implemente comportamiento dinámico, cálculos y visibilidad condicional. | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **Actualización de propiedades de campo** | Modifique los atributos de campos de formulario específicos como etiquetas, marcadores de posición, etc. | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` |
| **Acciones de envío** | Defina lo que sucede cuando un usuario envía el formulario. | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **Tema** | Aplicar temáticas de AEM Forms existentes para aplicar estilo al formulario. | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` |
| **Navegación y estructura** | Agregue elementos de navegación o reorganice partes del formulario. | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **Validación** | Establezca reglas de validación específicas para los campos. | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **Plan De Revisión** (Editor Universal) | Previsualice los cambios propuestos por el asistente antes de la ejecución. | `Add a contact form with fields for name, email, subject, and message.` (el asistente mostrará un plan de componentes y propiedades que creará y luego hará clic en &quot;Aplicar&quot;). |

## Prácticas recomendadas para obtener resultados óptimos

Para sacar el máximo partido al Asistente de IA, tenga en cuenta estos consejos:

- **Iniciar simple, Generar gradualmente:** Comience con comandos específicos más pequeños (por ejemplo, &quot;Agregar una entrada de texto para &#39;Nombre&#39;&quot;) en lugar de solicitudes de varios pasos demasiado complejas inicialmente.
- **Use terminología de AEM Forms:** Use términos como &quot;panel&quot;, &quot;campo de entrada de texto&quot;, &quot;grupo de casillas de verificación&quot;, &quot;acción de envío&quot;, &quot;regla&quot;, etc., para que el asistente los entienda mejor.
- **Campos de referencia claramente:** Al configurar los campos existentes, use la notación `@fieldName` (por ejemplo, `Make @firstName mandatory`).
- **Revisar planes** Siempre revise cuidadosamente los planes en busca de los cambios propuestos por el asistente en el Editor universal antes de hacer clic en &quot;Aplicar&quot;.
- **Validar manualmente:** Después de que el asistente realice los cambios, obtenga siempre una vista previa y pruebe el formulario para asegurarse de que se comporta y tiene el aspecto esperado. La IA es una herramienta potente, pero la validación final es clave.
- **Iterar y refinar:** Si la primera solicitud no produce el resultado exacto, intente reformular o desglosar la solicitud en pasos más pequeños.
- **Proporcionar comentarios:** Use el mecanismo de comentarios integrado para ayudar al asistente a aprender y mejorar (consulte la sección &quot;Comentarios y asistencia&quot;).

## Ayuda del producto con el asistente de IA

El Asistente de IA para AEM Forms no solo sirve para generar contenido; también puede ayudarle a aprender, comprender y utilizar varias funciones de AEM Forms.

### Temas de ayuda admitidos

Puede hacer preguntas al asistente como las siguientes:

- &quot;¿Cómo se crea un nuevo formulario adaptable desde cero?&quot;
- &quot;¿Qué es un panel en Adaptive Forms y cómo se utiliza?&quot;
- &quot;Explicar cómo aplicar una temática a un formulario.&quot;
- &quot;¿Qué tipos de diseño son compatibles con los formularios y paneles?&quot;
- &quot;¿Cómo configuro diferentes acciones de envío, como enviar un correo electrónico?&quot;
- &quot;¿Puede guiarme en el uso de un diseño de Figma para crear un formulario?&quot;
- &quot;¿Cuál es la mejor manera de crear un formulario de varios pasos?&quot;

### Cómo pedir ayuda:

1. Abra el asistente de IA en Forms Manager o el editor de Forms adaptable.
2. Escriba su pregunta en lenguaje natural (por ejemplo, &quot;¿Cómo añado un panel repetible?&quot;).
3. El asistente responderá con lo siguiente:
   - Instrucciones paso a paso.
   - Explicación de los conceptos de AEM Forms.
   - Vínculos a la documentación relevante de Adobe Experience League, si corresponde.

### Sugerencias para obtener mejor ayuda:

- **Sea específico:** haga una pregunta clara a la vez.
- **Usar palabras clave:** Incluir palabras clave relevantes para las características de AEM Forms o los elementos de la interfaz de usuario (por ejemplo, &quot;editor de formularios adaptables&quot;, &quot;editor de reglas&quot;, &quot;tema&quot;).
- **Cambiar expresión si es necesario:** Si el asistente no entiende o no proporciona la información deseada, intente simplificar la pregunta o use términos diferentes.


## Solución de problemas comunes

- **El Asistente No Responde:**
   - Asegúrese de que está trabajando activamente en un entorno compatible (Forms Manager, Editor de Forms adaptable o Editor universal).
   - Compruebe la conexión a Internet.
   - Intente cerrar y volver a abrir el panel Asistente de IA.

- **Respuestas inexactas o inesperadas:**
   - Reformule la solicitud para que sea más específica o sencilla.
   - Desglose una solicitud compleja en comandos individuales más pequeños.
   - Asegúrese de utilizar la terminología estándar de AEM Forms.

- **Problemas De Importación De Diseño (PDF/Figma/Image):**
   - Compruebe que el archivo de diseño sea claro, bien estructurado y legible.
   - Asegúrese de que el formato de archivo sea compatible (PDF, vínculo Figma, tipos de imagen comunes como PNG, JPG).
   - Para Figma, asegúrese de que el fotograma al que se dirige esté claramente definido y accesible.

- **Campo `@fieldName` No Reconocido:**
   - Compruebe el nombre exacto del campo en el formulario. Los nombres de campo distinguen entre mayúsculas y minúsculas y deben coincidir con precisión.
   - Asegúrese de que el campo ya existe si intenta modificarlo.


## Comentarios y asistencia

Su aportación es inestimable para la mejora continua del asistente de IA.

- **Proporcionar comentarios:** Use el comando o botón **&quot;Proporcionar comentarios&quot; integrado** en la interfaz del Asistente de IA para compartir sus experiencias, informar de problemas o sugerir mejoras. (por ejemplo, podría escribir `/feedback` o buscar un icono de comentarios).
- **Soporte oficial:** Para problemas críticos o para obtener más ayuda, comuníquese con los canales de soporte oficial de Adobe o con los contactos de soporte designados por su organización.


## Contenido relacionado

[Asistente de IA de AEM Forms: biblioteca de mensajes](/help/edge/docs/forms/ai-assistant-prompt-library.md)
