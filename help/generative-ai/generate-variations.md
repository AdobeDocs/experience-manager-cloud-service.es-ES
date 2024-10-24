---
title: Generar variaciones
description: Obtenga información sobre la generación de variaciones, accesible desde AEM as a Cloud Service y el Sidekick de Edge Delivery Services
exl-id: 9114037f-37b9-4b2f-a714-10933f69b2c3
feature: Generate Variations
role: Admin, Architect, Developer
source-git-commit: bbc51796c610af02b5260c063213cde2ef610ba2
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---


# Generar variaciones {#generate-variations}

Si está buscando una manera de optimizar sus canales digitales y acelerar la creación de contenido, puede utilizar Generar variaciones. Generate Variations utiliza inteligencia artificial (IA) generativa para crear variaciones de contenido basadas en mensajes; estos mensajes los proporciona Adobe o los crean y administran los usuarios. Después de crear variaciones, puede usar el contenido de su sitio web y también medir su éxito usando la funcionalidad [Experimentación](https://www.aem.live/docs/experimentation) de [Edge Delivery Services](/help/edge/overview.md).

Puede [acceder a Generar variaciones](#access-generate-variations) desde:

* [dentro de Adobe Experience Manager AEM () as a Cloud Service](#access-aemaacs)
* [el Sidekick AEM de Edge Delivery Services de la](#access-aem-sidekick)
* [en el Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)

>[!NOTE]
>
>En todos los casos, para usar Generar variaciones debe asegurarse de que se cumplan los [requisitos previos de acceso](#access-prerequisites).

Podrá hacer lo siguiente:

* [Introducción](#get-started) mediante una plantilla de solicitud que el Adobe ha creado para un caso de uso específico.
* Puede [editar un mensaje existente](#edit-the-prompt)
* O [cree y use sus propios indicadores](#create-prompt):
   * [Guarde sus indicadores](#save-prompt) para uso futuro
   * [Acceda y utilice avisos compartidos](#select-prompt) de toda su organización
* Defina los segmentos de [audience](#audiences) que se usarán en la solicitud al [generar contenido personalizado específico de la audiencia](#generate-copy).
* Previsualice el resultado junto al mensaje, antes de realizar modificaciones y refinar los resultados si es necesario.
* Use el Adobe Express [para generar imágenes](#generate-image) según las variaciones de copia; esto usa las capacidades de IA generativa de Firefly.
* Seleccione el contenido que desea utilizar en el sitio web o en un experimento.

## Nota legal y de uso {#legal-usage-note}

AEM La IA generativa y la generación de variaciones para la son herramientas poderosas, pero **usted** es responsable del uso de la salida.

Las entradas del servicio deben estar vinculadas a un contexto. Este contexto puede ser el material de promoción de la marca, el contenido del sitio web, los datos, los esquemas para dichos datos, las plantillas u otros documentos de confianza.

Debe evaluar la precisión de cualquier resultado según corresponda para su caso de uso.

Antes de usar Generar variaciones, debe aceptar las [Directrices del usuario de inteligencia artificial aplicada generativa de Adobe](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

[El uso de Generar variaciones](#generative-action-usage) está ligado al consumo de acciones generativas.

## Información general {#overview}

Cuando abra Generar variaciones (y expanda el panel izquierdo), verá lo siguiente:

![Generar variaciones - panel principal](assets/generate-variations-main-panel.png)

* Panel derecho
   * Esto depende de la selección que realice en el panel de navegación izquierdo.
   * De manera predeterminada, se muestran **plantillas de solicitud**.
* Navegación izquierda
   * A la izquierda de **Generar variaciones**, existe la opción (menú de sándwich) de expandir u ocultar el panel de navegación izquierdo.
   * **Plantillas de mensajes**:
      * Muestra vínculos a los distintos indicadores, que pueden incluir:
         * Proporcionado por el Adobe para ayudarle a generar contenido; marcado con el Adobe.
         * Creado por usted mismo.
         * Creado dentro de su organización IMS; marcado con un icono que muestra varios encabezados.
      * Incluye el vínculo [Nueva solicitud](#create-prompt) para crear su propia solicitud.
      * Puede **eliminar** mensajes creados por usted mismo o dentro de su organización IMS. Esto se realiza mediante el menú al que se accede con los puntos suspensivos de la tarjeta correspondiente.
   * [Favoritos](#favorites): muestra los resultados de generaciones anteriores que ha marcado como Favoritos.
   * [Recientes](#recents): proporciona vínculos a mensajes y sus entradas que ha utilizado recientemente.
   * **Ayuda y preguntas frecuentes**: vínculos a documentación, incluidas preguntas frecuentes.
   * **Directrices de usuario**: vínculos a las directrices legales.

## Introducción {#get-started}

La interfaz le guía a través del proceso de generación de contenido. Después de abrir la interfaz, el primer paso es seleccionar la solicitud que desee utilizar.

### Seleccionar indicador {#select-prompt}

En el panel principal, puede seleccionar:

* una plantilla de indicador proporcionada por el Adobe para empezar a generar contenido,
* [Nueva solicitud](#create-prompt) para crear su propia solicitud,
* una plantilla que haya creado únicamente para su uso,
* una plantilla que usted o alguien de su organización hayan creado.

Para diferenciar:

* Las indicaciones proporcionadas por el Adobe se marcan con el Adobe
* Los indicadores disponibles en toda la organización IMS se marcan con un icono de varios encabezados.
* Los indicadores privados no se marcan específicamente.

![Generar variaciones - solicitar plantillas](assets/generate-variations-prompt-templates.png)

### Proporcionar entradas {#provide-inputs}

Cada mensaje le pedirá que proporcione cierta información para que pueda obtener el contenido adecuado de la IA generativa.

Los campos de entrada le guían a través de qué información es necesaria. Para ayudarle, ciertos campos tienen valores predeterminados que puede utilizar o modificar según sea necesario, así como descripciones que explican los requisitos.

Existen varios campos de entrada clave que son comunes a varios indicadores (algunos campos no siempre están disponibles):

* **Recuento de**/**Número de**
   * Puede seleccionar cuántas variaciones de contenido desea crear en una generación.
   * Según el mensaje, puede tener una de varias etiquetas; por ejemplo, Recuento, Número de variaciones, Número de ideas, etc.
* **Audiencia Source**/**Audiencia de destino**
   * Ayuda a generar contenido personalizado para una audiencia específica.
   * El Adobe proporciona audiencias predeterminadas o puede especificar audiencias adicionales; consulte [Audiencias](#audiences).
* **Contexto adicional**
   * Inserte contenido relevante para ayudar a la inteligencia artificial aplicada a la generación a crear una mejor respuesta basada en la entrada. Por ejemplo, si está creando un banner web para una página o producto en particular, es posible que desee incluir información sobre la página o el producto.
* **Temperatura**
Utilice para modificar la temperatura del Adobe IA generativa:
   * Una temperatura más alta se aleja del indicador y conduce a más variación, aleatoriedad y creatividad.
   * Una temperatura más baja es más determinista y permanece más cerca de lo que está en el indicador.
   * De forma predeterminada, la temperatura se establece en 1. Puede experimentar con diferentes temperaturas si los resultados generados no son de su agrado.
* **Editar mensaje**
   * La [petición de datos subyacente se puede editar](#edit-the-prompt) para restringir los resultados generados.

### Generar copia {#generate-copy}

Después de rellenar los campos de entrada o modificar el mensaje, está listo para generar contenido y revisar las respuestas.

Seleccione **Generar** para ver las respuestas generadas por IA generativa. Las variaciones de contenido generadas se muestran en el mensaje que las generó.

![Generar variaciones - generar copia](assets/generate-variations-generate-content.png)

>[!NOTE]
>
>La mayoría de las plantillas de solicitud de Adobe incluyen **Motivo de IA** en la respuesta de variación. Esto proporciona transparencia sobre por qué la IA generativa generó esa variación en particular.

Cuando selecciona una sola variación, están disponibles las siguientes acciones:

* **Favorito**
   * Marcar como **favorito** para uso futuro (se mostrará en [Favoritos](#favorites)).
* Pulgares arriba/Pulgares abajo
   * Utilice los indicadores de pulgares hacia arriba / hacia abajo para notificar al Adobe de la calidad de las respuestas.
* **Copiar**
   * Copie en el portapapeles para utilizarlo durante la creación de contenido en su sitio web o en un [Experimento](https://www.aem.live/docs/experimentation).
* **Quitar**

Si necesita perfeccionar las entradas o la solicitud, puede realizar ajustes y seleccionar **Generar** de nuevo para obtener un conjunto de respuestas nuevas. Las nuevas peticiones de datos y respuestas se muestran debajo de la petición de datos y respuesta iniciales; puede desplazarse hacia arriba y hacia abajo para ver los distintos conjuntos de contenido.

Encima de cada conjunto de variaciones se encuentra el indicador que las creó, junto con una opción **Reutilizar**. Si alguna vez necesita volver a ejecutar una solicitud con sus entradas, seleccione **Volver a utilizar** para volver a cargarlas en **Entradas**.

### Generar imagen {#generate-image}

Después de generar variaciones de texto, puede generar imágenes en Adobe Express mediante las capacidades de IA generativa de Firefly.

>[!NOTE]
>
>**Generar imagen** solo está disponible si tiene un derecho de Adobe Express como parte de su organización IMS y acceso concedido a usted en el Admin Console.

Seleccione una variación, seguida de **Generar imagen**, para abrir directamente **Texto a imagen** en [Adobe Express](https://www.adobe.com/express/). El mensaje se rellena previamente en función de la selección de variante y las imágenes se generan automáticamente según ese mensaje.

![Generar variaciones - expresar imágenes](assets/generate-variations-express-images.png)

Puede realizar más cambios:

* [escriba su propio mensaje en el Adobe Express](https://helpx.adobe.com/firefly/using/tips-and-tricks.html) describiendo lo que desea ver,
* ajustar las opciones **Texto a imagen**,
* luego **Actualice** las imágenes generadas.

También puedes usar **Explorar más** para obtener más información.

Cuando termine, seleccione la imagen que desee y **Guardar** para cerrar el Adobe Express. La imagen se devuelve y se guarda con la variación.

![Generar variaciones - imagen rápida guardada](assets/generate-variations-express-image-saved.png)

Aquí puede pasar el ratón sobre la imagen para mostrar los elementos de acción de:

* **Copiar**: [copiar la imagen en el portapapeles para usarla en otro lugar](#use-content)
* **Editar**: abre el Adobe Express para poder realizar cambios en la imagen
* **Descargar**: descargue la imagen en el equipo local
* **Eliminar**: elimine la imagen de la variación

>[!NOTE]
>
>[Los Contentes credentials](https://helpx.adobe.com/creative-cloud/help/content-credentials.html) no persisten cuando se utilizan en la creación basada en documentos.

### Usar contenido {#use-content}

Para utilizar el contenido generado con IA generativa, debe copiar el contenido en el portapapeles para utilizarlo en otra parte.

Esto se realiza mediante los iconos de copia:

* Para texto: utilice el icono de copia visible en el panel de variaciones
* Para la imagen: pase el ratón sobre la imagen para ver el icono de copia

Una vez copiada en el portapapeles, puede pegar la información para utilizarla al crear contenido para el sitio web. También puede ejecutar un [experimento](https://www.aem.live/docs/experimentation).

## Favoritos {#favorites}

Después de revisar el contenido, puede guardar las variaciones seleccionadas como favoritas.

Una vez guardados, se muestran en **Favoritos** en el panel de navegación izquierdo. Los favoritos se mantienen (hasta que los **elimine** o borre la caché del explorador).

* Los favoritos y las variaciones se pueden copiar y pegar en el portapapeles para su uso en el contenido del sitio web.
* Los favoritos pueden ser **Eliminados**.

## Recientes {#recents}

Esta sección incluye vínculos a su actividad reciente. Se agrega una entrada **Reciente** después de seleccionar **Generar**. Tiene el nombre del mensaje y una marca de tiempo. Si selecciona un vínculo, se carga el mensaje, se rellenan los campos de entrada según corresponda y se muestran las variaciones generadas.

## Editar el indicador {#edit-the-prompt}

El mensaje subyacente se puede editar. Puede que desee hacer lo siguiente:

* Si los resultados generados que obtiene necesitan un mayor refinamiento
* Desea modificar y [guardar el mensaje](#save-prompt) para uso futuro

Seleccione **Editar solicitud**:

![Generar variaciones - mensaje de edición](assets/generate-variations-prompt-edit.png)

Esto abre el editor de mensajes, donde puede realizar los cambios:

![Generar variaciones - editor de mensajes](assets/generate-variations-prompt-editor.png)

### Agregar entradas de indicador {#add-prompt-inputs}

Al crear o editar una solicitud, es posible que desee añadir campos de entrada. Los campos de entrada actúan como variables en el mensaje y proporcionan la flexibilidad de usar el mismo mensaje en distintos escenarios. Permiten a los usuarios definir elementos específicos del mensaje, sin tener que escribir todo el mensaje.

* Un campo se define con llaves dobles `{{ }}` que encierran un nombre de marcador de posición.
Por ejemplo, `{{tone_of_voice}}`.

  >[!NOTE]
  >
  >No se permiten espacios entre llaves dobles.

* También se define en `METADATA`, con los siguientes parámetros:
   * `label`
   * `description`
   * `default`
   * `type`

#### Ejemplo: Agregar nuevo campo de texto: tono de voz {#example-add-new-text-field-tone-of-voice}

Para agregar un nuevo campo de texto titulado **Tono de voz**, use la sintaxis siguiente en el mensaje:

```prompt
{{@tone_of_voice, 
  label="Tone of voice",
  description="Indicate the desired tone of voice",
  default="optimistic, smart, engaging, human, and creative",
  type=text
}}
```

![Generar variaciones - mensaje editado con tono de voz](assets/generate-variations-prompt-edited.png)

<!--
#### Example: Add new dropdown field - Page Type {#example-add-new-dropdown-field-page-type}

To create an input field Page Type providing a dropdown selection:

1. Create a spreadsheet named `pagetype.xls` in the top-level directory of your folder structure.
1. Edit the spreadsheet:

   1. Create two columns: **Key** and **Value**.
   1. In the **Key** column, enter labels that will appear in the dropdown.
   1. In the **Value** column, describe the key value so the generative AI has context.

1. In your prompt, refer to the title of the spreadsheet along with the appropriate type. 

   ```prompt
   {{@page_type, 
     label="Page Type",
     description="Describes the type of page",
     spreadsheet=pagetype
   }}
   ```
-->

## Crear una solicitud {#create-prompt}

Cuando selecciona **Nueva solicitud** de **Plantillas de solicitud**, un panel nuevo le permitirá introducir una nueva solicitud. A continuación, puede especificarlas, junto con la **Temperatura**, para **Generar** contenido.

Consulte [Guardar solicitud](#save-prompt) para obtener más información sobre cómo guardar la solicitud en el futuro.

Consulte [Agregar entradas de solicitud](#add-prompt-inputs) para obtener más información sobre cómo agregar sus propias entradas de solicitud.

Si desea conservar el formato tanto en la interfaz de usuario como cuando se copia y pega en el flujo de creación basado en documentos, incluya lo siguiente en el mensaje:

<!-- CHECK - are the double-quotes needed? -->

* `"Format the response as an array of valid, iterable RFC8259 compliant JSON"`

La siguiente imagen muestra las ventajas de hacerlo:

* en el primer ejemplo se combinan `Title` y `Description`
* mientras que en el segundo ejemplo se les aplica formato por separado: esto se ha hecho incluyendo la solicitud JSON en el indicador.

![Generar variaciones - preguntar con Título y Descripción formateados por separado](assets/generate-variations-prompt-formatted.png)

## Guardar indicación {#save-prompt}

Después de editar o crear mensajes, es posible que desee guardarlos para usarlos en el futuro; solo para su organización IMS o para usted. La solicitud guardada aparecerá como una tarjeta de **Plantilla de solicitud**.

Cuando haya editado la solicitud, la opción **Guardar** estará disponible en la parte inferior de la sección Entradas, a la izquierda de **Generar**.

Cuando se selecciona, se abre el cuadro de diálogo **Guardar solicitud**:

![Generar variaciones - cuadro de diálogo para solicitud de guardado](assets/generate-variations-prompt-save-dialog.png)

1. Agregue un **Nombre del mensaje** único; utilizado para identificar el mensaje en **Plantillas del mensaje**.
   1. Un nombre nuevo y único crea una nueva plantilla de solicitud.
   1. Un nombre existente sobrescribe esa solicitud; se muestra un mensaje.
1. Si lo desea, añada una descripción.
1. Active o desactive la opción **Compartida en toda la organización**, en función de si el mensaje debe ser privado para usted o estar disponible en toda la organización IMS. Este estado se muestra en la tarjeta [resultante mostrada en las plantillas de mensajes](#select-prompt).
1. **Guardar** el mensaje; o **Cancelar** la acción.

>[!NOTE]
>
>Se le informará (advertirá) si está sobrescribiendo o actualizando un mensaje existente.

>[!NOTE]
>
>Desde **Plantillas de mensajes** puede eliminar mensajes (mediante el menú al que se accede con los puntos suspensivos) creados por usted mismo o dentro de su organización IMS.

## Audiencias {#audiences}

Para generar contenido personalizado, la inteligencia artificial aplicada a la generación debe comprender la audiencia. El Adobe proporciona varias audiencias predeterminadas o puede agregar las suyas propias.

Al añadir una audiencia, debe describirla en lenguaje natural. Por ejemplo:

* para crear una audiencia:
   * `Student`
* podría decir:
   * `The audience consists of students, typically individuals who are pursuing education at various academic levels, such as primary, secondary, or tertiary education. They are engaged in learning and acquiring knowledge in diverse subjects, seeking academic growth, and preparing for future careers or personal development.`

Se admiten dos fuentes de audiencia:

* [Adobe Target](#audience-adobe-target)
* [Archivo CSV](#audience-csv-file)

![Generar variaciones - orígenes de audiencia](assets/generate-variations-audiences.png)

### Audience - Adobe Target {#audience-adobe-target}

Si se selecciona una audiencia **Adobe Target** en el mensaje, se permite personalizar la generación de contenido para esa audiencia.

>[!NOTE]
>
>Para utilizar esta opción, su organización IMS debe tener acceso a Adobe Target.

1. Seleccione **Adobe Target**.
1. A continuación, seleccione la **Audiencia de destino** necesaria en la lista proporcionada.

   >[!NOTE]
   >
   >Para usar una audiencia **Adobe Target**, debe rellenarse el campo de descripción. Si no es así, la audiencia se muestra en la lista desplegable como no disponible. Para agregar una descripción, vaya a Target y [agregue una descripción de audiencia](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences).

   ![Generar variaciones - origen de audiencia - Adobe Target](assets/generate-variations-audiences-adobe-target.png)

#### Añadir audiencia de Adobe Target {#add-adobe-target-audience}

Consulte [Crear audiencias](https://experienceleague.adobe.com/en/docs/target-learn/tutorials/audiences/create-audiences) para crear una audiencia en Adobe Target.

### Audience: archivo CSV {#audience-csv-file}

Si se selecciona una audiencia de **archivo CSV** en el mensaje, se puede personalizar la generación de contenido para la **audiencia de destino** seleccionada.

El Adobe proporciona una serie de audiencias para utilizar.

1. Seleccione **archivo CSV**.
1. A continuación, seleccione la **Audiencia de destino** necesaria en la lista proporcionada.

   ![Generar variaciones - origen de la audiencia - archivo CSV](assets/generate-variations-audiences-csv-file.png)

#### Añadir archivo CSV de Audience {#add-audience-csv-file}

Puede agregar un archivo CSV desde varias plataformas (por ejemplo, Google Drive, Dropbox o Sharepoint) que tengan la capacidad de proporcionar una URL al archivo una vez que esté disponible públicamente.

>[!NOTE]
>
>En las plataformas compartidas, *debe* tener la capacidad de hacer que el archivo sea de acceso público.

Por ejemplo, para agregar una audiencia de un archivo en Google Drive:

1. En Google Drive, cree un archivo de hoja de cálculo con dos columnas:
   1. La primera columna se muestra en la lista desplegable.
   1. La segunda columna es la descripción de la audiencia.
1. Publish el archivo:
   1. Archivo -> Compartir -> publicar en la web -> CSV
1. Copie la URL en el archivo publicado.
1. Vaya a Generar variaciones.
1. Abra el Editor de mensajes.
1. Busque la audiencia **Adobe Target** en los metadatos y reemplace la URL.

   >[!NOTE]
   >
   >Asegúrese de que las comillas dobles (&quot;) se mantienen en ambos extremos de la dirección URL.

   Por ejemplo:

   ![Generar variaciones - agregar archivo CSV de audiencia](assets/generate-variations-audiences-csv-save.png)

## Uso de acciones generativas {#generative-action-usage}

La administración del uso depende de la acción realizada:

* Generar variaciones

  Una generación de una variante de copia es igual a una acción generativa. AEM Como cliente, tiene una serie de acciones generativas que se incluyen con su licencia de. Una vez consumida la asignación de derechos base, puede adquirir acciones adicionales.

  >[!NOTE]
  >
  >Ver [Adobe Experience Manager: Cloud Service | Descripción del producto](https://helpx.adobe.com/legal/product-descriptions/aem-cloud-service.html) para obtener más información acerca de los derechos básicos y póngase en contacto con el equipo de la cuenta si desea adquirir acciones más generativas.

* Adobe Express

  El uso de generación de imágenes se administra mediante derechos de Adobe Express y [créditos generativos](https://helpx.adobe.com/firefly/using/generative-credits-faq.html).

## Acceso a Generar variaciones {#access-generate-variations}

Después de cumplir los requisitos previos, puede acceder a Generate Variations desde AEM as a Cloud Service o desde el Sidekick de los Edge Delivery Services.

### Requisitos previos de acceso {#access-prerequisites}

Para utilizar Generar variaciones, debe asegurarse de que se cumplen los requisitos previos:

* [Acceso al as a Cloud Service en Experience Manager con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services)

#### Acceso al as a Cloud Service en Experience Manager con Edge Delivery Services{#access-to-aemaacs-with-edge-delivery-services}

Los usuarios que necesiten acceder a Generate Variations deben tener derecho a un entorno as a Cloud Service Experience Manager con Edge Delivery Services.

>[!NOTE]
>
>Si el contrato del as a Cloud Service de AEM Sites no incluye Edge Delivery Services, deberá firmar un nuevo contrato para obtener acceso.
>
>Póngase en contacto con el equipo de su cuenta para hablar sobre cómo puede pasar al as a Cloud Service de AEM Sites con los Edge Delivery Services.

Para conceder acceso a usuarios específicos, asigne su cuenta de usuario al perfil de producto correspondiente. AEM Consulte [Asignación de perfiles de producto de para obtener más información](/help/journey-onboarding/assign-profiles-cloud-manager.md).

### Acceso desde AEM as a Cloud Service {#access-aemaacs}

Se puede acceder a Generar variaciones desde el [Panel de navegación](/help/sites-cloud/authoring/basic-handling.md#navigation-panel) de AEM as a Cloud Service:

![Panel de navegación](/help/sites-cloud/authoring/assets/basic-handling-navigation.png)

### Acceso desde el AEM Sidekick {#access-aem-sidekick}

Se necesita alguna configuración para poder acceder a Generate Variations desde el Sidekick (de Edge Delivery Services).

1. Consulte el documento [Instalación del AEM Sidekick](https://www.aem.live/docs/sidekick-extension) para obtener información sobre cómo instalar y configurar el Sidekick.

1. Para utilizar la opción Generate Variations en el Sidekick (de Edge Delivery Services), incluya la siguiente configuración en sus proyectos de Edge Delivery Services en:

   * `tools/sidekick/config.json`

   Esto debe combinarse con la configuración existente y luego implementarse.

   Por ejemplo:

   ```prompt
   {
     // ...
     "plugins": [
       // ...
       {
         "id": "generate-variations",
         "title": "Generate Variations",
         "url": "https://experience.adobe.com/aem/generate-variations",
         "passConfig": true,
         "environments": ["preview","live", "edit"],
         "includePaths": ["**.docx**"]
       }
       // ...
     ]
   }
   ```

1. Es posible que deba asegurarse de que los usuarios tengan [acceso al as a Cloud Service del Experience Manager con Edge Delivery Services](#access-to-aemaacs-with-edge-delivery-services).

1. A continuación, puede acceder a la función seleccionando **Generar variaciones** en la barra de herramientas del Sidekick:

   AEM ![Generar variaciones - acceso desde la página de inicio de sesión de Sidekicj](assets/generate-variations-sidekick-toolbar.png)

## Información adicional {#further-information}

Para obtener más información, también puede leer:

* [GenAI genera variaciones en GitHub](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Experimentación con Edge Delivery Services](https://www.aem.live/docs/experimentation)

## Preguntas frecuentes {#faqs}

### Salida con formato {#formatted-outpu}

**La respuesta generada no me está dando el resultado con formato que necesito. ¿Cómo se modifica el formato? p. ej.: necesito un título y un subtítulo, pero la respuesta es solo el título**

1. Abra la solicitud real en modo de edición.
1. Vaya a Requisitos.
1. Encontrará requisitos que hablan sobre el resultado.
   1. Ejemplo: &quot;El texto debe constar de tres partes, un título, un cuerpo y una etiqueta de botón&quot;. o &quot;Dé formato a la respuesta como una matriz de objetos JSON válida con los atributos &quot;Title&quot;, &quot;Body&quot; y &quot;ButtonLabel&quot;.
1. Modifique los requisitos para adaptarlos a sus necesidades.

   >[!NOTE]
   >
   >Si tiene restricciones de recuento de palabras/caracteres en la nueva salida introducida, cree un requisito.

   Ejemplo: &quot;El texto del título no debe superar las 10 palabras o los 50 caracteres, incluidos los espacios&quot;.
1. Guarde la solicitud para uso futuro.

### Duración de la respuesta {#length-of-response}

**La respuesta generada es demasiado larga o demasiado corta. ¿Cómo se cambia la longitud?**

1. Abra la solicitud real en modo de edición.
1. Vaya a Requisitos.
1. Verá que para cada salida hay un límite correspondiente de palabra/carácter.
   1. Ejemplo: &quot;El texto del título no debe superar las 10 palabras o los 50 caracteres, incluidos los espacios&quot;.
1. Modifique los requisitos para adaptarlos a sus necesidades.
1. Guarde la solicitud para uso futuro.

### Mejore las respuestas {#improve-responses}

**Las respuestas que recibo no son exactamente lo que estoy buscando. ¿Qué puedo hacer para mejorarlos?**

1. Intente cambiar la temperatura en Configuración avanzada.
   1. Una temperatura más alta se aleja del indicador y conduce a más variación, aleatoriedad y creatividad.
   1. Una temperatura más baja es más determinista y se adhiere a lo que está en el indicador.
1. Abra la solicitud real en el modo de edición y revísela. Preste especial atención a la sección de requisitos que describe el tono de voz y otros criterios importantes.

### Comentarios en una solicitud {#comments-in-prompt}

**¿Cómo puedo usar comentarios en una solicitud?**

Los comentarios de una solicitud se utilizan para incluir notas, explicaciones o instrucciones que no están pensadas para formar parte del resultado real. Estos comentarios se encapsulan dentro de una sintaxis específica: comienzan y finalizan con llaves dobles y comienzan con un hash (por ejemplo, `{{# Comment Here }}`). Los comentarios ayudan a aclarar la estructura o la intención del mensaje de texto sin afectar a la respuesta generada.

### Buscar una solicitud compartida {#find-a-shared-prompt}

**¿Qué puedo hacer si no encuentro una plantilla de mensaje que alguien haya compartido?**

En esta situación hay varios detalles que comprobar:

1. Utilice la dirección URL de su entorno.
Por ejemplo, https://experience.adobe.com/#/aem/generate-variations
1. Asegúrese de que la organización de IMS seleccionada sea correcta.
1. Confirme que la solicitud se ha guardado como Compartida.

### Mensajes personalizados en la versión 2.0.0 {#custom-prompts-v200}

**En la versión 2.0.0, mis mensajes personalizados han desaparecido. ¿Qué puedo hacer?**

Si se cambia a la versión 2.0.0, las plantillas de mensajes personalizadas se romperán, por lo que no estarán disponibles.

Para recuperarlos:

1. Vaya a la carpeta prompt-template de Sharepoint.
1. Copie el mensaje.
1. Abra la aplicación Generar variaciones.
1. Seleccione la tarjeta Nuevo mensaje.
1. Pegue el mensaje.
1. Compruebe que el mensaje funciona.
1. Guarde el mensaje.

## Historial de versiones {#release-history}

Para obtener más información sobre las versiones actuales y anteriores, consulte las [Notas de la versión para generar variaciones](/help/generative-ai/release-notes-generate-variations.md)
