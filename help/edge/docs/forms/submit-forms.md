---
title: Preparación de la hoja de cálculo para aceptar datos
description: Cree formularios potentes más rápido con hojas de cálculo y campos de bloque de formularios adaptables.
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: ht
source-wordcount: '1001'
ht-degree: 100%

---

# Configure Google Sheets o los archivos de Microsoft Excel para empezar a aceptar datos


Una vez que haya [creado y previsualizado el formulario](/help/edge/docs/forms/create-forms.md), es hora de permitir que la hoja de cálculo correspondiente comience a recibir datos. Puede habilitar manualmente la hoja de cálculo para que acepte datos o utilizar las API de administrador para habilitar una hoja de cálculo que acepte datos.

![Ecosistema de creación basado en documentos](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->


## Habilitar manualmente la hoja de cálculo para que acepte datos

Para permitir que la hoja de cálculo acepte datos

1. Abra la hoja de cálculo que tiene el formulario y anexe una hoja nueva, cambiando el nombre a `incoming`.

   >[!WARNING]
   >
   > Si la hoja `incoming` no está presente, AEM no envía ningún dato a la hoja de cálculo.

1. En esta hoja, inserte una tabla denominada &quot;intake_form&quot;. Seleccione el número de columnas necesarias para hacer coincidir los nombres de los campos de formulario. A continuación, en la barra de herramientas, vaya a Insertar > Tabla y haga clic en Aceptar.

1. Cambie el nombre de la tabla por &quot;intake_form&quot;.  En Microsoft Excel, para cambiar el nombre de la tabla, seleccione la tabla y haga clic en Diseño de tabla.

1. A continuación, añada los nombres de los campos de formulario como encabezados de tabla. Para asegurarse de que los campos son exactamente los mismos, puede copiarlos y pegarlos en la hoja &quot;shared-default&quot;.  En la hoja &quot;shared-default&quot;, seleccione y copie los ID de formulario listados en la columna &quot;Name&quot;, excepto el campo de envío.

1. En la hoja &quot;incoming&quot;, seleccione Pegado especial > Transponer filas a columnas para copiar los ID de campo como encabezados de columna en esta nueva hoja. Mantener solo los campos cuyos datos necesitan capturar otros datos se puede ignorar.

   Cada valor de la columna `Name` de la hoja `shared-default`, excluyendo el botón de envío, puede servir como encabezado en la hoja `incoming`. Por ejemplo, vea la siguiente imagen que ilustra los encabezados de un formulario &quot;contáctenos&quot;:

   ![Campos para un formulario contáctenos](/help/edge/assets/contact-us-form-excel-sheet-fields.png)



1. Utilice la extensión de AEM Sidekick para obtener una vista previa de las actualizaciones del formulario. La hoja ya está lista para aceptar los envíos de formulario entrantes.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja `incoming` por primera vez.


Una vez añadidos los nombres de campo a la hoja `incoming`, el formulario estará listo para aceptar envíos. Puede obtener una vista previa del formulario y enviar datos a la hoja utilizándolo.

Una vez configurada la hoja para recibir datos, puede [previsualizar el formulario con el bloque de formularios adaptables](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizar peticiones POST](#use-admin-apis-to-send-data-to-your-sheet) para empezar a enviar datos a la hoja.

>[!WARNING]
>
>  Las hojas &quot;shared-default&quot; nunca deben contener información personal identificable o datos confidenciales con los que no se sienta cómodo si tienen acceso público.

### Utilice las API de administrador para habilitar una hoja de cálculo que acepte datos

También puede enviar una petición POST al formulario para habilitarla para que acepte datos y configurar los encabezados de la hoja `incoming`. Al recibir la petición POST, el servicio analiza el cuerpo de la solicitud y genera de forma autónoma los encabezados y hojas esenciales necesarios para la ingesta de datos.

Para utilizar las API de administrador para habilitar una hoja de cálculo que acepte datos:


1. Abra el libro que ha creado y cambie el nombre de la hoja predeterminada a `incoming`.

   >[!WARNING]
   >
   > Si la hoja `incoming` no existe, AEM no enviará ningún dato a este libro de trabajo.

1. Previsualice la hoja en la barra de tareas.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja `incoming` por primera vez.

1. Envíe la petición POST para generar los encabezados adecuados en la hoja `incoming` y añada las hojas `shared-default` a la hoja de cálculo, si no existe todavía.

   Para saber cómo dar formato a la petición POST para configurar la hoja, consulte la [Documentación de API de administrador](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Puede ver el ejemplo que se proporciona a continuación:

   **Petición**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```


   **Respuesta**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   Puede utilizar herramientas como cURL o Postman para ejecutar esta petición POST, como se muestra a continuación:

   ```JSON
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

   La petición POST mencionada anteriormente proporciona datos de muestra, incluidos los campos de formulario y sus respectivos valores de ejemplo. El servicio de administración utiliza estos datos para configurar el formulario.

   El formulario ahora está habilitado para aceptar datos. También observará los siguientes cambios en la hoja de cálculo:

## Cambios automáticos en la hoja una vez que está habilitada para aceptar datos.

Una vez que la hoja está configurada para recibir datos, se observan los siguientes cambios en la hoja de cálculo:

Se agrega una hoja denominada “Slack” al libro de Excel o a la hoja de Google Sheets. En esta hoja, puede configurar las notificaciones automáticas para un canal de Slack designado cada vez que se incorporen nuevos datos en la hoja de cálculo. En la actualidad, AEM admite notificaciones únicamente a las organizaciones AEM Engineering Slack y Adobe Enterprise Support.

1. Para configurar las notificaciones de Slack, escriba “teamId” en el espacio de trabajo de Slack y el nombre del canal o “ID”. También puede solicitar al bot de Slack (con el comando debug) para el “teamId” y “channel ID”. Es preferible utilizar el “ID de canal” en lugar del “nombre de canal”, ya que se mantiene después de cambiar el nombre del canal.

   >[!NOTE]
   >
   > Los formularios anteriores no tenían la columna “teamId”. El “teamId” se incluía en la columna del canal, separado por “#” o “/”.

1. Introduzca el título que desee y en los campos escriba los nombres de los campos que desea ver en la notificación de Slack. Cada encabezado debe separarse con una coma (por ejemplo, nombre, correo electrónico).

   >[!WARNING]
   >
   >  Las hojas &quot;shared-default&quot; nunca deben contener información personal identificable o datos confidenciales con los que no se sienta cómodo si tienen acceso público.


## Enviar datos a la hoja {#send-data-to-your-sheet}

Una vez que la hoja esté configurada para recibir datos, puede [previsualizar el formulario con el bloque de formularios adaptables](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [utilizar las API de administrador](#use-admin-apis-to-send-data-to-your-sheet) para comenzar a enviar datos a la hoja.

### Utilizar las API de administrador para enviar datos a la hoja

Puede enviar solicitudes POST directamente al formulario mediante hlx.page, hlx.live o el dominio de producción para enviar datos.


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> La dirección URL no debe tener la extensión .json. Debe publicar la hoja para que las operaciones POST funcionen en `.live` o en el dominio de producción.

#### Formato de los datos del formulario

Existen varias formas de dar formato a los datos del formulario en el cuerpo del POST. Puede utilizar lo siguiente:

* matriz de `name:value` pares:

  ```JSON
  {
    "data": [
      { "name": "name", "value": "Clark Kent" },
      { "name": "email", "value": "superman@example.com" },
      { "name": "subject", "value": "Regarding Product Inquiry" },
      { "name": "message", "value": "I have some questions about your products." },
      { "name": "phone", "value": "123-456-7890" },
      { "name": "company", "value": "Example Inc." },
      { "name": "country", "value": "United States" },
      { "name": "preferred_contact_method", "value": "Email" },
      { "name": "newsletter_subscribe", "value": true }
    ]
  }
  ```

  Por ejemplo

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
      --header 'Content-Type: application/json' \
      --data '{
      "data": [
          { "name": "name", "value": "Clark Kent" },
          { "name": "email", "value": "superman@example.com" },
          { "name": "subject", "value": "Regarding Product Inquiry" },
          { "name": "message", "value": "I have some questions about your        products." },
          { "name": "phone", "value": "123-456-7890" },
          { "name": "company", "value": "Example Inc." },
          { "name": "country", "value": "United States" },
          { "name": "preferred_contact_method", "value": "Email" },
          { "name": "newsletter_subscribe", "value": true }
      ]
  }'
  ```



* un objeto con `key:value` pares:

  ```JSON
      {
        "data": {
          "name": "Jessica Jones",
          "email": "jj@example.com",
          "subject": "Regarding Product Inquiry",
          "message": "I have some questions about your products.",
          "phone": "123-456-7890",
          "company": "Example Inc.",
          "country": "United States",
          "preferred_contact_method": "Email",
          "newsletter_subscribe": true
        }
      }
  ```

  Por ejemplo,

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
  --header 'Content-Type: application/json' \
  --data '{
      "data": {
          "Email": "khushwant@wknd.com",
          "Name": "khushwant",
          "Subject": "Regarding Product Inquiry",
          "Message": "I have some questions about your products.",
          "Phone": "123-456-7890",
          "Company": "Adobe Inc.",
          "Country": "United States",
          "PreferredContactMethod": "Email",
          "SubscribeToNewsletter": true
      }
  }'
  ```

* Cuerpo de la URL codificada (`x-www-form-urlencoded`) (con el `content-type`encabezado establecido en `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  Por ejemplo,

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

A continuación, puede [personalizar el mensaje de agradecimiento](/help/edge/docs/forms/thank-you-page-form.md).

## Consulte también

{{see-more-forms-eds}}
