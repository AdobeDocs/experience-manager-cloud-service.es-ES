---
title: Prácticas recomendadas para diseñar formularios de alto rendimiento
description: Conozca las prácticas recomendadas esenciales para crear formularios fáciles de usar, accesibles y de alto rendimiento con AEM Forms. Mejore la calidad de los datos, la experiencia del usuario y las tasas de éxito de envío.
feature: Edge Delivery Services
role: Admin, Developer
hide: true
hidefromtoc: true
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 100%

---

# Prácticas recomendadas para la creación de formularios

## Información general

Crear formularios eficaces va más allá de la implementación técnica: requiere comprender la psicología del usuario, los estándares de accesibilidad y la optimización del rendimiento. Esta guía exhaustiva proporciona prácticas recomendadas comprobadas para diseñar formularios que los usuarios realmente deseen completar.

### Lo que aprenderá

Al final de este documento, aprenderá a:

- Diseñar formularios accesibles y fáciles de usar que funcionen para todos
- Optimizar el rendimiento y los tiempos de carga de los formularios
- Gestionar los datos de usuario de forma responsable y transparente
- Implementar una gestión y validación adecuada de los errores
- Crear formularios que logren altas tasas de finalización

### Público destinatario

Esta guía está diseñada para:

- **Diseñadores de formularios** que desean crear mejores experiencias del usuario
- **Desarrolladores** que implementan la funcionalidad de formulario
- **Profesionales de UX** que optimizan flujos de trabajo de formularios
- **Partes interesadas del ámbito empresarial** que buscan mejorar los índices de conversión de formularios

### Principios clave

Los mejores formularios siguen estos principios básicos:

1. **Diseño centrado en el usuario**: centrarse en lo que los usuarios necesitan lograr
2. **Accesibilidad ante todo**: asegurarse de que todos puedan usar sus formularios
3. **Optimización del rendimiento**: los formularios rápidos se completan con mayor frecuencia
4. **Responsabilidad de los datos**: respetar la privacidad del usuario y minimizar la recopilación de datos
5. **Comunicación clara**: guiar a los usuarios a través del proceso sin problemas

Crear formularios excelentes va más allá de la tecnología. A continuación, le indicamos cómo asegurarse de que sus formularios sean fáciles de usar y cumplan sus objetivos:

## Diseño de formularios accesibles y fáciles de usar

- **Use etiquetas claras y visibles:** cada campo de formulario necesita una `<label>`. No confíe únicamente en el texto de marcadores de posición (el texto que aparece dentro del campo de entrada), ya que desaparece cuando los usuarios escriben y es perjudicial para la accesibilidad.

   - *Correcto:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   - *Incorrecto:* `<input type="email" placeholder="Email Address">`

- **Mantenga la sencillez:** utilice tipos de entrada HTML estándar (`<input type="date">`, `<input type="tel">`) siempre que sea posible. A menudo, tienen mejor compatibilidad y accesibilidad móvil que los widgets personalizados complejos.
- **Orden lógico y agrupación:** organice los campos de forma que tenga sentido para el usuario. Agrupe campos relacionados mediante `<fieldset>` y `<legend>`.
- **Proporcione instrucciones claras:** para cualquier campo que pueda ser confuso, proporcione texto de ayuda conciso o información sobre herramientas.
- **Navegación por teclado:** asegúrese de que los usuarios puedan navegar por todo el formulario usando solo el teclado (Tab, Mayús+Tab, Intro o barra espaciadora).
- **Gestión de errores:** haga que los errores sean evidentes y fáciles de corregir. Muestre los mensajes de error junto al campo correspondiente y explique lo que debe corregirse.
- **Garantice que sus formularios se carguen rápidamente y sean visibles**
- **Coloque los formularios en un lugar destacado:** si un formulario es importante, asegúrese de que los usuarios puedan verlo fácilmente sin tener que desplazarse demasiado (a ser posible, “sobre el pliegue”). Las investigaciones de Adobe muestran que muchos formularios obtienen poca interacción porque están ocultos.
- **Optimice los recursos:** mantenga cualquier JavaScript o CSS personalizado para sus formularios lo más pequeño posible para garantizar tiempos de carga rápidos. Edge Delivery Services ayuda con la carga de la página base, pero los scripts de formulario pesados pueden ralentizar el proceso.
- **Tratamiento responsable de los datos de los usuarios**
- **Pregunte solo lo necesario:** cuanta menos información de identificación personal (PII) solicite, mejor. Cada campo es un motivo potencial para que un usuario abandone el formulario.
- **Sea transparente:** explique claramente *por qué* necesita cierta información y *cómo se utilizará*. Proporcione un vínculo a la política de privacidad. Esto genera confianza.
- **Mejora de la experiencia del usuario: alternativas al Captcha**
- **Reconsidere los captchas visibles:** las pruebas de tipo “escriba el texto ondulado” o de “haga clic en todos los semáforos” pueden ser muy frustrantes para los usuarios, especialmente los que tienen discapacidades, y a menudo provocan altas tasas de abandono.
- **Considere alternativas:**
   - **Campos trampa:** añada un campo oculto que solo los bots rellenarían. Si tiene datos, es probable que el envío sea correo no deseado.
   - **Comprobaciones basadas en el tiempo:** mida la rapidez con la que se envía un formulario. Los envíos que son demasiado rápidos suelen ser bots.
   - **reCAPTCHA invisible (v3):** este servicio de Google analiza el comportamiento del usuario en segundo plano y solo presenta un desafío si el usuario parece sospechoso. Esto suele suponer una experiencia de usuario mucho mejor.

## Qué hacer y qué no hacer en el diseño de formularios

| ✅ Qué hacer para diseñar mejores formularios | ❌ Qué no hacer: aspectos que debe evitar |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Usar etiquetas `<label>` visibles en todos los campos | Utilizar únicamente texto de marcadores de posición en lugar de etiquetas adecuadas |
| Optar por tipos de entrada de HTML estándar (por ejemplo, `<input type="email">`) | Usar widgets personalizados demasiado complejos |
| Garantizar la navegación completa mediante el teclado | Proporcionar mensajes de error imprecisos o no proporcionarlos |
| Mostrar mensajes de error claros y procesables | Solicitar datos personales excesivos sin justificación |
| Pedir solo la información necesaria | Utilizar CAPTCHA visibles de difícil solución |
| Explicar cómo se utilizan los datos (información de privacidad o vínculos) | Ocultar el formulario en la parte inferior de la página |
| Utilizar técnicas de CAPTCHA invisibles o de comportamiento |                                                                  |
| Hacer que el formulario sea fácil de encontrar en la página (ubicación destacada) |                                                                  |


## Próximos pasos

Esta guía proporciona información general sobre el uso de formularios con Edge Delivery Services de AEM. Para obtener instrucciones paso a paso más detalladas sobre configuraciones específicas, consulte la documentación oficial de Adobe Experience Manager:

- [Creación basada en documentos con formularios de Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
- [Editor universal con formularios de Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Creación de documentos (DA) e incrustación de contenido](https://www.aem.live/developer/da-tutorial)
- [Servicio de envío de formularios de AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
