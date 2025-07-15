---
title: Prácticas recomendadas para diseñar Forms de alto rendimiento
description: Conozca las prácticas recomendadas esenciales para crear formularios fáciles de usar, accesibles y de alto rendimiento con AEM Forms. Mejore la calidad de los datos, la experiencia del usuario y las tasas de éxito de envío.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 67b6873b-bb93-4d38-963c-2ca65a1a644b
source-git-commit: 37b20a97942f381b46ce36a6a3f72ac019bba5b7
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# Prácticas recomendadas para crear Forms

## Información general

La creación de formularios eficaces va más allá de la implementación técnica: requiere comprender la psicología del usuario, los estándares de accesibilidad y la optimización del rendimiento. Esta guía completa proporciona prácticas recomendadas comprobadas para diseñar formularios que los usuarios realmente deseen completar.

### Lo que aprenderá

Al final de este documento, comprenderá lo siguiente:

* Diseñe formularios accesibles y fáciles de usar que funcionen para todos
* Optimizar el rendimiento y los tiempos de carga de los formularios
* Administrar los datos de usuario de forma responsable y transparente
* Implementar el control y la validación de errores adecuados
* Crear formularios que logren altas tasas de finalización

### Audiencia objetivo

Esta guía está diseñada para:

* **Diseñadores de formularios** que deseen crear mejores experiencias de usuario
* **Desarrolladores** que implementan la funcionalidad de formulario
* **profesionales de UX** que optimizan flujos de trabajo de formularios
* **Partes interesadas empresariales** que buscan mejorar las tasas de conversión de formularios

### Principios clave

Las mejores formas siguen estos principios básicos:

1. **Diseño centrado en el usuario**: Céntrese en lo que los usuarios necesitan lograr
2. **Primero accesibilidad** - Asegúrese de que todos puedan usar sus formularios
3. **Optimización del rendimiento**: los formularios rápidos se completan con mayor frecuencia
4. **Responsabilidad de los datos** - Respetar la privacidad del usuario y minimizar la recopilación de datos
5. **Borrar comunicación**: guíe a los usuarios a través del proceso sin problemas

La creación de grandes formas va más allá de la tecnología. A continuación se indica cómo garantizar que sus formularios sean fáciles de usar y logren sus objetivos:

## Diseño de Forms fácil de usar y accesible

* **Usar etiquetas claras y visibles:** Cada campo de formulario necesita un `<label>`. No confíe únicamente en el texto de marcador de posición (texto dentro del campo de entrada), ya que desaparece cuando los usuarios escriben y es incorrecto para la accesibilidad.
   * *Bueno:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *Incorrecto:* `<input type="email" placeholder="Email Address">`
* **Manténgalo simple:** Use tipos de entrada estándar de HTML (`<input type="date">`, `<input type="tel">`) siempre que sea posible. A menudo, tienen mejor compatibilidad y accesibilidad móvil que los widgets personalizados complejos.
* **Orden lógico y agrupación:** organice los campos de forma que tenga sentido para el usuario. Agrupar campos relacionados mediante `<fieldset>` y `<legend>`.
* **Proporcione instrucciones claras:** Para cualquier campo que pueda ser confuso, proporcione texto de ayuda conciso o información sobre herramientas.
* **Navegación por teclado:** Asegúrese de que los usuarios puedan navegar por todo el formulario usando solo el teclado (Tab, Mayús+Tab, Enter, Barra espaciadora).
* **Control de errores:** Haga que los errores sean obvios y fáciles de corregir. Muestre los mensajes de error junto al campo correspondiente y explique lo que debe corregirse.

* **Garantizar que Forms se cargue rápidamente y sea visible**

   * **Colocar Forms de forma destacada:** Si un formulario es importante, asegúrese de que los usuarios puedan verlo fácilmente sin tener que desplazarse demasiado (&quot;sobre el pliegue&quot; si es posible). La investigación de Adobe muestra que muchos formularios no interactúan bien porque están ocultos.
   * **Optimizar Assets:** Mantenga cualquier JavaScript o CSS personalizado para sus formularios lo más pequeño posible para garantizar tiempos de carga rápidos. Edge Delivery Services ayuda con la carga de la página base, pero los scripts de formulario pesados pueden ralentizar las cosas.

* **Administrar Datos De Usuario De Forma Responsable**
   * **Pregunte solo lo que necesita:** Cuanto menos información de identificación personal (PII) pida, mejor. Cada campo es un motivo potencial para que un usuario abandone el formulario.
   * **Sea transparente:** Explique claramente *por qué* necesita cierta información y *cómo se utilizará*. Vínculo a la política de privacidad. Esto genera confianza.

* **Mejorando la experiencia del usuario: alternativas Captcha**

   * **Repensar los captchas visibles:** Las pruebas de &quot;escribir el texto ondulado&quot; o de &quot;hacer clic en todos los semáforos&quot; pueden ser muy frustrantes para los usuarios, especialmente los que tienen discapacidades, y a menudo conducen a altas tasas de entrega.

* **Considerar alternativas:**
   * **Campos de honeypot:** Agregue un campo oculto que solo los bots rellenarían. Si tiene datos, es probable que el envío sea correo no deseado.
   * **Comprobaciones basadas en el tiempo:** Mida la rapidez con la que se envía un formulario. Los envíos que son demasiado rápidos suelen ser bots.
   * **reCAPTCHA invisible (v3):** Este servicio de Google analiza el comportamiento del usuario en segundo plano y sólo presenta un desafío si el usuario parece sospechoso. Esta suele ser una experiencia de usuario mucho mejor.

## Qué hacer y qué no hacer en el diseño de formularios

| ✅ Hacer: Para Una Mejor Forms | ❌ no lo hace: evite estos |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| Usar etiquetas `<label>` visibles en todos los campos | Utilice únicamente texto de marcador de posición en lugar de etiquetas adecuadas |
| Preferir tipos de entrada de HTML estándar (por ejemplo, `<input type="email">`) | Uso de widgets personalizados demasiado complejos |
| Garantizar la navegación completa mediante el teclado | Proporcionar mensajes de error imprecisos o que falten |
| Mostrar mensajes de error claros y procesables | Solicitar datos personales excesivos sin justificación |
| Pedir sólo la información necesaria | Utilizar CAPTCHA visibles de difícil solución |
| Explicar cómo se utilizan los datos (información de privacidad o vínculos) | Ocultar el formulario en las profundidades de la página |
| Utilizar técnicas CAPTCHA invisibles o de comportamiento |                                                                  |
| Facilitar la búsqueda del formulario en la página (ubicación destacada) |                                                                  |


## Siguientes pasos

Esta guía proporciona información general sobre el uso de formularios con AEM Edge Delivery Services. Para obtener instrucciones paso a paso más detalladas sobre configuraciones específicas, consulte la documentación oficial de Adobe Experience Manager:

* [Creación basada en documentos con Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universal con Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Creación de documentos (DA) e incrustación de contenido](https://www.aem.live/developer/da-tutorial)
* [Servicio de envío de AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
