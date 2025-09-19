---
title: Envío e integración de formularios
description: Obtenga información sobre cómo configurar los envíos de formularios e integrar formularios de Forms Experience Builder con sistemas externos, API y flujos de trabajo empresariales.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 1%

---


# Envío e integración de formularios

>[!NOTE]
>
> Forms Experience Builder está disponible en un programa de acceso anticipado. Antes de empezar, asegúrese de que ha solicitado y de que se le ha concedido acceso.

Forms Experience Builder proporciona potentes funciones de integración para conectar los formularios con sistemas externos, API y flujos de trabajo empresariales. Esta guía explica cómo configurar los envíos de formularios y configurar varios escenarios de integración.

## Opciones de configuración de envío

### Envíos de correo electrónico

Configurar formularios para enviar envíos por correo electrónico:

**Configuración básica del correo electrónico:**

- Establecimiento de direcciones de correo electrónico del destinatario
- Configurar plantillas de correo electrónico
- Adición de destinatarios CC y CCO
- Configurar notificaciones por correo electrónico

**Funciones de correo electrónico avanzadas:**

- Selección dinámica de destinatarios
- Plantillas de correo electrónico con datos de formulario
- Administración de archivos adjuntos
- Confirmación de envío de correo electrónico

### Integración de API de REST

Conectar formularios a API y servicios externos:

**Configuración del extremo de API:**

- Definición de URL de API de REST
- Configuración de métodos de autenticación
- Definición de encabezados y parámetros de solicitud
- Administrar datos de respuesta

**Asignación de datos:**

- Asignar campos de formulario a parámetros de API
- Transformar formatos de datos
- Administrar estructuras JSON anidadas
- Administrar respuestas de error

### Integración de almacenamiento en nube

Almacenar envíos de formularios en servicios de almacenamiento en la nube:

**Plataformas compatibles:**

- Almacenamiento del Blob de Microsoft Azure
- Amazon S3
- Almacenamiento de Google Cloud
- SharePoint Online

**Opciones de configuración:**

- Establecer credenciales de almacenamiento
- Configuración de estructuras de carpetas
- Establecer convenciones de nomenclatura de archivos
- Administración de permisos de acceso

### Integración de flujo de trabajo

Conectar formularios a flujos de trabajo de procesos empresariales:

**Microsoft Power Automate:**

- Déclencheur de flujos de trabajo al enviar formularios
- Paso de datos de formulario a pasos de flujo de trabajo
- Gestión de respuestas de flujo de trabajo
- Administrar procesos de aprobación

**Flujo de trabajo de Adobe:**

- Integración con el flujo de trabajo de AEM
- Configuración de cadenas de aprobación
- Configuración de pasos de notificación
- Administrar procesamiento de documentos

## Configuración de envíos de formularios

### Paso 1: Acceso a la configuración de envío

1. Abra el formulario en Forms Experience Builder
2. Vaya a la configuración de envío
3. Seleccione &quot;Configurar el envío de formularios&quot;
4. Elija su tipo de integración

### Paso 2: Configurar los envíos de correo electrónico

**Configuración básica del correo electrónico:**

    Configurar el envío de correo electrónico a hr@company.com con:
    - Asunto: &quot;Nueva solicitud de empleado&quot;
    - Incluir datos de formulario en el cuerpo del correo electrónico
    - Enviar confirmación al solicitante

**Configuración avanzada de correo electrónico:**

    Configurar enrutamiento dinámico de correo electrónico:
    - Si el departamento es igual a &quot;TI&quot;, enviar a it-hr@company.com
    - Si el departamento es igual a &quot;Ventas&quot;, enviar a sales-hr@company.com
    - De forma predeterminada a hr@company.com

### Paso 3: Configuración de la integración de API

**Configuración de la API de REST:**

    Enviar datos de formulario al extremo REST:
    - URL: https://api.company.com/forms/submit
    - Método: POST
    - Autenticación: token de portador
    - Tipo de contenido: application/json

**Ejemplo de asignación de datos:**

    Asignar campos de formulario a la API:
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - department -> user.department_id

### Paso 4: Configurar el almacenamiento en la nube

**Configuración del almacenamiento de Azure Blob:**

    Almacenar envíos de formularios en Azure:
    - Contenedor: form-submissions
    - Carpeta: /{year}/{month}/{day}/
    - Formato de archivo: JSON con datos adjuntos
    - Nivel de acceso: Privado

## Ejemplos de integración

### Formulario de comentarios del cliente

**Configuración de envío:**

- Notificación por correo electrónico al equipo de asistencia
- Almacenar datos en el sistema CRM mediante API
- Crear ticket de asistencia automáticamente
- Enviar correo electrónico de confirmación al cliente

**Implementación:**
Enviar formulario de comentarios de clientes a:
1. Enviar correo electrónico a <support@company.com> con detalles del formulario
2. PUBLICAR en la API de CRM para crear un registro de cliente
3. Flujo de trabajo de creación de tickets de asistencia de Déclencheur
4. Enviar correo electrónico de agradecimiento al cliente

### Formulario de incorporación de empleado

**Configuración de envío:**

- Enviar un correo electrónico al equipo de RRHH con nueva información de contratación
- Almacenar documentos en SharePoint
- flujo de trabajo de incorporación de déclencheur
- Crear cuentas de usuario en varios sistemas

**Implementación:**
Procesar la incorporación de los empleados:
1. Enviar correo electrónico a <hr@company.com> con los detalles del empleado
2. Cargar documentos en la carpeta de empleados de SharePoint
3. Inicie el flujo de trabajo de incorporación en Power Automate
4. Crear cuentas en el sistema de recursos humanos, correo electrónico y otras herramientas

### Formulario de generación de posibles clientes

**Configuración de envío:**

- Almacenar datos de posibles clientes en la plataforma de automatización de marketing
- Enviar notificación al equipo de ventas
- Agregar posible cliente al sistema CRM
- secuencia de correo electrónico de seguimiento de déclencheur

**Implementación:**
Generación de posibles clientes del proceso:
1. Publicar datos de posibles clientes en la API de Marketo
2. Crear registro de posibles clientes en Salesforce
3. Enviar correo electrónico al equipo de ventas con detalles del posible cliente
4. Inicie la secuencia de nutrición de correo electrónico automatizado

## Situaciones de integración avanzadas

### Procesamiento de formularios de varios pasos

**Integración compleja del flujo de trabajo:**

- Validación de datos de formulario con sistemas externos
- Procesar pagos mediante puertas de enlace de pago
- Generación de documentos y contratos
- Envío de notificaciones a varias partes interesadas

### Validación de datos en tiempo real

**Validación basada en API:**

- Validar direcciones de correo electrónico con el directorio de empresa
- Comprobar la disponibilidad del producto en el sistema de inventario
- Verificar la información del cliente en CRM
- Validar información de pago

### Enrutamiento de envío condicional

**Enrutamiento dinámico basado en datos de formulario:**

- Ruta a diferentes departamentos según el tipo de consulta
- Envíe a diferentes sistemas en función del nivel de cliente
- Procesar de forma diferente en función del estado de finalización del formulario
- Administrar distintas reglas de negocio por región

## Seguridad y cumplimiento

### Protección de datos

**Cifrado y seguridad:**

- Cifrado de datos confidenciales en tránsito
- Credenciales y tokens de API segura
- Implemente los controles de acceso adecuados
- Seguir políticas de retención de datos

### Requisitos de cumplimiento

**RGPD y privacidad:**

- Implementación de administración de consentimiento
- Proporcionar funciones de exportación de datos
- Habilitar solicitudes de eliminación de datos
- Mantener pistas de auditoría

**Estándares del sector:**

- Cumplimiento de la HIPAA para formularios de atención médica
- PCI DSS para procesamiento de pagos
- Cumplimiento de SOX para formularios financieros
- Regulaciones específicas del sector

## Pruebas y validación

### Prueba de envío

**Escenarios de prueba:**

- Verificar envío y formato de correo electrónico
- Prueba de conectividad y asignación de datos de API
- Validar cargas de almacenamiento en la nube
- Comprobar funcionalidad de déclencheur de flujo de trabajo

**Control de errores:**

- Probar escenarios de error de red
- Validar visualización del mensaje de error
- Comprobar mecanismos de reintento
- Verificar opciones de reserva

### Optimización de rendimiento

**Estrategias de optimización:**

- Implementación del procesamiento asincrónico
- Uso de operaciones por lotes para datos masivos
- Optimizar frecuencia de llamada de API
- Almacenar en caché datos a los que se accede frecuentemente

## Resolución de problemas de integración

### Problemas comunes

**Problemas con la entrega de correo electrónico:**

- Comprobar configuración del servidor SMTP
- Verificar direcciones de correo electrónico del destinatario
- Revisar configuración de filtro de correo no deseado
- Probar formato de plantilla de correo electrónico

**Problemas de integración de API:**

- Verificar URL de extremo de API
- Comprobar credenciales de autenticación
- Validar formato y encabezados de solicitud
- Revisar gestión de respuestas API

**Problemas de integración de almacenamiento:**

- Confirmar credenciales de almacenamiento
- Comprobar permisos de carpeta
- Comprobar límites de carga de archivos
- Probar la conectividad de red

### Obtención de ayuda

Para problemas de integración:

- [Preguntas frecuentes sobre Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Revise la [guía de introducción](forms-experience-builder-getting-started.md)
- Póngase en contacto con el administrador del sistema para obtener asistencia técnica
- Consulte la documentación de API para servicios externos

## Artículos relacionados

- [Información general sobre Forms Experience Builder](product-overview.md)
- [Introducción a Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementación y configuración de Forms Experience Builder](deploy-forms-experience-builder.md)
- [Importación y conversión inteligentes](intelligent-import-conversion.md)
- [Preguntas frecuentes](forms-experience-builder-frequently-asked-questions.md)
