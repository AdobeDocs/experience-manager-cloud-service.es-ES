---
title: Componente de página de SPA
description: En un SPA, el componente de página no proporciona los elementos HTML de sus componentes secundarios, sino que los delega en el marco de SPA. Este documento explica cómo esto hace que el componente de página de un SPA sea único.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Componente de página de SPA {#spa-page-component}

El componente de página de un SPA no proporciona los elementos HTML de sus componentes secundarios mediante un archivo JSP o HTL y objetos de recursos. Esta operación se delega en el marco de la EPA. La representación de componentes secundarios se obtiene como una estructura de datos JSON (es decir, el modelo). A continuación, los componentes de SPA se agregan a la página según el modelo JSON proporcionado. Por lo tanto, la composición del cuerpo inicial del componente de página difiere de sus homólogos HTML procesados previamente.

## Administración de modelos de página {#page-model-management}

La resolución y la administración del modelo de página se delegan en un [`PageModelManager`](blueprint.md#pagemodelmanager) módulo proporcionado. El SPA debe interactuar con el `PageModelManager` módulo cuando se inicializa para recuperar el modelo de página inicial y registrarse para actualizaciones de modelo, que se producen principalmente cuando el autor edita la página a través del Editor de páginas. El proyecto SPA `PageModelManager` es accesible como paquete npm. Como intérprete entre AEM y la SPA, el objetivo `PageModelManager` es acompañar a la SPA.

Para permitir la creación de la página, se debe agregar una biblioteca de cliente denominada `cq.authoring.pagemodel.messaging` para proporcionar un canal de comunicación entre la SPA y el editor de páginas. Si el componente de página SPA hereda del componente de página wcm/core de la página, hay las siguientes opciones para que la categoría de biblioteca del `cq.authoring.pagemodel.messaging` cliente esté disponible:

* Si la plantilla es editable, agregue la categoría de biblioteca de cliente a la directiva de página.
* Añada la categoría de la biblioteca del cliente mediante el uso `customfooterlibs.html` del componente de página.

No olvide limitar la inclusión de la `cq.authoring.pagemodel.messaging` categoría al contexto del editor de páginas.

## Tipo de datos de comunicación {#communication-data-type}

El tipo de datos de comunicación se define como un elemento HTML dentro del componente Página de AEM mediante el `data-cq-datatype` atributo . Cuando el tipo de datos de comunicación se establece en JSON, las solicitudes de GET llegan a los extremos del modelo de Sling de un componente. Una vez que se produce una actualización en el editor de páginas, la representación JSON del componente actualizado se envía a la biblioteca del modelo de páginas. A continuación, la biblioteca del modelo de página advierte al SPA de las actualizaciones.

**Componente de página SPA -`body.html`**

```
<div id="page"></div>
```

Además de ser una buena práctica para no retrasar la generación del DOM, el marco de SPA requiere que los scripts se agreguen al final del cuerpo.

**Componente de página SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Las propiedades del recurso meta que describen el contenido de SPA:

**Componente de página SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>El selector de modelo predeterminado se establece de forma estática al solicitar la representación del modelo de Sling de un componente.

## Metapropiedades {#meta-properties}

* `cq:wcmmode`:: Modo WCM de los editores (p. ej. página, plantilla)
* `cq:pagemodel_root_url`:: Dirección URL del modelo raíz de la aplicación. Es fundamental cuando se accede directamente a una página secundaria, ya que el modelo de página secundaria es un fragmento del modelo raíz de la aplicación. A continuación, el `PageModelManager` modelo inicial de la aplicación se recompone sistemáticamente al entrar en la aplicación desde su punto de entrada raíz.
* `cq:pagemodel_router`:: Habilitar o deshabilitar el [`ModelRouter`](routing.md) de la `PageModelManager` biblioteca
* `cq:pagemodel_route_filters`:: Lista separada por comas o expresiones regulares para proporcionar rutas que [`ModelRouter`](routing.md) deben ignorarse.

## Sincronización de superposiciones del editor de páginas {#page-editor-overlay-synchronization}

La sincronización de las superposiciones está garantizada por el mismo Observador de Mutación proporcionado por la `cq.authoring.page` categoría.

## Configuración de la estructura exportada de JSON del modelo Sling {#sling-model-json-exported-structure-configuration}

Cuando las funciones de enrutamiento están habilitadas, se supone que la exportación JSON del SPA contiene las distintas rutas de la aplicación gracias a la exportación JSON del componente de navegación AEM. La salida JSON del componente de navegación AEM se puede configurar en la directiva de contenido de página raíz del SPA mediante las dos propiedades siguientes:

* `structureDepth`:: Número correspondiente a la profundidad del árbol exportado
* `structurePatterns`:: Resto de la matriz de anexos correspondientes a la página que se va a exportar
