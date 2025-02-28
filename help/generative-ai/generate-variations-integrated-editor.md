---
title: Generar variaciones
description: Obtenga información sobre la generación de variaciones, accesible desde varios editores dentro de AEM as a Cloud Service
feature: Generate Variations
role: Admin, Architect, Developer, User
source-git-commit: 257fcd8df8bf216deec1fe96e64dd38e52f3ebe1
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 34%

---


# Generar variaciones: integrado en editores de AEM {#generate-variations-integrated-in-aem-editors}

Si busca una forma de optimizar sus canales digitales y acelerar la creación de contenido, puede utilizar la opción Generar variaciones integrada en los editores de AEM.

Generate Variations utiliza inteligencia artificial (IA) generativa para crear variaciones de contenido basadas en los datos introducidos. Después de crear variaciones, puede usar el contenido de su sitio web y también medir su éxito usando la funcionalidad [Experimentación](https://www.aem.live/docs/experimentation) de [Edge Delivery Services](/help/edge/overview.md).

Esto acelera la velocidad del contenido al crear rápidamente contenido de la marca en minutos. Esto, a su vez, ayuda a mejorar la conversión con nuevas variantes de copia.

Puede [acceder a Generar variaciones](#access-generate-variations) desde los siguientes editores ([una vez configurados](#access-generate-variations)):

* [en Sidekick de AEM Edge Delivery Services; para la creación basada en documentos](#access-aem-sidekick)
* [en el editor universal](#access-aem-universal-editor)
* [el editor de fragmentos de contenido](#access-aem-content-fragment-editor)

>[!IMPORTANT]
>
>Esta página utiliza la creación basada en documentos como base para los ejemplos, pero los principios se aplican a los demás editores.

>[!NOTE]
>
>En todos los casos, para usar “Generar variaciones” debe asegurarse de que se cumplan los [requisitos previos de acceso](#access-prerequisites).

>[!NOTE]
>
>Se puede acceder directamente a la versión independiente de [Generar variaciones](/help/generative-ai/generate-variations.md).

Podrá hacer lo siguiente:

* [Seleccione el contenido con el que desea trabajar](#select-the-content), entre los bloques existentes de su contenido
   * El bloque seleccionado dirige lo que se muestra y las acciones disponibles
* [Describa los cambios que desee](#describe-the-changes-you-want)
* [Genere variaciones de su contenido](#generate-copy), luego [tome acciones adicionales si lo desea](#take-further-action-on-a-variation)
* [Seleccionar y utilizar una variación](#use-a-generated-variation)
* Revisa tu [historial](#history)
* Ver tus [favoritos](#favorites)

## Aviso legal y de uso {#legal-usage-note}

<!--
Generative AI and Generate Variations for AEM are powerful tools – but **you** are responsible for use of the output.

Your inputs to the service should be tied to a context. This context can be your branding materials, website content, data, schemas for such data, templates, or other trusted documents.

You must evaluate the accuracy of any output as appropriate to your use case.

Before using Generate Variations you are recommended to read the [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).
-->

[El uso de “Generar variaciones”](#generative-action-usage) está ligado al consumo de acciones generativas.

## Información general {#overview}

Cuando abra Generar variaciones integradas en un editor, verá la extensión como un panel flotante que tiene tres pestañas.

![Generar variaciones: información general sobre la creación basada en documentos](assets/generate-variations-doc-based-overview.png)

* El editor:
   * Esto muestra el flujo de contenido en el editor.
   * Aquí puede seleccionar un bloque de contenido para utilizarlo en **Generar variaciones**.
* **Generar variaciones**:
   * Es un panel flotante con tres pestañas, que se puede reubicar como desee
   * [Generar](#get-started-with-generate-variations):
      * Muestra el [contenido que ha seleccionado](#select-the-content).
      * Proporciona **Sugerencias** de ejemplo para realizar cambios.
      * Le permite [describir los cambios que desea](#describe-the-changes-you-want).
      * Le permite [Generar](#generate-copy) nuevas variaciones.
      * Muestra las variaciones generadas. <!--, together with their [brand score](#the-brand-score).-->
      * [Realice más acciones en una variación](#take-further-action-on-a-variation).
      * [Usar una variación generada](#use-a-generated-variation).
   * [Historial](#history):
      * Muestra su historia reciente de generaciones.
   * [Favoritos](#favorites):
      * Muestra los resultados de generaciones anteriores que ha marcado como Favoritos.
   * **Términos de IA generativa de Adobe**: Vínculos a [Directrices del usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Introducción a la generación de variaciones {#get-started-with-generate-variations}

La interfaz le guía a través del proceso de generación de contenido. Después de abrir la interfaz, el primer paso es seleccionar el bloque de contenido que desea utilizar.

### Selección del contenido {#select-the-content}

En el flujo de contenido principal del editor, seleccione el contenido para el que desea generar variaciones. Esta **selección** se mostrará en la ficha **Generar**.

### Describa los cambios que desee {#describe-the-changes-you-want}

Para generar variaciones del contenido, debe describir los cambios que desee. Puede seleccionar una de las **sugerencias** proporcionadas o proporcionar su propia descripción.

También puede especificar **Modificadores** para proporcionar más contexto:

* **Hacer referencia a una página web**
Proporcione una URL para obtener más contexto.
* **Cargar información de contenido**
Actualice un archivo `.docx` que contenga detalles de la información breve de contenido (10 MB o menos).

### Generar copia {#generate-copy}

Después de describir los cambios que desea, seleccione **Generar** para ver las respuestas de IA generativa.

![Generar variaciones - generar copia basada en documento](assets/generate-variations-doc-based-generate-copy.png)

<!--
### The Brand Score {#the-brand-score}

The brand score shows you how on-brand the generated variation is.
-->

### Realizar más acciones en una variación {#take-further-action-on-a-variation}

Al seleccionar una sola variación, puede utilizar las siguientes acciones:

* **Editar**
   * Puede editar el texto de la variación generada.

      * Las actualizaciones se pueden previsualizar en la página web.

   * Guarde los cambios para usarlos más adelante.
* **Favorito**
   * Marque esta variación para referencia futura.
   * Una vez marcado, se mostrará en la ficha [Favoritos](#favorites).
* **Motivo de IA**
   * Para lograr una mayor transparencia, esto proporciona una breve descripción de por qué la IA generativa generó esa variación en particular.

### Usar una variación generada {#use-a-generated-variation}

Para usar el contenido generado con IA generativa, primero debe seleccionar y **Exportar a CSV**.

Después de la exportación, puede utilizar el contenido en cualquier otra parte; por ejemplo, al crear contenido para el sitio web. También puede ejecutar un [experimento](https://www.aem.live/docs/experimentation).

>[!NOTE]
>
>Cuando se accede a Generar variaciones desde [el Editor universal de AEM](#access-aem-universal-editor) o [el Editor de fragmentos de contenido de AEM](#access-aem-content-fragment-editor), el contenido generado seleccionado se guarda automáticamente en AEM.

## Historia {#history}

Esta pestaña muestra su actividad anterior como después de seleccionar **Generar**. se ha agregado una entrada **History**.

Si, en un momento posterior, selecciona el mismo contenido en el flujo principal y abre la pestaña **History**, verá todas las variaciones generadas para ese bloque.

## Favoritos {#favorites}

Después de revisar el contenido, puede guardar las variaciones seleccionadas como favoritas.

Una vez guardados, se muestran en **Favoritos**. Los favoritos se mantienen (hasta que los **elimine de sus favoritos** o borre la caché del explorador).

* Puede **Editar**, **No marcar como favorito** o mostrar la **justificación de IA** para una entrada.
* Una vez seleccionada una variación, también puede **Exportar a CSV**.

## Uso de acciones generativas {#generative-action-usage}

La administración del uso depende de la acción realizada:

* Generar variaciones

  Una generación de una variante de copia es igual a una acción generativa. Como cliente, dispone de un determinado número de acciones generativas que vienen con su licencia de AEM. Una vez que haya consumido los derechos básicos, podrá adquirir acciones adicionales.

  >[!NOTE]
  >
  >Consulte [Adobe Experience Manager: Cloud Service | Descripción del producto](https://helpx.adobe.com/legal/product-descriptions/aem-cloud-service.html) para obtener más información acerca de los derechos básicos, y póngase en contacto con el equipo de la cuenta si desea adquirir acciones más generativas.

## Acceso a “Generar variaciones” {#access-generate-variations}

Después de cumplir los requisitos previos, puede acceder a “Generar variaciones” desde AEM as a Cloud Service o desde la barra de tareas de Edge Delivery Services.

### Requisitos previos de acceso {#access-prerequisites}

Para utilizar “Generar variaciones”, debe asegurarse de que se cumplen los requisitos previos:

* [Acceso a Experience Manager as a Cloud Service con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services)

#### Acceso a Experience Manager as a Cloud Service con Edge Delivery Services{#access-to-aemaacs-with-edge-delivery-services}

Los usuarios que necesiten acceder a “Generar variaciones” deben tener derecho a un entorno de Experience Manager as a Cloud Service con Edge Delivery Services.

>[!NOTE]
>
>Si su contrato de AEM Sites as a Cloud Service no incluye Edge Delivery Services, deberá firmar un nuevo contrato para obtener acceso.
>
>Debe ponerse en contacto con su equipo de cuentas para hablar sobre cómo puede pasarse a AEM Sites as a Cloud Service con Edge Delivery Services.

Para conceder acceso a usuarios específicos, asigne su cuenta de usuario al perfil de producto correspondiente. Consulte [Asignación de perfiles de productos de AEM para obtener más detalles](/help/journey-onboarding/assign-profiles-cloud-manager.md).

### Acceso desde AEM Sidekick para la creación basada en documentos {#access-aem-sidekick}

El acceso desde AEM Sidekick se usa para la [creación basada en documentos](/help/edge/wysiwyg-authoring/authoring.md).

Es necesario realizar alguna configuración antes de poder acceder a “Generar variaciones” desde la barra de tareas (de Edge Delivery Services).

>[!NOTE]
>
>Consulte el documento [Instalación de la barra de tareas de AEM](https://www.aem.live/docs/sidekick-extension) para obtener información sobre cómo instalar y configurar la barra de tareas.

Para utilizar la opción Generar variaciones en Sidekick (de Edge Delivery Services), incluya las siguientes configuraciones en sus proyectos de Edge Delivery Services.

1. Habilite la aplicación en:

   * `tools/sidekick/config.json`

   Esto debe combinarse con la configuración existente y luego implementarse.

   Por ejemplo:

   ```prompt
   {
     "plugins": [
       {
         "id": "aem-genai-variations",
         "titleI18n": {
           "en": "Generate with AI"
         },
         "environments": [
           "preview"
         ],
         "includePaths": [
           "**.docx**"
         ],
         "event": "aem-genai-variations-sidekick"
       }
     ]
   }
   ```

1. Crear:

   * `/tools/sidekick/aem-genai-variations.js`

   Debe crear este archivo con el siguiente contenido:

   ```prompt
   (function () {
     let isAEMGenAIVariationsAppLoaded = false;
     function loadAEMGenAIVariationsApp() {
       const script = document.createElement('script');
       script.src = 'https://experience.adobe.com/solutions/aem-sites-genai-aem-genai-variations-mfe/static-assets/resources/sidekick/client.js?source=plugin';
       script.onload = function () {
         isAEMGenAIVariationsAppLoaded = true;
       };
       script.onerror = function () {
         console.error('Error loading AEMGenAIVariationsApp.');
       };
       document.head.appendChild(script);
     }
   
     function handlePluginButtonClick() {
       if (!isAEMGenAIVariationsAppLoaded) {
         loadAEMGenAIVariationsApp();
       }
     }
   
     // The code snippet for the Sidekick V1 extension, https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo?hl=en
     const sidekick = document.querySelector('helix-sidekick');
     if (sidekick) {
       // sidekick already loaded
       sidekick.addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
     } else {
       // wait for sidekick to be loaded
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('helix-sidekick')
           .addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
       }, { once: true });
     }
   
     // The code snippet for the Sidekick V2 extension, https://chromewebstore.google.com/detail/aem-sidekick/igkmdomcgoebiipaifhmpfjhbjccggml?hl=en
     const sidekickV2 = document.querySelector('aem-sidekick');
     if (sidekickV2) {
       // sidekick already loaded
       sidekickV2.addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
     } else {
       // wait for sidekick to be loaded
       document.addEventListener('sidekick-ready', () => {
         document.querySelector('aem-sidekick')
           .addEventListener('custom:aem-genai-variations-sidekick', handlePluginButtonClick);
       }, { once: true });
     }
   }());
   ```

1. Actualización:

   * `/scripts/scripts.js`

   Se debe actualizar para incluir la instrucción siguiente en la función `loadLazy()`:

   ```prompt
     import('../tools/sidekick/aem-genai-variations.js');
   ```

   Esto garantiza que `/tools/sidekick/aem-genai-variations.js` se cargue como parte del proceso de carga diferida.

   ![Generar variaciones - cargador diferido](assets/generate-variations-sidekick-lazyloader.png)

1. A continuación, es posible que tenga que asegurarse de que los usuarios disponen de [Acceso a Experience Manager as a Cloud Service con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services).

1. A continuación, puede acceder a la funcionalidad seleccionando **Generar con IA** en la barra de herramientas de Sidekick:

   ![Generar variaciones: acceso desde la barra de tareas de AEM](assets/generate-variations-doc-based-sidekick.png)

### Acceso desde el Editor universal de AEM {#access-aem-universal-editor}

El acceso desde [AEM Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md) está implementado como una extensión. Consulte [Extension Manager en AEM Experience Manager](https://developer.adobe.com/uix/docs/extension-manager/) para obtener más información.

### Acceso desde el Editor de fragmentos de contenido de AEM {#access-aem-content-fragment-editor}

El acceso desde [AEM Content Fragment Editor](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai) está implementado como una extensión. Consulte [Extension Manager en AEM Experience Manager](https://developer.adobe.com/uix/docs/extension-manager/) para obtener más información.

## Información adicional {#further-information}

Para obtener más información, también puede leer:

* [Generar variaciones de IA generativa en GitHub](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Experimentación de Edge Delivery Services](https://www.aem.live/docs/experimentation)

## Historial de versiones {#release-history}

Para más detalles sobre la versión actual, y las anteriores, consulte las [Notas de la versión de “Generar variaciones”](/help/generative-ai/release-notes-generate-variations.md).
