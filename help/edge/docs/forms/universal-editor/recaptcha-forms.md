---
title: 'Proteja su Forms con reCAPTCHA: una guía visual'
description: Aprenda a añadir fácilmente Google reCAPTCHA a los formularios de Edge Delivery Services para evitar envíos de correo no deseado y bots
feature: Edge Delivery Services
keywords: reCAPTCHA en formularios, Usar reCAPTCHA en el editor universal, Agregar reCAPTCHA en formularios, seguridad de formularios, protección contra correo no deseado
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 2%

---


# Proteja su Forms del spam con Google reCAPTCHA

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con su nombre de organización de GitHub y el nombre del repositorio.</span>



## ¿Por qué utilizar reCAPTCHA en los formularios?

| ![Seguridad](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protección para bots](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Experiencia del usuario](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Seguridad mejorada** | **Prevención de bots y spam** | **Experiencia de usuario perfecta** |
| Proteja sus formularios de actividades fraudulentas y ataques malintencionados | Evite que los bots automatizados inunden sus formularios con contenido irrelevante o perjudicial | El reCAPTCHA invisible funciona entre bastidores sin interrumpir a los usuarios legítimos |

Por ejemplo, un formulario de cálculo de impuestos con información financiera confidencial necesita protección contra el uso indebido. reCAPTCHA comprueba que los envíos proceden de usuarios reales, no de sistemas automatizados.

## Elija su solución reCAPTCHA

Edge Delivery Services Forms admite dos opciones de Google reCAPTCHA:

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA Standard](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA Standard**](#set-up-recaptcha-standard) |
| Detección de fraude de nivel empresarial Premium con funciones y personalización adicionales | Servicio gratuito con detección basada en puntuación que funciona de forma invisible en segundo plano |
| Ideal para: organizaciones grandes con necesidades de seguridad complejas | Ideal para: proyectos pequeños y medianos con necesidades básicas de protección |

Ambas opciones utilizan la detección basada en puntuación (de 0,0 a 1,0) para identificar interacciones humanas frente a bots sin interrumpir la experiencia del usuario.

## Configuración de reCAPTCHA Enterprise

### Paso 1: Consiga Sus Credenciales De Google Cloud

Antes de configurar reCAPTCHA Enterprise, necesitará lo siguiente:

- Un [proyecto de Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) con tu [identificador de proyecto](https://support.google.com/googleapi/answer/7014113)
- [Se habilitó la API de reCAPTCHA Enterprise](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) para su proyecto
- Una [clave de API](https://console.cloud.google.com/apis/credentials) para la autenticación
- Una [clave de sitio](https://console.cloud.google.com/security/recaptcha) para su dominio

### Paso 2: Crear un contenedor de configuración de nube

![Configuración de nube paso a paso](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Inicie sesión en la instancia de autor de AEM
2. Vaya a **Herramientas** > **General** > **Explorador de configuración**
3. Busque su formulario y seleccione **Propiedades**
4. Habilitar **configuraciones de nube** en el cuadro de diálogo
5. Guarde y publique su configuración

### Paso 3: Configurar el servicio reCAPTCHA Enterprise

![pantalla de configuración de reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Vaya a **Herramientas** > **Cloud Services** > **reCAPTCHA**
2. Vaya al formulario y haga clic en **Crear**
3. En el cuadro de diálogo:
   - Seleccionar **ReCAPTCHA Enterprise** versión
   - Escriba un título y un nombre
   - Añadir el ID del proyecto, la clave del sitio y la clave de la API
   - Seleccione **clave de sitio basada en la puntuación** como tipo de clave
   - Defina una puntuación de umbral (0-1) para distinguir a los humanos de los bots
4. Haga clic en **Crear** y publique la configuración

## Configuración del estándar reCAPTCHA

### Paso 1: Obtención de las claves API

Antes de empezar, [obtenga un par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) (clave del sitio y clave secreta) de la consola de Google reCAPTCHA.

>[!IMPORTANT]
>
>Los formularios de Edge Delivery Services solo admiten la versión **basada en puntuaciones de reCAPTCHA**.

### Paso 2: Crear un contenedor de configuración de nube

Siga los mismos pasos que en la versión Enterprise para crear y publicar un contenedor de configuración en la nube.

### Paso 3: Configurar el servicio estándar reCAPTCHA

![Pantalla de configuración estándar reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Vaya a **Herramientas** > **Cloud Services** > **reCAPTCHA**
2. Vaya al formulario y haga clic en **Crear**
3. En el cuadro de diálogo:
   - Seleccionar **ReCAPTCHA v2** versión
   - Escriba un título y un nombre
   - Añadir la clave del sitio y la clave secreta
4. Haga clic en **Crear** y publique la configuración

## Añadir reCAPTCHA al formulario

Ahora que ha configurado reCAPTCHA, es hora de agregarlo al formulario:

![Agregando el componente reCAPTCHA a un formulario](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. Abra el formulario en el editor universal
2. Vaya a la sección Formulario adaptable en el árbol de contenido
3. Haga clic en el icono **Agregar** y seleccione **Captcha (invisible)** de la lista Componentes de formularios adaptables
   - *También puede arrastrar y soltar el componente en su formulario*
4. Haga clic en **Publicar** para actualizar el formulario con la protección reCAPTCHA

El formulario está ahora protegido. Ver en:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![Formulario con la protección reCAPTCHA habilitada](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Validación de la integración de reCAPTCHA

Después de agregar reCAPTCHA al formulario, es esencial comprobar que funciona correctamente. Para validar la implementación, haga lo siguiente:

### Verificación visual

Aunque reCAPTCHA v2 (basado en puntuación) funciona de forma invisible, puede confirmar su presencia haciendo lo siguiente:

1. **Inspeccionar el origen de la página**: haga clic con el botón derecho en la página del formulario y seleccione &quot;Ver página Source&quot;
   - Busque la inclusión de scripts reCAPTCHA con la clave del sitio
   - Ejemplo: `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **Comprobar solicitudes de red**: uso de herramientas para desarrolladores de explorador (F12)
   - Envíe su formulario y busque solicitudes de red a `google.com/recaptcha`
   - Estas solicitudes indican que reCAPTCHA está activo en el formulario

### Pruebas funcionales

Para comprobar que reCAPTCHA está protegiendo realmente el formulario:

1. **Prueba de envío normal**:
   - Rellene el formulario con datos válidos
   - Envíe el formulario a un ritmo humano normal
   - Comprobar que el formulario se envía correctamente

2. **Prueba de comportamiento similar a un bot**:
   - Abra el formulario en una ventana de exploración privada o de incógnito
   - Rellene el formulario extremadamente rápido (comportamiento automatizado)
   - Enviar varias veces en sucesión rápida
   - Si reCAPTCHA funciona, estos envíos pueden bloquearse o marcarse

3. **Comprobar registros de envío de formularios**:
   - Revise los datos de envío del formulario
   - Cada envío debe incluir una puntuación reCAPTCHA
   - Puntuaciones cercanas a 1,0 indican probables usuarios humanos
   - Puntuaciones cercanas a 0,0 indican una posible actividad de bots

### Uso de Admin Console de Google reCAPTCHA

Para los usuarios empresariales, la consola de Google Cloud proporciona análisis detallados:

1. Vaya a [Google Cloud Console](https://console.cloud.google.com/)
2. Vaya a **Seguridad** > **reCAPTCHA**
3. Seleccione la clave del sitio
4. Revisar los gráficos y las estadísticas de evaluación
5. Busque:.
   - Patrones de tráfico
   - Distribuciones de puntuación
   - Actividades potencialmente fraudulentas

Para los usuarios de reCAPTCHA estándar, hay estadísticas básicas disponibles en [reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/).

### Ajuste de la implementación

En función de los resultados de validación:

- Si se bloquean usuarios legítimos, considere la posibilidad de reducir la puntuación del umbral
- Si todavía recibe correo no deseado, considere aumentar su puntuación de umbral
- Para problemas persistentes, revise la configuración de reCAPTCHA y asegúrese de que todas las claves se ingresan correctamente

Recuerde que reCAPTCHA utiliza el aprendizaje automático para mejorar con el tiempo, de modo que su eficacia puede aumentar a medida que aprende los patrones de tráfico del sitio.

## Resolución de problemas y preguntas frecuentes

| ![Pregunta](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![Respuesta](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **¿Qué sucede si no creo una configuración reCAPTCHA?** | El sistema buscará una configuración en el contenedor global. Si no existe ninguna, se producirá un error. |
| **¿Qué sucede si creo varias configuraciones?** | El sistema utiliza automáticamente la primera configuración creada. |
| **¿Por qué no son visibles mis cambios en la dirección URL publicada?** | Asegúrese de volver a publicar el formulario después de realizar los cambios. |
| **¿Qué servicios reCAPTCHA son compatibles?** | Edge Delivery Services Forms solo admite servicios reCAPTCHA basados en puntuación. |

## Pasos siguientes

Ahora que ha protegido su formulario con reCAPTCHA:

- **Valide la implementación**: siga los [pasos de validación](#-validating-your-recaptcha-integration) para asegurarse de que reCAPTCHA funciona correctamente
- **Supervisar el rendimiento**: Compruebe periódicamente si hay actividades sospechosas y distribuciones de puntuación en el panel reCAPTCHA de Google
- **Ajustar la configuración**: Ajuste la puntuación de umbral en función de sus necesidades de seguridad y los comentarios de la experiencia del usuario
- **Manténgase actualizado**: Mantenga su implementación de reCAPTCHA al día con las recomendaciones de seguridad más recientes de Google
- **Educar a su equipo**: Comparta conocimientos sobre cómo funciona reCAPTCHA y cómo interpretar los análisis
- **Recopilar comentarios**: supervise la experiencia del usuario para asegurarse de que no se bloquee a los usuarios legítimos

Recuerde que la protección eficaz de los formularios es un proceso continuo que requiere supervisión y ajustes periódicos.


