---
title: Cómo configurar una página de redireccionamiento o un mensaje de agradecimiento
description: Obtenga información sobre cómo se puede redirigir a los usuarios a una página web que los autores de formularios pueden configurar al crear el formulario o cómo se puede mostrar a los usuarios un mensaje de agradecimiento.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 3%

---


# Configuración de mensajes de agradecimiento y redirección de URL

Las experiencias posteriores al envío afectan significativamente a la satisfacción del usuario y a las tasas de finalización del formulario. El editor universal de Adobe proporciona opciones completas para configurar lo que los usuarios ven después de enviar formularios, ya sea mediante mensajes de agradecimiento personalizados o redirecciones estratégicas a páginas específicas.

Este artículo proporciona directrices detalladas sobre la implementación de mensajes de agradecimiento y redirecciones URL, incluidas consideraciones técnicas, prácticas recomendadas y directrices de experiencia del usuario para maximizar la eficacia de los envíos de formularios.

## Requisitos previos

Antes de configurar las experiencias posteriores al envío, asegúrese de lo siguiente:

**Configuración técnica:**

- Acceso al editor universal con los permisos adecuados
- Un formulario adaptable existente creado en el editor universal
- Comprensión de los requisitos de URL de redireccionamiento de su organización

**Consideraciones de planificación:**

- **Estrategia de mensajes**: defina el tono, la longitud y la información específica que se va a incluir en los mensajes de agradecimiento
- **Estrategia de redireccionamiento**: identifique las páginas de destino y asegúrese de que estén optimizadas para las experiencias posteriores a la finalización del formulario
- **Integración de Analytics**: Planifique cómo rastrear las interacciones del usuario con mensajes de agradecimiento o destinos de redirección

## Configurar mensajes de agradecimiento

Los mensajes de agradecimiento proporcionan un reconocimiento inmediato del envío correcto del formulario y pueden incluir contenido personalizado, pasos siguientes o información importante relacionada con el envío del usuario.

### Cuándo usar mensajes de agradecimiento

Los mensajes de agradecimiento funcionan mejor cuando:

- **Reconocimiento simple**: los usuarios necesitan confirmación sin requisitos de navegación adicionales
- **Contenido informativo**: debe proporcionar los pasos siguientes específicos o información importante
- **Coherencia de la marca**: el mensaje se puede diseñar para que se ajuste al estilo de comunicación de su organización
- **Experiencia de una sola página**: Los usuarios deben permanecer en la página actual para que el flujo de trabajo continúe

### Pasos de implementación

**1. Obtener acceso a propiedades de formulario**

Abra el formulario adaptable en el editor universal y haga clic en el icono **Editar propiedades del formulario** de la barra de herramientas. Esto abre el cuadro de diálogo de propiedades del formulario completo.

**2. Vaya a la configuración de agradecimiento**

En el cuadro de diálogo Propiedades del formulario, seleccione la pestaña **Gracias** para acceder a las opciones de configuración posteriores al envío.

**3. Configurar la visualización del mensaje**

Seleccione **Mostrar mensaje** de las opciones disponibles. Esto activa el editor de contenido del mensaje con funciones de texto enriquecido.

**4. Crear el contenido del mensaje**

En el campo **Contenido del mensaje**, cree su mensaje de agradecimiento con el editor de texto enriquecido. El editor admite:

- **Formato de texto**: opciones de negrita, cursiva, subrayado y color
- **Listas**: Listas numeradas y con viñetas para organizar la información
- **Vínculos**: Vínculos directos a recursos relevantes o pasos siguientes
- **Edición en pantalla completa**: haga clic en el icono de expansión para ampliar el área de trabajo de edición

### Consideraciones técnicas

**Comportamiento de visualización del mensaje:**

- Los mensajes aparecen en una superposición modal inmediatamente después del envío del formulario
- El contenido admite el formato HTML y mantiene un diseño interactivo
- Los usuarios pueden descartar los mensajes o configurarlos con temporizadores de cierre automático

**Directrices de contenido:**

- Mantenga los mensajes concisos mientras proporciona la información necesaria
- Incluya los siguientes pasos claros cuando corresponda
- Considere incluir números de referencia o detalles de confirmación
- Garantizar un formato compatible con dispositivos móviles

### Implementación de ejemplo

    ¡Gracias por su envío!
    
    Se ha recibido su solicitud y se le ha asignado el número de referencia #REF-2024-001234.
    
    **Qué sucede a continuación:**
    - Recibirá un correo electrónico de confirmación en un plazo de 15 minutos
    - Nuestro equipo revisará su envío en un plazo de 2 días hábiles
    - Nos pondremos en contacto con usted directamente si necesita información adicional
    
    **Necesita asistencia?** Póngase en contacto con nuestro equipo de asistencia en support@example.com

## Configuración de URL de redireccionamiento

Las direcciones URL de redireccionamiento dirigen automáticamente a los usuarios a páginas específicas después del envío del formulario, lo que permite una integración perfecta con los flujos de trabajo existentes o dirige a los usuarios al contenido relevante.

### Cuándo usar URL de redireccionamiento

Las direcciones URL de redireccionamiento son óptimas para:

- **Integración del flujo de trabajo**: Dirigiendo a los usuarios a paneles, páginas de cuenta o pasos siguientes en un proceso
- **Entrega de contenido**: muestra productos, servicios o información relevantes basados en las respuestas del formulario
- **Seguimiento de Analytics**: Direccionar a páginas con implementaciones de seguimiento específicas
- **Procesos de varios pasos**: Mover usuarios a la siguiente fase de flujos de trabajo complejos

### Pasos de implementación

**1. Obtener acceso a propiedades de formulario**

Abra el formulario adaptable en el editor universal y haga clic en el icono **Editar propiedades del formulario** para abrir el cuadro de diálogo de configuración del formulario.

**2. Vaya a la configuración de agradecimiento**

Seleccione la ficha **Gracias** en el cuadro de diálogo Propiedades del formulario para acceder a las opciones de configuración de redireccionamiento.

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

**Referencias de página AEM Sites**

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

## Prácticas recomendadas y recomendaciones

### Directrices de experiencia del usuario

**Optimización de mensajes:**

- **Claridad primero**: Asegúrese de que los usuarios entiendan inmediatamente que su envío se realizó correctamente
- **Valor añadido**: proporcione información que ayude a los usuarios en los pasos siguientes
- **Marca coherente**: mantenga el estilo visual y de voz de su organización
- **Consideración móvil**: Probar mensajes en varios tamaños de pantalla

**Optimización de redireccionamiento:**

- **Optimización de página**: Asegúrese de que los destinos de redireccionamiento estén optimizados para los visitantes posteriores al formulario
- **Rendimiento de carga**: compruebe que las páginas de redireccionamiento se cargan rápidamente para mantener la experiencia del usuario
- **Relevancia del contenido**: Asegúrese de que el contenido de redireccionamiento es relevante para el contexto del formulario

### Consideraciones de seguridad

**Validación de URL:**

- Implemente la validación adecuada para las direcciones URL de redireccionamiento para evitar redirecciones malintencionadas
- Considere los enfoques de lista blanca para los dominios de redireccionamiento permitidos
- Monitorice los patrones de redirección para detectar actividades inusuales

**Seguridad de contenido:**

- Desinfectar el contenido del mensaje de agradecimiento para evitar la inyección de secuencias de comandos
- Implementar directivas de seguridad de contenido adecuadas para el contenido de texto enriquecido
- Revisiones de seguridad periódicas de los destinos de redireccionamiento

### Análisis y seguimiento

**Consideraciones de implementación:**

- **Seguimiento de metas**: configure metas de análisis tanto para las vistas de mensajes de agradecimiento como para las finalizaciones de redireccionamiento
- **Asignación de recorrido de usuario**: Rastree cómo los usuarios interactúan con las experiencias posteriores al envío
- **Optimización de conversión**: mensajes de agradecimiento y destinos de redirección de la prueba A/B diferentes

**Estrategias de medición:**

- Monitorice el tiempo empleado en los mensajes de agradecimiento antes del despido
- Rastrear tasas de clics para vínculos dentro de mensajes de agradecimiento
- Analizar el comportamiento del usuario en las páginas de destino de redirección

## Puntos de comprobación de validación

Después de configurar la experiencia posterior al envío:

**Verificación de configuración:**

- Las propiedades del formulario muestran correctamente la opción de agradecimiento seleccionada
- El contenido del mensaje se muestra correctamente en el modo de vista previa
- Las direcciones URL de redireccionamiento tienen el formato correcto y son accesibles
- Todos los vínculos de los mensajes funcionan correctamente

**Pruebas de experiencia del usuario:**

- Envíe formularios de prueba para verificar la correcta visualización del mensaje de agradecimiento
- Prueba de la funcionalidad de redireccionamiento en distintos navegadores
- Verificar la respuesta móvil de los mensajes de agradecimiento
- Confirmar que los destinos de redirección se cargan correctamente

**Configuración de Analytics:**

- Códigos de seguimiento correctamente implementados para los mensajes de agradecimiento
- Seguimiento de destino de redirección configurado
- Se activan correctamente los eventos de finalización de objetivos

## Próximos pasos

Después de configurar correctamente la experiencia posterior al envío:

- **Monitorizar el rendimiento**: revise los análisis para comprender la participación del usuario con los mensajes de agradecimiento o las páginas de redirección
- **Iterar y mejorar**: Use los comentarios de los usuarios y las perspectivas de datos para refinar su estrategia posterior al envío
- **Implementación de escala**: aplique patrones exitosos en otros formularios de su organización

**Documentación relacionada:**

- [Guía de configuración de envío de formularios](submit-action.md)
- [Prácticas recomendadas de experiencia del usuario](responsive-layout.md)

