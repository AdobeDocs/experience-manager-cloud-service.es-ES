---
title: Creación de un formulario mediante la creación basada en documentos para el servicio de entrega perimetral de AEM Forms
description: ¡Crea formas perfectas, rápido! ⚡ AEM Forms Edge Delivery + creación basada en documentos = velocidad increíble y formularios compatibles con SEO para usuarios y motores de búsqueda más felices.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Creación de un formulario mediante la creación basada en documentos para el servicio de entrega perimetral de AEM Forms

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. La creación basada en documentos de AEM Forms Edge Delivery permite crear formularios utilizando herramientas conocidas como Word o Google Docs. Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft Sharepoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

Esta guía le explica lo siguiente:

* Preparación de la hoja de cálculo: Aprenda a configurar un archivo de hojas de cálculo de Excel o Google para la recopilación de datos y a agregarle campos de formulario.
* Enviar datos a la hoja: Aprenda a enviar datos a la hoja mediante solicitudes del POST.
* Publicación del formulario: integre el formulario en la página de AEM Sites o publíquelo como una página independiente.

Tanto si es un principiante como un profesional, esta guía le permite crear formularios hermosos y funcionales que encantan a los usuarios. Vamos a desbloquear la creación eficiente de formularios: ¡sumérjase ahora!

## Antes de comenzar

`WIP`

## Preparación de una hoja de cálculo para recibir datos

1. Cree un libro o una hoja de Google AEM de Microsoft Excel en cualquier parte bajo el directorio del proyecto de entrega perimetral de en Microsoft OneDrive o Google Drive. Este documento utiliza una hoja de Google denominada `contact-us.xlsx`, ubicado en la raíz de un proyecto de Adobe Experience Manager AEM ().

1. AEM Asegúrese de que el usuario de la plantilla (por ejemplo, helix@adobe.com) configurado para su proyecto tenga permisos de edición para la hoja.

1. Abra el libro que ha creado y cambie el nombre de la hoja predeterminada a entrante.

   >[!NOTE]
   >
   > AEM Si la hoja &quot;entrante&quot; no existe, no se envía ningún dato a este libro de trabajo, ya que no se envía ningún dato a la hoja de cálculo &quot;entrante&quot;.

1. Previsualice la hoja en la barra de tareas.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja &quot;entrante&quot; por primera vez.

1. Prepare la hoja agregando encabezados que coincidan con los datos que va a incluir. El siguiente ejemplo muestra los campos de un formulario &quot;contact-us&quot;:

   ![Campos para un formulario de contacto](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Puede hacerlo manualmente o mediante una solicitud de POST AEM a la ruta del formulario en el servicio de administración de la. El servicio de administración examinará los datos en el cuerpo del POST y generará los encabezados, las tablas y las hojas necesarias para introducir los datos de forma eficaz y aprovechar al máximo el servicio de Forms.

   Para saber cómo dar formato a la solicitud del POST para configurar la hoja, consulte la [Documentación de API de administración](https://www.hlx.live/docs/admin.html#tag/form). Además, observe el ejemplo que se proporciona a continuación:

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

Aunque el servicio de administración recomienda configurar la hoja, si prefiere crear los encabezados manualmente, consulte el documento titulado [Configuración manual de hojas de Forms](https://www.hlx.live/docs/manual-forms-sheet-setup).

Al enviar la solicitud del POST al servicio de administración, observará los siguientes cambios en el libro de trabajo:

* Se agrega una nueva hoja denominada &quot;shared-default&quot; al libro de Excel o a la hoja de Google. Los datos presentes en la hoja &quot;shared-default&quot; se recuperan al realizar una solicitud de GET a la hoja. Esta hoja sirve como una ubicación óptima para utilizar fórmulas de hoja de cálculo para resumir los datos entrantes, lo que la hace propicia para el consumo en otros contextos.

  Bajo ninguna circunstancia la hoja &quot;shared-default&quot; debe contener información personal identificable o datos sensibles que no se sienta cómodo con ser de acceso público.

* Se agrega una hoja denominada &quot;slack&quot; al libro de Excel o a la hoja de Google. En esta hoja, puede configurar las notificaciones automáticas para un canal de Slack designado cada vez que se incorporen nuevos datos en la hoja de cálculo. AEM AEM En la actualidad, el servicio admite notificaciones únicamente a la organización Slack de ingeniería de la organización de y a la organización de soporte Enterprise de Adobe.

   1. Para configurar las notificaciones del Slack, introduzca el &quot;teamId&quot; del espacio de trabajo del Slack y el &quot;nombre del canal&quot; o &quot;ID&quot;. También puede solicitar al bot de Slack (con el comando debug) los parámetros &quot;teamId&quot; y &quot;channel ID&quot;. Es preferible utilizar el &quot;ID de canal&quot; en lugar del &quot;nombre de canal&quot;, ya que sobrevive a los cambios de nombre de canal.

      >[!NOTE]
      >
      > Los formularios más antiguos no tenían la columna &quot;teamId&quot;. El &quot;teamId&quot; se incluía en la columna del canal, separado por &quot;#&quot; o &quot;/&quot;.

   1. Escriba el título que desee y en los campos escriba los nombres de los campos que desee ver en la notificación al Slack. Cada encabezado debe separarse con una coma (por ejemplo, nombre, correo electrónico).

Ahora, la hoja está configurada para recibir datos y puede enviar solicitudes de POST directamente a ella mediante hlx.page, hlx.live o su dominio de producción.


## Enviar datos a la hoja {#send-data-to-your-sheet}

Una vez que la hoja esté configurada para recibir datos, puede enviarle solicitudes de POST directamente mediante hlx.page, hlx.live o su dominio de producción para enviar datos.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> La dirección URL no debe tener la extensión .json. Debe publicar la hoja para que las operaciones de POST funcionen en .live o en el dominio de producción.

### Formato de datos para EDS Forms

Existen varias formas de dar formato a los datos del formulario en el cuerpo del POST.

* Matriz de pares nombre:valor:

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* Objeto con pares clave:valor

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

* `x-www-form-urlencoded` cuerpo (`content-type` el encabezado debe establecerse en `application/x-www-form-urlencoded`) &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



