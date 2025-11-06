---
title: Asistente de IA para AEM Forms (Forms Experience Builder)
description: Elabore formularios potentes más rápido mediante fragmentos de formulario
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 100%

---


# Introducción al asistente de IA para AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funcionalidad del Asistente de IA para AEM Forms (Forms Experience Builder) está disponible en el **programa para primeros usuarios**. Si le interesa, envíe un correo electrónico rápido desde su dirección de trabajo a mailto:aem-forms-ea@adobe.com para solicitar el acceso a la funcionalidad.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que el asistente de IA para AEM Forms sigue evolucionando durante el programa para los primeros usuarios.

El Asistente de IA para AEM Forms transforma la creación de los formularios: basta con describir lo que se necesita en lenguaje natural y observar cómo estos se generan. Disponible en la interfaz de usuario de administración de formularios, el editor de formularios adaptables y el editor universal, conoce sus intenciones y crea exactamente lo que busca.

## Introducción: simplemente hable con él

El Asistente de IA funciona como una conversación con un colega experto. En lugar de tener que aprender menús y configuraciones complejos, simplemente describa lo que desea crear.

### Inicio rápido

Póngase en marcha rápidamente viendo nuestro vídeo introductorio:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Acceso al Asistente de IA 

Puede acceder al asistente de IA desde tres ubicaciones diferentes en AEM Forms:

1. **IU de administración de formularios**
   - Vaya a Adobe Experience Manager > Forms > Formularios y documentos.
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono para abrir el panel Asistente de IA

   ![Icono del asistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Editor de formularios adaptables**
   - Vaya a Adobe Experience Manager > Forms > Formularios y documentos.
   - Seleccione y abra un formulario para editarlo
   - Haga clic en el icono del Asistente de IA de la interfaz del editor

   ![Icono del Asistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Editor universal**

   - Vaya a Adobe Experience Manager > Forms > Formularios y documentos.
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono del Asistente de IA de la interfaz del editor

### Cómo empezar: Conversaciones simples

La mejor manera de empezar con el Asistente de IA es a través del lenguaje natural. A continuación se muestra cómo:

**Describa únicamente lo que necesita:**

- &quot;Crear un formulario de contacto para mi sitio web&quot;
- &quot;Necesito un formulario de comentarios de los clientes con escalas de valoración&quot;
- &quot;Crear un formulario de registro para mi próximo evento&quot;
- &quot;Hacer una encuesta sencilla sobre la satisfacción del producto&quot;

**Añada detalles sobre la marcha:**

- &quot;Crear un formulario de contacto con campos de nombre, correo electrónico, teléfono y mensaje&quot;
- &quot;Necesito un formulario de registro con varios pasos para una conferencia&quot;
- &quot;Crear un formulario de comentarios de clientes con clasificaciones de 5 estrellas y secciones de comentarios&quot;

**Haga referencia a los campos existentes:**

- &quot;Hacer que el campo de correo electrónico sea obligatorio&quot; (para @email)
- &quot;Añadir validación al campo de número de teléfono&quot; (para @phoneNumber)
- &quot;Mostrar la información del cónyuge solo si se ha seleccionado &quot;casado&quot; (para @spouseInfo y @maritalStatus)

### Lo que también puede hacer

Más allá del lenguaje natural, el Asistente de IA ofrece formas adicionales de interactuar:

- **Cargar archivos**: adjunte imágenes, PDF o diseños de Figma para mostrar a la IA lo que está imaginando
- **Usar comandos rápidos**: escriba `/` para ver los métodos abreviados disponibles para las acciones comunes
- **Campos específicos de referencia**: use `@fieldName` para modificar los campos de formulario existentes (por ejemplo, `@firstName`, `@emailAddress`)

## Lo que puede crear: ejemplos que funcionan

Estos son ejemplos reales de lo que se puede lograr con un lenguaje simple y natural:

### Inicio de un nuevo formulario

**Enfoque simple:**

```
"Create a contact form"
```

**Método más detallado:**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**Con referencia al diseño:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Incorporación de elementos de formulario

**Incorporaciones básicas:**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**Especificaciones detalladas:**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### Creación de un comportamiento dinámico

**Lógica simple:**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**Reglas empresariales complejas:**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### Diseño de formularios

**Cambios en el diseño:**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**Mejoras en el diseño:**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### Envío e integración

**Envío básico:**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**Integración avanzada:**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## Cómo trabajar con archivos adjuntos

Cargue archivos para ayudar a la inteligencia artificial a comprender exactamente lo que está buscando:

### Tipos de archivo admitidos

| Tipo de archivo | Ideal para | Ejemplo de uso |
|-----------|----------|-------------|
| **Imágenes** (PNG, JPG, GIF) | Diseños de formularios, maquetas de IU, digitlizaciones de formularios en papel | &quot;Crear un formulario que coincida con este diseño&quot; |
| **Archivos de PDF** | Formularios existentes para convertir, especificaciones | &quot;Convertir este formulario de PDF a digital&quot; |
| **Archivos Sigma** | Diseño de prototipos, directrices de marca | “Construir este formulario a partir de mi diseño Figma” |
| **Archivos de diseño** | Referencias visuales, guías de estilo | &quot;Hacer coincidir el estilo de este diseño&quot; |

### Cómo utilizar los archivos adjuntos

1. **Haga clic en el icono de archivo adjunto** en la interfaz del Asistente de IA
2. **Seleccione el archivo** en su equipo
3. **Describa lo que desea** haciendo referencia al archivo adjunto:
   - &quot;Crear un formulario basado en este PDF adjunto&quot;
   - &quot;Crear un formulario de contacto que coincida con el diseño de esta imagen&quot;
   - &quot;Convertir este formulario en papel a una versión digital&quot;

### Prácticas recomendadas con archivos adjuntos

- **Use imágenes claras y de alta calidad** para un mejor análisis de IA
- **Céntrese en un concepto por archivo adjunto** (diseño, estilo, etc.)
- **Describa lo que desea** junto con el archivo adjunto
- **Mantenga los archivos por debajo de 10 MB** para un procesamiento óptimo

## Sugerencias para obtener mejores resultados

### Empiece de forma sencilla y vaya avanzando

- Empiece con solicitudes básicas: &quot;Crear un formulario de contacto&quot;
- Añada detalles gradualmente: &quot;Añadir validación al campo de correo electrónico&quot;
- Pruebe y perfeccione: &quot;Hacer que el campo de teléfono sea opcional&quot;

### Sea específico cuando sea necesario

- En lugar de: &quot;Hacer que se vea bien&quot;
- Pruebe: &quot;Utilizar colores profesionales y una tipografía limpia&quot;

### Use lenguaje natural

- En lugar de: &quot;Añadir componente de entrada de texto&quot;
- Pruebe: &quot;Añadir un campo para el nombre&quot;

### Haga referencia a los elementos existentes

- Use `@fieldName` para los campos existentes: &quot;Hacer que @email sea obligatorio&quot;
- Sea específico sobre los nombres de campo: &quot;Actualizar el campo @phoneNumber&quot;

### Desglose las solicitudes complejas

- En lugar de una solicitud grande, pruebe con varias más pequeñas
- Cree su formulario paso a paso
- Pruebe cada cambio antes de pasar al siguiente

## Ayuda y aprendizaje del producto

El Asistente de IA también puede enseñarle sobre las funciones de AEM Forms:

### Formule preguntas como:

- &quot;¿Cómo se crea un formulario de varios pasos?&quot;
- &quot;¿Cuál es la diferencia entre paneles y secciones?&quot;
- &quot;¿Cómo se configuran las notificaciones por correo electrónico?&quot;
- &quot;¿Cuáles son las prácticas recomendadas para los formularios fáciles de usar en dispositivos móviles?&quot;
- &quot;¿Cómo se aplican las temáticas a los formularios?&quot;

### Obtenga ayuda sobre:

- Conceptos y terminología de AEM Forms
- Instrucciones paso a paso para funciones complejas
- Prácticas recomendadas y consideraciones
- Solución de problemas comunes

## Referencia de funciones avanzadas

Para usuarios que deseen explorar capacidades avanzadas:

### Comandos rápidos

Escriba `/` para ver los métodos abreviados disponibles:

| Comando | Función | Ejemplos |
|---------|---------|---------|
| `/create-form` | Iniciar un nuevo formulario | `/create-form customer survey` |
| `/add-form` | Añadir formulario en el editor universal | `/add-form contact form` |
| `/update-layout` | Cambiar estructura de formulario | `/update-layout wizard with 3 steps` |
| `/update-field` | Modificar propiedades de campo | `/update-field @email to be required` |
| `/create-rule` | Añadir comportamiento dinámico | `/create-rule show @spouse if married` |
| `/create-panel` | Añadir contenedores de campo | `/create-panel Personal Information` |
| `/configure-submit` | Configurar el envío de formularios | `/configure-submit to email support` |
| `/help` | Obtener ayuda | `/help multi-step forms` |

### Sintaxis de referencia de campo

Use `@fieldName` para hacer referencia a los campos existentes:

- `@firstName`: campo de nombre
- `@email`: campo de correo electrónico
- `@phoneNumber`: campo de número de teléfono
- `@dateOfBirth`: campo de fecha de nacimiento

### tipos de componentes

Utilice estos términos para obtener los mejores resultados:

- `text input`: campo de texto de línea única
- `text area`: campo de texto multilínea
- `dropdown`: lista de selección
- `checkbox`: casilla de verificación única
- `checkbox group`: varias casillas de verificación
- `radio group`: grupo de botones de opción
- `date picker`: selección de fecha
- `file upload`: archivo adjunto
- `panel`: contenedor para agrupar campos

## Resolución de problemas

### Problemas comunes y soluciones

**El Asistente de IA no responde:**

- Compruebe su conexión a Internet
- Asegúrese de que está en un entorno compatible
- Cierre y vuelva a abrir el panel Asistente de IA

**Resultados inesperados:**

- Intente reformular su solicitud de forma más específica
- Desglose las solicitudes complejas en pasos más pequeños
- Use la terminología estándar de AEM Forms

**Las referencias de campo no funcionan:**

- Compruebe que los nombres de los campos se escriben exactamente tal como aparecen
- Use la sintaxis `@fieldName` para los campos existentes
- Asegúrese de que el campo exista antes de hacer referencia a él

**Problemas de importación de diseño:**

- Verifique que los archivos sean claros y estén bien estructurados
- Use formatos compatibles (PDF, PNG, JPG, Figma)
- Asegúrese de que el tamaño del archivo sea inferior a 10 MB

## Comentarios y asistencia 

Ayúdenos a mejorar el asistente de IA:

- **Facilite comentarios**: utilice el botón de comentarios de la interfaz del Asistente de IA
- **Problemas de informe**: póngase en contacto con el servicio de asistencia de Adobe a través de los canales oficiales
- **Comparta experiencias**: sus comentarios ayudan a mejorar el asistente para todos

## Recursos relacionados

[Asistente de IA de AEM Forms: biblioteca de indicaciones](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)
