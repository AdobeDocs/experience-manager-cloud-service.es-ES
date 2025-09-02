---
title: 'Forms Experience Builder: prácticas recomendadas'
description: Prácticas recomendadas completas para crear formularios eficaces con Forms Experience Builder, que abarcan el diseño, la experiencia del usuario, el rendimiento y la coherencia de la marca.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---


# Forms Experience Builder: prácticas recomendadas

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa de usuarios que lo adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta guía de prácticas recomendadas se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las prácticas recomendadas, las recomendaciones y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de adopción anticipada.

Esta guía completa proporciona prácticas recomendadas comprobadas para crear formularios eficaces y fáciles de usar mediante Forms Experience Builder. Estas prácticas se derivan de implementaciones exitosas y de los comentarios de los usuarios en varios sectores y casos de uso.

## Prácticas recomendadas de diseño de formularios

### Manténgalo Simple

**Comenzar con campos esenciales**

- Comience solo con la información más necesaria para reducir la saturación del usuario
- Agregar complejidad gradualmente según las necesidades del usuario y los requisitos empresariales
- Evite pedir información que realmente no necesita o utiliza
- Tenga en cuenta el tiempo y la carga cognitiva del usuario al diseñar formularios

**Usar etiquetas claras y descriptivas**

- Haga que los propósitos de los campos sean inmediatamente obvios con etiquetas descriptivas
- Evite la jerga técnica o la terminología interna que los usuarios no entenderán
- Utilice convenciones de etiquetado coherentes en todos los formularios
- Proporcione contexto cuando los requisitos de campo puedan no ser obvios

**Proporcionar orientación útil**

- Incluir texto de ayuda para campos complejos con ejemplos y requisitos de formato
- Usar texto de marcador de posición para mostrar los formatos de entrada esperados
- Proporcionar instrucciones claras para la carga de archivos, incluidos los formatos aceptados y los límites de tamaño
- Guía a los usuarios a través de procesos de varios pasos con indicadores de progreso

**Probar a fondo**

- Validar todas las rutas y escenarios de usuario antes de la implementación
- Pruebe formularios con usuarios reales de su audiencia destinataria
- Compruebe que toda la lógica condicional funciona correctamente
- Asegúrese de que la gestión de errores proporcione comentarios claros y procesables

### Divulgación progresiva

**Mostrar campos relevantes basados en el contexto**

- Mostrar campos adicionales solo cuando sean relevantes para las selecciones del usuario
- Utilice la lógica condicional para reducir la carga cognitiva y la longitud de la forma
- Agrupar campos relacionados en secciones lógicas
- Ocultar opciones avanzadas hasta que los usuarios indiquen que las necesitan

**Implementación de ejemplo:**

    Cree una regla que muestre @spouseInformation panel únicamente cuando @maritalStatus igual a &quot;Casado&quot;

**Borrar navegación y progreso**

- Ayudar a los usuarios a comprender dónde se encuentran en los formularios de varios pasos
- Proporcionar una navegación clara entre las secciones del formulario
- Mostrar indicadores de progreso para formularios más largos
- Permitir que los usuarios guarden el progreso y regresen más tarde

## Prácticas recomendadas de experiencia del usuario

### Diseño Mobile-First

**Optimización de diseño adaptable**

- Diseñar formularios con usuarios móviles como consideración principal
- Uso de diseños de una sola columna para dispositivos móviles
- Asegúrese de que los objetivos táctiles tengan el tamaño adecuado (mínimo de 44 píxeles).
- Probar formularios en varios tamaños y orientaciones de dispositivo

**Interacciones táctiles**

- Implementar botones y campos de entrada más grandes para interfaces táctiles
- Utilice los tipos de entrada adecuados para corregir el déclencheur de los teclados móviles
- Evite las interacciones dependientes del ratón que no funcionan en dispositivos táctiles
- Proporcionar comentarios visuales claros para las interacciones del usuario

### Cumplimiento de accesibilidad

**Directrices WCAG 2.1**

- Siga las Directrices de accesibilidad del contenido web para un diseño inclusivo
- Garantizar relaciones de contraste de color adecuadas (mínimo 4.5:1 para texto normal)
- Proporcionar texto alternativo para todas las imágenes e iconos
- Implementar la estructura de encabezados y el HTML semántico adecuados

**Navegación por teclado**

- Asegúrese de que todos los elementos de formulario sean accesibles mediante la navegación mediante el teclado
- Proporcionar indicadores de enfoque claros para todos los elementos interactivos
- Implementar el orden de tabulación lógico mediante campos de formulario
- Incluir vínculos de omisión de navegación para formularios complejos

**Compatibilidad con Screen Reader**

- Utilice etiquetas ARIA y descripciones adecuadas para los campos de formulario
- Proporcionar mensajes de error claros que se anuncien a los lectores de pantalla
- Asegúrese de que los cambios en el contenido dinámico se anuncien correctamente
- Probar formularios con software de lector de pantalla real

### Optimización de rendimiento

**Velocidad de carga**

- Optimizar los tiempos de carga del formulario minimizando el tamaño inicial del paquete
- Implementación de la carga diferida en secciones de formulario no críticas
- Optimización de imágenes y recursos para la entrega web
- Habilitar estrategias de almacenamiento en caché adecuadas para los recursos estáticos

**Rendimiento de tiempo de ejecución**

- Utilice el tiempo de validación adecuado para equilibrar la experiencia del usuario y el rendimiento
- Implementar la devolución para la validación en tiempo real a fin de reducir las solicitudes del servidor
- Almacenar en caché los datos a los que se accede con frecuencia y resultados de validación
- Optimizar la ejecución de lógica condicional para formularios complejos

**Guardado automático y protección de datos**

- Implementar el guardado automático del progreso del formulario para evitar la pérdida de datos
- Proporcionar capacidad sin conexión siempre que sea posible para completar formularios
- Incluir lógica de reintento para envíos fallidos
- Ofrecer opciones de exportación de datos como copia de seguridad para usuarios

## Prácticas recomendadas para la coherencia de marcas

### Preparar Brand Assets por adelantado

**Crear plantillas de marca**

- Desarrollar plantillas de formulario estandarizadas con la identidad visual de su organización
- Incluir esquemas de color, tipografía y patrones de diseño coherentes
- Prepare componentes reutilizables que coincidan con las directrices de marca
- Documente los estándares de estilo para una implementación coherente entre equipos

**Definir directrices de estilo**

- Establezca un estilo de campo, diseños de botones y estándares de espaciado coherentes
- Cree una guía de estilo que incluya códigos de color, especificaciones de fuente y reglas de diseño
- Definición de patrones de interacción y directrices de animación
- Preparar mensajes de error y texto de ayuda específicos de la marca

**Biblioteca de componentes de compilación**

- Crear componentes de formulario reutilizables que coincidan con la identidad de su marca.
- Desarrollar patrones de navegación coherentes y elementos de la interfaz de usuario
- Preparar iconos, logotipos y recursos visuales de marca para la integración de formularios
- Establecer plantillas para tipos de formularios comunes (contacto, registro, comentarios)

### Estrategias de implementación de marca

**Peticiones de datos de estilo para coherencia**

Incluya instrucciones específicas de la marca en las indicaciones:

    Cree un formulario de contacto profesional usando:
    - Azul corporativo (#003366) para los botones y encabezados principales
    - Abra la familia de fuentes Sans para todos los elementos de texto
    - Tamaño de fuente mínimo de 16 píxeles para el cumplimiento de la accesibilidad
    - Espaciado coherente de 24 píxeles entre las secciones del formulario
    - Logotipo de la compañía en el encabezado con la colocación correcta de la marca

**Administración de biblioteca de plantillas**

- Mantener una colección de plantillas de formulario con marca para casos de uso comunes
- Control de versiones de las plantillas de marca para garantizar la coherencia
- Proporcionar documentación clara para el uso y la personalización de plantillas
- Revisión y actualización periódicas de los activos de marca para mantener los estándares actuales.

>[!NOTE]
>
>**Componentes personalizados**: coordine con su equipo de desarrollo el uso de componentes específicos de la organización y su compatibilidad con Forms Experience Builder antes de implementar elementos de marca personalizados.

## Prácticas recomendadas de contenido y comunicación

### Enfoques de creación de formularios

**Dos métodos principales**

Elija el método de creación más adecuado para sus necesidades:

1. **Crear desde cero**: ideal para formularios nuevos con requisitos específicos
2. **Importar y convertir**: ideal para modernizar formularios y documentos existentes

**Indicadores de lenguaje natural**

- Sea específico y detallado en las descripciones de los formularios
- Utilice un lenguaje claro y centrado en el negocio en lugar de términos técnicos
- Proporcionar contexto sobre el propósito del formulario y la audiencia de destino
- Incluir los requisitos de validación y reglas de negocio en las peticiones de datos iniciales

### Estrategia de desarrollo incremental

**Inicio sencillo, complejidad de compilación**

- Comience con la estructura básica del formulario y los campos esenciales
- Agregar reglas de validación y lógica empresarial de forma incremental
- Pruebe cada adición antes de continuar con la siguiente mejora
- Recopilar comentarios de los usuarios en cada fase del desarrollo

**Ejemplo de enfoque incremental:**

    Paso 1: &quot;Crear un formulario de contacto básico con campos de nombre, correo electrónico y mensaje&quot;
    Paso 2: &quot;Hacer @name y @email campos obligatorios con la validación adecuada&quot;
    Paso 3: &quot;Agregar texto de marcador de posición y texto de ayuda para la guía del usuario&quot;
    Paso 4: &quot;Agregar lógica condicional basada en el tipo de consulta&quot;

### Prácticas recomendadas de referencia de campos

**Convenciones de nombres coherentes**

- Utilice nombres de campo claros y descriptivos que coincidan con su propósito
- Mantener patrones de nomenclatura coherentes en todos los formularios
- Utilice camelCase o snake_case de forma coherente en todos los formularios
- Convenciones de nomenclatura de campos de documento para coherencia de equipo

**Referencias de campo efectivas**

- Usar sintaxis `@fieldName` al modificar campos existentes
- Especifique a qué campos hace referencia en los formularios complejos
- Agrupar modificaciones de campo relacionadas en solicitudes únicas
- Compruebe los nombres de los campos antes de utilizarlos en la lógica condicional

## Prácticas recomendadas de integración y envío

### Estrategia de envío multicanal

**Acciones primarias y secundarias**

- Configurar los extremos de envío principales para los procesos empresariales principales
- Configurar acciones secundarias para notificaciones, confirmaciones y copias de seguridad de datos
- Implementar la gestión de errores y la lógica de reintentos para los envíos fallidos
- Proporcionar comentarios del usuario para todos los estados de envío (éxito, error, procesamiento)

**Planificación de la integración**

- Comience con la configuración básica de envío y agregue integraciones gradualmente
- Pruebe cada integración por separado antes de combinar varios extremos
- Documentar los requisitos de API y los métodos de autenticación
- Plan de transformación de datos y requisitos de asignación

### Gestión y recuperación de errores

**Mensajes de error descriptivos**

- Proporcionar mensajes de error claros y procesables que ayuden a los usuarios a resolver problemas
- Evite códigos de error técnicos o mensajes del sistema en contenido orientado al usuario
- Ofrecer acciones alternativas cuando falle el envío principal
- Incluir información de contacto para los usuarios que necesitan ayuda adicional

**Protección y recuperación de datos**

- Implementar el guardado de datos locales para la recuperación del formulario después de errores
- Proporcionar opciones para que los usuarios descarguen sus datos de formulario como copia de seguridad
- Configurar la monitorización y las alertas para los errores de envío
- Planificar procedimientos de recuperación para interrupciones o mantenimiento del sistema

## Prácticas recomendadas de rendimiento y análisis

### Monitorización y optimización

**Métricas clave de rendimiento**

- Rastrear tasas de finalización de formularios y puntos de abandono
- Monitorización de tiempos de carga y patrones de interacción del usuario
- Eficacia de validación de medidas y tasas de error
- Analizar comentarios de usuarios y puntuaciones de satisfacción

**Mejora continua**

- Revisión periódica del análisis de formularios para identificar oportunidades de optimización
- Pruebas A/B de diferentes diseños de formulario y flujos de usuarios
- Recopilación y análisis de comentarios de usuarios para realizar mejoras iterativas
- Evaluación del rendimiento frente a los estándares del sector

### Calidad de datos y validación

**Estrategias de validación inteligentes**

- Implementar validación en tiempo real para comentarios inmediatos del usuario
- Utilice la validación progresiva para guiar a los usuarios por requisitos complejos
- Proporcione mensajes de validación claros que expliquen cómo corregir errores
- Equilibre la rigurosidad de la validación con consideraciones de experiencia del usuario

**Integridad de datos**

- Implementación de la validación entre campos para la coherencia de datos
- Utilice tipos de entrada y restricciones adecuados para evitar datos no válidos
- Proporcione ejemplos de formato de datos y directrices para campos complejos
- Auditoría periódica de la calidad de los datos presentados y la eficacia de la validación

## Prácticas recomendadas de seguridad y cumplimiento

### Protección de datos

**Privacidad por diseño**

- Recopile únicamente los datos mínimos necesarios para el propósito de su negocio
- Implementar políticas de retención y eliminación de datos adecuadas
- Proporcionar avisos de privacidad y mecanismos de consentimiento claros
- Garantizar el cumplimiento de las normas de protección de datos (RGPD, CCPA, etc.)

**Implementación de seguridad**

- Utilizar el cifrado HTTPS para todos los envíos de formularios y la transmisión de datos
- Implemente la validación y el saneamiento de entrada adecuados
- Configurar la carga segura de archivos con las restricciones adecuadas y la detección de virus
- Auditorías periódicas de seguridad y evaluaciones de vulnerabilidad

### Consideraciones de cumplimiento

**Requisitos normativos**

- Comprender e implementar los requisitos de cumplimiento específicos del sector
- Documente las medidas de cumplimiento para fines de auditoría
- Revisión periódica de los cambios regulatorios y su impacto en los formularios
- Formación del personal sobre los requisitos de cumplimiento y la aplicación

**Cumplimiento de accesibilidad**

- Siga las directrices WCAG 2.1 AA para la accesibilidad
- Pruebas de accesibilidad regulares con tecnologías de asistencia
- Pruebas de usuario con personas con discapacidades
- Documentación de las funciones de accesibilidad y medidas de cumplimiento

## Prácticas recomendadas de Team Collaboration

### Documentación e intercambio de conocimientos

**Documentación de formulario**

- Mantener una documentación clara de los propósitos, requisitos y reglas empresariales del formulario
- Extremos de integración de documentos, flujos de datos y dependencias
- Mantener el historial de versiones y los registros de cambios para actualizaciones de formularios
- Comparta las prácticas recomendadas y las lecciones aprendidas entre los equipos

**Formación y adopción**

- Impartir formación a los integrantes del equipo sobre las funciones de Forms Experience Builder
- Establezca directrices para la creación coherente de formularios en toda la organización
- Sesiones periódicas de intercambio de conocimientos sobre nuevas funciones y prácticas recomendadas
- Programas de tutoría para nuevos usuarios de la plataforma

### Garantía de calidad

**Procesos de revisión**

- Implementar procesos de revisión por pares para el diseño y la implementación de formularios
- Establezca protocolos de prueba para la funcionalidad del formulario y la experiencia del usuario
- Auditorías periódicas de los formularios existentes para las oportunidades de optimización
- Recopilación de comentarios de usuarios internos y usuarios finales

**Estándares y directrices**

- Desarrollar normas organizativas para el diseño y la implementación de formularios
- Creación de plantillas y directrices para tipos de formulario comunes
- Establecer procesos de aprobación para nuevos formularios y cambios importantes
- Revisión y actualización periódicas de las normas organizativas

## Prácticas recomendadas avanzadas

### Campos inteligentes mejorados LLM

**Aprovechando el conocimiento de IA**

- Utilice los conocimientos integrados de la IA para obtener opciones de campo completas
- Solicite campos inteligentes para datos geográficos, clasificaciones comerciales y estándares del sector
- Implementar la población de campos inteligente para mejorar la experiencia del usuario
- Pruebe la precisión y la integridad de los campos inteligentes para sus casos de uso específicos

**Ejemplos de campos inteligentes**

    &quot;Agregar un campo de aeropuerto de salida con todos los aeropuertos principales de todo el mundo, incluidos los códigos IATA&quot;
    &quot;Crear un campo industrial completo utilizando la clasificación NAICS estándar&quot;
    &quot;Incluir un menú desplegable de certificación profesional que se adapte en función del campo de trabajo&quot;

### Lógica de formulario avanzada

**Reglas de negocios complejas**

- Divida la lógica empresarial compleja en componentes más pequeños y comprobables
- Documente claramente los requisitos de las reglas empresariales antes de la implementación
- Pruebe exhaustivamente los casos extremos y los escenarios de excepción
- Proporcionar comentarios claros del usuario sobre las violaciones de reglas de negocio

**Comportamiento de formulario dinámico**

- Utilizar la divulgación progresiva para mostrar campos relevantes basados en los datos introducidos por el usuario
- Implementar valores predeterminados inteligentes que los usuarios puedan anular
- Crear formularios adaptables que se ajusten en función del comportamiento y las preferencias del usuario.
- Equilibrar la automatización con el control de usuario y la transparencia

## Validación y pruebas

### Estrategia completa de pruebas

**Pruebas multinivel**

- Pruebas unitarias para componentes de formulario individuales y reglas de validación
- Pruebas de integración para puntos finales de envío y flujos de datos
- Pruebas de aceptación de usuarios con grupos de usuarios representativos
- Pruebas de rendimiento en diversas condiciones de carga

**Validación entre plataformas**

- Probar formularios en diferentes exploradores y versiones
- Validar la experiencia móvil en varios dispositivos y tamaños de pantalla
- Pruebas de accesibilidad con diferentes tecnologías de asistencia
- Prueba de condición de red para varias velocidades de conexión

### Métricas de calidad

**Indicadores de éxito**

- Tasas de finalización de formularios superiores a los puntos de referencia del sector
- Tasas de error bajas y puntuaciones de satisfacción del usuario altas
- Tiempos de carga rápidos e interacciones de usuario adaptables
- Integración correcta con sistemas y procesos back-end

**Supervisión continua**

- Revisión regular de las métricas de rendimiento del formulario y los comentarios del usuario
- Identificación y resolución proactivas de problemas
- Análisis de tendencias para el uso y la eficacia del formulario
- Comparación con los estándares del sector y las prácticas recomendadas

Para obtener instrucciones adicionales y ejemplos detallados, consulte la [Guía de introducción a Forms Experience Builder](forms-ai-assistant-getting-started.md) y la [Biblioteca de mensajes de Forms Experience Builder](ai-assistant-prompt-library.md).
