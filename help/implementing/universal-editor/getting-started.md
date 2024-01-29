---
title: Introducción al editor universal en AEM
description: Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
source-git-commit: 453cbaeabd28223cac5e732a551aa71f5a425839
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 71%

---


# Introducción al editor universal en AEM {#getting-started}

Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.

>[!TIP]
>
>Si prefiere ir directamente a un ejemplo, puede revisar la [Aplicación de muestra del editor universal en GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

{{universal-editor-status}}

## Pasos para la incorporación {#onboarding}

Aunque el editor universal puede editar contenido desde cualquier fuente, este documento utilizará una aplicación AEM como ejemplo.

AEM Hay que seguir varios pasos para incorporar la aplicación de e instrumentarla para que utilice el editor universal.

1. [Solicite acceso al editor universal.](#request-access)
1. [Incluya la biblioteca principal del editor universal.](#core-library)
1. [Añada la configuración OSGi necesaria.](#osgi-configurations)
1. [Instrumente la página.](#instrument-page)

Este documento le guiará a través de estos pasos.

## Solicite acceso al editor universal {#request-access}

Primero debe solicitar acceso al editor universal. Abrir [`https://experience.adobe.com/#/aem/editor&quot;](https://experience.adobe.com/#/aem/editor), inicie sesión y valide si tiene acceso al editor universal.

En caso de que no tenga acceso, puede solicitarlo a través de un formulario vinculado en la misma página.

![Solicite acceso al editor universal](assets/request-access.png)

Haga clic en **Solicitud de acceso** y rellene el formulario como se le indica para solicitarlo. Un representante del Adobe revisará su solicitud y se pondrá en contacto para analizar su caso práctico.

## Incluya la biblioteca principal del editor universal {#core-library}

Para poder instrumentar la aplicación para su uso con el editor universal, debe incluir la siguiente dependencia.

```javascript
@adobe/universal-editor-cors
```

Para activar la instrumentación, se debe añadir la siguiente importación a su `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativa para aplicaciones que no sean React {#alternative}

Si no va a implementar una aplicación React o requiere un procesamiento del lado del servidor, otro método consiste en incluir lo siguiente en el cuerpo del documento.

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

Los atributos de instrumentación añadidos a la página constan principalmente de [Microdatos de HTML,](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) un estándar del sector que también se puede utilizar para hacer que HTML sea más semántico, para hacer que los documentos de HTML sean indexables, etc.

### Creación de conexiones {#connections}

Las conexiones que se utilizan en la aplicación se almacenan como etiquetas `<meta>` en la `<head>` de la página.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - Esta es una clasificación de la conexión con dos opciones.
   * `system` - Para extremos de conexión
   * `config` - Para [definir opciones de configuración opcionales](#configuration-settings)
* `<referenceName>`: se trata de un nombre corto que se reutiliza en el documento para identificar la conexión. P. ej., `aemconnection`
* `<protocol>`: indica qué complemento de persistencia utilizar del servicio de persistencia del editor universal. P. ej., `aem`
* `<url>`: esta es la URL del sistema en la que deben persistir los cambios. P. ej., `http://localhost:4502`

El identificador `urn:adobe:aue:system` representa la conexión para el Editor universal de Adobe.

`data-aue-resource` utilizará el prefijo `urn` para abreviar el identificador.

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>`: esta es la referencia mencionada en la etiqueta `<meta>`. P. ej., `aemconnection`
* `<resource>`: es un puntero al recurso en el sistema de destino. P. ej., una ruta de contenido AEM como `/content/page/jcr:content`

>[!TIP]
>
>Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los atributos y tipos de datos que requiere el editor universal.

### Conexión de ejemplo {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Opciones de configuración {#configuration-settings}

Puede usar el complemento `config` en el URN de la conexión para establecer los extremos de servicio y extensión si es necesario.

Si no desea utilizar el servicio de editor universal, que se aloja mediante Adobe, sino su propia versión alojada, puede establecerlo en una metaetiqueta. Para sobrescribir el extremo de servicio predeterminado que proporciona el Editor universal, establezca su propio extremo de servicio:

* Meta name - `urn:adobe:aue:config:service`
* Meta content - `content="https://adobe.com"` (ejemplo)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Si solo desea tener ciertas extensiones habilitadas para una página, puede establecerlas en una metaetiqueta. Para recuperar extensiones, establezca los extremos de la extensión:

* Meta name: `urn:adobe:aue:config:extensions`
* Meta content: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (ejemplo)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Todo listo para usar el editor Universal {#youre-ready}

La aplicación ya está instrumentada para utilizar el editor universal.

Diríjase a[Creación de contenido con el editor universal](authoring.md) para descubrir lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](publishing.md) - Descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.
