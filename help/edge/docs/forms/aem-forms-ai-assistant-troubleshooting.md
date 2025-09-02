---
title: 'Forms Experience Builder: Guía de resolución de problemas'
description: Guía completa de solución de problemas para Forms Experience Builder, que cubre problemas comunes, soluciones y técnicas de depuración para la creación y administración de formularios.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 6a7810fd-2860-410b-867d-8d29afd5297d
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 1%

---


# Forms Experience Builder: Guía de resolución de problemas

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa de usuarios que lo adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta guía de solución de problemas se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Los problemas, las soluciones y las técnicas de depuración pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa de adopción anticipada.

Esta completa guía para la resolución de problemas le ayuda a identificar, diagnosticar y resolver problemas comunes al trabajar con Forms Experience Builder. La guía está organizada por categorías de problemas con correcciones rápidas y soluciones detalladas.

## Referencia rápida: problemas comunes

| Problema | Corrección rápida |
|-------|-----------|
| **La interfaz no se carga** | Actualice el explorador, compruebe la conexión a Internet y los permisos de acceso anticipado |
| **Los comandos no funcionan** | Pruebe `/help` o use lenguaje natural en lugar de comandos de barra diagonal |
| **@fieldName no reconocido** | Revise la ortografía, asegúrese de que el campo exista primero y compruebe la sintaxis del nombre del campo |
| **Error al cargar el archivo** | Utilice PDF/JPG/PNG con menos de 10 MB y compruebe la compatibilidad del formato de archivo |
| **El formulario tiene un aspecto incorrecto** | Sea más específico: &quot;Hacer que sea compatible con dispositivos móviles&quot; en lugar de &quot;corregir el diseño&quot; |
| **Error de integración** | Compruebe las credenciales y los permisos de la API y la disponibilidad del extremo |
| **El formulario no se envía** | Comprobar la configuración de la acción de envío y las reglas de validación |
| **No se muestran errores de validación** | Verificar la configuración de validación de campos y la ubicación de mensajes de error |
| **Problemas de diseño móvil** | Revisar la configuración de diseño interactivo y el tamaño de los campos |
| **Los campos no aparecen** | Comprobación de la lógica condicional y las reglas de visibilidad |
| **Errores de importación** | Comprobar la compatibilidad y los límites de tamaño del formato de archivo |
| **Problemas de rendimiento** | Optimizar el recuento de campos y eliminar validaciones innecesarias |
| **Problemas de accesibilidad** | Revisar las etiquetas de campo, los atributos ARIA y el orden de tabulación |

**¿Aún necesita ayuda?** escriba `/help` seguido de su pregunta específica o comuníquese con el administrador del sistema para obtener asistencia técnica.

## Problemas de acceso y autenticación

### No se puede acceder a Forms Experience Builder

**Síntomas:**

- Interfaz de Forms Experience Builder no visible
- &quot;Acceso denegado&quot; o mensajes de error similares
- Falta el icono de Forms Experience Builder en el editor

**Soluciones:**

1. **Verificar inscripción en el programa de acceso anticipado**
   - Confirme que ha sido aprobado para el programa de adopción anticipada
   - Compruebe que su solicitud se haya enviado desde su correo electrónico de trabajo oficial
   - Comuníquese con `aem-forms-ea@adobe.com` si el acceso sigue pendiente

2. **Comprobar configuración del entorno**
   - Verifique que AEM Forms esté habilitado para su entorno
   - Asegúrese de que utiliza un navegador compatible (Chrome, Firefox, Safari, Edge).
   - Borrar la caché y las cookies del explorador
   - Deshabilitar las extensiones de explorador que puedan interferir

3. **Verificar permisos de usuario**
   - Confirme que tiene las funciones de usuario y los permisos adecuados
   - Consulte con el administrador del sistema los derechos de acceso
   - Verifique que ha iniciado sesión con la cuenta correcta

### Problemas de carga de interfaz

**Síntomas:**

- Interfaz en blanco o parcialmente cargada
- Girando los indicadores de carga que no se completan
- Errores de JavaScript en la consola del explorador

**Soluciones:**

1. **Solución de problemas del explorador**
   - Actualizar la página (Ctrl+F5 o Cmd+Mayús+R)
   - Pruebe con otro navegador o modo incógnito/privado
   - Buscar actualizaciones del explorador e instalar si están disponibles
   - Deshabilitar los bloqueadores de anuncios y las extensiones de privacidad temporalmente

2. **Conectividad de red**
   - Verificar una conexión estable a Internet
   - Comprobar si el cortafuegos corporativo está bloqueando los dominios necesarios
   - Realizar pruebas con otra conexión de red si es posible
   - Póngase en contacto con el soporte técnico para problemas de configuración de red

3. **Problemas de caché y almacenamiento**
   - Borrar la caché del explorador y el almacenamiento local
   - Restablecer la configuración predeterminada del explorador
   - Compruebe el espacio disponible en disco en el dispositivo
   - Intente acceder a desde un dispositivo diferente

## Problemas de comandos e interacción

### Los Comandos De Barra No Funcionan

**Síntomas:**

- `/create-form` u otros comandos de barra diagonal no reconocidos
- No aparecen sugerencias de autocompletar
- Los comandos generan mensajes de error

**Soluciones:**

1. **Verificación de sintaxis de comando**
   - Asegúrese de que el formato de comando es correcto: `/command-name description`
   - Comprobar errores tipográficos en los nombres de comando
   - Utilice el lenguaje natural como alternativa: &quot;Crear un formulario de contacto&quot;
   - Pruebe `/help` para verificar la disponibilidad del comando

2. **Comandos específicos de contexto**
   - Compruebe que está en el contexto correcto del editor (editor universal o editor de Forms adaptable)
   - Algunos comandos solo funcionan en entornos específicos
   - Comprobar la referencia de comandos para los requisitos de contexto

3. **Enfoques alternativos**
   - Utilizar lenguaje natural en lugar de comandos de barra diagonal
   - Divida comandos complejos en solicitudes más pequeñas y sencillas
   - Pruebe la creación de formularios paso a paso en lugar de un comando complejo único

### Las Referencias De Campo No Funcionan

**Síntomas:**

- `@fieldName` referencias no reconocidas
- Mensajes de error sobre campos desconocidos
- Las modificaciones de campo no se aplican correctamente

**Soluciones:**

1. **Verificación de nombre de campo**
   - Comprobar la ortografía exacta de los nombres de campo (con distinción entre mayúsculas y minúsculas)
   - Asegúrese de que el campo exista antes de hacer referencia a él
   - Utilice el nombre de campo exacto como se creó, no la etiqueta de visualización
   - Verificar las convenciones de nomenclatura de campos (camelCase, snake_case, etc.)

2. **Sintaxis de referencia de campo**
   - Usar sintaxis `@fieldName` adecuada sin espacios
   - Evite los caracteres especiales en las referencias de campo
   - Buscar caracteres invisibles o problemas de formato
   - Intente volver a crear la referencia de campo manualmente

3. **Referencias de campo de depuración**
   - Mostrar primero todos los campos existentes: &quot;Mostrar todos los campos de formulario actuales&quot;
   - Cree campos antes de hacer referencia a ellos en las reglas
   - Usar nombres de campo simples sin caracteres complejos
   - Referencias de campo de prueba de a una por vez

## Problemas de creación y diseño de formularios

### El formulario no se crea como se esperaba

**Síntomas:**

- Faltan campos solicitados en el formulario generado
- Tipos de campo o diseños incorrectos
- La estructura del formulario no coincide con la descripción

**Soluciones:**

1. **Mejorar la especificidad del indicador**
   - Obtenga más información en las descripciones de los formularios
   - Especificar tipos de campo exactos y requisitos de validación
   - Incluir las preferencias de diseño y los requisitos de experiencia del usuario
   - Divida los formularios complejos en solicitudes más pequeñas e incrementales

2. **Enfoque de desarrollo iterativo**
   - Comenzar con la estructura básica del formulario
   - Adición de campos y funciones de forma incremental
   - Pruebe cada adición antes de continuar
   - Refinamiento mediante conversación en lugar de una sola solicitud compleja

3. **Ejemplo de mejores indicadores**

   En lugar de:

       Crear un formulario para clientes
   
   Utilice:

       Crear un formulario de contacto de cliente con:
       - Nombre completo (campo de texto obligatorio)
       - Dirección de correo electrónico (requerida con la validación)
       - Número de teléfono (opcional, con formato)
       - Mensaje (área de texto requerida, máximo 500 caracteres)
       - Enviar a notificación por correo electrónico
   

### Problemas de diseño y estilo

**Síntomas:**

- El formulario parece dañado en dispositivos móviles
- Espaciado o alineación incoherentes
- Los campos no se muestran correctamente
- Jerarquía visual deficiente

**Soluciones:**

1. **Capacidad de respuesta móvil**
   - Solicitar optimizaciones específicas para móviles: &quot;Hacer que este formulario sea compatible con dispositivos móviles&quot;
   - Especificar requisitos de diseño interactivo
   - Realizar pruebas en dispositivos móviles reales
   - Uso de diseños de una sola columna para móviles

2. **Mejoras de diseño**
   - Especifique los requisitos de diseño: &quot;Organizar los campos de dirección en dos columnas&quot;
   - Solicite un estilo específico: &quot;Utilice colores profesionales y una tipografía limpia&quot;
   - Especificar las necesidades de espaciado y alineación
   - Solicitar cumplimiento de accesibilidad

3. **Coherencia de marca**
   - Preparar directrices de marca antes de crear formularios
   - Incluir códigos de color y fuentes específicos en las solicitudes
   - Utilizar un estilo coherente en todos los formularios
   - Crear plantillas de marca para reutilizarlas

### Problemas de lógica condicional

**Síntomas:**

- Las reglas no se activan según lo esperado
- Campos que se muestran u ocultan incorrectamente
- La lógica de validación no funciona
- Fallo de reglas empresariales complejas

**Soluciones:**

1. **Simplificación de reglas**
   - Divida las reglas complejas en condiciones más pequeñas y sencillas
   - Prueba de cada regla individualmente antes de combinarla
   - Utilice condiciones claras y específicas: &quot;Mostrar @spouseInfo cuando @maritalStatus igual a &#39;Casado&#39;&quot;
   - Evite inicialmente la lógica anidada o demasiado compleja

2. **Prueba y depuración de reglas**
   - Probar todas las rutas y escenarios de usuario posibles
   - Comprobar nombres y valores de campo en condiciones
   - Compruebe la distinción entre mayúsculas y minúsculas en las condiciones de regla
   - Utilice el modo de depuración para rastrear la ejecución de reglas

3. **Implementación de lógica empresarial**
   - Documente claramente los requisitos comerciales antes de la implementación
   - Implementación de reglas de forma incremental y prueba cada paso
   - Proporcionar comentarios claros al usuario cuando se activan las reglas
   - Gestión de casos extremos y escenarios de excepción

## Problemas de importación y conversión de archivos

### Errores de importación de PDF

**Síntomas:**

- Los archivos de PDF no se cargan ni procesan
- Campos o contenido que faltan en formularios convertidos
- Mensajes de error durante la conversión a PDF
- Reconocimiento de campo defectuoso de PDF

**Soluciones:**

1. **Tamaño y formato de archivo**
   - Asegúrese de que los archivos de PDF tengan menos de 10 MB
   - Utilice PDF de alta calidad basados en texto (no imágenes escaneadas)
   - Compruebe que PDF no está cifrado ni protegido por contraseña
   - Intente convertir PDF al formato de imagen si la extracción de texto falla

2. **Optimización de la calidad de PDF**
   - Utilizar PDF con campos de formulario claros y bien definidos
   - Garantizar un buen contraste y un texto legible
   - Evite diseños complejos o elementos superpuestos
   - Proporcionar contexto adicional en la solicitud de conversión

3. **Mejora de conversión**
   - Describir en detalle la estructura del formulario esperada
   - Especificar tipos de campo y requisitos de validación
   - Solicitar mejoras específicas: &quot;Añadir capacidad de respuesta y validación móviles&quot;
   - Revisar y perfeccionar manualmente los formularios convertidos

### Problemas de conversión de imágenes y capturas de pantalla

**Síntomas:**

- Reconocimiento deficiente de campos a partir de imágenes
- Tipos de campo o diseños incorrectos
- Faltan elementos de formulario
- Errores o tiempos de espera de conversión

**Soluciones:**

1. **Requisitos de calidad de imagen**
   - Utilice imágenes de alta resolución (mínimo 300 ppp)
   - Garantizar una buena iluminación y contraste
   - Evite sombras, reflejos o distorsiones
   - Recortar imágenes para centrarse únicamente en el contenido del formulario

2. **Formatos de imagen óptimos**
   - Uso de formatos PNG o JPG para obtener mejores resultados
   - Evite las imágenes comprimidas de GIF o de baja calidad
   - Asegúrese de que el texto sea claramente legible en la imagen
   - Pruebe distintas orientaciones de imagen si es necesario

3. **Guía de conversión**
   - Proporcionar descripciones detalladas de la estructura del formulario
   - Especifique explícitamente los tipos de campo y los requisitos
   - Solicitar mejoras específicas durante la conversión
   - Prepárese para realizar ajustes manuales después de la conversión

## Problemas de integración y envío

### Errores de envío de formularios

**Síntomas:**

- Forms no se envía correctamente
- Mensajes de error durante el envío
- Los datos no llegan a los destinos previstos
- Errores de tiempo de espera durante el envío

**Soluciones:**

1. **Configuración de acción de envío**
   - Verificar que la acción de envío esté configurada correctamente
   - Compruebe los extremos de la API y las credenciales de autenticación
   - Pruebe primero con el envío simple por correo electrónico
   - Validar requisitos de formato de datos

2. **Red y conectividad**
   - Compruebe la conectividad a Internet y la estabilidad de la red
   - Verificar configuración del cortafuegos para permitir envíos de formularios
   - Probar desde diferentes conexiones de red
   - Compruebe si hay restricciones de seguridad o proxy corporativo

3. **Problemas de validación de datos**
   - Asegúrese de que se hayan rellenado todos los campos obligatorios
   - Comprobar que los formatos de datos coinciden con requisitos de API
   - Compruebe si hay caracteres especiales o problemas de codificación
   - Realizar la prueba primero con un conjunto de datos mínimo

### Problemas de integración de API

**Síntomas:**

- Los extremos de API de REST no responden
- Errores de autenticación
- No coinciden los formatos de datos
- Tiempos de espera o errores de integración

**Soluciones:**

1. **Verificación de configuración de API**
   - Verifique que las direcciones URL de extremo de API sean correctas y accesibles
   - Compruebe las credenciales y los permisos de autenticación
   - Prueba independiente de los extremos de la API con herramientas como Postman
   - Verifique que la API acepte el formato de datos correcto (JSON, XML, etc.)

2. **Problemas de asignación de datos**
   - Asegúrese de que los nombres de los campos de formulario coincidan con los requisitos de parámetros API
   - Compruebe si faltan campos obligatorios.
   - Comprobar la compatibilidad del tipo de datos (cadenas, números, fechas)
   - Realizar pruebas con datos de ejemplo para identificar problemas de asignación

3. **Control y depuración de errores**
   - Habilitar el registro de errores detallado para llamadas API
   - Compruebe los códigos de respuesta de API y los mensajes de error
   - Implementar la lógica de reintentos para errores temporales
   - Proporcionar opciones de reserva para los usuarios cuando falle la API

### Problemas de integración de correo electrónico

**Síntomas:**

- Correos electrónicos de confirmación no enviados
- Correos electrónicos dirigidos a carpetas de correo no deseado
- Formato de correo electrónico incorrecto
- Faltan datos de formulario en correos electrónicos

**Soluciones:**

1. **Configuración de correo electrónico**
   - Verificar que las direcciones de correo electrónico tengan el formato correcto
   - Comprobar la configuración y autenticación de SMTP
   - Pruebe primero con direcciones de correo electrónico simples
   - Comprobar permisos y cuotas del servidor de correo electrónico

2. **Optimización de entrega de correo electrónico**
   - Utilice los encabezados de correo electrónico e información del remitente adecuados
   - Evitar palabras de déclencheur de spam en las líneas de asunto
   - Incluir mecanismos adecuados de cancelación de suscripción
   - Prueba de envío de correo electrónico a diferentes proveedores

3. **Contenido y formato**
   - Verificar que los datos del formulario tengan el formato correcto en los correos electrónicos
   - Compruebe si hay caracteres especiales o problemas de codificación
   - Prueba de plantillas de correo electrónico con varias combinaciones de datos
   - Asegúrese de que el contenido del correo electrónico sea accesible y legible

## Problemas de rendimiento y carga

### Carga lenta de formulario

**Síntomas:**

- Forms tarda mucho tiempo en cargarse inicialmente
- Interacciones lentas del usuario
- Tiempos de espera durante operaciones de formulario
- Bajo rendimiento en dispositivos móviles

**Soluciones:**

1. **Optimización de formularios**
   - Reducción del número de campos y la complejidad
   - Implementación de la carga diferida en secciones no críticas
   - Optimización de imágenes y recursos para la entrega web
   - Quitar lógica o reglas de validación innecesarias

2. **Optimización de explorador y dispositivo**
   - Borrar la caché del explorador y los archivos temporales
   - Cierre las pestañas y aplicaciones innecesarias del explorador
   - Comprobar la memoria y el almacenamiento del dispositivo disponible
   - Pruebe exploradores diferentes para comparar el rendimiento

3. **Optimización de red**
   - Probar con diferentes conexiones de red
   - Compruebe si hay congestión de red o limitaciones de ancho de banda
   - Si es posible, utilice una conexión por cable en lugar de WiFi
   - Póngase en contacto con el soporte técnico de TI para problemas de rendimiento de red

### Problemas de rendimiento de validación

**Síntomas:**

- Respuestas de validación lentas
- Visualización del mensaje de error aplazado
- Congelación de formularios durante la validación
- Errores de tiempo de espera durante validación de campo

**Soluciones:**

1. **Optimización de validación**
   - Reducir la frecuencia de la validación en tiempo real
   - Implementar la devolución para llamadas de validación
   - Simplificar reglas de validación complejas
   - Utilice la validación del lado del cliente siempre que sea posible

2. **Simplificación de reglas**
   - Dividir la validación compleja en reglas más pequeñas
   - Eliminación de validaciones innecesarias entre campos
   - Optimizar la lógica condicional para el rendimiento
   - Resultados de validación de caché donde corresponda

3. **Mejoras en la experiencia del usuario**
   - Proporcione comentarios inmediatos para realizar validaciones sencillas
   - Utilice validación progresiva en lugar de tiempo real para reglas complejas
   - Mostrar indicadores de carga durante los procesos de validación
   - Permitir que los usuarios continúen mientras los procesos de validación se realizan en segundo plano

## Solución de problemas avanzada

### Modo de depuración y diagnóstico

**Habilitar información de depuración**

Utilice estas indicaciones para obtener información más detallada sobre los problemas del formulario:

    Habilite el modo de depuración para identificar problemas con el envío de formularios y la validación de campos
    
    Analizar errores de formularios: comprobar reglas de validación, respuestas de API y patrones de entrada de usuarios
    
    Mostrar información detallada sobre la estructura del formulario y la configuración de campos

### Técnicas de análisis de errores

**Método de depuración sistemática**

1. **Aislar el problema**
   - Pruebas con una configuración mínima del formulario
   - Eliminación temporal de funciones complejas
   - Prueba de componentes individuales por separado
   - Utilizar el proceso de eliminación para identificar la causa raíz

2. **Recopilar información de diagnóstico**
   - Compruebe si la consola del explorador contiene errores de JavaScript
   - Revisar solicitudes y respuestas de red
   - Documente los pasos exactos para reproducir el problema
   - Recopilar capturas de pantalla y mensajes de error

3. **Variables de entorno de prueba**
   - Pruebe diferentes exploradores y dispositivos
   - Realizar pruebas con diferentes cuentas de usuario y permisos
   - Verificar en diferentes entornos de red
   - Comparar con formularios o configuraciones en funcionamiento

### Análisis y monitorización de registros

**Depuración de la consola del explorador**

1. Abrir herramientas para desarrolladores de exploradores (F12)
2. Compruebe si hay errores de JavaScript en la pestaña Consola
3. Pestaña Revisar red para solicitudes fallidas
4. Ficha Supervisar rendimiento para operaciones lentas

**Patrones de error comunes**

- **Errores de CORS**: Problemas de solicitudes de origen cruzado con integraciones de API
- **Errores de autenticación**: Credenciales no válidas o tokens caducados
- **Errores de validación**: conflictos de reglas de validación de campos o errores de sintaxis
- **Tiempos de espera de red**: Conexiones de red lentas o poco fiables

## Obtención de ayuda adicional

### Recursos de autoservicio

**Sistema de ayuda integrado**

- Utilice el comando `/help` seguido de preguntas específicas
- Acceso a la ayuda contextual dentro de la interfaz de Forms Experience Builder
- Revise cuidadosamente los mensajes de error para obtener instrucciones específicas
- Consulte la [Guía de introducción de Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Recursos de documentación**

- [Biblioteca de mensajes de Forms Experience Builder](ai-assistant-prompt-library.md)
- [Prácticas recomendadas para Forms Experience Builder](aem-forms-ai-assistant-best-practices.md)
- [Documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es)

### Escalación y asistencia

**Cuándo ponerse en contacto con el soporte técnico**

- Los problemas persisten después de probar las soluciones documentadas
- Problemas de todo el sistema que afectan a varios usuarios
- Problemas de seguridad o integridad de los datos
- Problemas de integración que requieren configuración en el nivel del sistema

**Información para proporcionar**

- Descripción detallada del problema y pasos a seguir
- Capturas de pantalla o grabaciones de pantalla del problema
- Información del sistema y del explorador
- Mensajes de error y registros de la consola
- Detalles de configuración e integración de formularios

**Métodos de contacto**

- Administrador del sistema: para problemas de entorno y acceso
- Soporte técnico: para problemas complejos de integración y configuración
- Programa de acceso anticipado: `aem-forms-ea@adobe.com` para problemas específicos del programa

### Comunidad e intercambio de conocimientos

**Prácticas recomendadas para la resolución de problemas**

- Soluciones de documentos para referencia futura
- Compartir enfoques de solución de problemas correctos con los integrantes del equipo
- Contribución a la base de conocimientos organizativos
- Participar en comunidades de usuarios y foros

**Mejora continua**

- Revisión periódica de problemas y soluciones comunes
- Actualizar procedimientos de resolución de problemas en función de nuevos hallazgos
- Sesiones de formación e intercambio de conocimientos
- Comentarios sobre las mejoras de funciones para el equipo de producto

Esta guía de solución de problemas se actualiza continuamente en función de los comentarios de los usuarios y las nuevas funciones de Forms Experience Builder. Para obtener la información más reciente y los recursos adicionales, consulte la [documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es).
