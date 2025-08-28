---
title: Configuración de una página de redireccionamiento o un mensaje de agradecimiento
description: Obtenga información sobre cómo redirigir a los usuarios a una página web que los autores de formularios puedan configurar al crear el formulario o cómo se puede mostrar a los usuarios un mensaje de agradecimiento.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
exl-id: cacd7b0a-aad0-4b5d-a6a0-e4bac4cb196d
source-git-commit: ede73b19e4b50770f14ed52067c5fa04323b2ba4
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 100%

---

# Configuración de mensajes de agradecimiento y URL de redireccionamiento

Las experiencias posteriores al envío afectan significativamente a la satisfacción del usuario y a las tasas de finalización del formulario. El editor universal de Adobe proporciona opciones completas para configurar lo que los usuarios ven después de enviar los formularios, ya sea mediante mensajes de agradecimiento personalizados o redireccionamientos estratégicos a páginas específicas.

Este artículo proporciona directrices detalladas sobre la implementación de mensajes de agradecimiento y URL de redireccionamiento, incluidas consideraciones técnicas, prácticas recomendadas y directrices de experiencia del usuario para maximizar la eficacia de los envíos de formularios.

## Requisitos previos

Antes de configurar las experiencias posteriores al envío, asegúrese de que tiene lo siguiente:

**Configuración técnica:**

- Acceso al editor universal con los permisos adecuados
- Un formulario adaptable existente creado en el editor universal
- Comprensión de los requisitos de la URL de redireccionamiento de su organización

**Consideraciones sobre la planificación:**

- **Estrategia de mensajes**: defina el tono, la longitud y la información específica que se va a incluir en los mensajes de agradecimiento
- **Estrategia de redireccionamiento**: identifique las páginas de destino y asegúrese de que estén optimizadas para las experiencias posteriores a la finalización del formulario
- **Integración de análisis**: planifique cómo rastrear las interacciones del usuario con mensajes de agradecimiento o destinos de redirección

## Configurar mensajes de agradecimiento

Los mensajes de agradecimiento proporcionan un reconocimiento inmediato del envío correcto del formulario y pueden incluir contenido personalizado, pasos siguientes o información importante relacionada con el envío del usuario.

### Cuándo usar mensajes de agradecimiento

Los mensajes de agradecimiento funcionan mejor cuando:

- **Reconocimiento simple**: los usuarios necesitan confirmación sin requisitos de navegación adicionales
- **Contenido informativo**: debe proporcionar los pasos siguientes específicos o información importante
- **Coherencia de la marca**: el mensaje se puede diseñar para que se ajuste al estilo de comunicación de su organización
- **Experiencia de una sola página**: los usuarios deben permanecer en la página actual para que el flujo de trabajo continúe

### Pasos de implementación

**1. Acceder a las propiedades del formulario**

Abra el formulario adaptable en el editor universal y haga clic en el icono **Editar propiedades del formulario** de la barra de herramientas. Esto abre el cuadro de diálogo de propiedades del formulario completo.

**2. Ir a la configuración de agradecimiento**

En el cuadro de diálogo Propiedades del formulario, seleccione la pestaña **Agradecimiento** para acceder a las opciones de configuración posteriores al envío.

**3. Configurar la visualización del mensaje**

Seleccione **Mostrar mensaje** de las opciones disponibles. Esto activa el editor de contenido del mensaje con funciones de texto enriquecido.

**4. Crear el contenido del mensaje**

En el campo **Contenido del mensaje**, cree su mensaje de agradecimiento con el editor de texto enriquecido. El editor admite:

- **Formato de texto**: opciones de negrita, cursiva, subrayado y color
- **Listas**: listas de números y con viñetas para organizar la información
- **Vínculos**: vínculos directos a recursos relevantes o pasos siguientes
- **Edición en pantalla completa**: haga clic en el icono de expansión para ampliar el área de trabajo de edición

### Consideraciones técnicas

**Comportamiento de visualización del mensaje:**

- Los mensajes aparecen en una superposición modal inmediatamente después del envío del formulario
- El contenido admite el formato HTML y mantiene un diseño interactivo
- Los usuarios pueden descartar los mensajes o configurarlos con temporizadores de cierre automático

**Directrices de contenido:**

- Haga que los mensajes sean concisos a la vez que proporciona la información necesaria
- Incluya los siguientes pasos que se deben seguir con claridad cuando corresponda
- Considere incluir números de referencia o detalles de confirmación
- Asegúrese de usar un formato compatible con dispositivos móviles

### Ejemplo de implementación

    Gracias por el envío.
    
    Se ha recibido su solicitud y se le ha asignado el número de referencia #REF-2024-001234.
    
    **Qué sucede a continuación:**
    - Recibirá un correo electrónico de confirmación en un plazo de 15 minutos
    - Nuestro equipo revisará su solicitud en un plazo de 2 días hábiles
    - Nos pondremos en contacto con usted directamente si necesitamos información adicional
    
    **¿Necesita asistencia?** Póngase en contacto con nuestro equipo de asistencia en support@example.com

## Configuración de la URL de redireccionamiento

Las direcciones URL de redireccionamiento dirigen automáticamente a los usuarios a páginas específicas después del envío del formulario, lo que permite una integración perfecta con los flujos de trabajo existentes o dirige a los usuarios al contenido relevante.

### Cuándo usar URL de redireccionamiento

Las direcciones URL de redireccionamiento son óptimas para:

- **Integración del flujo de trabajo**: dirigiendo a los usuarios a paneles, páginas de cuenta o pasos siguientes en un proceso
- **Entrega de contenido**: muestra productos, servicios o información relevantes basados en las respuestas del formulario
- **Seguimiento de análisis**: redirigir a páginas con implementaciones de seguimiento específicas
- **Procesos de varios pasos**: hacer que los usuarios pasen a la siguiente fase en flujos de trabajo complejos

### Pasos de implementación

**1. Acceder a propiedades de formulario**

Abra el formulario adaptable en el editor universal y haga clic en el icono **Editar propiedades del formulario** para abrir el cuadro de diálogo de configuración del formulario.

**2. Ir a la configuración de agradecimiento**

Seleccione la pestaña **Agradecimiento** en el cuadro de diálogo Propiedades del formulario para acceder a las opciones de configuración de redireccionamiento.

**3. Habilitar funcionalidad de redireccionamiento**

Elija **Redirigir a la dirección URL** de las opciones disponibles después del envío.

**4. Configurar URL de destino**

Introduzca la dirección URL de destino en el campo proporcionado. El sistema admite varios formatos de URL para una implementación flexible.

### Opciones de configuración de URL

**URL absolutas**

Direcciones web completas, incluidos protocolo y dominio:

    https://www.example.com/thank-you
    https://dashboard.example.com/user/profile

**Rutas relativas**

Rutas relativas a su dominio actual:

    /thank-you
    /dashboard/user-profile
    ../confirmation-page.html

**Referencias de página de AEM Sites**

Referencias a otras páginas dentro de la implementación de AEM Sites:

    /content/mysite/en/thank-you
    /content/mysite/en/next-step

### Consideraciones técnicas

**Comportamiento de redirección:**

- Las redirecciones se producen inmediatamente después de enviar correctamente el formulario
- El historial del explorador incluye la redirección para la correcta funcionalidad del botón Atrás
- La temporización de redireccionamiento se puede configurar con retrasos opcionales

**Validación de URL:**

- El sistema valida el formato de la URL antes de permitir la configuración
- Las direcciones URL relativas se resuelven en el dominio actual
- Las direcciones URL externas requieren la configuración adecuada de CORS si es necesario

## Buenas prácticas y recomendaciones

### Directrices de experiencia del usuario

**Optimización de mensajes:**

- **Claridad primero**: asegurarse de que los usuarios entiendan inmediatamente que su envío se realizó correctamente
- **Valor añadido**: proporcione información que ayude a los usuarios en los pasos siguientes
- **Promoción de la marca coherente**: mantenga el estilo visual y de voz de la organización
- **Consideración móvil**: pruebe mensajes en varios tamaños de pantalla

**Optimización de redirección:**

- **Optimización de página**: asegurarse de que los destinos de redireccionamiento estén optimizados para los visitantes posteriores al formulario
- **Rendimiento de carga**: comprobar que las páginas de redireccionamiento se cargan rápidamente para mantener la experiencia del usuario
- **Relevancia del contenido**: asegurarse de que el contenido de redireccionamiento es relevante para el contexto del formulario

### Consideraciones sobre la seguridad

**Validación de URL:**

- Implementar la validación adecuada para las direcciones URL de redireccionamiento para evitar redirecciones malintencionadas
- Considere los enfoques de lista blanca para los dominios de redireccionamiento permitidos
- Monitorizar los patrones de redireccionamiento para detectar actividades inusuales

**Seguridad del contenido:**

- Limpiar el contenido del mensaje de agradecimiento para evitar la inyección de scrips
- Implementar directivas de seguridad de contenido adecuadas para el contenido de texto enriquecido
- Revisiones de seguridad periódicas de los destinos de redireccionamiento

### Análisis y seguimiento

**Consideraciones de implementación:**

- **Seguimiento de metas**: configurar metas de análisis tanto para las vistas de mensajes de agradecimiento como para las finalizaciones de redireccionamiento
- **Asignación de recorridos de usuario**: realizar un seguimiento de la forma en la que los usuarios interactúan con las experiencias posteriores al envío
- **Optimización de conversión**: realizar pruebas A/B con diferentes mensajes de agradecimiento y destinos de redireccionamiento

**Estrategias de medición:**

- Monitorizar el tiempo empleado en los mensajes de agradecimiento antes de despedirse
- Realizar un seguimiento de las tasas de clics para vínculos dentro de mensajes de agradecimiento
- Analizar el comportamiento del usuario en las páginas de destino de redireccionamiento

## Puntos de comprobación de validación

Después de configurar la experiencia posterior al envío:

**Verificación de configuración:**

- Las propiedades del formulario muestran correctamente la opción de agradecimiento seleccionada
- El contenido del mensaje se muestra correctamente en el modo Previsualización
- Las direcciones URL de redireccionamiento tienen el formato correcto y son accesibles
- Todos los vínculos de los mensajes funcionan correctamente

**Pruebas de la experiencia del usuario:**

- Enviar formularios de prueba para verificar la correcta visualización del mensaje de agradecimiento
- Probar la funcionalidad de redireccionamiento en distintos navegadores
- Verificar la respuesta móvil de los mensajes de agradecimiento
- Confirmar que los destinos de redireccionamiento se cargan correctamente

**Configuración de análisis:**

- Códigos de seguimiento implementados correctamente para los mensajes de agradecimiento
- Seguimiento de destino de redireccionamiento configurado
- Activación correcta de los eventos de finalización de objetivos

## Próximos pasos

Después de configurar correctamente la experiencia posterior al envío:

- **Monitorizar el rendimiento**: revisar los análisis para comprender la participación del usuario con los mensajes de agradecimiento o las páginas de redireccionamiento
- **Iterar y mejorar**: usar los comentarios de los usuarios y las perspectivas de datos para perfeccionar la estrategia posterior al envío
- **Implementación a escala**: aplicar patrones exitosos en otros formularios de la organización

**Documentación relacionada:**

- [Guía de configuración de envío de formularios](submit-action.md)
- [Prácticas recomendadas de experiencia del usuario](responsive-layout.md)
