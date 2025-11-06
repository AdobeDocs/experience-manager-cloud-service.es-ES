---
title: Información general del editor universal para desarrolladores de AEM
description: Si es un desarrollador de AEM interesado en cómo funciona el editor universal y cómo utilizarlo en su proyecto, este documento le ofrece una guía de introducción de extremo a extremo de la instrumentación del proyecto de WKND para trabajar con el editor universal.
exl-id: d6f9ed78-f63f-445a-b354-f10ea37b0e9b
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 100%

---


# Información general del editor universal para desarrolladores de AEM {#developer-overview}

Si es un desarrollador de AEM interesado en cómo funciona el editor universal y cómo utilizarlo en su proyecto, este documento le ofrece una guía de introducción de extremo a extremo de la instrumentación del proyecto de WKND para trabajar con el editor universal.

## Función {#purpose}

Este documento sirve como introducción para desarrolladores sobre cómo funciona el editor universal y cómo instrumentar la aplicación para trabajar con él.

Para ello, toma un ejemplo estándar con el que la mayoría de los desarrolladores de AEM están familiarizados; los componentes principales y el sitio WKND. Además, instrumenta algunos componentes de ejemplo para que se puedan editar con el editor universal.

>[!TIP]
>
>Este documento incluye pasos adicionales para ilustrar cómo funciona el editor universal y tiene la intención de profundizar la comprensión del editor por parte del desarrollador. Por lo tanto, no toma la ruta más directa para instrumentar una aplicación, sino la más ilustrativa del editor universal y su funcionamiento.
>
>Si desea ponerse en marcha lo antes posible, consulte el documento de [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md).

## Requisitos previos {#prerequisites}

Para seguir esta información general, debe tener disponible lo siguiente.

* [Una instancia de desarrollo local de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es)
   * Su instancia de desarrollo local debe estar [configurada con HTTPS para fines de desarrollo en `localhost`](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=es).
   * [Se debe instalar el sitio de demostración de WKND](https://github.com/adobe/aem-guides-wknd).
* [Acceso al editor universal](/help/implementing/universal-editor/getting-started.md#onboarding).
* [Un servicio de editor universal local](/help/implementing/universal-editor/local-dev.md) que se ejecuta con fines de desarrollo.
   * Asegúrese de dirigir el explorador para que [acepte el certificado autofirmado de los servicios locales](/help/implementing/universal-editor/local-dev.md#editing).

Más allá del conocimiento general del desarrollo web, este documento supone un conocimiento básico del desarrollo de AEM. Si no tiene experiencia con el desarrollo de AEM, considere la posibilidad de revisar [el tutorial de WKND antes de continuar](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

## Inicie AEM e inicie sesión en el editor universal {#sign-in}

Si aún no lo ha hecho, debe tener la instancia de desarrollo local de AEM en ejecución con WKND instalado y HTTPS habilitado como [se detalla en los requisitos previos](#prerequisites). Esta información general supone que la instancia se está ejecutando en `https://localhost:8443`.

1. Abra la página maestra de WKND en inglés en el editor de AEM.

   ```text
   https://localhost:8443/editor.html/content/wknd/language-masters/en.html
   ```

1. En el menú **Información de la página** del editor, seleccione **Ver como publicado**. Se abre la misma página en una nueva pestaña con el editor de AEM deshabilitado.

   ```text
   https://localhost:8443/content/wknd/language-masters/en.html?wcmmode=disabled
   ```

1. Copie este vínculo.

1. Ahora inicie sesión en el editor universal.

   ```text
   https://experience.adobe.com/#/aem/editor
   ```

1. Pegue el vínculo que copió antes del contenido de WKND en el campo **URL del sitio** del editor universal y haga clic en **Abrir**.

   ![Abra la página de WKND en el editor universal](assets/dev-ue-open.png)

## El editor universal intenta cargar el contenido {#sameorigin}

El editor universal carga el contenido que se va a editar en un marco. La configuración predeterminada de AEM para las opciones de X-Frame lo impide, lo que puede verse con claridad en el explorador como un error y detallarse en la salida de la consola al intentar cargar la copia local de WKND.

![Error del explorador debido a la opción SAMEORIGIN](assets/dev-sameorigin.png)

La opción de X-Frame `sameorigin` impide procesar páginas de AEM dentro de un marco. Debe quitar este encabezado para permitir que las páginas se carguen en el editor universal.

1. Abra el administrador de configuración. 

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Edite la configuración OSGi `org.apache.sling.engine.impl.SlingMainServlet`

   ![Propiedad OSGi para SAMEORIGIN](assets/dev-sameorigin-osgi.png)

1. Elimine la propiedad `X-Frame-Options=SAMEORIGIN` de la propiedad **Encabezados de respuesta adicionales**.

1. Guarde los cambios.

Ahora, si vuelve a cargar el editor universal, verá que se carga la página de AEM.

>[!TIP]
>
>* Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#sameorigin) para obtener más información sobre esta configuración OSGi.
>* Consulte el documento [Configuración de OSGi para Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información sobre OSGi en AEM.

## Gestión de cookies del mismo sitio {#samesite-cookies}

Cuando el editor universal carga la página, se carga en la página de inicio de sesión de AEM con el fin de garantizar que se ha autenticado para realizar cambios.

Sin embargo, no puede iniciar sesión de manera correcta. Al mostrar la consola del explorador, puede ver que el explorador ha bloqueado la entrada en el marco

![Entrada bloqueada](assets/dev-cross-origin.png)

La cookie del token de inicio de sesión se envía a AEM como un dominio de terceros. Por lo tanto, se deben permitir cookies del mismo sitio en AEM.

1. Abra el administrador de configuración. 

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Edite la configuración OSGi `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`

   ![Propiedad OSGi para cookies del mismo sitio](assets/dev-cross-origin-osgi.png)

1. Cambie la propiedad **Atributo SameSite para la cookie de token de inicio de sesión** a `None`.

1. Guarde los cambios.

Ahora, si vuelve a cargar el editor universal, puede iniciar sesión de forma correcta en AEM y se cargará la página de destino.

>[!TIP]
>
>* Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#samesite-cookies) para obtener más información sobre esta configuración OSGi.
>* Consulte el documento [Configuración de OSGi para Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información sobre OSGi en AEM.

## El editor universal se conecta al marco remoto {#ue-connect-remote-frame}

Con la página cargada en el editor universal y la sesión iniciada en AEM, el editor universal intenta conectarse al marco remoto. Esto se realiza mediante una biblioteca de JavaScript que debe cargarse en el marco remoto. Si la biblioteca de JavaScript no está presente, la página acaba generando un error de tiempo de espera en la consola.

![Error de tiempo de espera](assets/dev-timeout.png)

Debe añadir la biblioteca de JavaScript necesaria al componente de página de la aplicación WKND.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. En `/apps/wknd/components/page`, edite el archivo `customheaderlibs.html`.

   ![Edición del archivo customheaderlibs.html](assets/dev-customheaderlibs.png)

1. Añada la biblioteca de JavaScript al final del archivo.

   ```html
   <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
   ```

1. Haga clic en **Guardar todo** y vuelva a cargar el editor universal.

La página ahora se carga con la biblioteca de JavaScript adecuada para permitir que el editor universal se conecte a su página y el error de tiempo de espera ya no aparece en la consola.

>[!TIP]
>
>* La biblioteca se puede cargar en el encabezado o en el pie de página.

>[!NOTE]
>
>Ya no se aconseja el método recomendado antes para incluir la biblioteca de JavaScript, `<script src="https://universal-editor-service.experiencecloud.live/corslib/LATEST"></script>` o a través de npmjs.com, ya que el paquete ha quedado obsoleto.
>
>Si una aplicación sigue utilizando el paquete obsoleto, el editor universal muestra una advertencia en la IU de que se ha detectado un paquete obsoleto.

## Definición de una conexión para mantener los cambios {#connection}

La página de WKND ahora se carga de forma correcta en el editor universal y la biblioteca de JavaScript se carga para conectar el editor a la aplicación.

Sin embargo, es probable que haya observado que no puede interactuar con la página en el editor universal. En realidad, el editor universal no puede editar su página. Para que el editor universal pueda editar el contenido, debe definir una conexión para que sepa dónde escribirlo. Para el desarrollo local, debe escribir en la instancia de desarrollo local de AEM en `https://localhost:8443`.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. En `/apps/wknd/components/page`, edite el archivo `customheaderlibs.html`.

   ![Edición del archivo customheaderlibs.html](assets/dev-instrument-app.png)

1. Añada los metadatos necesarios para la conexión con la instancia local de AEM al final del archivo.

   ```html
   <meta name="urn:adobe:aue:system:aem" content="aem:https://localhost:8443">
   ```

   * Siempre se recomienda la versión más reciente de la biblioteca. Si necesita una versión anterior, consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#alternative).

1. Añada los metadatos necesarios para la conexión al servicio del editor universal local al final del archivo.

   ```html
   <meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
   ```

1. Haga clic en **Guardar todo** y vuelva a cargar el editor universal.

Ahora, el editor universal no solo puede cargar de forma correcta el contenido de la instancia de desarrollo local de AEM, sino que también sabe dónde conservar los cambios realizados con el servicio de editor universal local. Este es el primer paso para instrumentar la aplicación de modo que se pueda editar con el editor universal.

>[!TIP]
>
>* Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#connection) para obtener más información sobre los metadatos de conexión.
>* Consulte el documento [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md#service) para obtener más información sobre la estructura del editor universal.
>* Consulte el documento [Desarrollo local de AEM con el editor universal](/help/implementing/universal-editor/local-dev.md) para obtener más información sobre cómo conectarse a una versión autoalojada del editor universal.

## Instrumentación de componentes {#instrumenting-components}

Sin embargo, es probable que observe que todavía puede hacer poco con el editor universal. Si intenta hacer clic en el teaser de la parte superior de la página de WKND en el editor universal, no puede seleccionarlo (ni nada más en la página).

Los componentes también deben estar instrumentados para poder editarlos con el editor universal. Para ello, debe editar el componente de teaser. Por lo tanto, debe superponer los componentes principales, ya que estos se encuentran en `/libs`, lo cual es inmutable.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Seleccione el nodo `/libs/core/wcm/components` y haga clic en **Nodo de superposición** en la barra de herramientas.

1. Con `/apps/` seleccionado como **Ubicación de superposición**, haga clic en **Aceptar**.

   ![Superposición del teaser](assets/dev-overlay-teaser.png)

1. Seleccione el nodo `teaser` en `/libs/core/wcm/components` y haga clic en **Copiar** en la barra de herramientas.

1. Seleccione el nodo superpuesto en `/apps/core/wcm/components` y haga clic en **Pegar** en la barra de herramientas.

1. Haga doble clic en el archivo `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` para editarlo.

   ![Edición del archivo teaser.html](assets/dev-edit-teaser.png)

1. Al final del primer `div`, en la línea 26 aproximadamente, añada los detalles de instrumentación para el componente.

   ```text
   data-aue-resource="urn:aem:${resource.path}"
   data-aue-type="component"
   data-aue-label="Teaser"
   ```

1. Haga clic en **Guardar todo** en la barra de herramientas y vuelva a cargar el editor universal.

1. En el editor universal, haga clic en el componente de teaser en la parte superior de la página y verá que ahora puede seleccionarlo.

1. Si hace clic en el icono **Árbol de contenido** en el panel de propiedades del editor universal, verá que el editor reconoce todos los teasers de la página ahora que la ha instrumentado. El teaser que seleccionó es el resaltado.

   ![Selección del componente de teaser instrumentado](assets/dev-select-teaser.png)

>[!TIP]
>
>Consulte el documento [Uso de la fusión de recursos de Sling en Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md) para obtener más información sobre la superposición de nodos.

## Instrumentación de subcomponentes del teaser {#subcomponents}

Ahora puede seleccionar el teaser, pero aún no editarlo. Esto se debe a que el teaser está formado por diferentes componentes, como la imagen y el componente de título. Debe instrumentar estos subcomponentes para poder editarlos.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Seleccione el nodo `/apps/core/wcm/components/teaser/v2/teaser/` y haga doble clic en el archivo `title.html`.

   ![Edición del archivo title.html](assets/dev-edit-title.png)

1. Inserte las siguientes propiedades al final de la etiqueta `h2` (cerca de la línea 17).

   ```text
   data-aue-prop="jcr:title"
   data-aue-type="text"
   data-aue-label="Title"
   ```

1. Haga clic en **Guardar todo** en la barra de herramientas y vuelva a cargar el editor universal.

1. Haga clic en el título del mismo componente de teaser en la parte superior de la página y verá que ahora puede seleccionarlo. El árbol de contenido también muestra el título como parte del componente de teaser seleccionado.

   ![Selección del título dentro del teaser](assets/dev-select-title.png)

Ahora puede editar el título del componente de teaser.

## ¿Qué significa todo esto? {#what-does-it-mean}

Ahora que puede editar el título del teaser, vamos a dedicar un momento a revisar lo que ha logrado y cómo.

Ha identificado el componente de teaser en el editor universal mediante su instrumentación.

* `data-aue-resource` identifica el recurso de AEM que se está editando.
* `data-aue-type` define que los elementos deben tratarse como un componente de página (en lugar de, por ejemplo, un contenedor).
* `data-aue-label` muestra una etiqueta descriptiva en la IU para el teaser seleccionado.

También ha instrumentado el componente de título dentro del componente de teaser.

* `data-aue-prop` es el atributo JCR que se escribe.
* `data-aue-type` es la forma en que se debe editar el atributo. En este caso, con el editor de texto, ya que es un título (en lugar de, por ejemplo, el editor de texto enriquecido).

## Definición de encabezados de autenticación {#auth-header}

Ahora puede editar el título del teaser en línea y los cambios se mantienen en el explorador.

![Título editado del teaser](assets/dev-edited-title.png)

Sin embargo, si vuelve a cargar el explorador, se vuelve a cargar el título anterior. Esto se debe a que, aunque el editor universal sabe cómo conectarse a su instancia de AEM, aún no puede autenticarse en ella para escribir cambios en el JCR.

Si muestra la pestaña de red de las herramientas para desarrolladores del explorador y busca `update`, verá que se encuentra con un error 401 al intentar editar el título.

![Error al intentar editar el título](assets/dev-edit-error.png)

Cuando se utiliza el editor universal para editar el contenido de producción de AEM, el editor universal emplea el mismo token de IMS que se usó para iniciar sesión en el editor y autenticarse en AEM para facilitar la escritura en el JCR.

Cuando se desarrolla de manera local, no se puede utilizar el proveedor de identidad de AEM, ya que los tókenes de IMS solo se pasan a dominios propiedad de Adobe. Debe proporcionar manualmente una forma de autenticarse configurando de manera explícita un encabezado de autenticación.

1. En la interfaz del editor universal, haga clic en el icono **Encabezados de autenticación** de la barra de herramientas.

1. Copie el encabezado de autenticación necesario para autenticarse en la instancia local de AEM y haga clic en **Guardar**.

   ![Configuración de proveedores de autenticación](assets/dev-authentication-headers.png)

1. Vuelva a cargar el editor universal y, a continuación, edite el título del teaser.

Ya no se notifican errores en la consola del explorador y los cambios se mantienen en la instancia de desarrollo de AEM local.

Si investiga el tráfico en las herramientas para desarrolladores del explorador y busca los eventos de `update`, podrá ver los detalles de la actualización.

![Edición correcta del título del teaser](assets/dev-edit-title-successfully.png)

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

* `connections` es la conexión con su instancia local de AEM
* `target` es el nodo y las propiedades exactos que se actualizan en el JCR
* `value` es la actualización que ha realizado usted.

Puede ver que el cambio se ha mantenido en el JCR.

![Actualización en el JCR](assets/dev-write-back-jcr.png)

>[!TIP]
>
>Hay muchas herramientas disponibles en línea para generar los encabezados de autenticación necesarios para los fines de prueba y desarrollo.
>
>El ejemplo del encabezado de autenticación básico `Basic YWRtaW46YWRtaW4=` es para la combinación de usuario y contraseña de `admin:admin`, como es común en el desarrollo de AEM local.

## Instrumentación de la aplicación para el panel de propiedades {#properties-rail}

Ahora tiene una aplicación instrumentada para poder editarla con el editor universal.

Actualmente, la edición se limita a la edición en línea del título del teaser. Sin embargo, hay casos en los que la edición in situ no es suficiente. El texto, por ejemplo el título del teaser, se puede editar donde está mediante la introducción con el teclado. Sin embargo, los elementos más complicados deben poder mostrarse y permitir la edición de datos estructurados independientemente de cómo se representen en el explorador. El panel de propiedades es precisamente para esto.

Para actualizar la aplicación de modo que utilice el panel de propiedades para la edición, vuelva al archivo de encabezado del componente de página de la aplicación. Aquí es donde ya ha establecido las conexiones con la instancia de desarrollo de AEM local y con el servicio de editor universal local. Aquí es donde debe definir los componentes editables en la aplicación y sus modelos de datos.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. En `/apps/wknd/components/page`, edite el archivo `customheaderlibs.html`.

   ![Edición del archivo customheaderlibs.html](assets/dev-instrument-properties-rail.png)

1. Al final del archivo, añada el script necesario para definir los componentes.

   ```html
   <script type="application/vnd.adobe.aue.component+json">
   {
     "groups": [
       {
         "title": "General Components",
         "id": "general",
         "components": [
           {
             "title": "Teaser",
             "id": "teaser",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/teaser"
                 }
               }
             }
           },
           {
             "title": "Title",
             "id": "title",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/title"
                 }
               }
             }
           }
         ]
       }
     ]
   }
   </script>
   ```

1. Debajo, al final del archivo, añada el script necesario para definir el modelo.

   ```html
   <script type="application/vnd.adobe.aue.model+json">
   [
     {
       "id": "teaser",
       "fields": [
         {
           "component": "text-input",
           "name": "jcr:title",
           "label": "Title",
           "valueType": "string"
         },
         {
           "component": "text-area",
           "name": "jcr:description",
           "label": "Description",
           "valueType": "string"
         }
       ]
     },
     {
       "id": "title",
       "fields": [
         {
           "component": "select",
           "name": "type",
           "value": "h1",
           "label": "Type",
           "valueType": "string",
           "options": [
             { "name": "h1", "value": "h1" },
             { "name": "h2", "value": "h2" },
             { "name": "h3", "value": "h3" },
             { "name": "h4", "value": "h4" },
             { "name": "h5", "value": "h5" },
             { "name": "h6", "value": "h6" }
           ]
         }
       ]
     }
   ]
   </script>
   ```

1. Haga clic en **Guardar todo** en la barra de herramientas.

## ¿Qué significa todo esto? {#what-does-it-mean-2}

Para poder editar con el panel de propiedades, los componentes deben estar asignados a `groups`, de modo que cada definición comience como una lista de grupos que contengan los componentes.

* `title` es el nombre del grupo.
* `id` es el identificador único del grupo, en este caso los componentes generales que componen el contenido de la página en lugar de componentes avanzados para el diseño de página, por ejemplo.

Cada grupo tiene, por tanto, una matriz de `components`.

* `title` es el nombre del componente.
* `id` es el identificador único del componente, en este caso un teaser.

A continuación, cada componente tiene una definición de complemento que define cómo se asigna el componente a AEM.

* `aem` es el complemento que administra la edición. Esto se puede considerar como el servicio que procesa el componente.
* `page` define qué tipo de componente es, en este caso un componente de página estándar.
* `resourceType` es la asignación al componente de AEM real.

A continuación, cada componente debe asignarse a un `model` para definir los campos editables individuales.

* `id` es el identificador único del modelo, que debe coincidir con el ID del componente.
* `fields` es una matriz de los campos individuales.
* `component` es el tipo de entrada, como texto o área de texto.
* `name` es el nombre de campo en el JCR al que está asignado el campo.
* `label` es la descripción del campo que aparece en la interfaz de usuario del editor.
* `valueType` es el tipo de datos.

## Instrumentación del componente para el panel Propiedades {#properties-rail-component}

También debe definir en el nivel de componente qué modelo debe utilizar el componente.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. Haga doble clic en el archivo `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` para editarlo.

   ![Edición del archivo teaser.html](assets/dev-edit-teaser.png)

1. Al final del primer `div`, aproximadamente en la línea 32, después de las propiedades añadidas previamente, añada los detalles de instrumentación para el modelo que utilizará el componente teaser.

   ```text
   data-aue-model="teaser"
   ```

1. Haga clic en **Guardar todo** en la barra de herramientas y vuelva a cargar el editor universal.

Ahora está listo para probar el panel de propiedades instrumentado para su componente.

1. En el editor universal, haga clic en el título del teaser para editarlo una vez más.

1. Haga clic en el panel de propiedades para mostrar la pestaña de propiedades y ver los campos que acaba de instrumentar.

   ![Panel de propiedades instrumentadas](assets/dev-properties-rail-instrumented.png)

Ahora puede editar el título del teaser ya sea en línea como lo ha hecho anteriormente, o en el panel de propiedades. En ambos casos, los cambios se mantienen en la instancia de desarrollo de AEM local.

## Adición de campos adicionales al panel Propiedades {#add-fields}

Con la estructura básica del modelo de datos para el componente que ya ha implementado, puede añadir campos adicionales siguiendo el mismo modelo.

Por ejemplo, puede añadir un campo para ajustar el estilo del componente.

1. Abra CRXDE Lite.

   ```text
   https://localhost:8443/crx/de
   ```

1. En `/apps/wknd/components/page`, edite el archivo `customheaderlibs.html`.

   ![Edición del archivo customheaderlibs.html](assets/dev-instrument-styles.png)

1. En el script de definición del modelo, añada un elemento adicional a la matriz `fields` para el campo de estilo. Recuerde añadir una coma después del último campo, antes de insertar el nuevo.

   ```json
   {
      "component": "select",
      "name": "cq:styleIds",
      "label": "Style",
      "valueType": "string",
        "multi": true,
      "options": [
        {"name": "hero", "value":"1555543212672"},
        {"name": "card", "value":"1605057868937"}
      ]
   }
   ```

1. Haga clic en **Guardar todo** en la barra de herramientas y vuelva a cargar el editor universal.

1. Haga clic en el título del teaser para editarlo una vez más.

1. Haga clic en el panel de propiedades y compruebe que hay un nuevo campo para ajustar el estilo del componente.

   ![Panel de propiedades instrumentadas con el campo de estilo](assets/dev-style-instrumented.png)

Cualquier campo en el JCR del componente se puede exponer en el editor universal de esta manera.

## Resumen {#summary}

¡Enhorabuena! Ahora puede instrumentar sus propias aplicaciones de AEM para que funcionen con el editor universal.

Cuando empiece a instrumentar su propia aplicación, tenga en cuenta los pasos básicos que ha realizado en este ejemplo.

1. [Ha configurado su entorno de desarrollo](#prerequisites).
   * AEM se ejecuta localmente en HTTPS con WKND instalado
   * Servicio de editor universal que se ejecuta localmente en HTTPS
1. Ha actualizado la configuración de OSGi de AEM para permitir que su contenido se cargue de forma remota.
   * [`org.apache.sling.engine.impl.SlingMainServlet`](#sameorigin)
   * [`com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`](#samesite-cookies)
1. [Ha añadido la biblioteca `universal-editor-embedded.js` al archivo `customheaderlibs.html` del componente de página de la aplicación](#ue-connect-remote-frame).
1. [Ha definido una conexión para mantener los cambios en el archivo `customheaderlibs.html` del componente de página de la aplicación](#connection).
   * Ha definido una conexión con la instancia de desarrollo de AEM local.
   * También ha definido una conexión con el servicio de editor universal local.
1. [Ha instrumentado el componente teaser](#instrumenting-components).
1. [Ha instrumentado los subcomponentes del teaser](#subcomponents).
1. [Ha definido un encabezado de autenticación personalizado para poder guardar los cambios mediante el servicio de editor universal local](#auth-header).
1. [Ha instrumentado la aplicación para que use el panel de propiedades](#properties-rail).
1. [Ha instrumentado el componente teaser para que use el panel de propiedades](#properties-rail-component).

Puede seguir estos mismos pasos para instrumentar su propia aplicación y utilizarla con el editor universal. Todas las propiedades en el JCR se pueden exponer al editor universal.

## Recursos adicionales {#additional-resources}

Consulte los siguientes documentos para obtener más información y detalles sobre las funciones del editor universal.

* Si desea ponerse en marcha lo antes posible, consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md).
* Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#sameorigin) para obtener más información sobre las configuraciones de OSGi necesarias.
* Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md#connection) para obtener más información sobre los metadatos de conexión.
* Consulte el documento [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md#service) para obtener más información sobre la estructura del editor universal.
* Consulte el documento [Desarrollo local de AEM con el editor universal](/help/implementing/universal-editor/local-dev.md) para obtener más información sobre cómo conectarse a una versión autoalojada del editor universal.
* Consulte el documento [Uso de la fusión de recursos de Sling en Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md) para obtener más información sobre la superposición de nodos.

