---
title: 'Forms Experience Builder: prácticas recomendadas'
description: Prácticas recomendadas completas para crear formularios eficaces con Forms Experience Builder, que abarcan el diseño, la experiencia del usuario, el rendimiento y la coherencia de marca.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 100%

---


# Forms Experience Builder: prácticas recomendadas

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa para primeros usuarios. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta guía de prácticas recomendadas se está probando en la actualidad con el producto y está sujeta a actualizaciones y revisiones. Las prácticas recomendadas, las recomendaciones y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

Esta guía completa proporciona prácticas recomendadas comprobadas para crear formularios eficaces y fáciles de usar mediante Forms Experience Builder. Estas prácticas se derivan de implementaciones exitosas y de los comentarios de los usuarios en varios sectores y casos de uso.

## Prácticas recomendadas de diseño de formularios

### Apueste por la simplicidad

**Comience con los campos esenciales**

- Comience solo con la información más necesaria para reducir la saturación del usuario
- Añada complejidad de manera gradual según las necesidades del usuario y los requisitos empresariales
- Evite pedir información que realmente no necesita o utiliza
- Tenga en cuenta el tiempo y la carga cognitiva del usuario al diseñar formularios

**Use etiquetas claras y descriptivas**

- Haga que los propósitos de los campos sean evidentes de inmediato con etiquetas descriptivas
- Evite la jerga técnica o la terminología interna que los usuarios no entenderán
- Utilice convenciones de etiquetado coherentes en todos los formularios
- Proporcione contexto cuando los requisitos de campo puedan no ser obvios

**Proporcione orientación útil**

- Incluya texto de ayuda para campos complejos con ejemplos y requisitos de formato
- Use texto de marcador de posición para mostrar los formatos de entrada esperados
- Proporcione instrucciones claras para la carga de archivos, incluidos los formatos aceptados y los límites de tamaño
- Guíe a los usuarios a través de procesos de varios pasos con indicadores de progreso

**Realice pruebas exhaustivas**

- Valide todas las rutas y escenarios de usuario antes de la implementación
- Pruebe los formularios con usuarios reales de su público destinatario
- Compruebe que toda la lógica condicional funciona según lo esperado
- Asegúrese de que la gestión de errores proporcione comentarios claros y procesables

### Divulgación progresiva

**Muestre los campos relevantes basados en el contexto**

- Muestre los campos adicionales solo cuando sean relevantes para las selecciones del usuario
- Utilice la lógica condicional para reducir la carga cognitiva y la longitud de la forma
- Agrupe los campos relacionados en secciones lógicas
- Oculte las opciones avanzadas hasta que los usuarios indiquen que las necesitan

**Ejemplo de implementación:**

    Cree una regla que muestre el panel @spouseInformation solo cuando @maritalStatus sea igual a “Casado”

**Navegación y progreso claros**

- Ayude a los usuarios a comprender dónde se encuentran en los formularios de varios pasos
- Proporcione una navegación clara entre las secciones del formulario
- Muestre los indicadores de progreso para formularios más largos
- Permita que los usuarios guarden el progreso y regresen más tarde

## Prácticas recomendadas de experiencia del usuario

### Diseño que prioriza los dispositivos móviles

**Optimización de diseño adaptable**

- Diseñe los formularios con los usuarios móviles como consideración principal
- Use diseños de una sola columna para dispositivos móviles
- Asegúrese de que los objetivos táctiles tengan el tamaño adecuado (mínimo 44 píxeles)
- Pruebe los formularios en varios tamaños y orientaciones de dispositivo

**Interacciones táctiles**

- Implemente botones y campos de entrada más grandes para las interfaces táctiles
- Utilice los tipos de entrada adecuados para activar los teclados móviles correctos
- Evite las interacciones dependientes del ratón que no funcionan en dispositivos táctiles
- Proporcione comentarios visuales claros para las interacciones del usuario

### Conformidad de accesibilidad

**Directrices WCAG 2.1**

- Siga las directrices de accesibilidad del contenido web para un diseño inclusivo
- Garantice relaciones de contraste de color adecuadas (mínimo 4,5:1 para texto normal)
- Proporcione texto alternativo para todas las imágenes e iconos
- Implemente la estructura de encabezados y el HTML semántico adecuados

**Navegación por teclado**

- Asegúrese de que todos los elementos de formulario sean accesibles mediante la navegación por teclado
- Proporcione indicadores de enfoque claros para todos los elementos interactivos
- Implemente el orden de tabulación lógico mediante campos de formulario
- Incluya vínculos de omisión de navegación para formularios complejos

**Compatibilidad con el lector de pantalla**

- Utilice etiquetas ARIA y descripciones adecuadas para los campos de formulario
- Proporcione mensajes de error claros que se anuncien a los lectores de pantalla
- Asegúrese de que los cambios en el contenido dinámico se anuncien de forma correcta
- Pruebe los formularios con software de lector de pantalla real

### Optimización de rendimiento

**Velocidad de carga**

- Optimice los tiempos de carga del formulario minimizando el tamaño inicial del paquete
- Implemente la carga diferida en secciones de formulario no críticas
- Optimice las imágenes y recursos para la entrega web
- Habilite estrategias de almacenamiento en caché adecuadas para los recursos estáticos

**Rendimiento de tiempo de ejecución**

- Utilice el tiempo de validación adecuado para equilibrar la experiencia del usuario y el rendimiento
- Implemente la devolución para la validación en tiempo real a fin de reducir las solicitudes del servidor
- Almacene en caché los datos a los que se accede con frecuencia y los resultados de validación
- Optimice la ejecución de lógica condicional para formularios complejos

**Guardado automático y protección de datos**

- Implemente el guardado automático del progreso del formulario para evitar la pérdida de datos
- Proporcione capacidad sin conexión siempre que sea posible para completar los formularios
- Incluya lógica de reintento para envíos fallidos
- Ofrezca opciones de exportación de datos como copia de seguridad para usuarios

## Prácticas recomendadas para la coherencia de marca

### Prepare los recursos de marca con antelación

**Cree plantillas de marca**

- Desarrolle plantillas de formulario estandarizadas con la identidad visual de su organización
- Incluya esquemas de color, tipografía y patrones de diseño coherentes
- Prepare componentes reutilizables que coincidan con las directrices de marca
- Documente los estándares de estilo para una implementación coherente entre equipos

**Defina directrices de estilo**

- Establezca un estilo de campo, diseños de botones y estándares de espaciado coherentes
- Cree una guía de estilo que incluya códigos de color, especificaciones de fuente y reglas de diseño
- Defina patrones de interacción y directrices de animación
- Prepare mensajes de error y texto de ayuda específicos de la marca

**Generar biblioteca de componentes**

- Crear componentes de formulario reutilizables que coincidan con la identidad de marca
- Desarrollar patrones de navegación coherentes y elementos de la interfaz de usuario
- Preparar iconos, logotipos y recursos visuales de la marca para la integración de formularios
- Establecer plantillas para tipos de formularios comunes (contacto, registro, comentarios)

### Estrategias de implementación de marca

**Indicaciones de estilo para coherencia**

Incluir instrucciones específicas de la marca en las indicaciones:

    Crear un formulario de contacto profesional usando:
    - Azul corporativo (#003366) para los botones y encabezados principales
    - Familia de fuentes Open Sans para todos los elementos de texto
    - Tamaño de fuente mínimo de 16 píxeles para el cumplimiento de accesibilidad
    - Espaciado coherente de 24 píxeles entre las secciones del formulario
    - Logotipo de la compañía en el encabezado con colocación correcta de la marca

**Administración de biblioteca de plantillas**

- Mantener una colección de plantillas de formularios con marca para casos de uso comunes
- Control de versiones de las plantillas de marca para garantizar la coherencia
- Proporcionar documentación clara acerca del uso y la personalización de plantillas
- Revisar y actualizar periódicamente los recursos de la marca para mantener los estándares actuales

>[!NOTE]
>
>**Componentes personalizados**: coordine con su equipo de desarrollo el uso de componentes específicos de la organización y su compatibilidad con Forms Experience Builder antes de implementar elementos de marca personalizados.

## Prácticas recomendadas de contenido y comunicación

### Enfoques de creación de formularios

**Dos métodos principales**

Elija el método de creación más adecuado para sus necesidades:

1. **Crear desde cero**: ideal para formularios nuevos con requisitos específicos
2. **Importar y convertir**: ideal para modernizar formularios y documentos existentes

**Indicaciones de lenguaje natural**

- Sea específico y detallado en las descripciones de los formularios
- Utilice un lenguaje claro y centrado en el negocio en lugar de términos técnicos
- Proporcione contexto sobre el propósito del formulario y el público destinatario
- Incluya los requisitos de validación y regla empresarial en las indicaciones iniciales

### Estrategia de desarrollo incremental

**Empiece de forma sencilla y vaya generando complejidad**

- Comenzar con una estructura de formulario básica y los campos esenciales
- Añadir reglas de validación y lógica empresarial de forma incremental
- Probar cada adición antes de pasar a la mejora siguiente
- Recopilar los comentarios de los usuarios en cada fase de desarrollo

**Ejemplo de enfoque incremental:**

    Paso 1: “Crear un formulario de contacto básico con campos de nombre, correo electrónico y mensaje”
    Paso 2: “Hacer @name y @email campos obligatorios con la validación adecuada”
    Paso 3: “Añadir texto de marcador de posición y texto de ayuda para guiar al usuario”
    Paso 4: “Añadir lógica condicional basada en el tipo de consulta”

### Prácticas recomendadas de referencia de campos

**Convenciones de nomenclatura coherentes**

- Utilizar nombres de campo claros y descriptivos que coincidan con el propósito
- Mantener patrones de nomenclatura coherentes en todos los formularios
- Utilizar camelCase o snake_case de forma coherente en todos los formularios
- Documentar las convenciones de nomenclatura de campos para favorecer la coherencia de equipo

**Referencias de campo efectivas**

- Usar la sintaxis `@fieldName` al modificar los campos existentes
- Ser específico sobre los campos a los que se hace referencia en los formularios complejos
- Agrupar las modificaciones de campo relacionadas en solicitudes únicas
- Comprobar los nombres de los campos antes de utilizarlos en la lógica condicional

## Prácticas recomendadas de integración y envío

### Estrategia de envío multicanal

**Acciones principales y secundarias**

- Configurar los puntos finales de envío principales para los procesos empresariales principales
- Configurar las acciones secundarias para notificaciones, confirmaciones y copias de seguridad de datos
- Implementar la gestión de errores y reintentar la lógica en los envíos fallidos
- Proporcionar comentarios del usuario para todos los estados de envío (éxito, error, procesamiento)

**Planificación de la integración**

- Comenzar con la configuración básica de envío y añadir integraciones gradualmente
- Probar cada integración por separado antes de combinar varios puntos finales
- Documentar los requisitos de API y los métodos de autenticación
- Planificar la transformación de datos y los requisitos de asignación

### Gestión y recuperación de errores

**Mensajes de error fáciles de usar**

- Proporcionar mensajes de error claros y procesables que ayuden a los usuarios a resolver problemas
- Evitar códigos de error técnicos o mensajes del sistema en contenido destinado al usuario
- Ofrecer acciones alternativas cuando falle el envío principal
- Incluir información de contacto para los usuarios que necesiten ayuda adicional

**Protección de datos y recuperación**

- Implementar el almacenamiento local de datos para la recuperación del formulario después de los errores
- Proporcionar opciones para que los usuarios descarguen los datos de sus formularios como copia de seguridad
- Configurar la monitorización y las alertas para los errores de envío
- Planificar procedimientos de recuperación por si tienen lugar interrupciones o tareas de mantenimiento del sistema

## Prácticas recomendadas de rendimiento y análisis

### Monitorización y optimización

**Métricas de rendimiento clave**

- Rastrear las tasas de finalización de formularios y puntos de abandono
- Monitorizar los tiempos de carga y patrones de interacción del usuario
- Medir la eficacia de validación y tasas de error
- Analizar los comentarios de usuarios y puntuaciones de satisfacción

**Mejora continua**

- Revisión periódica del análisis de formularios para identificar oportunidades de optimización
- Pruebas A/B de diferentes diseños de formulario y flujos de usuarios
- Recopilación y análisis de comentarios de usuarios para realizar mejoras iterativas
- Referencia comparativa del rendimiento frente a los estándares del sector

### Calidad de datos y validación

**Estrategias de validación inteligentes**

- Implementar validación en tiempo real para comentarios inmediatos del usuario
- Utilizar la validación progresiva para guiar a los usuarios por requisitos complejos
- Proporcionar mensajes de validación claros que expliquen cómo corregir errores
- Equilibrar la rigurosidad de la validación con consideraciones de la experiencia del usuario

**Integridad de datos**

- Implementar la validación entre campos para favorecer la coherencia de datos
- Utilizar tipos de entrada y restricciones adecuados para evitar datos no válidos
- Proporcionar ejemplos de formato de datos y directrices para campos complejos
- Auditoría periódica de la calidad de los datos enviados y la eficacia de la validación

## Prácticas recomendadas de seguridad y cumplimiento

### Protección de datos

**Privacidad desde el diseño**

- Recopilar únicamente los datos mínimos necesarios para el propósito de su negocio
- Implementar políticas de retención y eliminación de datos adecuadas
- Proporcionar avisos de privacidad y mecanismos de consentimiento claros
- Garantizar el cumplimiento de las normas de protección de datos aplicables (RGPD, CCPA, etc.)

**Implementación de seguridad**

- Usar cifrado HTTPS para todos los envíos de formularios y transmisión de datos
- Implementar una validación y limpieza de entrada adecuadas
- Configurar la carga segura de archivos con las restricciones y detección de virus adecuadas
- Auditorías periódicas de seguridad y evaluaciones de vulnerabilidad

### Consideraciones de cumplimiento

**Requisitos normativos**

- Comprender e implementar los requisitos de cumplimiento específicos del sector
- Documentar las medidas de cumplimiento para fines de auditoría
- Revisión periódica de los cambios normativos y su impacto en los formularios
- Formación del personal sobre los requisitos de cumplimiento y su implementación

**Cumplimiento de accesibilidad**

- Seguir las directrices WCAG 2.1 AA en materia de accesibilidad
- Pruebas de accesibilidad periódicas con tecnologías de asistencia
- Pruebas de usuario con personas con discapacidades
- Documentación de las funciones de accesibilidad y medidas de cumplimiento

## Prácticas recomendadas de colaboración en equipo

### Documentación y uso compartido de conocimientos

**Documentación de formulario**

- Mantener una documentación clara de los propósitos, requisitos y reglas empresariales del formulario
- Puntos finales de integración de documentos, flujos de datos y dependencias
- Mantener el historial de versiones y los registros de cambios para actualizaciones de formularios
- Compartir las prácticas recomendadas y las lecciones aprendidas entre los equipos

**Formación y adopción**

- Impartir formación a los integrantes del equipo sobre las funciones de Forms Experience Builder
- Establecer directrices para la creación coherente de formularios en toda la organización
- Sesiones periódicas de uso compartido de conocimientos sobre nuevas funciones y prácticas recomendadas
- Programas de tutoría para nuevos usuarios de la plataforma

### Garantía de calidad

**Procesos de revisión**

- Implementar procesos de revisión de homólogos para el diseño de formularios y su implementación
- Establecer protocolos de prueba para la funcionalidad del formulario y la experiencia del usuario
- Auditorías periódicas de los formularios existentes para identificar oportunidades de optimización
- Recopilación de comentarios de usuarios internos y usuarios finales

**Estándares y directrices**

- Desarrollar estándares de la organización para el diseño de formularios y su implementación
- Crear plantillas y directrices para tipos de formulario comunes
- Establecer procesos de aprobación para nuevos formularios y cambios importantes
- Revisión y actualización periódicas de los estándares de la organización

## Prácticas recomendadas avanzadas

### Campos inteligentes mejorados LLM

**Utilización de conocimientos de IA**

- Utilizar los conocimientos integrados de la IA para obtener opciones de campo completas
- Solicitar campos inteligentes para datos geográficos, clasificaciones comerciales y estándares del sector
- Implementar una población de campos inteligente para una experiencia del usuario mejorada
- Probar la precisión y la integridad de los campos inteligentes para casos de uso específicos

**Ejemplos de campos inteligentes**

    “Añadir un campo de aeropuerto de salida con todos los aeropuertos principales de todo el mundo, incluidos los códigos IATA”
    “Crear un campo de industria exhaustivo utilizando la clasificación NAICS estándar”
    “Incluir un menú desplegable de certificación profesional que se adapte en función del campo de trabajo”

### Lógica de formulario avanzada

**Reglas empresariales complejas**

- Dividir la lógica empresarial compleja en componentes más pequeños y comprobables
- Documentar claramente los requisitos de las reglas empresariales antes de la implementación
- Probar exhaustivamente los casos extremos y los escenarios de excepción
- Proporcionar comentarios claros del usuario sobre las infracciones de reglas empresariales

**Comportamiento de formularios dinámicos**

- Utilizar la divulgación progresiva para mostrar campos relevantes basados en los datos introducidos por el usuario
- Implementar valores predeterminados inteligentes que los usuarios puedan anular
- Crear formularios adaptables que se ajusten en función del comportamiento y las preferencias del usuario.
- Equilibrar la automatización con el control de usuario y la transparencia

## Validación y pruebas

### Estrategia completa de pruebas

**Pruebas multinivel**

- Pruebas de unidad para componentes de formulario individuales y reglas de validación
- Pruebas de integración para puntos finales de envío y flujos de datos
- Pruebas de aceptación de usuarios con grupos de usuarios representativos
- Pruebas de rendimiento en diversas condiciones de carga

**Validación en plataformas múltiples**

- Probar formularios en diferentes exploradores y versiones
- Validar la experiencia móvil en varios dispositivos y tamaños de pantalla
- Pruebas de accesibilidad con diferentes tecnologías de asistencia
- Pruebas de estado de la red para varias velocidades de conexión

### Métricas de calidad

**Indicadores de éxito**

- Tasas de finalización de formularios superiores a los puntos de referencia del sector
- Tasas de error bajas y puntuaciones de satisfacción del usuario altas
- Tiempos de carga rápidos e interacciones de usuario adaptables
- Integración correcta con sistemas back-end y procesos

**Monitorización continua**

- Revisión periódica de las métricas de rendimiento del formulario y comentarios de los usuarios
- Identificación y resolución proactivas de problemas
- Análisis de tendencias sobre el uso y la eficacia del formulario
- Referencia comparativa con los estándares del sector y las prácticas recomendadas

Para obtener instrucciones adicionales y ejemplos detallados, consulte la [Guía de introducción a Forms Experience Builder](forms-ai-assistant-getting-started.md) y la [Biblioteca de indicaciones de Forms Experience Builder](ai-assistant-prompt-library.md).
