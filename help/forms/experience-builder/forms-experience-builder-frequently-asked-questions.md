---
title: 'Forms Experience Builder: preguntas frecuentes'
description: Encuentre respuestas a preguntas comunes sobre Forms Experience Builder, incluida la configuración, el uso, la resolución de problemas y las prácticas recomendadas.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Forms Experience Builder: preguntas frecuentes

>[!NOTE]
>
> Forms Experience Builder está disponible en un programa de acceso anticipado. Antes de empezar, asegúrese de que ha solicitado y de que se le ha concedido acceso.

Estas preguntas frecuentes tratan sobre las preguntas más comunes acerca de Forms Experience Builder, desde la configuración básica hasta las funciones avanzadas y la resolución de problemas.

## Preguntas generales

### ¿Qué es Forms Experience Builder?

Forms Experience Builder es una herramienta de creación de formularios con tecnología de IA que le permite crear formularios digitales sofisticados utilizando un lenguaje conversacional. En lugar de las interfaces tradicionales de arrastrar y soltar o la codificación compleja, simplemente debe describir lo que desea y la API crea el formulario.

### ¿Quién puede utilizar Forms Experience Builder?

Forms Experience Builder está diseñado para:

- **Creadores de formularios** que desean crear formularios de forma rápida y eficaz
- **Usuarios empresariales** que necesitan crear formularios sin experiencia técnica
- **Desarrolladores** que desean aprovechar la IA para crear prototipos de formularios rápidos
- **Administradores** que necesitan configurar y administrar flujos de trabajo de creación de formularios

### ¿Forms Experience Builder está disponible para todos los clientes de AEM Forms?

Forms Experience Builder está disponible actualmente a través de un programa de acceso anticipado. Póngase en contacto con su representante de Adobe para solicitar acceso y obtener más información sobre la disponibilidad para su organización.

## Instalación y configuración

### ¿Cuáles son los requisitos previos para utilizar Forms Experience Builder?

Antes de usar Forms Experience Builder, asegúrese de lo siguiente:

- Acceso a Forms Experience Builder mediante el programa de acceso anticipado
- AEM Forms as a Cloud Service con componentes principales de Forms adaptable
- Comprensión básica de los conceptos de formulario y los requisitos empresariales

Para conocer los requisitos técnicos detallados, consulte [Implementar y configurar Forms Experience Builder](deploy-forms-experience-builder.md).

### ¿Cómo habilito Forms Experience Builder en mi entorno?

La configuración de Forms Experience Builder depende de la implementación de AEM Forms:

**Para Edge Delivery Services:**

- Preparar el proyecto para Edge Delivery Services Forms
- Habilitar Forms Experience Builder en el editor universal

**Para formularios basados en componentes principales:**

- Asegúrese de que los componentes principales de Forms adaptable estén habilitados
- Configuración de Forms Experience Builder en el editor de Forms adaptable

### ¿Puedo usar Forms Experience Builder con formularios existentes?

Sí, Forms Experience Builder puede trabajar con formularios existentes de varias formas:

- Importar y convertir PDF forms existente
- Mejore los formularios adaptables existentes con funciones impulsadas por IA
- Agregar campos inteligentes a las estructuras de formulario actuales

## Creación de formularios

### ¿Cómo se crea el primer formulario?

Comience con una descripción sencilla de lo que desea:

    Crear un formulario de contacto con campos de nombre, correo electrónico y mensaje

La API generará la estructura básica del formulario, que puede mejorar con funciones, validación y estilo adicionales.

### ¿Qué tipos de formularios puedo crear?

Forms Experience Builder admite varios tipos de formularios:

- Formularios de contacto y comentarios
- Formularios de registro e incorporación
- Formularios de encuesta y evaluación
- Formularios de varios pasos con lógica condicional
- Forms con cargas de archivos y validación compleja

### ¿Puedo crear formularios de varios pasos?

Sí, puede crear formularios de varios pasos con lenguaje natural:

    Crear un formulario progresivo con 3 pasos: información personal, preferencias, confirmación

La API configurará automáticamente la estructura del formulario con navegación entre pasos.

### ¿Cómo se agrega validación a los campos del formulario?

Agregar validación mediante comandos de lenguaje natural:

    @email un campo obligatorio con validación de formato de correo electrónico
    Agregar validación de formato de número de teléfono de EE. UU. a @phoneNumber
    Establecer validación de edad: debe tener 18 años o más para @dateOfBirth

## Funciones avanzadas

### ¿Qué son los campos inteligentes mejorados con LLM?

Los campos inteligentes mejorados con LLM son campos de formulario inteligentes que vienen previamente rellenados con opciones relevantes de las bases de conocimiento de IA. Por ejemplo:

- Desplegables de países con todos los países del mundo
- Clasificaciones del sector con códigos estándar
- Datos geográficos con estados, ciudades y códigos postales

### ¿Cómo se importan documentos existentes en formularios?

Puede importar varios tipos de documentos:

- **PDF forms**: cargar PDF estáticos o interactivos
- **Imágenes**: Cargar fotos de formularios en papel o capturas de pantalla
- **Archivos de diseño**: Importar diseños Figma u otros formatos de diseño

Utilice el icono de datos adjuntos de Forms Experience Builder para cargar el documento y describir los requisitos de conversión.

### ¿Puedo integrar formularios con sistemas externos?

Sí, Forms Experience Builder admite varias opciones de integración:

- Envíos de correo electrónico con plantillas personalizadas
- Integración de la API de REST con servicios externos
- Integración de almacenamiento en la nube (Azure, AWS, Google Cloud)
- Integración de flujos de trabajo (Power Automate, AEM Workflow)

## Resolución de problemas

### La inteligencia artificial no entiende mi solicitud. ¿Qué debo hacer?

Pruebe estos enfoques:

- Sea más específico en la descripción
- Desglose las solicitudes complejas en pasos más pequeños
- Usar referencias de campo (@fieldName) para cambios de destino
- Proporcione ejemplos claros de lo que desea

### La validación del formulario no funciona. ¿Cómo lo arreglo?

Compruebe estos problemas comunes:

- Verificar que los nombres de campo coincidan exactamente (distingue entre mayúsculas y minúsculas)
- Asegúrese de que la sintaxis de validación sea correcta
- Probar las reglas de validación individualmente
- Revisar mensajes de error para problemas específicos

### La lógica condicional no se activa correctamente. ¿Qué pasa?

Solucionar problemas de lógica condicional mediante:

- Garantizar que se haga referencia correctamente a los nombres de campo
- Comprobación de sintaxis y condiciones de regla
- Pruebas con diferentes combinaciones de entrada
- Verificación de que los tipos de campo coinciden con los requisitos de regla

### La interfaz no se carga. ¿Qué debo hacer?

Pruebe estas soluciones:

- Actualice el explorador y borre la caché
- Compruebe su conexión a Internet
- Compruebe que tiene los permisos de acceso adecuados
- Póngase en contacto con el administrador del sistema si los problemas persisten

## Prácticas recomendadas

### ¿Cómo puedo crear mejores formularios con Forms Experience Builder?

Siga estas prácticas recomendadas:

- **Sea específico**: Proporcione descripciones detalladas de lo que desea
- **Empiece por lo simple**: Empiece con la estructura básica y agregue la complejidad gradualmente
- **Realizar pruebas exhaustivas**: validar toda la funcionalidad del formulario antes de la implementación
- **Usar desarrollo incremental**: generación de formularios paso a paso

### ¿Qué debo evitar al crear formularios?

Evite estos errores comunes:

- Ser demasiado vago en sus descripciones
- Intentando crear todo a la vez
- Omitir pruebas y validación
- No tener en cuenta la respuesta móvil

### ¿Cómo puedo asegurarme de que mis formularios sean accesibles?

Forms Experience Builder incluye funciones de accesibilidad:

- Comprobación automática del cumplimiento WCAG
- Compatibilidad con lectores de pantalla
- Compatibilidad con navegación por teclado
- Opciones del modo de alto contraste

## Integración e implementación

### ¿Cómo implemento formularios creados con Forms Experience Builder?

Forms creado con Forms Experience Builder sigue los procesos de implementación estándar de AEM Forms:

- Publicar formularios a través del entorno de creación de AEM
- Configurar extremos de envío de formularios
- Configuración de flujos de trabajo de procesamiento de formularios
- Probar formularios en el entorno de producción

### ¿Puedo personalizar las respuestas y el comportamiento de la IA?

Sí, puede configurar varios aspectos:

- Estilo de respuesta (conciso, detallado, equilibrado)
- Preferencias de idioma y terminología
- Opciones de personalización de interfaz
- Configuración de accesibilidad

### ¿Cómo obtengo ayuda con Forms Experience Builder?

Para obtener soporte adicional:

- Consulte la [guía de introducción](forms-experience-builder-getting-started.md)
- Revise la [guía de implementación y configuración](deploy-forms-experience-builder.md)
- Póngase en contacto con el administrador del sistema
- Póngase en contacto con el soporte de Adobe para problemas técnicos

## Artículos relacionados

- [Información general sobre Forms Experience Builder](product-overview.md)
- [Introducción a Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementación y configuración de Forms Experience Builder](deploy-forms-experience-builder.md)
- [Campos inteligentes mejorados por LLM](forms-experience-builder-llm-smart-fields.md)
- [Importación y conversión inteligentes](intelligent-import-conversion.md)
- [Envío e integración de formularios](form-submission-integration.md)
