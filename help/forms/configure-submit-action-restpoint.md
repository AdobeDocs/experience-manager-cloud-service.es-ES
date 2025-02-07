---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: Punto final REST de AEM Forms, Enviar a punto final REST, Publicar datos en URL REST, Configurar acción de punto final REST
feature: Adaptive Forms, Core Components
title: ¿Configurar una acción de envío para un formulario adaptable?
role: User, Developer
source-git-commit: c20b8909bb884f14bd7fe59f190de3cd375a7111
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 88%

---

# Configurar un formulario adaptable para la acción de envío del punto final REST

Utilice la acción **[!UICONTROL Enviar al punto final REST]** para publicar los datos enviados en una URL de REST. La URL puede ser de un servidor interno (el servidor en el que se procesa el formulario) o externo.

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

## Ventajas

Algunas de las ventajas de configurar la acción de envío **[!UICONTROL Enviar al punto final REST]** para los formularios adaptables son:

* Permite la integración perfecta de los datos del formulario con los sistemas y servicios externos a través de las API de RESTful.
* Proporciona flexibilidad para manejar envíos de datos de formularios adaptables, lo que admite estructuras de datos dinámicas y complejas.
* Admite la asignación dinámica de campos de formulario a parámetros en la dirección URL del punto final REST, lo que permite envíos de datos adaptables y personalizables.


## Configurar la acción de envío Enviar al punto final REST {#steps-to-configure-submit-to-restendpoint-submit-action}

Para configurar la acción de envío en función de la especificación de API abierta de Swagger:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Enviar al punto final REST]**.
   ![Configuración de la acción de Enviar a punto final REST](/help/forms/assets/submit-action-restendpoint.png)

   Para enviar datos a un servidor interno, proporcione la ruta del recurso. Los datos se publican en la ruta del recurso. Por ejemplo, `/content/restEndPoint`. Para esas peticiones POST se utiliza la información de autenticación de la solicitud de envío.

   Para enviar datos a un servidor externo, proporcione una URL. El formato de la URL es el siguiente `https://host:port/path_to_rest_end_point`. Asegúrese de configurar la ruta para controlar la petición POST de forma anónima.

   ![Asignación de valores de campo pasados como parámetros de la página de agradecimiento](assets/post-enabled-actionconfig.png)

   En el ejemplo anterior, el usuario ha escrito información en `textbox` y se captura mediante el parámetro `param1`. La sintaxis para anunciar datos capturados con `param1` es la siguiente:

   `String data=request.getParameter("param1");`

   Del mismo modo, los parámetros que utiliza para publicar datos XML y archivos adjuntos son `dataXml` y `attachments`.

   Por ejemplo, utiliza estos dos parámetros en el script para analizar los datos en un punto final de REST. Se utiliza la siguiente sintaxis para almacenar y analizar los datos:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   En este ejemplo, `data` almacena los datos XML y `att` almacena datos adjuntos.

   La acción de envío **[!UICONTROL Enviar al punto final REST]** envía los datos rellenados en el formulario a una página de confirmación configurada como parte de la petición HTTP GET. Puede añadir el nombre de los campos que desea solicitar. El formato de la solicitud es el siguiente:

   `{fieldName}={request parameter name}`

   Como se muestra en la siguiente imagen, `param1` y `param2` se pasan como parámetros con valores copiados de los campos **cuadro de texto** y **del cuadro numérico** para la siguiente acción.

   ![Configurar la acción de envío del punto final de REST.](assets/action-config.png)

   También puede **[!UICONTROL Habilitar la petición POST]** y proporcionar una URL para publicar la solicitud. Para enviar datos al servidor de AEM que aloja el formulario, utilice una ruta relativa correspondiente a la ruta raíz del servidor de AEM. Por ejemplo, `/content/forms/af/SampleForm.html`. Para enviar datos a cualquier otro servidor, utilice la ruta absoluta.

1. Haga clic en **[!UICONTROL Listo]**.

### Configurar la acción de envío en función del extremo de REST de servicio {#config-service-endpoint-auth}

<span class="preview">: la capacidad Punto final de servicio está en el programa de usuarios que la adoptaron por anticipado y solo se aplica a los componentes principales. Puede enviar un correo electrónico a aem-forms-ea@adobe.com desde su ID oficial para unirse al programa de usuarios pioneros y solicitar acceso a esta funcionalidad. </span>

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Enviar al punto final REST]**.
1. Habilite la solicitud de POST.
1. Especifique la URL del extremo REST.
1. Seleccione la configuración que ha creado para su Tipo de autenticación de extremo de REST de servicio y los Tipos de contenido. Para obtener más información acerca del tipo de autenticación y los tipos de contenido, visite [configurar fuentes de datos](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint).
   ![Configurar el extremo REST](assets/rest-service-endpoint-config.png)
1. Haga clic en Listo.

## Prácticas recomendadas

* Al publicar datos en un servidor externo, asegúrese de que la dirección URL sea segura y configure la ruta para gestionar la petición POST de forma anónima a fin de proteger la información confidencial.
* Para pasar los campos como parámetros en una URL REST, todos los campos deben tener nombres de elementos diferentes, incluso si se colocan en paneles diferentes.

## Artículos relacionados

{{af-submit-action}}
