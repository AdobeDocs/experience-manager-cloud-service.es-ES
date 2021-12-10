---
title: ¿Configurar el envío asincrónico para Forms adaptable?
description: Obtenga información sobre cómo configurar el envío asincrónico para Forms adaptable. Descubra más información sobre cómo funciona el envío asincrónico para Adaptive Forms.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 026f4920-f8f9-4b08-b1b0-af50229633d7
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Envío asíncrono de Forms adaptable {#asynchronous-submission-of-adaptive-forms}

Tradicionalmente, los formularios web se configuran para enviarse sincrónicamente. En el envío sincrónico, cuando los usuarios envían un formulario, se les redirige a una página de reconocimiento, a una página de agradecimiento o, en caso de error en el envío, a una página de error. Sin embargo, las experiencias web modernas, como las aplicaciones de una sola página, están ganando popularidad cuando la página web permanece estática mientras que la interacción cliente-servidor se produce en segundo plano. Puede configurar el envío asincrónico para proporcionar esta experiencia con Forms adaptable.

En el envío asincrónico, cuando un usuario envía un formulario, el desarrollador del formulario rellena una experiencia independiente como redirigir a otro formulario o a una sección independiente del sitio web. El autor también puede añadir servicios independientes, como el envío de datos a un almacén de datos diferente o añadir un motor de análisis personalizado. En caso de envío asincrónico, un formulario adaptable se comporta como una aplicación de una sola página, ya que el formulario no se vuelve a cargar o su URL no cambia cuando los datos del formulario enviados se validan en el servidor.

Siga leyendo para obtener más información sobre el envío asincrónico en Forms adaptable.

## Configuración del envío asincrónico {#configure}

Para configurar el envío asincrónico de un formulario adaptable:

1. En el modo de creación de formularios adaptables, seleccione el objeto Contenedor de formulario y pulse ![cmppr1](assets/configure-icon.svg) para abrir sus propiedades.
1. En el **[!UICONTROL Envío]** sección propiedades, habilitar **[!UICONTROL Usar envío asincrónico]**.
1. En el **[!UICONTROL Al enviar]** , seleccione una de las siguientes opciones para realizar el envío correcto del formulario.

   * **[!UICONTROL Redirigir a URL]**: Redirige a la dirección URL o página especificada en el envío del formulario. Puede especificar una dirección URL o examinar para elegir la ruta a una página en la **[!UICONTROL Dirección URL/ruta de redireccionamiento]** campo .
   * **[!UICONTROL Mostrar mensaje]**: Muestra un mensaje sobre el envío del formulario. Puede escribir un mensaje en el campo de texto debajo del **[!UICONTROL Mostrar mensaje]** . El campo de texto admite el formato de texto enriquecido.

1. Toque ![check-button1](assets/save_icon.svg) para guardar las propiedades.

## Funcionamiento del envío asincrónico {#how-asynchronous-submission-works}

[!DNL Experience Manager Forms] proporciona controladores de éxito y de errores listos para usar para los envíos de formularios. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se envía un formulario, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el suceso success o error del envío. La información se pasa como parámetros al controlador correspondiente para ejecutar la función.

Además, los autores y desarrolladores de formularios pueden escribir reglas a nivel de formulario para anular los controladores predeterminados. Para obtener más información, consulte [Anular los controladores predeterminados mediante reglas](#custom).

Primero vamos a revisar la respuesta del servidor para los eventos de éxito y de error.

### Respuesta del servidor para el evento de éxito de envío {#server-response-for-submission-success-event}

La estructura de la respuesta del servidor para el evento de éxito de envío es la siguiente:

```json
{oneOf: [
{  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouOption : {type : "string"}
   }},
  properties : {
     contentType : {"type" : "string",  "enum" : ["xmlschema", "jsonschema"]},
    data : {type : "string", description : "Form data in XML or  JSON  format"},
   thankYouContent: {type: "string"}
   }
]

}
```

La respuesta del servidor en caso de que el envío del formulario se realice correctamente incluye:

* Tipo de formato de datos del formulario: XML o JSON
* Datos de formulario en formato XML o JSON
* Opción seleccionada para redireccionar a una página o mostrar un mensaje como se ha configurado en el formulario
* Dirección URL de la página o contenido del mensaje, según la configuración del formulario

El controlador de éxito lee la respuesta del servidor y, en consecuencia, redirige a la dirección URL de la página configurada o muestra un mensaje.

### Respuesta del servidor para el evento de error de envío {#server-response-for-submission-error-event}

La estructura de la respuesta del servidor para el evento de error de envío es la siguiente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La respuesta del servidor en caso de error en el envío del formulario incluye:

* Motivo del error, error de CAPTCHA o validación del lado del servidor
* Lista de objetos de error, que incluye la expresión SOM del campo en el que se ha producido un error al efectuar la validación y el mensaje de error correspondiente

El controlador de errores lee la respuesta del servidor y, en consecuencia, muestra el mensaje de error en el formulario.

## Anular los controladores predeterminados mediante reglas {#custom}

Los desarrolladores y autores de formularios pueden escribir reglas, a nivel de formulario, para anular los controladores predeterminados. La respuesta del servidor para eventos de éxito y error se expone en el nivel de formulario, al que los desarrolladores pueden acceder mediante `$event.data` en las reglas.

Realice los siguientes pasos para escribir reglas para controlar los eventos de éxito y error.

1. Abra el formulario adaptable en modo de creación, seleccione cualquier objeto de formulario y pulse ![edit-rules1](assets/edit-rules-icon.svg) para abrir el editor de reglas.
1. Select **[!UICONTROL Formulario]** en el árbol Objetos de formulario y pulse **[!UICONTROL Crear]**.
1. Choose **[!UICONTROL se ha enviado correctamente]** o **[!UICONTROL error de envío]** de la variable **[!UICONTROL Seleccionar estado]** lista desplegable.
1. Defina un **[!UICONTROL Entonces]** para el estado seleccionado. Por ejemplo, seleccione **[!UICONTROL Navegar a]** y después escriba o pegue una dirección URL. También puede arrastrar cualquier función con la función **[!UICONTROL Funciones]** a la regla.

   ![controlador de envío correcto](assets/form-submission-handler.png)

1. Toque **[!UICONTROL Listo]** para guardar la regla.
