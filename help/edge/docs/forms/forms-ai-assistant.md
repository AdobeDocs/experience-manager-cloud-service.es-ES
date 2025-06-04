---
title: Asistente de IA para AEM Forms (Forms Experience Builder)
description: Elabore formularios potentes más rápido mediante fragmentos de formulario
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: a8d64082-a23f-4919-ad66-042faad77d29
source-git-commit: ab071b9159f3d4db275313080d7c14a46096c4de
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---

# Asistente de IA para AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funcionalidad Asistente de IA para AEM Forms (Forms Experience Builder) está disponible en **programa de adopción anticipada**. Si está interesado, envíe un correo electrónico rápido desde su dirección de trabajo a mailto:aem-forms-ea@adobe.com para solicitar acceso a la funcionalidad.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que el asistente de IA para AEM Forms sigue evolucionando durante el programa de los primeros usuarios.

El asistente de IA para AEM Forms transforma la forma en que se crean los formularios: basta con describir lo que se necesita en lenguaje natural y observar cómo cobran vida los formularios. Disponible en la interfaz de usuario de administración de Forms, el editor de Forms adaptable y el editor universal, comprende sus intenciones y crea exactamente lo que busca.

## Primeros pasos: Hable con él

El asistente de IA funciona como una conversación con un colega experto. En lugar de aprender menús y configuraciones complejos, simplemente describe lo que desea crear.

### Inicio rápido

Póngase en marcha rápidamente viendo nuestro vídeo introductorio:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Acceso al asistente de IA

Puede acceder al asistente de IA desde tres ubicaciones diferentes en AEM Forms:

1. **IU de administración de Forms**
   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono para abrir el panel Asistente de IA

   ![Icono de asistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Editor de Forms adaptable**
   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Seleccione y abra un formulario para editarlo
   - Haga clic en el icono Ayudante de IA de la interfaz del editor

   ![Icono de asistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Editor universal**

   - Vaya a Adobe Experience Manager > Forms > Forms y documentos
   - Busque el icono Asistente de IA en la parte izquierda de la interfaz
   - Haga clic en el icono Ayudante de IA de la interfaz del editor

### Cómo empezar: Conversaciones simples

La mejor manera de empezar con el asistente de IA es a través del lenguaje natural. A continuación se muestra cómo:

**Solo describe lo que necesitas:**

- &quot;Crear un formulario de contacto para mi sitio web&quot;
- &quot;Necesito un formulario de comentarios de clientes con escalas de valoración&quot;
- &quot;Crear un formulario de registro para mi próximo evento&quot;
- &quot;Haga una encuesta sencilla sobre la satisfacción del producto&quot;

**Agregar detalles sobre la marcha:**

- &quot;Crear un formulario de contacto con campos de nombre, correo electrónico, teléfono y mensaje&quot;
- &quot;Necesito un formulario de registro de varios pasos para una conferencia&quot;
- &quot;Cree un formulario de comentarios de clientes con clasificaciones de 5 estrellas y secciones de comentarios&quot;

**Haga referencia a los campos existentes:**

- &quot;Hacer que el campo de correo electrónico sea obligatorio&quot; (por @email)
- &quot;Agregar validación al campo de número de teléfono&quot; (por @phoneNumber)
- &quot;Mostrar la información del cónyuge solo si se selecciona casado&quot; (por @spouseInfo y @maritalStatus)

### Lo que también puede hacer

Más allá del lenguaje natural, el asistente de IA ofrece formas adicionales de interactuar:

- **Cargar archivos**: adjunta imágenes, PDF o diseños de Figma para mostrar a la IA lo que estás imaginando
- **Use comandos rápidos**: escriba `/` para ver los métodos abreviados disponibles para las acciones comunes
- **Campos específicos de referencia**: use `@fieldName` para modificar los campos de formulario existentes (por ejemplo, `@firstName`, `@emailAddress`)

## Qué Puede Crear: Ejemplos Que Funcionan

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

**Con referencia de diseño:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Adición de elementos de formulario

**Adiciones básicas:**

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

**Reglas de negocio complejas:**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### Diseño y presentación de formularios

**Cambios de diseño:**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**Mejoras de diseño:**

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

## Uso de archivos adjuntos

Cargue archivos para ayudar a la inteligencia artificial a comprender exactamente lo que está buscando:

### Tipos de archivo admitidos

| Tipo de archivo | Mejor para | Ejemplo de uso |
|-----------|----------|-------------|
| **Imágenes** (PNG, JPG, GIF) | Diseños de formularios, maquetas de IU, escaneos de formularios en papel | &quot;Crear un formulario que coincida con este diseño&quot; |
| **Archivos de PDF** | Formularios existentes para convertir, especificaciones | &quot;Convertir este formulario de PDF a digital&quot; |
| **Archivos Figma** | Diseño de prototipos, directrices de marca | &quot;Construye este formulario a partir de mi diseño Figma&quot; |
| **Archivos de diseño** | Referencias visuales, guías de estilo | &quot;Hacer coincidir el estilo de este diseño&quot; |

### Cómo utilizar archivos adjuntos

1. **Haga clic en el icono de datos adjuntos** en la interfaz del Ayudante de IA
2. **Seleccione su archivo** de su dispositivo
3. **Describa lo que desea** haciendo referencia al archivo adjunto:
   - &quot;Crear un formulario basado en este PDF adjunto&quot;
   - &quot;Crear un formulario de contacto que coincida con el diseño de esta imagen&quot;
   - &quot;Convertir este formulario en papel a una versión digital&quot;

### Prácticas recomendadas con archivos adjuntos

- **Use imágenes claras y de alta calidad** para un mejor análisis de IA
- **Céntrese en un concepto por archivo adjunto** (diseño, estilo, etc.)
- **Describa lo que desea** junto con el archivo adjunto
- **Mantener archivos de menos de 10 MB** para un procesamiento óptimo

## Sugerencias para obtener mejores resultados

### Inicio sencillo, acumulación

- Comience con solicitudes básicas: &quot;Crear un formulario de contacto&quot;
- Añadir detalles gradualmente: &quot;Añadir validación al campo de correo electrónico&quot;
- Probar y perfeccionar: &quot;Hacer que el campo de teléfono sea opcional&quot;

### Sea específico cuando sea necesario

- En lugar de: &quot;Hacer que se vea bien&quot;
- Pruebe: &quot;Utilice colores profesionales y una tipografía limpia&quot;

### Usar lenguaje natural

- En lugar de: &quot;Añadir componente de entrada de texto&quot;
- Pruebe: &quot;Añadir un campo para el nombre&quot;

### Elementos existentes de referencia

- Usar `@fieldName` para campos existentes: &quot;Hacer que el @email sea obligatorio&quot;
- Sea específico sobre los nombres de campo: &quot;Actualizar el campo @phoneNumber&quot;

### Desglose de solicitudes complejas

- En lugar de una solicitud grande, pruebe con varias más pequeñas
- Cree su formulario paso a paso
- Pruebe cada cambio antes de pasar al siguiente

## Ayuda y aprendizaje del producto

El asistente de IA también puede enseñarle sobre las funciones de AEM Forms:

### Hacer preguntas como:

- &quot;¿Cómo se crea un formulario de varios pasos?&quot;
- &quot;¿Cuál es la diferencia entre paneles y secciones?&quot;
- &quot;¿Cómo configuro las notificaciones por correo electrónico?&quot;
- &quot;¿Cuáles son las mejores prácticas para los formularios fáciles de usar en dispositivos móviles?&quot;
- &quot;¿Cómo se aplican las temáticas a los formularios?&quot;

### Obtener Ayuda Sobre:

- Conceptos y terminología de AEM Forms
- Instrucciones paso a paso para funciones complejas
- Prácticas recomendadas y recomendaciones
- Solución de problemas comunes

## Referencia de funciones avanzadas

Para usuarios que deseen explorar capacidades avanzadas:

### Comandos rápidos

Escriba `/` para ver los métodos abreviados disponibles:

| Comando | Función | Ejemplos |
|---------|---------|---------|
| `/create-form` | Iniciar un formulario nuevo | `/create-form customer survey` |
| `/add-form` | Agregar formulario en el editor universal | `/add-form contact form` |
| `/update-layout` | Cambiar estructura de formulario | `/update-layout wizard with 3 steps` |
| `/update-field` | Modificar propiedades del campo | `/update-field @email to be required` |
| `/create-rule` | Añadir comportamiento dinámico | `/create-rule show @spouse if married` |
| `/create-panel` | Agregar contenedores de campo | `/create-panel Personal Information` |
| `/configure-submit` | Configurar el envío de formularios | `/configure-submit to email support` |
| `/help` | Obtener ayuda | `/help multi-step forms` |

### Sintaxis de referencia de campo

Usar `@fieldName` para hacer referencia a campos existentes:

- `@firstName` - Campo de nombre
- `@email` - Campo de correo electrónico
- `@phoneNumber` - Campo de número de teléfono
- `@dateOfBirth` - Campo de fecha de nacimiento

### Tipos de componentes

Utilice estos términos para obtener los mejores resultados:

- `text input` - Campo de texto de una sola línea
- `text area` - Campo de texto multilínea
- `dropdown` - Seleccionar lista
- `checkbox` - Una casilla de verificación
- `checkbox group` - Varias casillas de verificación
- `radio group` - Grupo de botones de opción
- `date picker` - Selección de fecha
- `file upload` - Archivo adjunto
- `panel`: contenedor para agrupar campos

## Solución de problemas

### Problemas comunes y soluciones

**El Asistente de IA no responde:**

- Compruebe su conexión a Internet
- Asegúrese de que está en un entorno compatible
- Cierre y vuelva a abrir el panel Ayudante de IA

**Resultados inesperados:**

- Intente reformular la solicitud más específicamente
- Desglose las solicitudes complejas en pasos más pequeños
- Uso de la terminología estándar de AEM Forms

**Las Referencias De Campo No Funcionan:**

- Comprobar que los nombres de los campos se escriban exactamente como aparecen
- Usar sintaxis `@fieldName` para campos existentes
- Asegúrese de que el campo exista antes de hacer referencia a él

**Problemas de importación de diseño:**

- Verifique que los archivos sean claros y estén bien estructurados
- Usar formatos compatibles (PDF, PNG, JPG, Figma)
- Asegúrese de que el tamaño del archivo sea inferior a 10 MB

## Comentarios y asistencia

Ayúdenos a mejorar el asistente de IA:

- **Proporcionar comentarios**: utilice el botón de comentarios de la interfaz del Asistente de IA
- **Problemas del informe**: Póngase en contacto con el soporte técnico de Adobe a través de canales oficiales
- **Compartir experiencias**: tus datos ayudan a mejorar el asistente para todos

## Recursos relacionados

[Asistente de IA de AEM Forms: biblioteca de mensajes](/help/edge/docs/forms/ai-assistant-prompt-library.md)
