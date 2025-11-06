---
title: Páginas de error personalizadas
description: AEM incluye un controlador de error estándar para administrar errores HTTP, que se puede personalizar.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Personalización de páginas de error {#customizing-error-pages}

AEM incluye un controlador de error estándar para administrar errores HTTP; por ejemplo, mostrando:

![Mensaje de error estándar](assets/error-message-standard.png)

Para responder a los errores, AEM proporciona un script `404.jsp` en `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Como AEM se basa en Apache Sling, hay más información disponible [en la documentación de gestión de errores de Apache](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html).

>[!NOTE]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está habilitado de manera predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está **siempre** deshabilitado (incluso si está configurado como habilitado).

>[!NOTE]
>
>Para obtener más información sobre la administración de errores con Dispatcher, consulte [Configuración de páginas de error de CDN](/help/implementing/dispatcher/cdn-error-pages.md).

## Personalizar páginas mostradas por el controlador de error {#how-to-customize-pages-shown-by-the-error-handler}

Puede desarrollar sus propias secuencias de comandos para personalizar las páginas que muestra el controlador de errores cuando se produce un error. Para ello, usa [el mecanismo de superposición estándar de AEM](/help/implementing/developing/introduction/overlays.md) para que las páginas personalizadas se creen en `/apps` y se superpongan las páginas predeterminadas que se encuentran en `/libs`.

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
>El script `404.jsp` se ha diseñado específicamente para permitir la autenticación de AEM; en particular, para permitir el inicio de sesión del sistema en caso de estos errores.
>
>Por lo tanto, la sustitución de esta secuencia de comandos debe realizarse con mucho cuidado.

### Personalización de la Respuesta a Errores HTTP 500 {#customizing-the-response-to-http-errors}

El error interno del servidor HTTP [500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un error del lado del servidor, como que el servidor encontró una condición inesperada que le impidió cumplir la solicitud.

Cuando el procesamiento de la solicitud resulta en una excepción, el marco de Apache Sling (en el que se basa AEM):

* Registra la excepción
* Y vuelve en el cuerpo de la respuesta:
   * El código de respuesta HTTP 500
   * El seguimiento de pila de excepciones

Si [personaliza las páginas mostradas por el controlador de error](#how-to-customize-pages-shown-by-the-error-handler), se puede crear un script `500.jsp`. Sin embargo, solo se usa si `HttpServletResponse.sendError(500)` se ejecuta explícitamente; es decir, desde un receptor de excepciones.

De lo contrario, el código de respuesta se establece en 500, pero no se ejecuta el script `500.jsp`.

Para controlar 500 errores, el nombre de archivo de la secuencia de comandos del controlador de errores debe ser el mismo que la clase de excepción (o superclase). Para controlar todas estas excepciones, puede crear un script `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>En AEM as a Cloud Service, la CDN proporciona una página de error genérica cuando se recibe un error 5XX del backend. Para permitir que pase la respuesta real del servidor, debe agregar el siguiente encabezado a la respuesta: `x-aem-error-pass: true`.
>Esto solo funciona para respuestas procedentes de AEM o de la capa Apache/Dispatcher. Otros errores inesperados procedentes de capas de infraestructura intermedias seguirán mostrando la página de error genérica.

>[!CAUTION]
>
>En una instancia de autor, [Filtro de depuración de CQ WCM](/help/implementing/deploying/configuring-osgi.md) está habilitado de manera predeterminada. Esto siempre resulta en el código de respuesta 200. El controlador de error predeterminado responde escribiendo el seguimiento de pila completo en la respuesta.
>
>Para un controlador de error personalizado, se necesitan respuestas con código 500, por lo que el filtro de depuración de [CQ WCM debe deshabilitarse](/help/implementing/deploying/configuring-osgi.md). Esto garantiza que se devuelva el código de respuesta 500, lo que a su vez déclencheur el controlador de error de Sling correcto.
>
>En una instancia de publicación, el filtro de depuración de CQ WCM está **siempre** deshabilitado (incluso si está configurado como habilitado).
