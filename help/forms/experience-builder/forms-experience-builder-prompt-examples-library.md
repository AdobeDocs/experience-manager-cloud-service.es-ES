---
title: 'Forms Experience Builder: biblioteca de indicaciones'
description: Colección de patrones de indicaciones probadas y ejemplos para crear formularios con la asistencia de IA en la IU para la administración de formularios, el editor de formularios adaptables y el editor universal.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 38%

---


# Forms Experience Builder: biblioteca de indicaciones

Colección de patrones de indicaciones reutilizables y ejemplos optimizados para Forms Experience Builder. Esta biblioteca optimizada se centra en los dos métodos de creación principales: Crear desde cero e Importar y convertir, con compatibilidad mejorada para campos inteligentes con tecnología LLM y coherencia de marca.

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa para primeros usuarios. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## Uso de esta biblioteca de indicaciones

Esta biblioteca proporciona patrones de indicaciones reutilizables para escenarios comunes de creación de formularios. Para conocer las prácticas recomendadas completas, consulte la [Guía de introducción a Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

### Sugerencias rápidas para esta biblioteca

- **Empiece con ejemplos**: use las indicaciones proporcionadas como plantillas y adáptelas a sus necesidades
- **Dos métodos de creación**: elija los enfoques Crear desde cero o Importar y convertir
- **Especifique**: añada sus propios detalles a los ejemplos genéricos
- **Haga pruebas exhaustivas**: valide siempre los resultados en el entorno específico

### Plantillas y estilos de marca

**Prepare los recursos de marca con antelación para crear formularios de forma coherente:**

- **Plantillas de marca**: prepare plantillas de formulario estandarizadas con los colores, las fuentes y los patrones de diseño de su organización
- **Directrices de estilo**: defina un estilo de campo, diseños de botón y estándares de espaciado coherentes que Forms Experience Builder pueda aplicar.
- **Biblioteca de componentes**: colabore con su equipo de desarrollo para preparar componentes de formulario reutilizables que coincidan con su identidad de marca
- **Recursos visuales**: prepare logotipos, iconos y elementos de fondo para la integración de formularios


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

**Paso 2 - Añadir campos obligatorios:**

    Agregue campos para @firstName, @lastName, @email, @phoneNumber con la validación adecuada

**Paso 3 - Añadir lógica empresarial:**

    Crear una regla: si el @age es menor de 18 años, mostrar la sección de información para padres/tutores

**Paso 4 - Mejorar con preferencias:**

    Agregar un panel de preferencias con @newsletterSubscription, @marketingConsent, @termsAccepted

**Paso 5 - Añadir carga de archivos:**

    Incluir un campo de carga de archivo para @profilePicture con un límite de tamaño de 5 MB

## Creación y administración de formularios

**Cuándo se usa:** cuando necesite crear formularios nuevos o modificar los existentes.

**Cómo se usa:** Elija uno de los dos métodos siguientes: Crear desde cero o Importar y convertir (vea la [Guía de introducción](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

**Indicación de ejemplo - Creación de formularios simples:**

    Crear un formulario de comentarios de clientes con:
    - Clasificación del producto (de 1 a 5 estrellas)
    - Campo de comentarios para comentarios detallados
    - Correo electrónico del cliente (opcional)
    - Enviar a notificación por correo electrónico

**Indicación de ejemplo - Creación de formularios complejos:**

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

**Indicaciones de administración de formularios:**

    Importe este formulario de solicitud de PDF y conviértalo en un formulario adaptable con validación mejorada
    
    Actualice el formulario de contacto existente para incluir identificadores de medios sociales y el método de contacto preferido
    
    Reorganice el formulario de registro en un asistente de tres pasos: información personal, preferencias, confirmación

## Configuración y administración de campos

**Cuándo se usa:** cuando deba añadir, modificar o configurar los campos de formulario.

**Cómo se usa:** especifique los tipos de campo, los requisitos de validación y las expectativas de la experiencia del usuario. 

**Indicación de ejemplo - Adición de campo básico:**

    Agregue un campo de entrada de texto para &quot;Nombre de la compañía&quot; con el marcador de posición &quot;Escriba el nombre de su compañía&quot;

**Indicación de ejemplo - Configuración de campo avanzado:**

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

**Indicaciones de configuración de campo:**

    Haga que @email campo sea obligatorio con validación en tiempo real y mensaje de error personalizado
    
    Agregue un menú desplegable para @country con opciones para EE. UU., Canadá, Reino Unido, Alemania, Francia y &quot;Otros&quot;
    
    Configure @phoneNumber campo con el formato (XXX) XXX-XXXX y la validación
    
    Agregue un campo de carga de archivo para @resume con restricciones de PDF y DOC, máximo de 5 MB

## Campos inteligentes mejorados LLM

**Cuándo se usa:** cuando necesite campos con opciones prerrellenadas que aprovechen la base de conocimiento de la IA.

**Cómo se usa:** solicite campos que requieran conjuntos de datos completos; la IA puede rellenar automáticamente las opciones con sus conocimientos integrados.

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

**Clasificaciones de compañía:**

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

**Normas técnicas:**

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

**Indicaciones de campo inteligente de ejemplo:**

    &quot;Agregar un campo de aeropuerto de salida con todos los principales aeropuertos del mundo, incluidos los códigos IATA y los nombres de ciudades&quot;
    
    &quot;Crear un campo industrial completo utilizando la clasificación estándar de NAICS con subcategorías tecnológicas&quot;
    
    &quot;Incluir un menú desplegable de certificación profesional que se adapte en función del campo de trabajo seleccionado&quot;
    
    &quot;Agregar un campo de número de teléfono internacional que dé formato según el país seleccionado&quot;
    
    &quot;Crear un campo de selección universitaria con las principales instituciones organizadas por país y clasificación&quot;

## Creación de reglas y lógica empresarial

**Cuándo se usa:** cuando necesite implementar lógica condicional, reglas de validación o procesos empresariales.

**Cómo se usa:** describa con claridad la lógica empresarial, especificando condiciones y acciones.

**Indicación de ejemplo - Lógica condicional simple:**

    Cree una regla que muestre el panel @spouseInformation solo cuando @maritalStatus sea igual a “Casado”

**Indicación de ejemplo - Reglas empresariales complejas:**

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

**Indicación de ejemplo - Envío multicanal estándar:**

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

- `@email`: campo de correo electrónico de referencia
- `@firstName`: campo de nombre de referencia
- `@maritalStatus`: campo de estado civil de referencia

### tipos de componentes

**Componentes de entrada:**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**Componentes de contenedor:**

- `fieldset`, `panel`, `repeatable`, `wizard`

### Propiedades del componente

**Propiedades universales (todos los componentes):**

- **Tipo**: tipo de componente
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
- Envíos de API REST
- Almacenamiento en la nube (Azure, SharePoint)
- Automatización del flujo de trabajo (Power Automate, Workfront Fusion)
- Plataformas de marketing (Marketo)
- Integraciones de CRM

### Instrucciones de sintaxis de indicación

- **Referencias de campo**: use `@fieldName` para los campos existentes
- **Comandos**: use `/command` para acciones específicas
- **Lenguaje natural**: describa los requisitos de forma clara y específica

### Lista de comprobación de validación

Para obtener prácticas recomendadas y directrices de validación completas, consulte la [Guía de introducción a Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

*Esta biblioteca de indicaciones se actualiza continuamente en función de los comentarios de los usuarios y las nuevas capacidades de Forms Experience Builder. Para obtener las últimas funciones y ejemplos, consulte la [documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es).*
