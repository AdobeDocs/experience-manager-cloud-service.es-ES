---
title: Introducción a Forms Experience Builder
description: Aprenda a utilizar Forms Experience Builder para crear y administrar formularios con divulgación progresiva para todos los tipos de usuarios
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 6%

---


# Introducción a Forms Experience Builder

>[!NOTE]
>
> La funcionalidad Forms Experience Builder está disponible en el **programa de acceso anticipado (EA)**. Si está interesado, envíe un mensaje de correo electrónico rápido desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso a la funcionalidad.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que Forms Experience Builder continúa evolucionando durante el programa de acceso anticipado.

Esta guía completa le ayuda a empezar a crear y administrar formularios mediante la tecnología de IA conversacional. Tanto si es un principiante que busca crear su primer formulario como si es un usuario avanzado que busca aprovechar las sofisticadas funciones, encontrará información detallada y ejemplos prácticos para guiar a su recorrido a través de las funcionalidades de Forms Experience Builder.

## Requisitos previos y configuración

### &#x200B;1. Solicitar acceso

Forms Experience Builder está disponible actualmente como parte del programa de acceso anticipado (EA). Para participar y obtener acceso, necesitará la siguiente información:

**Información necesaria**

- **ID de organización de IMS**: su identificador de organización de Adobe
- **ID de programa**: el identificador de programa específico dentro de Adobe Experience Cloud
- **Detalles del proyecto**: escala de tiempo, ámbito y casos de uso previstos
- **Correo electrónico de trabajo oficial**: asociado a la cuenta de Adobe de su organización

**Cómo obtener el ID de organización de IMS y el ID de programa**

Para ver los pasos detallados para localizar el ID de organización de IMS y el ID de programa, consulte:

- [Guía de configuración de Adobe Experience Cloud Organization](/help/onboarding/cloud-manager-introduction.md)
- [Administración de programas y entornos](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

**Solicitar acceso**

1. Recopile su ID de organización de IMS y el ID de programa mediante las guías anteriores
2. Enviar un correo electrónico a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso
3. Incluya en su solicitud:
   - Nombre de organización e ID de organización de IMS
   - ID de programa
   - Cronología y ámbito del proyecto
   - Casos de uso previstos y objetivos empresariales

>[!IMPORTANT]
>
> **Programa de disponibilidad limitada**: el acceso a Forms Experience Builder está sujeto a la aprobación de los interesados internos. Adobe revisará su solicitud en función de la capacidad del programa y la alineación con los criterios de Acceso anticipado. La aprobación no está garantizada y depende de la disponibilidad actual del programa.

### &#x200B;2. Compruebe que Forms está activado

Antes de usar Forms Experience Builder, asegúrate de que [AEM Forms está habilitado para tu entorno](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurar el entorno


- **Para Edge Delivery Services (EDS):**

   - [Configuración del entorno para Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   - [Crear un nuevo formulario con la plantilla de Edge Delivery Forms](/help/edge/docs/forms/universal-editor/create-forms.md)

- **Para formularios basados en componentes principales:**

   - En la instancia de Adobe Experience Manager, acceda a Forms > Forms y documentos
   - [Crear una nueva página con la plantilla de componentes principales](/help/forms/creating-adaptive-form-core-components.md)


## Inicio rápido

### Acceso a Forms Experience Builder

Forms Experience Builder está disponible en la interfaz de usuario de administración de Forms, en el editor universal y en el editor de Forms adaptable. Puede utilizar cualquiera de estos métodos para acceder al formulario:

**IU de administración de Forms (para componentes principales)**

1. **Vaya a Forms**: Vaya a AEM > Forms > Forms y documentos
1. Haga clic en el icono de Forms Experience Builder en la barra de herramientas. Se encuentra cerca de la parte superior izquierda de la interfaz de usuario.
   ![Icono del asistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}
1. Comience la creación de su formulario conversacional


**Editor de Forms adaptable (para componentes principales)**

1. Vaya a AEM > Forms > Forms y documentos
2. [Crear un nuevo formulario con la plantilla Componentes principales](/help/forms/creating-adaptive-form-core-components.md)
3. Abra el formulario para editarlo
4. Haga clic en el icono de Forms Experience Builder en la barra de herramientas del editor
   ![Icono del asistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

5. Comience la creación de su formulario conversacional


**Editor universal (para Edge Delivery Services Forms)**

1. Siga la [guía de configuración de Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) para crear su página EDS
1. Navegue hasta la página EDS en el editor universal
1. Busque el icono de Forms Experience Builder en el panel derecho
1. Haga clic para abrir la interfaz de conversación



### Su primer formulario

| Ejemplo de conversación |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Intente esta conversación para crear un formulario de contacto completo (basado en la demostración de la Cumbre):**<br><br>**Usted:** &quot;Cree un formulario de contacto para capturar información personal, como el nombre completo, la dirección de correo electrónico, el número de teléfono, el nombre de la empresa, el puesto y un campo de mensaje para consultas&quot;<br><br>**AI:** Seleccione una plantilla<br>    Lista desplegable para seleccionar una plantilla <br><br>**AI:** Seleccione un tema<br>    Menú desplegable para seleccionar un tema <br><br>**IA:** Crear formulario | ![Su primer formulario](/help/edge/docs/forms/assets/create-form.png) |
| <br>**AI:** Abrir formulario creado | </br> El formulario se crea y se abre en el editor |


### Comandos esenciales

| Símbolo | Función | Uso de ejemplo |
|--------|---------|---------------|
| `/` | Acciones rápidas y métodos abreviados | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Hacer referencia a campos de formulario existentes | `@email`, `@firstName`, `Make @phoneNumber required` |
| Texto sin formato | Conversación natural | &quot;Agregar un campo de número de teléfono requerido&quot;, &quot;Crear validación para correo electrónico&quot; |

**Ejemplos de comandos específicos:**

- `/create-form customer survey` - Crea un nuevo formulario de encuesta a clientes
- `/add-field @email validation` - Agrega validación al campo de correo electrónico existente
- `/create-rule show @spouse if @maritalStatus equals married` - Crea una lógica condicional
- `/configure-submit to email support@company.com` - Configura el envío de correo electrónico
- `/help multi-step forms`: obtiene ayuda sobre la creación de formularios de varios pasos

### Sugerencias para alcanzar el éxito

- **Sea específico**: &quot;Agregar un campo de correo electrónico requerido con validación&quot; funciona mejor que &quot;agregar correo electrónico&quot;
- **Hacer referencia a campos existentes**: usar `@fieldName` al modificar formularios
- **Pedir ayuda**: escriba `/help` seguido de su pregunta
- **Iterar**: realice un cambio a la vez para obtener mejores resultados


## Formas de empezar a crear un formulario

### &#x200B;1. Comience con las instrucciones en lenguaje natural

Describa los requisitos de los formularios en lenguaje natural y Forms Experience Builder generará la estructura completa del formulario:

**Ejemplos:**

- &quot;Crear un formulario de solicitud de préstamo con información personal, detalles financieros y cargas de documentos&quot;
- &quot;Cree un formulario de comentarios de clientes con clasificaciones, comentarios y categorías de productos&quot;
- &quot;Necesito un formulario de registro de varios pasos para una conferencia con procesamiento de pagos&quot;

### &#x200B;2. Importar y convertir

Transforme formularios y documentos existentes en experiencias modernas e interactivas:

**Fuentes compatibles:**

- **PDF forms**: cargue archivos PDF estáticos para convertirlos en formularios digitales interactivos con validaciones.
- **Capturas de pantalla o imágenes**: cargue una foto de formularios en papel para generar versiones digitales funcionales
- **XFA Forms**: convierta formularios basados en XFA heredados a formularios adaptables modernos

**Cómo importar:**

1. Haga clic en el icono de datos adjuntos en la interfaz de Forms Experience Builder
2. Cargue el archivo (PDF, imagen, diseño Figma, etc.)
3. Describa sus necesidades:
   - &quot;Convertir este formulario de PDF a una versión digital&quot;
   - &quot;Crear un formulario que coincida con este diseño de captura de pantalla&quot;
   - &quot;Construir este formulario a partir de mi diseño Figma&quot;

**Tipos de archivo compatibles:**

- **Imágenes** (PNG, JPG, GIF): diseños de formulario, maquetas de interfaz de usuario, formularios escaneados, bocetos dibujados a mano
- **Archivos de PDF**: formularios, especificaciones, documentos, AcroForms y formularios XFA existentes
- **Capturas de pantalla**: Capturas de pantalla de aplicaciones de escritorio/móviles, fotos de formularios en papel, bocetos de pizarra electrónica
- **Bocetos dibujados a mano**: bocetos de servilleta, mallas metálicas, dibujos conceptuales (fotografiados)

### Interacciones clave

#### Incorporación de elementos de formulario

**Incorporaciones básicas:**

    👤 Usted: &quot;Agregar una sección para información personal&quot;
    👤 Usted: &quot;Incluir una carga de archivo para la reanudación&quot;
    👤 Usted: &quot;Agregar un menú desplegable para la selección de país&quot;

**Especificaciones detalladas:**

    👤 Usted: &quot;Agregar un panel de información personal con campos para nombre completo, fecha de nacimiento, número de teléfono y dirección de correo electrónico&quot;
    👤 Usted: &quot;Incluir un componente de carga de archivos seguro para documentos, limitado a archivos de PDF de menos de 5 MB&quot;
    👤 Usted: &quot;Agregar un menú desplegable de país con opciones para EE. UU., Canadá, Reino Unido y Alemania&quot;

#### Creación de un comportamiento dinámico

**Lógica simple:**

    👤 Usted: &quot;Mostrar campos adicionales cuando se selecciona &#39;Otro&#39;&quot;
    🤖 AI: &quot;Se creó una regla condicional que muestra campos adicionales cuando se elige &#39;Otro&#39;&quot;
    
    👤 Usted: &quot;Hacer que el campo de correo electrónico sea obligatorio&quot;
    🤖 AI: &quot;Se ha actualizado el campo de correo electrónico para que sea necesario con la validación&quot;
    
    👤 Usted: &quot;Calcular el total automáticamente&quot;
    🤖 AI: &quot;Se ha agregado la lógica de cálculo para calcular los totales automáticamente&quot;

**Reglas empresariales complejas:**

    👤 Usted: &quot;Mostrar los campos de información del cónyuge solamente cuando el estado civil está establecido en &#39;Casado&#39;&quot;
    🤖 AI: &quot;Se creó una regla condicional que muestra los campos del cónyuge basados en el estado civil&quot;
    
    👤 Usted: &quot;Calcula el costo total multiplicando la cantidad y el precio, luego agrega el 10% de impuestos&quot;
    🤖 AI: &quot;Se agregó la lógica de cálculo con el cálculo de cantidad, precio e impuestos&quot;
    
    👤 Usted: &quot;Habilita el botón de envío solo cuando se completan todos los campos obligatorios y se aceptan los términos&quot;
    🤖 AI: &quot;Se creó la lógica de validación que permite el envío solo cuando se cumplen todas las condiciones&quot;

#### Diseño de formularios

**Cambios en el diseño:**

    👤 Usted: &quot;Convertir este formulario en un formulario de varios pasos&quot;
    🤖 AI: &quot;Se convirtió el formulario en un diseño progresivo con navegación&quot;
    
    👤 Usted: &quot;Organizar campos en dos columnas&quot;
    🤖 AI: &quot;Se actualizó el diseño para mostrar campos en una disposición de dos columnas&quot;
    
    👤 Usted: &quot;Convertir en un diseño de acordeón&quot;
    🤖 AI: &quot;Se transformó el formulario para utilizar secciones de estilo de acordeón&quot;

**Mejoras en el diseño:**

    👤 Usted: &quot;Crear un formulario de estilo asistente con 3 pasos: información personal, preferencias y revisión&quot;
    🤖 AI: &quot;Se creó un formulario de asistente con tres pasos y navegación distintos&quot;
    
    👤 Usted: &quot;Organizar los campos de dirección en un diseño compacto de dos columnas&quot;
    🤖 AI: &quot;Campos de dirección organizados en un formato compacto de dos columnas&quot;
    
    👤 Usted: &quot;Actualizar el diseño para que coincida con el modelo de alambres adjunto&quot;
    🤖 AI: &quot;Se ha modificado el diseño para que coincida con la referencia de diseño proporcionada&quot;

### Configuración de envío

Forms Experience Builder puede configurar varios extremos de envío para conectar los formularios con sistemas y servicios externos:

| Tipo de acción de envío | Comando de instalación | Caso práctico |
|------------------|---------------|----------|
| **Correo electrónico** | &quot;Enviar formulario al correo electrónico&quot; | Notificaciones y confirmaciones para envíos de formularios |
| **API DE REST** | &quot;Enviar al punto final REST&quot; | Aplicaciones personalizadas y sistemas de terceros |
| **Almacenamiento en la nube** | &quot;Guardar en Azure/SharePoint&quot; | Almacenamiento de documentos y administración de archivos |
| **Flujo de trabajo** | &quot;Conectarse a Power Automate&quot; | Automatización y aprobaciones de procesos empresariales |
| **Marketing** | &quot;Integración con Marketo&quot; | Administración de posibles clientes y automatización de marketing |

**Ejemplos de configuración de envío avanzada:**

    👤 Usted: &quot;Enviar envíos de formularios a hr@company.com y crear un caso en nuestro sistema CRM&quot;
    🤖 AI: &quot;Envío de correo electrónico configurado y acción de envío de CRM&quot;
    
    👤 Usted: &quot;Enviar datos a nuestro extremo de API de REST y déclencheur el nuevo flujo de trabajo del cliente&quot;
    🤖 AI: &quot;Configurar el envío de API de REST con déclencheur de flujo de trabajo&quot;
    
    👤 Usted: &quot;Enviar respuestas por correo electrónico al equipo de ventas y agregar el posible cliente a nuestra plataforma de automatización de marketing&quot;
    🤖 AI: &quot;Envío multicanal configurado con automatización de correo electrónico y marketing&quot;





## Operaciones de formulario avanzadas


### Creación de reglas complejas

Cree una lógica empresarial y de validación sofisticada que responda a las interacciones del usuario y garantice la integridad de los datos:

    👤 Usted: &quot;Mostrar la sección de direcciones solo si el usuario selecciona &#39;Enviar a otra dirección&#39;&quot;
    🤖 AI: &quot;Se creó una regla condicional que muestra/oculta el panel de direcciones según la selección de la casilla de verificación&quot;

### Creación de formularios de varios pasos

    👤 Usted: &quot;Crear un formulario progresivo con 3 pasos: información personal, preferencias, confirmación&quot;
    🤖 AI: &quot;Se creó un formulario progresivo con navegación entre pasos y validación en cada fase&quot;

### Tipos de campo avanzados

- Carga de archivos con restricciones de validación y tamaño para la administración de documentos
- Selector de fechas con restricciones y reglas de negocio para la programación
- Lista desplegable con opciones dinámicas que cambian según las selecciones de los usuarios
- Botones de opción con lógica condicional para árboles de decisión complejos


### Conversión de PDF a formulario

    👤 Usted: &quot;Convertir este PDF en un formulario interactivo&quot;
    🤖 AI: &quot;Analizó el PDF y creó un formulario con los tipos de campo y la validación adecuados&quot;





## Ayuda y aprendizaje del producto

Forms Experience Builder también puede enseñarle sobre las funciones de AEM Forms:

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

## Prácticas recomendadas

### Diseño de formulario

- **Simplifique**: Comience con campos esenciales y agregue complejidad solo cuando sea necesario para evitar abrumar a los usuarios
- **Use etiquetas claras**: haga que los propósitos de los campos sean obvios con etiquetas descriptivas que guíen a los usuarios a través del formulario
- **Proporcionar texto de ayuda**: guíe a los usuarios a través de campos complejos con ayuda contextual y ejemplos
- **Realizar pruebas exhaustivas**: valide todas las rutas de usuario para asegurarse de que los formularios funcionan correctamente en todos los escenarios

### Experiencia del usuario

- **Divulgación progresiva**: mostrar campos relevantes basados en el contexto para reducir la carga cognitiva y mejorar las tasas de finalización
- **Borrar navegación**: Ayude a los usuarios a comprender dónde se encuentran en el formulario y qué pasos quedan por realizar
- **Diseño interactivo**: compruebe que los formularios funcionan en todos los dispositivos y tamaños de pantalla para lograr la máxima accesibilidad
- **Accesibilidad**: siga las directrices de WCAG para que las personas con discapacidades puedan utilizar los formularios

### Rendimiento

- **Optimizar recuento de campos**: solo pida la información necesaria para reducir el abandono de formularios y mejorar las tasas de finalización
- **Use la validación apropiada**: Evite errores antes del envío para proporcionar comentarios y orientación inmediatos
- **Tasas de finalización de pruebas**: supervise y mejore la efectividad de los formularios mediante análisis y comentarios de los usuarios
- **Actualizaciones regulares**: mantenga los formularios al día con las necesidades de la empresa y las expectativas de los usuarios para obtener un rendimiento óptimo

### Coherencia de marca

- **Crear plantillas de marca**: prepare plantillas de formulario con marca con los colores, las fuentes y el estilo de su organización antes de comenzar a crear formularios
- **Definir estándares de estilo**: establezca estilos de botón, diseños de campo y directrices de espaciado coherentes a los que se pueda hacer referencia en las solicitudes
- **Usar recursos de marca**: prepare logotipos, códigos de color y directrices de marca para facilitar la referencia al crear formularios
- **Biblioteca de plantillas**: genere una colección de plantillas de formulario de marca para casos de uso comunes (contacto, registro, comentarios)
- **Instrucciones de estilo**: Incluir instrucciones específicas de la marca: &quot;Usar azul de la compañía (#1234AB) para botones y fuentes corporativas Helvetica&quot;



## Resolución de problemas

| Problema | Corrección rápida |
|-------|-----------|
| **La interfaz no se carga** | Actualice el explorador, compruebe la conexión a Internet |
| **Los comandos no funcionan** | `/help` o use lenguaje natural en su lugar |
| **@fieldName no reconocido** | Revise la ortografía, asegúrese de que el campo exista primero |
| **Error al cargar el archivo** | Utilice PDF/JPG/PNG con menos de 10 MB |
| **El formulario tiene un aspecto incorrecto** | Sea más específico: &quot;Hacerlo compatible con dispositivos móviles&quot; |
| **Error en la configuración de envío** | Verificar las credenciales y los permisos de API |

**¿Aún necesita ayuda?** escriba `/help` seguido de su pregunta específica o comuníquese con el administrador del sistema.

Para obtener soporte adicional, consulte la [Biblioteca de mensajes de Forms Experience Builder](ai-assistant-prompt-library.md) principal o póngase en contacto con el administrador del sistema para obtener asistencia técnica.
