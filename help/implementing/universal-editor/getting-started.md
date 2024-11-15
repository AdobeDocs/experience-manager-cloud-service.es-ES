---
title: Introducción al editor universal en AEM
description: Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 72%

---


# Introducción al editor universal en AEM {#getting-started}

Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.

>[!TIP]
>
>Si prefiere ir directamente a un ejemplo, puede revisar la [Aplicación de muestra del editor universal en GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

AEM Aunque el editor universal puede editar contenido desde cualquier fuente, este documento utiliza una aplicación de la aplicación de la como ejemplo. Este documento le guiará a través de estos pasos.

## Instrumentación de la página {#instrument-page}

El servicio de editor universal requiere un [nombre de recurso uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) para identificar y utilizar el sistema back-end correcto para el contenido de la aplicación que se está editando. Por lo tanto, se requiere un esquema URN para volver a asignar contenido a los recursos de contenido.

### Creación de conexiones {#connections}

Las conexiones que se utilizan en la aplicación se almacenan como etiquetas `<meta>` en la `<head>` de la página.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>`: esta es una clasificación de la conexión con dos opciones.
   * `system` - Para extremos de conexión
   * `config` - Para [definir la configuración opcional](#configuration-settings)
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
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Opciones de configuración {#configuration-settings}

Puede usar el prefijo `config` en el URN de conexión para establecer los extremos de servicio y extensión si es necesario.

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

Diríjase a[Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) para descubrir lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/publishing.md): aprenda cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.

