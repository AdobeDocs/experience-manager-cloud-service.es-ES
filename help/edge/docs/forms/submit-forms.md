---
title: Preparar la hoja de cálculo para aceptar datos
description: Cree formularios potentes más rápido mediante hojas de cálculo y campos de bloque de formularios.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---


# Preparar la hoja de cálculo para aceptar datos

Una vez que haya [creación y previsualización del formulario](/help/edge/docs/forms/create-forms.md)Sin embargo, es hora de permitir que la hoja de cálculo correspondiente comience a recibir datos.

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

Para habilitar la hoja de cálculo:

1. Abra la hoja de cálculo que tiene el formulario y anexe una hoja nueva, cambiando el nombre a `incoming`.

   >[!WARNING]
   >
   > Si la variable `incoming` AEM La hoja de cálculo no está presente, no se envía ningún dato a la hoja de cálculo, por lo que no se envía ningún dato a la hoja de cálculo.

1. Reflejar los nombres de los campos de formulario, los valores de la variable `Name` en la columna`shared-default` , a los encabezados de la hoja `incoming` hoja.

   Cada valor de `Name` de la columna `shared-default` hoja, excluyendo el botón de envío, sirve como encabezado en la `incoming` hoja. Por ejemplo, vea la siguiente imagen que ilustra los encabezados de un formulario de &quot;contacto&quot;:

   ![Campos para un formulario de contacto](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Utilice la barra de tareas para previsualizar la hoja.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja de cálculo `incoming` por primera vez.


Una vez añadidos los nombres de campo a `incoming` , el formulario estará listo para aceptar envíos. Puede obtener una vista previa del formulario y enviar datos a la hoja mediante él.

También observará los siguientes cambios en la hoja de cálculo:

Se agrega una hoja denominada &quot;Slack&quot; al libro de Excel o a la hoja de Google. En esta hoja, puede configurar las notificaciones automáticas para un canal de Slack designado cada vez que se incorporen nuevos datos en la hoja de cálculo. AEM AEM En la actualidad, el servicio admite notificaciones únicamente a la organización Slack de ingeniería de la organización de y a la organización de soporte Enterprise de Adobe.

1. Para configurar las notificaciones de Slack, introduzca el &quot;teamId&quot; del espacio de trabajo del Slack y el &quot;nombre del canal&quot; o &quot;ID&quot;. También puede solicitar al bot de Slack (con el comando debug) los parámetros &quot;teamId&quot; y &quot;channel ID&quot;. Es preferible utilizar el &quot;ID de canal&quot; en lugar del &quot;nombre de canal&quot;, ya que sobrevive a los cambios de nombre de canal.

   >[!NOTE]
   >
   > Los formularios más antiguos no tenían la columna &quot;teamId&quot;. El &quot;teamId&quot; se incluía en la columna del canal, separado por &quot;#&quot; o &quot;/&quot;.

1. Introduzca el título que desee y en los campos introduzca los nombres de los campos que desea ver en la notificación al Slack. Cada encabezado debe separarse con una coma (por ejemplo, nombre, correo electrónico).

   >[!WARNING]
   >
   >  Las hojas &quot;compartidas por defecto&quot; nunca deben contener información personal identificable o datos confidenciales que no le resulte cómodo tener acceso público.


## (Opcional) Utilice las API de administrador para permitir que una hoja de cálculo acepte datos

También puede enviar una solicitud de POST al formulario para permitir que acepte datos y configure los encabezados del `incoming` hoja. Al recibir la solicitud del POST, el servicio analiza el cuerpo de la solicitud y genera de forma autónoma los encabezados y hojas esenciales necesarios para la ingesta de datos.

Para utilizar las API de administrador para permitir que una hoja de cálculo acepte datos:


1. Abra el libro que ha creado y cambie el nombre de la hoja predeterminada a `incoming`.

   >[!WARNING]
   >
   > Si la variable `incoming` AEM La hoja de cálculo no existe. No se enviará ningún dato a este libro de trabajo.

1. Previsualice la hoja en la barra de tareas.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja de cálculo `incoming` por primera vez.

1. Envíe la solicitud del POST para generar los encabezados adecuados en la `incoming` y añada la etiqueta `shared-default` a la hoja de cálculo, si no existe todavía.

   Para saber cómo dar formato a la solicitud del POST para configurar la hoja, consulte la [Documentación de API de administración](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Puede ver el ejemplo que se proporciona a continuación:

   **Solicitud**

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

   Puede utilizar herramientas como curl o Postman para ejecutar esta solicitud de POST, como se muestra a continuación:

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

   La solicitud de POST mencionada proporciona datos de ejemplo, incluidos los campos de formulario y sus respectivos valores de ejemplo. El servicio de administración utiliza estos datos para configurar el formulario.

   El formulario ahora está habilitado para aceptar datos. También observará los siguientes cambios en la hoja de cálculo:

Se agrega una hoja denominada &quot;Slack&quot; al libro de Excel o a la hoja de Google. En esta hoja, puede configurar las notificaciones automáticas para un canal de Slack designado cada vez que se incorporen nuevos datos en la hoja de cálculo. AEM AEM En la actualidad, el servicio admite notificaciones únicamente a la organización Slack de ingeniería de la organización de y a la organización de soporte Enterprise de Adobe.

1. Para configurar las notificaciones de Slack, introduzca el &quot;teamId&quot; del espacio de trabajo del Slack y el &quot;nombre del canal&quot; o &quot;ID&quot;. También puede solicitar al bot de Slack (con el comando debug) los parámetros &quot;teamId&quot; y &quot;channel ID&quot;. Es preferible utilizar el &quot;ID de canal&quot; en lugar del &quot;nombre de canal&quot;, ya que sobrevive a los cambios de nombre de canal.

   >[!NOTE]
   >
   > Los formularios más antiguos no tenían la columna &quot;teamId&quot;. El &quot;teamId&quot; se incluía en la columna del canal, separado por &quot;#&quot; o &quot;/&quot;.

1. Introduzca el título que desee y en los campos introduzca los nombres de los campos que desea ver en la notificación al Slack. Cada encabezado debe separarse con una coma (por ejemplo, nombre, correo electrónico).


La hoja ahora está configurada para recibir datos, puede [previsualizar el formulario mediante el bloque de formularios](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [usar solicitudes de POST](#use-admin-apis-to-send-data-to-your-sheet) para comenzar a enviar datos a la hoja.

>[!WARNING]
>
>  Las hojas &quot;compartidas por defecto&quot; nunca deben contener información personal identificable o datos confidenciales que no le resulte cómodo tener acceso público.

## Enviar datos a la hoja {#send-data-to-your-sheet}

Una vez que la hoja esté configurada para recibir datos, puede [previsualizar el formulario mediante el bloque de formularios](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) o [Uso de API de administrador](#use-admin-apis-to-send-data-to-your-sheet) para comenzar a enviar datos a la hoja.

### Utilice las API de administrador para enviar datos a la hoja

Puede enviar solicitudes de POST directamente al formulario mediante hlx.page, hlx.live o el dominio de producción para enviar datos.


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> La dirección URL no debe tener la extensión .json. Debe publicar la hoja para que las operaciones del POST funcionen en `.live` o en el dominio de producción.

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

* URL codificada (`x-www-form-urlencoded`) cuerpo (con `content-type` encabezado establecido en `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  Por ejemplo,

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

A continuación, puede personalizar el mensaje de agradecimiento, [configurar una página de agradecimiento](/help/edge/docs/forms/thank-you-page-form.md), o [establecer redirecciones](/help/edge/docs/forms/thank-you-page-form.md).

## Más información

* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)