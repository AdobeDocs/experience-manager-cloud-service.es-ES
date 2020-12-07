---
title: Páginas de error personalizadas
description: AEM incluye un controlador de error estándar para el manejo de errores HTTP, que se puede personalizar.
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Personalización de páginas de error {#customizing-error-pages}

AEM viene con un controlador de error estándar para controlar los errores HTTP; por ejemplo, mostrando:

![Mensaje de error estándar](assets/error-message-standard.png)

Para responder a los errores, AEM proporciona una secuencia de comandos `404.jsp` en `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Debido a que AEM se basa en Apache Sling, hay más información disponible [en la documentación de gestión de errores de Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>En una instancia de autor, [el filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está habilitado de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está **siempre** deshabilitado (aunque esté configurado como habilitado).

## Cómo personalizar páginas mostradas por el controlador de errores {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se encuentra un error. Para ello, aprovechará [AEM mecanismo de superposición estándar](/help/implementing/developing/introduction/overlays.md) para que las páginas personalizadas se creen en `/apps` y superpongan las páginas predeterminadas que se encuentran en `/libs`.

1. En el repositorio, copie las secuencias de comandos predeterminadas:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   La ruta de destino no existe de forma predeterminada, por lo que deberá crearla al hacerlo por primera vez.

1. Ir a `/apps/sling/servlet/errorhandler`. Aquí puede:

   * edite la secuencia de comandos existente adecuada para proporcionar la información requerida. O bien
   * cree y edite una nueva secuencia de comandos para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>La secuencia de comandos `404.jsp` se ha diseñado específicamente para adaptarse a AEM autenticación; en particular, permitir el inicio de sesión del sistema en caso de estos errores.
>
>Por lo tanto, el reemplazo de este script debe realizarse con bueno cuidado.

### Personalización de la respuesta a los errores HTTP 500 {#customizing-the-response-to-http-errors}

El error interno del servidor HTTP [500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un error en el servidor, como el servidor que encuentra una condición inesperada que le impidió cumplir la solicitud.

Cuando el procesamiento de solicitudes resulta en una excepción, el marco de trabajo Apache Sling (en el que AEM está integrado):

* Registra la excepción
* Y regresa en el cuerpo de la respuesta:
   * Código de respuesta HTTP 500
   * Seguimiento de pila de excepciones

Al [personalizar las páginas que muestra el controlador de errores](#how-to-customize-pages-shown-by-the-error-handler) se puede crear una secuencia de comandos `500.jsp`. Sin embargo, sólo se utiliza si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un captador de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero la secuencia de comandos `500.jsp` no se ejecuta.

Para gestionar errores 500, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para gestionar todas estas excepciones, puede crear una secuencia de comandos `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>En una instancia de autor, [el filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está habilitado de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de errores personalizado, se necesitan respuestas con código 500, por lo que el [filtro de depuración de CQ WCM debe deshabilitarse.](/help/implementing/deploying/configuring-osgi.md) Esto garantiza que se devuelve el código de respuesta 500, que a su vez activa el controlador de error Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está **siempre** deshabilitado (aunque esté configurado como habilitado).
