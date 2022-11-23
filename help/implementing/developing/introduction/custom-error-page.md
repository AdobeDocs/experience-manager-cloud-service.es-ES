---
title: Páginas de error personalizadas
description: AEM incluye un controlador de error estándar para gestionar errores HTTP, que se puede personalizar.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: db997127c6cbba434b86990852d1ba590d5f12a5
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---

# Personalización de páginas de error {#customizing-error-pages}

AEM incluye un controlador de error estándar para gestionar errores HTTP; por ejemplo, mostrando:

![Mensaje de error estándar](assets/error-message-standard.png)

Para responder a errores, AEM proporciona un `404.jsp` script bajo `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Como AEM se basa en Apache Sling, hay más información disponible [en la documentación de gestión de errores de Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento completo de la pila en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es **always** deshabilitado (incluso si está configurado como habilitado).

## Cómo personalizar páginas mostradas por el controlador de errores {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se encuentra un error. Para ello, aprovechará [AEM mecanismo de superposición estándar](/help/implementing/developing/introduction/overlays.md) para que las páginas personalizadas se creen en `/apps` y superponga las páginas predeterminadas que se encuentran en `/libs`.

1. En el repositorio, copie los scripts predeterminados:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   La ruta de destino no existe de forma predeterminada, por lo que deberá crearla al hacerlo por primera vez.

1. Vaya a `/apps/sling/servlet/errorhandler`. Aquí puede:

   * edite la secuencia de comandos existente adecuada para proporcionar la información necesaria. O bien
   * cree y edite una nueva secuencia de comandos para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>La variable `404.jsp` el script se ha diseñado específicamente para adaptarse a AEM autenticación; en particular, permitir el inicio de sesión en el sistema en caso de estos errores.
>
>Por lo tanto, el reemplazo de esta secuencia de comandos debe realizarse con bueno cuidado.

### Personalización de la respuesta a errores HTTP 500 {#customizing-the-response-to-http-errors}

El HTTP [500 Error interno del servidor](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un error del lado del servidor, como que el servidor encuentra una condición inesperada que le impidió cumplir la solicitud.

Cuando el procesamiento de la solicitud resulta en una excepción, el marco Apache Sling (que AEM está activado):

* Registra la excepción
* Y vuelve al cuerpo de la respuesta:
   * El código de respuesta HTTP 500
   * Seguimiento de pila de excepciones

Por [personalización de las páginas que muestra el controlador de errores](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` se puede crear una secuencia de comandos. Sin embargo, solo se usa si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un captador de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero la variable `500.jsp` no se ejecuta la secuencia de comandos.

Para gestionar 500 errores, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para gestionar todas estas excepciones, puede crear una secuencia de comandos `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>En AEM como Cloud Service, la CDN proporciona una página de error genérica cada vez que se recibe un error 5XX del servidor. Para permitir que pase la respuesta real del servidor, debe añadir el siguiente encabezado a la respuesta:
>`x-aem-error-pass: true`
>Esto solo funcionará para las respuestas procedentes de AEM o de la capa de Apache/Dispatcher. Otros errores inesperados procedentes de capas de infraestructura intermedias seguirán mostrando la página de error genérico.

>[!CAUTION]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento completo de la pila en la respuesta.
>
>Para un controlador de error personalizado, se necesitan respuestas con el código 500, por lo que se requiere la variable [El filtro de depuración de CQ WCM debe deshabilitarse.](/help/implementing/deploying/configuring-osgi.md) Esto garantiza que se devuelva el código de respuesta 500, que a su vez déclencheur el gestor de errores de Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es **always** deshabilitado (incluso si está configurado como habilitado).
