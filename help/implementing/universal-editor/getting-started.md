---
title: Introducción al editor universal en AEM
description: Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: c4dcb1cecb756f746ecb856fcfd65d73833a5ee0
workflow-type: ht
source-wordcount: '979'
ht-degree: 100%

---


# Introducción al editor universal en AEM {#getting-started}

Obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.

>[!TIP]
>
>Si prefiere ir directamente a un ejemplo, puede revisar la [Aplicación de muestra del editor universal en GitHub](https://github.com/adobe/universal-editor-sample-editable-app).

Aunque el editor universal puede editar contenido desde cualquier fuente, este documento utilizará una aplicación de AEM como ejemplo. Este documento le guiará a través de estos pasos.

## Instrumentación de la página {#instrument-page}

El editor universal requiere una biblioteca JavaScript para procesar y editar la página en el editor.

Además, el servicio del editor universal requiere un [nombre de recurso uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) para identificar y utilizar el sistema back-end correcto para el contenido de la aplicación que se edita. Por lo tanto, se requiere un esquema URN para volver a asignar contenido a los recursos de contenido.

### Inclusión de la biblioteca CORS del editor universal {#cors-library}

Para que el editor universal se conecte a su aplicación, esta debe incluir la biblioteca CORS del editor universal. Añada el siguiente script a su aplicación.

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### Creación de conexiones {#connections}

Las conexiones que se utilizan en la aplicación se almacenan como etiquetas `<meta>` en la `<head>` de la página.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>`: esta es una clasificación de la conexión con dos opciones.
   * `system`: para puntos finales de conexión
   * `config`: para [definir la configuración opcional](#configuration-settings)
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

Puede usar el prefijo `config` en el URN de conexión para establecer los puntos finales de servicio y extensión si es necesario.

Si no desea utilizar el servicio de editor universal, que aloja Adobe, sino su propia versión alojada, puede establecerlo en una metaetiqueta. Para sobrescribir el punto final de servicio predeterminado que proporciona el editor universal, establezca el suyo propio:

* Metanombre: `urn:adobe:aue:config:service`
* Metacontenido: `content="https://adobe.com"` (ejemplo)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Si solo desea tener ciertas extensiones habilitadas para una página, puede establecerlas en una metaetiqueta. Para recuperar extensiones, establezca los puntos finales de la extensión:

* Metanombre: `urn:adobe:aue:config:extensions`
* Metacontenido: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (ejemplo)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Defina para qué rutas de contenido o `sling:resourceType` se debe abrir el editor universal. (Opcional) {#content-paths}

Si tiene un proyecto de AEM existente que usa [el editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), cuando los autores de contenido editan las páginas, estas se abren de forma automática con el editor de páginas. Puede definir qué editor debe abrir AEM en función de las rutas de contenido o `sling:resourceType`, para que la experiencia sea perfecta para los autores, con independencia del editor que se requiera para el contenido seleccionado.

1. Abra el administrador de configuración. 

   `http://<host>:<port>/system/console/configMgr`

1. Busque **Servicio de URL del editor universal** en la lista y haga clic en **Editar los valores de configuración**.

1. Defina para qué rutas de contenido o `sling:resourceType` se debe abrir el editor universal.

   * En el campo **Asignación de apertura del editor universal**, proporcione las rutas para las que se abre el editor universal.
   * En el campo **Sling:resourceTypes, que abrirá el editor universal**, indique una lista de recursos que el editor universal abrirá directamente.

1. Haga clic en **Guardar**.

1. Compruebe la [configuración de su externalizador](/help/implementing/developing/tools/externalizer.md) y asegúrese de que dispone al menos de los entornos local, de autor y de publicación establecidos como en el ejemplo siguiente.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una vez completados estos pasos de configuración, AEM abrirá el editor universal para las páginas en el siguiente orden.

1. AEM comprobará las asignaciones de `Universal Editor Opening Mapping` y, si el contenido se encuentra en alguna de las rutas definidas, se abrirá para él el editor universal.
1. Para el contenido que no se encuentra en las rutas definidas en `Universal Editor Opening Mapping`, AEM comprueba si el `resourceType` del contenido coincide con los definidos en **Sling:resourceTypes, que abrirá el editor universal**. Si el contenido coincide con uno de esos tipos, el editor universal se abre para él en `${author}${path}.html`.
1. De lo contrario, AEM abre el editor de páginas.

Las siguientes variables están disponibles para definir las asignaciones en el campo **Asignación de apertura del editor universal**.

* `path`: ruta de contenido del recurso que se va a abrir
* `localhost`: entrada del externalizador para `localhost` sin esquema, p. ej., `localhost:4502`
* `author`: entrada del externalizador para el autor sin esquema, p. ej., `localhost:4502`
* `publish`: entrada del externalizador para la publicación sin esquema, p. ej., `localhost:4503`
* `preview`: entrada del externalizador para la vista previa sin esquema, p. ej., `localhost:4504`
* `env`: `prod`, `stage`, `dev` según los modos de ejecución de Sling definidos
* `token`: token de consulta necesario para `QueryTokenAuthenticationHandler`

### Asignaciones de ejemplo {#example-mappings}

* Abra todas las páginas de `/content/foo` en AEM Author:

   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Esto da como resultado la apertura de `https://localhost:4502/content/foo/x.html?login-token=<token>`

* Abra todas las páginas de `/content/bar` en un servidor NextJS remoto y proporcione todas las variables como información:

   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Esto da como resultado la apertura de `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

## Todo listo para usar el editor Universal {#youre-ready}

La aplicación ya está instrumentada para utilizar el editor universal.

Diríjase a[Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) para descubrir lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.

{{ue-headless-auth}}

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](/help/implementing/universal-editor/publishing.md): descubra cómo el editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.

