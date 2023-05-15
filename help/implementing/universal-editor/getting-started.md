---
title: Introducción al editor universal en AEM
description: Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
source-git-commit: e62ddc2a72d12ad356decc0e2a933d8c7d308469
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 98%

---

# Introducción al editor universal en AEM {#getting-started}

Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.

>[!TIP]
>
>Si prefiere ir directamente a un ejemplo, puede revisar la [Aplicación de muestra del editor universal en GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

## Pasos para la incorporación {#onboarding}

Aunque el editor universal puede editar contenido desde cualquier fuente, este documento utilizará una aplicación AEM como ejemplo.

Hay varios pasos para incorporar la aplicación de AEM e instrumentarla para utilizar el editor universal.

1. [Solicite acceso al editor universal.](#request-access)
1. [Incluya la biblioteca principal del editor universal.](#core-library)
1. [Añada la configuración OSGi necesaria.](#osgi-configurations)
1. [Instrumente la página.](#instrument-page)

Este documento le guiará a través de estos pasos.

## Solicite acceso al editor universal {#request-access}

Primero debe solicitar acceso al editor universal. Vaya a [https://experience.adobe.com/#/aem/editor](https://experience.adobe.com/#/aem/editor), inicie sesión y valide si tiene acceso al Editor universal.

En caso de que no tenga acceso, puede solicitarlo a través de un formulario vinculado en la misma página.

![Solicite acceso al editor universal](assets/request-access.png)

Haga clic en **Solicitud de acceso** y rellene el formulario como se le indica para solicitarlo. Un representante del Adobe revisará su solicitud y se pondrá en contacto para analizar su caso práctico.

## Incluya la biblioteca principal del editor universal {#core-library}

Para que la aplicación se pueda instrumentar para su uso con el editor universal, debe incluir la siguiente dependencia.

```javascript
@adobe/universal-editor-cors
```

Para activar la instrumentación, debe agregarse la siguiente importación a su `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativa para aplicaciones que no sean React {#alternative}

Si no va a implementar una aplicación React o requiere procesamiento del lado del servidor, un método alternativo es incluir lo siguiente en el cuerpo del documento.

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## Añada las configuraciones de OSGi necesarias {#osgi-configurations}

Para poder editar contenido en su aplicación con el editor universal en AEM, es necesario realizar la configuración de cookies y CORS.

Deberá establecer las siguientes [configuraciones de OSGi en la instancia de creación de AEM.](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` en `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* Elimine el encabezado X-FRAME-OPTIONS: SAMEORIGIN en`org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

La cookie del token de inicio de sesión debe enviarse a AEM como un dominio de terceros. Por lo tanto, la cookie del mismo sitio deberá configurarse explícitamente como `None`.

Esta propiedad debe establecerse en la configuración de OSGi `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options: SAMEORIGIN evita el procesamiento de páginas AEM dentro del iframe. Al eliminar el encabezado, se pueden cargar las páginas.

Esta propiedad debe establecerse en la configuración de OSGi `org.apache.sling.engine.impl.SlingMainServlet`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## Instrumentación de la página {#instrument-page}

El servicio de editor universal requiere un [nombre de recurso uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) para identificar y utilizar el sistema back-end correcto para el contenido de la aplicación que se está editando. Por lo tanto, se requiere un esquema URN para volver a asignar contenido a los recursos de contenido.

Los atributos de instrumentación agregados a la página constan principalmente de [microdatos del HTML,](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) un estándar del sector que también puede utilizarse para hacer que el HTML sea más semántico, que los documentos HTML sean indizables, etc.

### Creación de conexiones {#connections}

Las conexiones que se utilizan en la aplicación se almacenan como etiquetas `<meta>` en la `<head>` de la página.

```html
<meta name="urn:adobe:aem:editor:aemconnection:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>`: se trata de un nombre corto que se reutiliza en el documento para identificar la conexión. P. ej., `aemconnection`
* `<protocol>`: indica qué complemento de persistencia utilizar del servicio de persistencia del editor universal. P. ej., `aem`
* `<url>`: esta es la URL del sistema en la que deben persistir los cambios. P. ej., `http://localhost:4502`

El identificador `adobe:aem:editor:aemconnection` representa la conexión para el Editor universal de Adobe.

`itemid` utilizará el prefijo `urn` para abreviar el identificador.

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>`: esta es la referencia mencionada en la etiqueta `<meta>`. P. ej., `aemconnection`
* `<resource>`: es un puntero al recurso en el sistema de destino. P. ej., una ruta de contenido AEM como `/content/page/jcr:content`

>[!TIP]
>
>Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los atributos y tipos de datos que requiere el editor universal.

### Conexión de ejemplo {#example}

```html
<html>
<head>
    <meta name="urn:adobe:aem:editor:aemconnection:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aem:editor:aemconnection:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

## Todo listo para usar el editor Universal {#youre-ready}

La aplicación ya está instrumentada para utilizar el editor universal.

Consulte el documento [Creación de contenido con el editor universal](authoring.md) para aprender lo fácil e intuitivo que es para los autores de contenido crear contenido con el editor universal.

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el editor universal.
* [Publicación de contenido con el editor universal](publishing.md): descubra cómo el editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Arquitectura de editor universal](architecture.md): obtenga información sobre la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.
