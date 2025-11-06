---
title: Implementación y configuración de Forms Experience Builder
description: Aprenda a utilizar Forms Experience Builder para crear y administrar formularios con divulgación progresiva para todos los tipos de usuarios
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 977f227e-e941-4797-ba74-53d5b8c60ca9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 74%

---

# Implementación y configuración de Forms Experience Builder

>[!NOTE]
>
> Forms Experience Builder está disponible en un programa de acceso anticipado. Antes de empezar, asegúrese de que ha solicitado y de que se le ha concedido acceso. Para obtener instrucciones completas, consulte la información de [Incorporación](product-overview.md#onboarding) .

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de acceso anticipado.

Esta guía completa le ayuda a empezar a crear y administrar formularios mediante la tecnología de IA conversacional. Tanto si no tiene experiencia y desea crear su primer formulario, como si tiene conocimientos avanzados y desea aprovechar las sofisticadas funciones, encontrará información detallada y ejemplos prácticos que le guiarán a través de las funcionalidades de Forms Experience Builder.

## Requisitos previos y configuración

### Requisitos de acceso

Antes de usar Forms Experience Builder, asegúrese de lo siguiente:

* **Acceso a Forms Experience Builder** - Disponible a través del programa de acceso anticipado
* **AEM Forms as a Cloud Service**: entorno de creación de producción con componentes principales de Forms adaptable
* **Comprensión básica**: familiaridad con los conceptos de formularios y los requisitos empresariales

### Verificar que los formularios estén habilitados

Antes de usar Forms Experience Builder, asegúrese de que [AEM Forms está habilitado para su entorno](/help/forms/setup-forms-cloud-service.md).

### Configurar su entorno

El proceso de configuración depende de la implementación de AEM Forms. Elija la ruta que coincida con su proyecto.

**Para Edge Delivery Services**

Si utiliza Edge Delivery Services Forms y, principalmente, utiliza el editor universal. [Prepare su proyecto para Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md). Se trata de una configuración única para habilitar Forms Experience Builder.

**Para formularios basados en componentes principales**

Si usa Forms adaptable basado en componentes principales en el entorno de creación de AEM, asegúrese de que [los componentes principales de Forms adaptable estén habilitados](/help/forms/enable-adaptive-forms-core-components.md) para su entorno.



## Inicio rápido

### Acceso al generador de experiencias de Forms

Puede acceder a Forms Experience Builder desde tres ubicaciones principales, según el flujo de trabajo y el tipo de formulario.


**1. Editor de Forms adaptable (para componentes principales)**

Puede iniciar el generador directamente mientras edita un formulario específico.

1. Vaya a **AEM > Forms > Forms y documentos**.
1. [Cree un nuevo formulario con una plantilla de componentes principales](/help/forms/creating-adaptive-form-core-components.md) o abra uno existente.
1. Seleccione el icono **Forms Experience Builder** en la barra de herramientas del editor para abrir la interfaz conversacional.

   ![Icono del asistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

**1. Editor universal (para Edge Delivery Services Forms)**

Para los formularios enviados mediante Edge Delivery Services, el generador está integrado en el editor universal.

1. Abra el formulario de Edge Delivery Services en el editor universal.
2. Seleccione el icono **Forms Experience Builder** en el panel derecho para iniciar la interfaz conversacional.

### Su primer formulario

| Ejemplo de conversación |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Intente esta conversación para crear un formulario de contacto completo (basado en la demostración de la Cumbre):**<br><br>**Usted:** “Crea un formulario de contacto para capturar información personal, como el nombre completo, la dirección de correo electrónico, el número de teléfono, el nombre de la empresa, el puesto y un campo de mensaje para consultas”<br><br>**IA:** seleccione una plantilla<br>    Lista desplegable para seleccionar una plantilla <br><br>**IA:** seleccione un tema<br>    Menú desplegable para seleccionar un tema <br><br>**IA:** crear formulario | ![Su primer formulario](/help/edge/docs/forms/assets/create-form.png) |
| <br>**IA:** abrir formulario creado | </br> El formulario se crea y se abre en el editor |


### Comandos esenciales

| Símbolo | Función | Uso de ejemplo |
|--------|---------|---------------|
| `/` | Acciones rápidas y métodos abreviados | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Hacer referencia a campos de formulario existentes | `@email`, `@firstName`, `Make @phoneNumber required` |
| Texto sin formato | Conversación natural | “Añade un campo de número de teléfono requerido”, “Crea una validación para correo electrónico” |

**Ejemplos de comandos específicos:**

* `/create-form customer survey` - Crea un nuevo formulario de encuesta a clientes
* `/add-field @email validation` - Añade validación al campo de correo electrónico existente
* `/create-rule show @spouse if @maritalStatus equals married` - Crea una lógica condicional
* `/configure-submit to email support@company.com` - Configura el envío de correo electrónico
* `/help multi-step forms` - Obtiene ayuda sobre la creación de formularios de varios pasos

### Sugerencias de éxito

* **Sea específico**: “Añadir un campo de correo electrónico obligatorio con validación” funciona mejor que “añadir correo electrónico”
* **Haga referencia a campos existentes**: usar `@fieldName` al modificar formularios
* **Pedir ayuda**: escriba `/help` seguido de su pregunta
* **Iterar**: realice un cambio cada vez para obtener mejores resultados


## Formas de empezar a crear un formulario

### Comience con las indicaciones de lenguaje natural

Describa los requisitos de los formularios en lenguaje natural y Forms Experience Builder generará la estructura completa del formulario:

**Ejemplos:**

* &quot;Crear un formulario de solicitud de préstamo con información personal, detalles financieros y cargas de documentos&quot;
* “Crear un formulario de comentarios de los clientes con valoraciones, comentarios y categorías de productos”
* “Necesito un formulario de registro con varios pasos para una conferencia con procesamiento de pagos”


### Interacciones clave

#### Adición de elementos de formulario

**Incorporaciones básicas:**

    👤 Usted: “añade una sección para información personal”
    👤 Usted: “incluye una carga de archivo para la reanudación”
    👤 Usted: “añade un menú desplegable para la selección de país”

**Especificaciones detalladas:**

    👤 Usted: “añade un panel de información personal con campos para nombre completo, fecha de nacimiento, número de teléfono y dirección de correo electrónico”
    👤 Usted: “incluye un componente de carga de archivos seguro para documentos, limitado a archivos de PDF de menos de 5 MB”
    👤 Usted: “añade un menú desplegable de país con opciones para EE. UU., Canadá, Reino Unido y Alemania”

#### Creación de un comportamiento dinámico

**Lógica simple:**

    👤 Usted: “Muestra campos adicionales cuando se selecciona &#39;Otro&#39;”
    🤖 IA: “Se creó una regla condicional que muestra campos adicionales cuando se elige &#39;Otro&#39;”
    
    👤 Usted: “Haz que el campo de correo electrónico sea obligatorio”
    🤖 IA: “Se ha actualizado el campo de correo electrónico para que sea obligatorio con la validación&quot;
    
    👤 Usted: “Calcula el total automáticamente”
    🤖 IA: “Se ha añadido la lógica de cálculo para calcular los totales automáticamente”

**Reglas empresariales complejas:**

    👤 Usted: “Muestra los campos de información del cónyuge solamente cuando el estado civil está establecido en &#39;Casado&#39;”
    🤖 IA: “Se creó una regla condicional que muestra los campos del cónyuge basados en el estado civil”
    
    👤 Usted: “Calcula el costo total multiplicando la cantidad y el precio, luego añade el 10 % de impuestos”
    🤖 IA: “Se añadió la lógica de cálculo con el cálculo de cantidad, precio e impuestos”
    
    👤 Usted: “Habilita el botón de envío solo cuando se completan todos los campos obligatorios y se aceptan los términos”
    🤖 IA: “Se creó la lógica de validación que permite el envío solo cuando se cumplen todas las condiciones”

#### Diseño y presentación del formulario

**Cambios en el diseño:**

    👤 Usted: “Convierte este formulario en un formulario de varios pasos”
    🤖 IA: “Se convirtió el formulario en un diseño progresivo con navegación”
    
    👤 Usted: “Organiza campos en dos columnas”
    🤖 IA: “Se actualizó el diseño para mostrar campos en una disposición de dos columnas”
    
    👤 Usted: “Conviértelo en un diseño de acordeón”
    🤖 IA: “Se transformó el formulario para utilizar secciones de estilo de acordeón”

**Mejoras en el diseño:**

    👤 Usted: “Crea un formulario de estilo asistente con 3 pasos: información personal, preferencias y revisión”
    🤖 IA: “Se creó un formulario de asistente con tres pasos y navegación distintos”
    
    👤 Usted: “Organiza los campos de dirección en un diseño compacto de dos columnas”
    🤖 IA: “Campos de dirección organizados en un formato compacto de dos columnas”
    
    👤 Usted: “Actualiza el diseño para que coincida con la malla metálica adjunta”
    🤖 IA: “Se ha modificado el diseño para que coincida con la referencia de diseño proporcionada”

### Enviar configuración

Forms Experience Builder puede configurar varios puntos finales de envío para conectar los formularios con sistemas y servicios externos:

| Tipo de acción de envío | Comando de configuración | Caso práctico |
|------------------|---------------|----------|
| **Correo electrónico** | “Enviar formulario al correo electrónico” | Notificaciones y confirmaciones para envíos de formularios |
| **API DE REST** | “Enviar al punto final REST” | Aplicaciones personalizadas y sistemas de terceros |
| **Almacenamiento en la nube** | “Guardar en Azure/SharePoint” | Almacenamiento de documentos y administración de archivos |
| **Flujo de trabajo** | “Enviar a Power Automate” | Automatización de procesos empresariales y aprobaciones |
| **Marketing** | “Integrar con Marketo” | Gestión de posibles clientes y automatización de marketing |

**Ejemplos de configuración de envío avanzada:**

    👤 Usted: “Envía envíos de formularios a hr@company.com y crea un caso en nuestro sistema CRM”
    🤖 IA: “Envío de correo electrónico configurado y acción de envío de CRM”
    
    👤 Usted: “Envía datos a nuestro punto final de API de REST y activa el nuevo flujo de trabajo del cliente”
    🤖 IA: “Configurado el envío de API de REST con activadores de flujo de trabajo”
    
    👤 Usted: “Envía respuestas por correo electrónico al equipo de ventas y añade el posible cliente a nuestra plataforma de automatización de marketing”
    🤖 IA: “Envío multicanal configurado con automatización de correo electrónico y marketing”





## Operaciones de formulario avanzadas


### Creación de reglas complejas

Cree una lógica empresarial y de validación sofisticada que responda a las interacciones del usuario y garantice la integridad de los datos:

    👤 Usted: “Muestra la sección de direcciones solo si el usuario selecciona &#39;Enviar a otra dirección&#39;”
    🤖 IA: “Se creó una regla condicional que muestra/oculta el panel de direcciones según la selección de la casilla de verificación”

### Creación de formularios de varios pasos

    👤 Usted: “Crea un formulario progresivo con 3 pasos: información personal, preferencias, confirmación”
    🤖 IA: “Se creó un formulario progresivo con navegación entre pasos y validación en cada fase”

### Tipos de campo avanzados

* Carga de archivos con validación y restricciones de tamaño para la administración de documentos
* Selectores de fechas con restricciones y reglas empresariales para la programación
* Listas desplegables con opciones dinámicas que cambian según las selecciones de los usuarios
* Botones de opción con lógica condicional para árboles de decisión complejos


### Conversión de PDF a formulario

    👤 Usted: “Convierte este PDF en un formulario interactivo”
    🤖 IA: “Se analizó el PDF y se creó un formulario con los tipos de campo y la validación adecuados”





## Ayuda y aprendizaje sobre productos

Forms Experience Builder también puede enseñarle las funciones de AEM Forms:

### Haga preguntas como:

* &quot;¿Cómo se crea un formulario de varios pasos?&quot;
* &quot;¿Cuál es la diferencia entre paneles y secciones?&quot;
* &quot;¿Cómo se configuran las notificaciones por correo electrónico?&quot;
* &quot;¿Cuáles son las prácticas recomendadas para los formularios fáciles de usar en dispositivos móviles?&quot;
* &quot;¿Cómo se aplican las temáticas a los formularios?&quot;

### Obtener ayuda sobre:

* Conceptos y terminología de AEM Forms
* Instrucciones paso a paso para funciones complejas
* Prácticas recomendadas y consideraciones
* Solución de problemas comunes


Para obtener soporte adicional, consulte la [Biblioteca de indicaciones de Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md) principal o póngase en contacto con el administrador del sistema para recibir asistencia técnica.
