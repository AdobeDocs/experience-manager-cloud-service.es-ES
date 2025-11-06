---
title: Introducción a Forms Experience Builder
description: Aprenda los conceptos básicos de la creación de su primer formulario con tecnología de IA con Forms Experience Builder. Tutorial paso a paso con ejemplos y prácticas recomendadas.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 8%

---

# Introducción a Forms Experience Builder {#getting-started-forms-experience-builder}

Forms Experience Builder revoluciona la creación de formularios al aprovechar la IA para transformar descripciones de lenguajes naturales en formularios digitales completamente funcionales. Esta guía le ayudará a crear su primer formulario y a comprender los conceptos principales que hacen que Forms Experience Builder sea potente.

## ¿Qué es Forms Experience Builder? {#what-is-forms-experience-builder}

Forms Experience Builder es una herramienta de creación de formularios con tecnología de IA que le permite crear formularios digitales sofisticados utilizando un lenguaje conversacional. En lugar de las interfaces tradicionales de arrastrar y soltar o la codificación compleja, simplemente debe describir lo que desea y la API crea el formulario.

**Funcionalidades clave:**

* **Creación de formularios en un idioma natural**: describa los requisitos del formulario en inglés sin formato

* **Importación y conversión inteligentes**: transforme documentos existentes en formularios interactivos

* **Generación de campos inteligentes**: campos con tecnología de IA con opciones rellenadas previamente

* **Automatización de la lógica empresarial**: cree reglas condicionales y valide mediante conversación

* **Integración del sistema**: conecte los formularios a los flujos de trabajo empresariales existentes

## Requisitos previos {#prerequisites-getting-started}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* **Acceso a Forms Experience Builder** - Disponible a través del programa de acceso anticipado
* **AEM Forms as a Cloud Service**: entorno de creación de producción con componentes principales de Forms adaptable
* **Comprensión básica**: familiaridad con los conceptos de formularios y los requisitos empresariales

Para conocer los requisitos técnicos detallados y la configuración del entorno, consulte [Implementar y configurar Forms Experience Builder](deploy-forms-experience-builder.md).

## Formas de crear formularios {#two-ways-to-create-forms}

Después de usar el Asistente de Forms para seleccionar una plantilla de [componentes principales](/help/forms/creating-adaptive-form-core-components.md) o [Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md), un tema y otras opciones, Forms Experience Builder ofrece dos enfoques principales para la creación de formularios:

### &#x200B;1. Crear desde cero {#create-from-scratch}

Cree formularios utilizando las descripciones en lenguaje natural de sus necesidades.

**Cuándo usar:**

* Creación de nuevos formularios a partir de requisitos

* Crear formularios para nuevos procesos empresariales

* Cuando tiene especificaciones claras pero no hay documentos

**Ejemplo:**

    Cree un formulario de comentarios de clientes con:
    &#x200B;- Clasificación del producto (de 1 a 5 estrellas)
    &#x200B;- Campo de comentarios para comentarios detallados
    &#x200B;- Correo electrónico del cliente (opcional)
    &#x200B;- Enviar a notificación por correo electrónico

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### &#x200B;2. Importar y convertir {#import-and-convert}

Transforme los documentos existentes en formularios digitales interactivos.

Antes de utilizar esta opción, cargue el archivo PDF o una imagen del formulario. PDF puede ser un formulario de PDF basado en AcroForm o en XFA. Para [otros tipos de PDF forms](https://experienceleague.adobe.com/es/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents), use la opción [Preparar formulario](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) en Adobe Acrobat para convertirlos en un AcroForm

**Cuándo usar:**

* Conversión de PDF forms existente

* Modernización de procesos basados en papel

* Cuando ya tiene diseños de formulario para mejorar

**Ejemplo:**

    /create-form convierten el archivo PDF adjunto en un formulario adaptable

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## Su primer formulario: tutorial paso a paso {#first-form-tutorial}

Vamos a crear un formulario de contacto sencillo para comprender el flujo de trabajo básico.

### Paso 1: Comience con una descripción sencilla {#step-1-simple-description}

Comience con una descripción básica del formulario:

    Cree un formulario de contacto básico con campos de nombre, correo electrónico, teléfono y mensaje

Esto crea un formulario con tres campos esenciales.

![Formulario con tres campos esenciales: creado con el indicador de lenguaje natural](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### Paso 2: Agregar validación y requisitos {#step-2-add-validation}

Mejore el formulario con reglas de validación:

    Haga que los campos @name y @email sean obligatorios con la validación adecuada

El símbolo `@` hace referencia a campos específicos para las modificaciones de destino.

![Se agregó la validación en el generador de experiencias de formulario mediante la solicitud en lenguaje natural](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### Paso 3: Mejorar la experiencia del usuario {#step-3-improve-ux}

Añada texto de marcador de posición y directrices útiles:

    Añada texto de marcador de posición: @name “Su nombre completo”, @email “your.email@company.com”, @message “Díganos cómo podemos ayudarle”

![Se ha agregado validación mediante peticiones de datos en lenguaje natural en el generador de experiencias de formularios](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### Paso 4: Añadir funciones avanzadas {#step-4-advanced-features}

Incluya funciones adicionales:

    Agregar dos desplegables
    
    &#x200B;- queryType con opciones: &quot;Pregunta general&quot;, &quot;Solicitud de soporte&quot;, &quot;Consulta de ventas&quot;, &quot;Asociación&quot;
    
    &#x200B;- priorityLevel con opciones (Baja, Medium, Alta)


![Se ha agregado un menú desplegable de componentes utilizando indicaciones en lenguaje natural en el creador de experiencias de Forms](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### Paso 5: Implementar la lógica condicional {#step-5-conditional-logic}

Cree un comportamiento inteligente y según el contexto añadiendo reglas como las siguientes:

    Ocultar el @urgencyLevel desplegable al cargar el formulario
    Mostrar @urgencyLevel desplegable (bajo, Medium, alto) solo cuando @inquiryType igual a &quot;Solicitud de asistencia&quot;

Estas son dos reglas independientes: una oculta el menú desplegable de nivel de urgencia cuando se carga el formulario y la otra lo muestra solo cuando el tipo de consulta es &quot;Solicitud de asistencia&quot;. Debe crear cada regla con una solicitud independiente; solo se puede crear una regla a la vez.

## Explicación del enfoque de conversación de IA {#ai-conversation-approach}

Forms Experience Builder utiliza una interfaz conversacional en la que puede:

### Campos de referencia con símbolos @ {#reference-fields}

Usar `@fieldName` para hacer referencia a campos específicos:

    @email un campo obligatorio
    Agregar validación a @phoneNumber para el formato de EE.UU.
    Cambiar @submitButton texto a &quot;Enviar mensaje&quot;

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### Usar comandos de lenguaje natural {#natural-language-commands}

Describa lo que desea en un inglés sencillo:

    &#x200B;- Agregar una sección para la información de la compañía
    &#x200B;- Crear un menú desplegable para la selección de departamentos
    &#x200B;- Incluir una carga de archivo para la reanudación
    &#x200B;- Configurar notificaciones por correo electrónico cuando se envíe el formulario

### Generar gradualmente {#build-incrementally}

Empiece por lo simple y añada complejidad gradualmente:

1. **Estructura básica**: cree primero los campos esenciales
2. **Agregar validación** - Implementar campos obligatorios y validación de formato
3. **Mejorar UX**: agrega marcadores de posición, texto de ayuda y estilo
4. **Implementar lógica** - Agregar reglas condicionales y lógica empresarial
5. **Configurar envío** - Configurar procesamiento y notificaciones de formularios


## Patrones de formulario comunes {#common-form-patterns}

### Formularios de contacto y comentarios {#contact-feedback-forms}

**Formulario de contacto básico:**

    Crear un formulario de contacto con:
    &#x200B;- Nombre (obligatorio)
    &#x200B;- Correo electrónico (obligatorio, validado)
    &#x200B;- Lista desplegable de asunto (General, Soporte, Ventas, Asociación)
    &#x200B;- Mensaje (obligatorio, multilínea)
    &#x200B;- Botón de envío

**Formulario de comentarios de clientes:**

    Cree un formulario de comentarios de clientes con:
    &#x200B;- Clasificación del producto (de 1 a 5 estrellas)
    &#x200B;- Campo de comentarios para comentarios detallados
    &#x200B;- Correo electrónico del cliente (opcional)
    &#x200B;- Enviar a notificación por correo electrónico

### Formularios de registro e incorporación {#registration-onboarding-forms}

**Registro de usuario:**

    Crear un formulario de registro de usuario con:
    &#x200B;- Información personal (nombre, correo electrónico, teléfono)
    &#x200B;- Preferencias de cuenta (newsletter, notificaciones)
    &#x200B;- Aceptación de términos y condiciones
    &#x200B;- Creación de contraseña con validación de seguridad

**Incorporación de empleados:**

    Crear un formulario de incorporación de empleado con:
    &#x200B;- Datos personales e información de contacto
    &#x200B;- Información de empleo y fecha de inicio
    &#x200B;- Cargas de documentos (currículum, ID, formularios de impuestos)
    &#x200B;- Selección de beneficios y preferencias

### Formularios de encuesta y evaluación {#survey-assessment-forms}

**Encuesta de satisfacción del cliente:**

    Crear una encuesta de satisfacción del cliente con:
    &#x200B;- Clasificación general (escala 1-10)
    &#x200B;- Clasificaciones de categoría (producto, servicio, soporte técnico)
    &#x200B;- Secciones de comentarios abiertos
    &#x200B;- Información demográfica (opcional)

**Evaluación de aptitudes:**

    Crear un formulario de evaluación de aptitudes con:
    &#x200B;- Categorías de aptitudes con niveles de competencia
    &#x200B;- Duración de la experiencia para cada aptitud
    &#x200B;- Información de certificación y formación
    &#x200B;- Autoevaluación y objetivos

## Pruebas y validación {#testing-validation}

### Pruebe siempre los formularios {#always-test-forms}

Antes de implementar cualquier formulario:

1. **Probar todos los campos**: compruebe que la validación funciona correctamente

2. **Verificar lógica condicional** - Comprobar que las reglas se déclencheur correctamente

3. **Envío de prueba** - Confirmar que los datos se han procesado correctamente

4. **Validar en diferentes dispositivos** - Garantizar la compatibilidad con dispositivos móviles

5. **Revisión con las partes interesadas**: obtenga comentarios de los usuarios finales

### Patrones de validación comunes {#validation-patterns}

**Validación de correo electrónico:**

    Agregar validación de formato de correo electrónico al campo @email

**Validación de número de teléfono:**

    Agregar validación de formato de número de teléfono de EE. UU. a @phoneNumber

**Validación de edad:**

    Agregar validación de edad: debe tener 18 años o más para @dateOfBirth

**Validación de carga de archivos:**

    Agregar validación de tipo de archivo: solo se permiten PDF, DOC y DOCX para @resume
    Agregar límite de tamaño de archivo: máximo 5 MB para @resume

## Próximos pasos {#next-steps}

Ahora que comprende los conceptos básicos, explore estos temas avanzados:

* **[Campos inteligentes mejorados con LLM](forms-experience-builder-llm-smart-fields.md)**: cree campos con opciones rellenadas previamente mediante el conocimiento de IA
* **[Creación de formularios con tecnología de IA](forms-experience-builder-prompt-examples-library.md)**: patrones y ejemplos de mensajes avanzados
* **[Importación y conversión inteligentes](intelligent-import-conversion.md)**: transforme documentos existentes en formularios
* **[Envío e integración de formularios](form-submission-integration.md)**: conecte los formularios a sus sistemas empresariales


## Artículos relacionados

* [Información general sobre Forms Experience Builder](product-overview.md)
* [Campos inteligentes mejorados por LLM](forms-experience-builder-llm-smart-fields.md)
* [Creación de formularios con tecnología de IA](forms-experience-builder-prompt-examples-library.md)
* [Importación y conversión inteligentes](intelligent-import-conversion.md)
* [Envío e integración de formularios](form-submission-integration.md)
* [Preguntas frecuentes](forms-experience-builder-frequently-asked-questions.md)
