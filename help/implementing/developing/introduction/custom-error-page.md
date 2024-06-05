---
title: Páginas de error personalizadas
description: AEM viene con un controlador de error estándar para administrar errores HTTP, que se puede personalizar.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Personalización de páginas de error {#customizing-error-pages}

AEM viene con un controlador de error estándar para la administración de errores HTTP; por ejemplo, mostrando:

![Mensaje de error estándar](assets/error-message-standard.png)

AEM Para responder a los errores, proporciona un valor de tipo `404.jsp` script en `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>AEM Debido a que se basa en Apache Sling, hay disponible más información [en la documentación de gestión de errores de Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es **siempre** desactivado (incluso si está configurado como activado).

## Personalizar páginas mostradas por el controlador de error {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se produce un error. Para ello, utilice [AEM mecanismo de superposición estándar de la](/help/implementing/developing/introduction/overlays.md) para que las páginas personalizadas se creen en `/apps` y superponer las páginas predeterminadas que se encuentran en `/libs`.

1. En el repositorio, copie los scripts predeterminados:

   * de `/libs/sling/servlet/errorhandler/`
   * hasta `/apps/sling/servlet/errorhandler/`

   La ruta de destino no existe de forma predeterminada, por lo que debe crearla al hacerlo por primera vez.

1. Navegue hasta `/apps/sling/servlet/errorhandler`. Aquí puede hacer lo siguiente:

   * edite la secuencia de comandos existente adecuada para proporcionar la información necesaria. O bien
   * cree y edite un nuevo script para el código requerido.

1. Guarde los cambios y pruebe.

>[!CAUTION]
>
>El `404.jsp` AEM La secuencia de comandos se ha diseñado específicamente para permitir la autenticación de los usuarios; en particular, para permitir el inicio de sesión en el sistema en caso de errores.
>
>Por lo tanto, la sustitución de esta secuencia de comandos debe realizarse con mucho cuidado.

### Personalización de la Respuesta a Errores HTTP 500 {#customizing-the-response-to-http-errors}

El HTTP [500 Error interno del servidor](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un error del lado del servidor como que el servidor encontró una condición inesperada que le impidió cumplir la solicitud.

AEM Cuando el procesamiento de solicitudes resulta en una excepción, el marco de trabajo de Apache Sling (en el que se basa el procesamiento de la):

* Registra la excepción
* Y vuelve en el cuerpo de la respuesta:
   * El código de respuesta HTTP 500
   * El seguimiento de pila de excepciones

Por [personalización de las páginas mostradas por el controlador de error](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` se puede crear el script. Sin embargo, solo se utiliza si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un receptor de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero la variable `500.jsp` no se ejecuta el script.

Para controlar 500 errores, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para gestionar todas estas excepciones, puede crear un script `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>AEM En calidad de Cloud Service, la red de distribución de contenido (CDN) proporciona una página de error genérica cuando se recibe un error de 5XX desde el servidor. Para permitir que la respuesta real del backend pase, debe agregar el siguiente encabezado a la respuesta: `x-aem-error-pass: true`.
>AEM Esto solo funciona para respuestas procedentes de la capa de o de Apache/Dispatcher. Otros errores inesperados procedentes de capas de infraestructura intermedias seguirán mostrando la página de error genérica.

>[!CAUTION]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está activada de forma predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de error personalizado, se necesitan respuestas con código 500, por lo que la variable [El filtro de depuración de CQ WCM debe estar desactivado](/help/implementing/deploying/configuring-osgi.md). Esto garantiza que se devuelva el código de respuesta 500, lo que a su vez déclencheur el controlador de error de Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM es **siempre** desactivado (incluso si está configurado como activado).
