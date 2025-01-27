---
title: Plantillas de correo electrónico de HTML en Forms adaptable en Forms as a Cloud Service
description: Aprenda a utilizar las plantillas de correo electrónico con formularios adaptables.
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: b9364394f683fa8af5d28723e5f10b20b001ea37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 4%

---

# Plantillas de correo electrónico en Forms adaptable

El Forms adaptable permite utilizar plantillas de correo electrónico de texto sin formato y de HTML. Las plantillas de correo electrónico de HTML le permiten enviar correos electrónicos enriquecidos, personalizados y visualmente atractivos cuando se envía un formulario. Estos correos electrónicos se pueden personalizar con los datos del formulario y mejorar mediante varias etiquetas de correo electrónico, como imágenes y vínculos. Con Forms adaptable, puede cargar un archivo que contenga una plantilla de HTML o utilizar un editor de texto sin formato para crear estas plantillas.

![plantillas de correo electrónico de HTML](/help/forms/assets/html-email.png)

Este artículo le ayuda a configurar y utilizar plantillas de correo electrónico en Forms adaptable. Al final, usted será capaz de:

* [Configuración de una plantilla de HTML para un formulario adaptable](#configure-an-html-template-for-an-adaptive-form)
* [Configurar una plantilla de correo electrónico de texto sin formato para un formulario adaptable](#configure-a-plain-text-template-for-an-adaptive-form)
* [Uso de datos de formularios en las plantillas de correo electrónico](#use-form-data-in-your-email-templates)


A continuación se muestra una breve descripción general de los pasos involucrados:

1. Abra el formulario adaptable para editarlo.
1. Configurar la acción de envío [Enviar correo electrónico](/help/forms/configure-submit-action-send-email.md).
1. Seleccione o cargue una plantilla de HTML, o introdúzcala manualmente.
1. Pruebe la configuración de correo electrónico.

## Configuración de una plantilla de HTML para un formulario adaptable

Puede configurar un formulario adaptable para enviar un correo electrónico tras el envío mediante la acción de envío [**Enviar correo electrónico**](/help/forms/configure-submit-action-send-email.md). La acción proporciona dos métodos para configurar una plantilla de HTML:

### Opción 1: Seleccionar un archivo que contenga la plantilla de HTML

Antes de continuar, asegúrese de haber cargado la plantilla de HTML en el entorno de AEM Forms.

1. Abra el formulario adaptable para editarlo.
1. Vaya al **Explorador de contenido**, seleccione el **Contenedor de la guía** y pulse el icono de propiedades. Aparece un cuadro de diálogo con el título `Adaptive Form Container`.
1. Vaya a la pestaña **Envío** y seleccione la acción de envío **Enviar correo electrónico**.
1. Habilite la opción **Usar plantilla externa**.
1. Habilite la opción **Usar plantilla de HTML**.
1. Haga clic en el icono de la carpeta para la opción Ruta de la plantilla externa y busque y seleccione la plantilla del HTML.
1. Haga clic en Listo para guardar la configuración.

La plantilla del HTML ahora está configurada para el formulario adaptable.

### Opción 2: introducir o pegar manualmente una plantilla de HTML

1. Abra el formulario adaptable para editarlo.
1. Vaya al **Explorador de contenido**, seleccione el **Contenedor de la guía** y pulse el icono de propiedades. Aparece un cuadro de diálogo con el título `Adaptive Form Container`.
1. Vaya a la pestaña **Envío** y seleccione la acción de envío **Enviar correo electrónico**.
1. Habilite la opción **Usar plantilla externa**.
1. Habilite la opción **Usar plantilla de HTML**.
1. Escriba o pegue su código de HTML directamente en el cuadro **Plantilla de correo electrónico** proporcionado.


## Configurar una plantilla de texto sin formato para un formulario adaptable

Puede configurar un formulario adaptable para enviar un correo electrónico tras el envío mediante la acción de envío [**Enviar correo electrónico**](/help/forms/configure-submit-action-send-email.md). La acción proporciona dos métodos para configurar una plantilla de texto sin formato:

### Opción 1: Seleccionar un archivo que contenga la plantilla

Antes de continuar, asegúrese de haber cargado la plantilla de HTML en el entorno de AEM Forms.

1. Abra el formulario adaptable para editarlo.
1. Vaya al **Explorador de contenido**, seleccione el **Contenedor de la guía** y pulse el icono de propiedades. Aparece un cuadro de diálogo con el título `Adaptive Form Container`.
1. Vaya a la pestaña **Envío** y seleccione la acción de envío **Enviar correo electrónico**.
1. Habilite la opción **Usar plantilla externa**.
1. Haga clic en el icono de la carpeta para la opción **Ruta de la plantilla externa** y busque para seleccionar la plantilla de texto sin formato.
1. Haga clic en Listo para guardar la configuración.

La plantilla ahora está configurada para el formulario adaptable.

### Opción 2: introducir o pegar manualmente una plantilla de HTML

1. Abra el formulario adaptable para editarlo.
1. Vaya al **Explorador de contenido**, seleccione el **Contenedor de la guía** y pulse el icono de propiedades. Aparece un cuadro de diálogo con el título `Adaptive Form Container`.
1. Vaya a la pestaña **Envío** y seleccione la acción de envío **Enviar correo electrónico**.
1. Escriba o pegue su código de plantilla de texto sin formato directamente en el cuadro **Plantilla de correo electrónico** proporcionado.

## Uso de datos de formulario en las plantillas de correo electrónico

Puede incluir datos de formulario en las plantillas de correo electrónico mediante marcadores de posición. Estos marcadores de posición se sustituyen dinámicamente por valores de campo de formulario reales cuando se envía el correo electrónico. Por ejemplo:

* ${name}: El valor del campo denominado &quot;name&quot;.
* ${email}: El valor del campo denominado &quot;correo electrónico&quot;.
* ${message}: El valor del campo denominado &quot;message&quot;.

### Plantilla de correo electrónico del HTML de muestra

Este es un ejemplo de una plantilla de correo electrónico de HTML que utiliza marcadores de posición de datos de formulario:

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### Plantilla de correo electrónico de texto sin formato de muestra

Este es un ejemplo de plantilla de correo electrónico de texto sin formato:

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

Reemplace los marcadores de posición (${name}, ${email}, etc.) con los nombres de los campos de formulario correspondientes en el formulario adaptable.

## Prácticas recomendadas para plantillas de correo electrónico de HTML

* Asegúrese de que los estilos estén en línea para mejorar la compatibilidad con los clientes de correo electrónico.
* Haga que la plantilla sea adaptable para disfrutar de una mejor experiencia en dispositivos móviles.
* Utilice herramientas como Litmus o Correo electrónico con ácido para previsualizar el correo electrónico en varios clientes de correo electrónico.
* Asegúrese de que los nombres de marcador de posición coincidan exactamente con los nombres de campo de formulario.
* Compruebe si faltan etiquetas o si son incorrectas en la plantilla del HTML.
* Compruebe que la acción de envío [Enviar correo electrónico](/help/forms/configure-submit-action-send-email.md) esté configurada correctamente.
