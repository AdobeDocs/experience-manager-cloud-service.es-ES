---
title: Creación de un formulario mediante la creación basada en documentos para Forms Edge Delivery Service de AEM
description: Elabore formularios perfectos, ¡y rápido! ⚡ Edge Delivery Services de AEM Forms + creación basada en documentos = velocidad increíble, formularios compatibles con SEO y motores de búsqueda para usuarios más satisfechos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 100%

---


# Creación de un formulario mediante la creación basada en documentos para Forms Edge Delivery Service de AEM

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. La creación basada en documentos de AEM Forms Delivery Edge le permite crear formularios usando herramientas como Word o Google Docs. Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft SharePoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

Esta guía le explica lo siguiente:

* Preparación de la hoja de cálculo: aprenda a configurar un archivo de Excel o Google Sheets para la recopilación de datos y a añadirle campos de formulario.
* Envío de datos a la hoja: aprenda a enviar datos a su hoja mediante peticiones POST.
* Publicación del formulario: integre su formulario en la página de AEM Sites o publíquelo como una página independiente.

Tanto si es un principiante como si es un profesional, esta guía le permite crear formularios hermosos y funcionales que les encantan a los usuarios. Vamos a descubrir cómo crear formularios eficientes: ¡láncese ahora!

## Antes de comenzar

`WIP`

## Preparación de la hoja de cálculo para recibir datos

1. Cree un libro de trabajo de Microsoft Excel o una hoja de Google en cualquier parte del directorio de proyectos de AEM Edge Delivery en Microsoft OneDrive o Google Drive. Este documento utiliza una hoja de Google denominada `contact-us.xlsx`, ubicada en la raíz de un proyecto de Adobe Experience Manager (AEM).

1. Asegúrese de que el usuario de AEM (por ejemplo, helix@adobe.com) configurado para su proyecto tenga permisos de edición para la hoja.

1. Abra el libro de trabajo que ha creado y cambie el nombre de la hoja predeterminada a &quot;entrante&quot;.

   >[!NOTE]
   >
   > Si la hoja &quot;entrante&quot; no existe, AEM no enviará ningún dato a este libro de trabajo.

1. Previsualice la hoja en la barra de tareas.

   >[!NOTE]
   >
   >Incluso si ya ha previsualizado la hoja anteriormente, debe volver a previsualizarla después de crear la hoja &quot;entrante&quot; por primera vez.

1. Prepare la hoja añadiendo encabezados que coincidan con los datos que va a incluir. El siguiente ejemplo muestra los campos de un formulario &quot;contáctenos&quot;:

   ![Campos para un formulario contáctenos](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Puede hacerlo manualmente o mediante una petición POST a la ruta del formulario en el servicio de administración de AEM. El servicio de administración examinará los datos en el cuerpo de POST y generará los encabezados, las tablas y las hojas adecuadas para ingestar los datos de forma eficaz y aprovechar al máximo el servicio de formularios.

   Para saber cómo dar formato a la petición POST para configurar la hoja, consulte la [Documentación de API de administrador](https://www.hlx.live/docs/admin.html?lang=es#tag/form). Además, eche una ojeada al ejemplo que se muestra a continuación:

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

Aunque el servicio de administración recomienda configurar la hoja, si prefiere crear los encabezados manualmente, consulte el documento titulado [Configuración manual de hojas de formularios](https://www.hlx.live/docs/manual-forms-sheet-setup).

Tras enviar la petición POST al servicio de administración, detectará los siguientes cambios en el libro de trabajo:

* Se ha añadido una hoja denominada “shared-default” al libro de trabajo de Excel o a la hoja de Google. Los datos presentes en la hoja &quot;shared-default&quot; se recuperan al realizar una petición GET a la hoja. Esta hoja sirve de ubicación óptima para utilizar fórmulas de hoja de cálculo para resumir los datos entrantes, lo que la hace propicia para el consumo en otros contextos.

  Bajo ningún concepto la hoja &quot;shared-default&quot; debe contener información personal identificable o datos confidenciales con los que no se sienta cómodo si tienen acceso público.

* Se ha añadido una hoja denominada “Slack” al libro de trabajo de Excel o a la hoja de Google. En esta hoja, puede configurar las notificaciones automáticas para un canal de Slack designado cada vez que se incorporen nuevos datos en la hoja de cálculo. En la actualidad, AEM admite notificaciones únicamente a las organizaciones AEM Engineering Slack y Adobe Enterprise Support.

   1. Para configurar las notificaciones de Slack, escriba “teamId” en el espacio de trabajo de Slack y el nombre del canal o “ID”. También puede solicitar al bot de Slack (con el comando debug) para el “teamId” y “channel ID”. Es preferible utilizar el “ID de canal” en lugar del “nombre de canal”, ya que se mantiene después de cambiar el nombre del canal.

      >[!NOTE]
      >
      > Los formularios anteriores no tenían la columna “teamId”. El “teamId” se incluía en la columna del canal, separado por “#” o “/”.

   1. Introduzca el título que desee y en los campos escriba los nombres de los campos que desea ver en la notificación de Slack. Cada encabezado debe separarse con una coma (por ejemplo, nombre, correo electrónico).

Ahora, la hoja está configurada para recibir datos y puede enviarle peticiones POST directamente mediante hlx.page, hlx.live o su dominio de producción.


## Enviar datos a la hoja {#send-data-to-your-sheet}

Una vez que la hoja esté configurada para recibir datos, puede enviarle peticiones POST directamente mediante hlx.page, hlx.live o su dominio de producción para enviar datos.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> La dirección URL no debe tener la extensión .json. Debe publicar la hoja para que las operaciones POST funcionen en .live o en el dominio de producción.

### Formato de datos para formularios de EDS

Existen varias formas de dar formato a los datos del formulario en el cuerpo de POST.

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

* `x-www-form-urlencoded` cuerpo (`content-type` el encabezado debe establecerse en `application/x-www-form-urlencoded`)
&#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



