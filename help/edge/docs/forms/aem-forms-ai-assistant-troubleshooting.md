---
title: 'Forms Experience Builder: Guía de resolución de problemas'
description: Guía completa de resolución de problemas para Forms Experience Builder, que trata problemas comunes, soluciones y técnicas de depuración para la creación y administración de formularios.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 6a7810fd-2860-410b-867d-8d29afd5297d
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 100%

---


# Forms Experience Builder: Guía de resolución de problemas

>[!NOTE]
>
> Forms Experience Builder está disponible en el programa para primeros usuarios. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta guía de resolución de problemas se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Los problemas, las soluciones y las técnicas de depuración pueden cambiar a medida que Forms Experience Builder siga evolucionando durante el programa para primeros usuarios.

Esta completa guía de resolución de problemas le ayuda a identificar, diagnosticar y resolver problemas comunes que se pueden dar al trabajar con Forms Experience Builder. La guía está organizada por categorías de problemas con correcciones rápidas y soluciones detalladas.

## Referencia rápida: Problemas comunes

| Problema | Corrección rápida |
|-------|-----------|
| **La interfaz no se carga** | Actualice el explorador, compruebe la conexión a Internet y los permisos de acceso anticipado |
| **Los comandos no funcionan** | Pruebe `/help` o use lenguaje natural en lugar de comandos de barra diagonal |
| **@fieldName no reconocido** | Revise la ortografía, asegúrese primero de que el campo existe y compruebe la sintaxis del nombre del campo |
| **Error al cargar el archivo** | Utilice PDF/JPG/PNG de menos de 10 MB, compruebe la compatibilidad del formato de archivo |
| **El aspecto del formulario no es correcto** | Sea más específico: “Hacerlo compatible con dispositivos móviles” en lugar de “Corregir diseño” |
| **Error de integración** | Compruebe las credenciales de API y los permisos, así como la disponibilidad del punto final |
| **Formulario no se envía** | Compruebe la configuración de la acción de envío y las reglas de validación |
| **No se muestran los errores de validación** | Compruebe la configuración de validación de campos y la ubicación de los mensajes de error |
| **Problemas de diseño para móviles** | Revise la configuración del diseño interactivo y el tamaño de los campos |
| **Los campos no aparecen** | Compruebe la lógica condicional y las reglas de visibilidad |
| **Errores de importación** | Compruebe la compatibilidad del formato de archivo y los límites de tamaño |
| **Problemas de rendimiento** | Optimice el recuento de campos y elimine validaciones innecesarias |
| **Problemas de accesibilidad** | Revise las etiquetas de campo, los atributos ARIA y el orden de tabulación |

**¿Aún necesita ayuda?** Escriba `/help` seguido de su pregunta específica o póngase en contacto con el administrador del sistema para obtener asistencia técnica.

## Problemas de acceso y autenticación

### No se puede acceder a Forms Experience Builder

**Síntomas:**

- Interfaz de Forms Experience Builder no visible
- “Acceso denegado” o mensajes de error similares
- Falta el icono de Forms Experience Builder en el editor

**Soluciones:**

1. **Verifique la inscripción en el programa de acceso anticipado**
   - Confirme que ha sido aprobado para el programa para primeros usuarios
   - Compruebe que su solicitud se haya enviado desde su correo electrónico de trabajo oficial
   - Contacte con `aem-forms-ea@adobe.com` si el acceso sigue pendiente

2. **Compruebe la configuración del entorno**
   - Verifique que AEM Forms esté habilitado para su entorno
   - Asegúrese de estar utilizando un explorador compatible (Chrome, Firefox, Safari, Edge)
   - Borre la caché del explorador y las cookies
   - Deshabilite las extensiones del explorador que puedan interferir

3. **Verifique los permisos de usuario**
   - Confirme que tiene las funciones de usuario y los permisos adecuados
   - Consulte con el administrador del sistema sus derechos de acceso
   - Verifique que ha iniciado sesión con la cuenta correcta

### Problemas de carga de interfaz

**Síntomas:**

- Interfaz en blanco o parcialmente cargada
- Los indicadores de carga giran pero no terminan
- Errores de JavaScript en la consola del explorador

**Soluciones:**

1. **Solución de problemas del explorador**
   - Actualice la página (Ctrl+F5 o Cmd+Mayús+R)
   - Pruebe con otro explorador o en modo incógnito/privado
   - Compruebe si hay actualizaciones del explorador e instálelas si hay alguna disponible
   - Deshabilite los bloqueadores de anuncios y las extensiones de privacidad temporalmente

2. **Conectividad de red**
   - Verifique que la conexión a Internet es estable
   - Compruebe si el cortafuegos corporativo está bloqueando los dominios necesarios
   - Realice pruebas con otra conexión de red, si es posible
   - Póngase en contacto con el soporte informático si tiene problemas de configuración de red

3. **Problemas de caché y de almacenamiento**
   - Borre la caché del explorador y el almacenamiento local
   - Restablezca la configuración predeterminada del explorador
   - Compruebe el espacio disponible en disco de su dispositivo
   - Intente acceder desde un dispositivo diferente

## Problemas de comandos e interacción

### Los comandos de barra no funcionan

**Síntomas:**

- `/create-form` u otros comandos de barra diagonal no se reconocen
- No aparecen sugerencias de autocompletar
- Los comandos generan mensajes de error

**Soluciones:**

1. **Verificación de la sintaxis del comando**
   - Asegúrese de que el formato del comando es correcto: `/command-name description`
   - Compruebe si hay errores tipográficos en los nombres de los comandos
   - Utilice el lenguaje natural como alternativa: “Crear un formulario de contacto”
   - Pruebe `/help` para verificar la disponibilidad del comando

2. **Comandos específicos de contexto**
   - Compruebe que está en el contexto del editor correcto (editor universal o editor de formularios adaptable)
   - Algunos comandos solo funcionan en entornos específicos
   - Compruebe la referencia del comando para los requisitos de contexto

3. **Enfoques alternativos**
   - Utilice lenguaje natural en lugar de comandos de barra diagonal
   - Divida comandos complejos en solicitudes más pequeñas y sencillas
   - Pruebe la creación de formularios paso a paso en lugar de un comando único complejo

### Las referencias de campo no funcionan

**Síntomas:**

- Referencias de `@fieldName` no reconocidas
- Mensajes de error sobre campos desconocidos
- Las modificaciones de campo no se aplican correctamente

**Soluciones:**

1. **Verificación de nombre de campo**
   - Compruebe la ortografía exacta de los nombres de campo (con distinción entre mayúsculas y minúsculas)
   - Asegúrese de que el campo exista antes de hacer referencia a él
   - Utilice el nombre de campo exacto tal y como se creó, no la etiqueta de visualización
   - Verifique las convenciones de nomenclatura de campos (camelCase, snake_case, etc.)

2. **Sintaxis de referencia de campo**
   - Use la sintaxis `@fieldName` correcta, sin espacios
   - Evite los caracteres especiales en las referencias de campo
   - Compruebe si hay caracteres invisibles o problemas de formato
   - Intente volver a crear la referencia de campo manualmente

3. **Depuración de referencias de campo**
   - Enumere primero todos los campos existentes: “Mostrar todos los campos de formulario actuales”
   - Cree los campos antes de hacer referencia a ellos en las reglas
   - Use nombres de campo sencillos, sin caracteres complejos
   - Pruebe las referencias de campo de una en una

## Problemas de creación y diseño de formularios

### El formulario no se crea como se esperaba

**Síntomas:**

- Al formulario generado le faltan campos solicitados
- Tipos de campo o diseños incorrectos
- La estructura del formulario no coincide con la descripción

**Soluciones:**

1. **Mejorar la especificidad de la indicación**
   - Proporcione descripciones de formularios más detalladas
   - Especifique los tipos de campo exactos y los requisitos de validación
   - Incluya las preferencias de diseño y los requisitos de experiencia del usuario
   - Divida los formularios complejos en solicitudes más pequeñas e incrementales

2. **Enfoque de desarrollo iterativo**
   - Empiece con la estructura básica del formulario
   - Añada campos y funciones de forma incremental
   - Pruebe cada adición antes de continuar
   - Perfeccione mediante la conversación en lugar de usar una única solicitud compleja

3. **Ejemplo de mejores indicaciones**

   En lugar de:

       Crear un formulario para clientes
   
   Use:

       Crear un formulario de contacto de cliente con:
       - Nombre completo (campo de texto obligatorio)
       - Dirección de correo electrónico (obligatoria con la validación)
       - Número de teléfono (opcional, con formato)
       - Mensaje (área de texto obligatoria, 500 caracteres como máximo)
       - Enviar a notificación por correo electrónico
   
### Problemas de diseño y estilo

**Síntomas:**

- El formulario aparece truncado en dispositivos móviles
- Espaciado o alineación incoherentes
- Los campos no se muestran correctamente
- Jerarquía visual deficiente

**Soluciones:**

1. **Capacidad de respuesta móvil**
   - Solicite optimizaciones específicas para móviles: “Hacer que este formulario sea compatible con dispositivos móviles”
   - Especifique los requisitos de diseño interactivo
   - Realice pruebas en dispositivos móviles reales
   - Use diseños de una sola columna para móviles

2. **Mejoras de diseño**
   - Especifique los requisitos de diseño: “Organizar los campos de dirección en dos columnas”
   - Solicite un estilo específico: “Utilizar colores profesionales y una tipografía limpia”
   - Especifique las necesidades de espaciado y alineación
   - Solicite el cumplimiento de accesibilidad

3. **Coherencia de marca**
   - Prepare directrices de marca antes de crear formularios
   - Incluya códigos de color y fuentes específicos en las solicitudes
   - Utilice un estilo coherente en todos los formularios
   - Cree plantillas de marca para reutilizarlas

### Problemas de lógica condicional

**Síntomas:**

- Las reglas no se activan según lo esperado
- Campos que se muestran u ocultan incorrectamente
- La lógica de validación no funciona
- Reglas empresariales complejas que fallan

**Soluciones:**

1. **Simplificación de reglas**
   - Divida las reglas complejas en condiciones más pequeñas y sencillas
   - Pruebe cada regla individualmente antes de combinarla
   - Utilice condiciones claras y específicas: “Mostrar @spouseInfo cuando @maritalStatus sea ‘Casado’”
   - Evite inicialmente la lógica anidada o demasiado compleja

2. **Prueba y depuración de reglas**
   - Pruebe todas las rutas y escenarios de usuario posibles
   - Compruebe los nombres y valores de campo de las condiciones
   - Compruebe la distinción entre mayúsculas y minúsculas en las condiciones de la regla
   - Utilice el modo de depuración para rastrear la ejecución de reglas

3. **Implementación de lógica empresarial**
   - Documente claramente los requisitos empresariales antes de la implementación
   - Implemente las reglas de forma incremental y pruebe cada paso
   - Proporcione comentarios claros al usuario cuando se activen las reglas
   - Gestione los casos extremos y escenarios de excepción

## Problemas de importación y conversión de archivos

### Errores de importación de PDF

**Síntomas:**

- Los archivos PDF no se cargan ni procesan
- A los formularios convertidos les faltan campos o contenido
- Mensajes de error durante la conversión a PDF
- Reconocimiento inadecuado de los campos del PDF

**Soluciones:**

1. **Tamaño y formato de archivo**
   - Asegúrese de que el tamaño de los archivos PDF sea inferior a 10 MB
   - Utilice archivos PDF de alta calidad basados en texto (no imágenes escaneadas)
   - Compruebe que el PDF no está cifrado ni protegido por contraseña
   - Intente convertir el PDF al formato de imagen si la extracción de texto fallara

2. **Optimización de la calidad de PDF**
   - Utilice archivos PDF con campos de formulario claros y bien definidos
   - Garantice que el texto es legible y con buen contraste
   - Evite diseños complejos o elementos superpuestos
   - Proporcione contexto adicional en la solicitud de conversión

3. **Mejora de conversión**
   - Describa en detalle la estructura del formulario esperada
   - Especifique los tipos de campo y los requisitos de validación
   - Solicite mejoras específicas: “Añadir capacidad de respuesta y validación para móviles”
   - Revise y perfeccione manualmente los formularios convertidos

### Problemas de conversión de imágenes y capturas de pantalla

**Síntomas:**

- Reconocimiento inadecuado de los campos de las imágenes
- Tipos de campo o diseños incorrectos
- Faltan elementos de formulario
- Errores de conversión o tiempos de espera

**Soluciones:**

1. **Requisitos de calidad de imagen**
   - Utilice imágenes de alta resolución (300 ppp como mínimo)
   - Asegúrese de una buena iluminación y contraste
   - Evite sombras, reflejos o distorsiones
   - Recorte las imágenes para centrarse únicamente en el contenido del formulario

2. **Formatos de imagen óptimos**
   - Use los formatos PNG o JPG para obtener mejores resultados
   - Evite las imágenes GIF o comprimidas de baja calidad
   - Asegúrese de que el texto sea claramente legible en la imagen
   - Pruebe distintas orientaciones de imagen, si es necesario

3. **Guía de conversión**
   - Proporcione descripciones detalladas de la estructura del formulario
   - Especifique explícitamente los tipos de campo y los requisitos
   - Solicite mejoras específicas durante la conversión
   - Prepárese para realizar ajustes manuales después de la conversión

## Problemas de integración y envío

### Errores de envío de formularios

**Síntomas:**

- Los formularios no se envían correctamente
- Mensajes de error durante el envío
- Los datos no llegan a los destinos previstos
- Errores de tiempo de espera durante el envío

**Soluciones:**

1. **Configuración de la acción de envío**
   - Verifique que la acción de envío se ha configurado correctamente
   - Compruebe los puntos finales de la API y las credenciales de autenticación
   - Pruebe primero con el envío simple por correo electrónico
   - Valide los requisitos de formato de datos

2. **Red y conectividad**
   - Compruebe la conectividad a Internet y la estabilidad de la red
   - Verifique que la configuración del cortafuegos permite el envío de formularios
   - Pruebe desde distintas conexiones de red
   - Compruebe si hay restricciones de seguridad o proxy corporativo

3. **Problemas de validación de datos**
   - Asegúrese de que se han rellenado todos los campos obligatorios
   - Verifique que los formatos de datos coinciden con los requisitos de API
   - Compruebe si hay caracteres especiales o problemas de codificación
   - Pruebe primero con un conjunto de datos mínimo

### Problemas de integración de API

**Síntomas:**

- Los puntos finales de API de REST no responden
- Errores de autenticación
- Discrepancias en el formato de datos
- Tiempos de espera o errores de integración

**Soluciones:**

1. **Verificación de configuración de API**
   - Verifique que las URL de punto final de API sean correctas y accesibles
   - Compruebe las credenciales de autenticación y los permisos
   - Pruebe los puntos finales de API por separado con herramientas como Postman
   - Verifique que la API acepta el formato de datos correcto (JSON, XML, etc.)

2. **Problemas de asignación de datos**
   - Asegúrese de que los nombres de los campos del formulario coincidan con los requisitos de parámetros de API
   - Compruebe si faltan campos obligatorios
   - Verifique la compatibilidad del tipo de datos (cadenas, números, fechas)
   - Pruebe con datos de muestra para identificar problemas de asignación

3. **Gestión y depuración de errores**
   - Habilite el registro de errores detallado para las llamadas API
   - Compruebe los códigos de respuesta de API y los mensajes de error
   - Implemente la lógica de reintentos para errores temporales
   - Proporcione opciones de reserva para los usuarios cuando falle la API

### Problemas de integración de correo electrónico

**Síntomas:**

- Los correos electrónicos de confirmación no se envían
- Los correos electrónicos se dirigen a las carpetas de correo no deseado
- Formato de correo electrónico incorrecto
- Faltan datos del formulario en los correos electrónicos

**Soluciones:**

1. **Configuración de correo electrónico**
   - Verifique que las direcciones de correo electrónico tienen el formato correcto
   - Compruebe la configuración y autenticación de SMTP
   - Pruebe primero con direcciones de correo electrónico simples
   - Verifique los permisos y las cuotas del servidor de correo electrónico

2. **Optimización de envío de correo electrónico**
   - Utilice encabezados de correo electrónico e información del remitente adecuados
   - Evite usar en las líneas de asunto palabras que puedan definir el mensaje como spam
   - Incluya mecanismos adecuados para cancelar la suscripción
   - Pruebe a enviar correos electrónicos a diferentes proveedores

3. **Contenido y formato**
   - Verifique que los datos del formulario tienen el formato correcto en los correos electrónicos
   - Compruebe si hay caracteres especiales o problemas de codificación
   - Prueba de plantillas de correo electrónico con varias combinaciones de datos
   - Asegúrese de que el contenido del correo electrónico sea accesible y legible

## Problemas de rendimiento y carga

### Carga lenta de formularios

**Síntomas:**

- Forms tarda mucho tiempo en cargarse inicialmente
- Interacciones lentas del usuario
- Tiempos de espera durante las operaciones de formulario
- Bajo rendimiento en dispositivos móviles

**Soluciones:**

1. **Optimización de formulario**
   - Reduzca el número de campos y la complejidad
   - Implemente la carga diferida en secciones no críticas
   - Optimice las imágenes y recursos para la entrega web
   - Quite lógica o reglas de validación innecesarias

2. **Optimización de explorador y dispositivo**
   - Borre la caché del explorador y los archivos temporales
   - Cierre las pestañas y aplicaciones innecesarias del explorador
   - Compruebe la memoria y el almacenamiento disponibles del dispositivo
   - Pruebe exploradores diferentes para comparar el rendimiento

3. **Optimización de red**
   - Pruebe con diferentes conexiones de red
   - Compruebe si hay congestión de red o limitaciones de ancho de banda
   - Utilice una conexión por cable en lugar de WiFi, si es posible
   - Contacte con el soporte de TI para problemas de rendimiento de red

### Problemas de rendimiento de validación

**Síntomas:**

- Respuestas de validación lentas
- Visualización del mensaje de error aplazado
- Congelación de formularios durante la validación
- Errores de tiempo de espera durante la validación de campos

**Soluciones:**

1. **Optimización de validación**
   - Reduzca la frecuencia de la validación en tiempo real
   - Implemente la devolución para llamadas de validación
   - Simplifique las reglas de validación complejas
   - Use la validación del lado del cliente siempre que sea posible

2. **Simplificación de reglas**
   - Divida la validación compleja en reglas más pequeñas
   - Quite validaciones innecesarias entre campos
   - Optimice la lógica condicional para el rendimiento
   - Almacene en caché los resultados de la validación cuando proceda

3. **Mejoras en la experiencia del usuario**
   - Proporcione comentarios inmediatos para validaciones sencillas
   - Utilice la validación progresiva, en lugar de en tiempo real, para reglas complejas
   - Muestre indicadores de carga durante los procesos de validación
   - Permita que los usuarios continúen mientras los procesos de validación se realizan en segundo plano

## Resolución de problemas avanzada

### Modo de depuración y diagnóstico

**Habilitación de información de depuración**

Utilice estas indicaciones para obtener información más detallada sobre los problemas del formulario:

    Habilite el modo de depuración para identificar problemas con el envío de formularios y la validación de campos
    
    Analice los errores del formulario: compruebe las reglas de validación, respuestas de API y patrones de entrada de usuarios
    
    Muestre información detallada sobre la estructura del formulario y la configuración de campos

### Técnicas de análisis de errores

**Método de depuración sistemática**

1. **Aislamiento del problema**
   - Pruebe con una configuración mínima del formulario
   - Elimine de forma temporal las funciones complejas
   - Pruebe los componentes individuales por separado
   - Use el proceso de eliminación para identificar la causa raíz

2. **Recopilación de información de diagnóstico**
   - Busque errores de JavaScript en la consola del explorador
   - Revise las solicitudes y respuestas de red
   - Documente los pasos exactos para reproducir el problema
   - Recopile capturas de pantalla y mensajes de error

3. **Variables de entorno de prueba**
   - Pruebe diferentes exploradores y dispositivos
   - Haga pruebas con diferentes cuentas de usuario y permisos
   - Verifíquelo en diferentes entornos de red
   - Compárelo con formularios o configuraciones en funcionamiento

### Análisis y monitorización de registros

**Depuración de la consola del explorador**

1. Abra las herramientas para desarrolladores de exploradores (F12)
2. Compruebe los errores de JavaScript en la pestaña Consola.
3. Revise la pestaña Red para ver las solicitudes fallidas
4. Monitorice la pestaña Rendimiento para detectar operaciones lentas

**Patrones de error comunes**

- **Errores de CORS**: problemas de solicitudes de origen cruzado con integraciones de API
- **Errores de autenticación**: credenciales no válidas o tókenes caducados
- **Errores de validación**: conflictos de reglas de validación de campos o errores de sintaxis
- **Tiempos de espera de red**: conexiones de red lentas o poco fiables

## Obtención de ayuda adicional

### Recursos de autoservicio

**Sistema de ayuda integrado**

- Utilice el comando `/help` seguido de preguntas específicas
- Acceda a la ayuda contextual dentro de la interfaz de Forms Experience Builder
- Revise con cuidado los mensajes de error para obtener instrucciones específicas
- Consulte la [Guía de introducción de Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Recursos de documentación**

- [Biblioteca de indicaciones de Forms Experience Builder](ai-assistant-prompt-library.md)
- [Prácticas recomendadas para Forms Experience Builder](aem-forms-ai-assistant-best-practices.md)
- [Documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es)

### Escalación y asistencia 

**Cuándo contactar con asistencia**

- Los problemas persisten después de probar las soluciones documentadas
- Problemas de todo el sistema que afectan a varios usuarios
- Problemas de seguridad o integridad de los datos
- Problemas de integración que requieren configuración en el nivel del sistema

**Información que debe proporcionar**

- Descripción detallada del problema y pasos para reproducirlo
- Capturas o grabaciones de pantalla del problema
- Información del sistema y del explorador
- Mensajes de error y registros de la consola
- Detalles de configuración e integración de formularios

**Métodos de contacto**

- Administrador del sistema: para problemas de entorno y acceso
- Soporte técnico: para problemas complejos de integración y configuración
- Programa de acceso anticipado: `aem-forms-ea@adobe.com` para problemas específicos del programa

### Comunidad e intercambio de conocimientos

**Prácticas recomendadas para resolver problemas**

- Documente las soluciones para referencia futura
- Comparta enfoques de resolución de problemas correctos con los integrantes del equipo
- Contribuya a la base de conocimiento de la organización
- Participe en comunidades y foros de usuarios

**Mejora continua**

- Revisión periódica de problemas y soluciones comunes
- Actualización de los procedimientos de resolución de problemas a partir de nuevos hallazgos
- Sesiones de formación e intercambio de conocimientos
- Comentarios sobre las mejoras de funciones para el equipo de producto

Esta guía de resolución de problemas se actualiza de forma continua de acuerdo con los comentarios de los usuarios y las nuevas capacidades de Forms Experience Builder. Para obtener la información más reciente y recursos adicionales, consulte la [documentación de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es).
