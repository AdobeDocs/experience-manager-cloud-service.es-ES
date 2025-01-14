---
title: Componente de página SPA
description: En un recurso, el componente de página no proporciona los elementos HTML SPA de sus componentes secundarios, sino que los delega en el SPA de trabajo de la página de trabajo. SPA En este documento se explica cómo hace que el componente de página de una página sea único en un sitio de trabajo de la.
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
feature: Developing
role: Admin, Architect, Developer
source-git-commit: e06766160009eaa1bbc41bbf7cfad967a5195e71
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 7%

---

# Componente de página SPA {#spa-page-component}

SPA El componente de página para una no proporciona los elementos HTML de sus componentes secundarios a través de un archivo JSP o HTL y objetos de recurso. Esta operación se delega al marco de trabajo de las SPA. La representación de los componentes secundarios se obtiene como una estructura de datos JSON (es decir, el modelo ). SPA A continuación, se añaden los componentes de la a la página según el modelo JSON proporcionado. Como tal, la composición inicial del cuerpo del componente de página difiere de sus homólogos HTML procesados previamente.

{{ue-over-spa}}

## Administración de modelos de página {#page-model-management}

La resolución y la administración del modelo de página se delegan a un módulo [`PageModelManager`](blueprint.md#pagemodelmanager) proporcionado. SPA El módulo debe interactuar con el módulo `PageModelManager` cuando se inicialice para recuperar el modelo de página inicial y registrarse para obtener actualizaciones de modelo, que se producen principalmente cuando el autor está editando la página a través del Editor de páginas. SPA El proyecto `PageModelManager` es accesible para el usuario como paquete npm de la aplicación de seguridad de datos (npm). AEM SPA SPA Al ser un intérprete entre la y la de los usuarios, el `PageModelManager` debe acompañar a los usuarios de la red de servicios de traducción de la zona de trabajo de la.

SPA Para permitir la creación de la página, se debe agregar una biblioteca de cliente llamada `cq.authoring.pagemodel.messaging` para proporcionar un canal de comunicación entre el editor de páginas y el editor de páginas. SPA Si el componente de página de la página de la hereda del componente wcm/core de la página, existen las siguientes opciones para que la categoría de biblioteca de cliente `cq.authoring.pagemodel.messaging` esté disponible:

* Si la plantilla es editable, agregue la categoría de biblioteca de cliente a la directiva de página.
* Agregue la categoría de biblioteca de cliente mediante el `customfooterlibs.html` del componente de página.

No olvide limitar la inclusión de la categoría `cq.authoring.pagemodel.messaging` al contexto del editor de páginas.

## Tipo de datos de comunicación {#communication-data-type}

El tipo de datos de comunicación se establece como un elemento de HTML AEM dentro del componente Página de la con el atributo `data-cq-datatype`. Cuando el tipo de datos de comunicación está establecido en JSON, las solicitudes de GET llegan a los extremos del modelo Sling de un componente. Una vez que se produce una actualización de estado en el editor de páginas, la representación JSON del componente actualizado se envía a la biblioteca del Modelo de página. SPA A continuación, la biblioteca de modelo de página advierte a los usuarios de las actualizaciones que se han realizado en su.

SPA **Componente de página de -`body.html`**

```
<div id="page"></div>
```

SPA Además de ser una buena práctica para no retrasar la generación de DOM, el marco de trabajo de la requiere que se añadan los scripts al final del cuerpo.

SPA **Componente de página de -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

SPA Las propiedades del recurso meta que describen el contenido de la:

SPA **Componente de página de -`customheaderlibs.html`**

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
>El selector de modelo predeterminado se establece de forma estática al solicitar la representación del modelo Sling de un componente.

## Metapropiedades {#meta-properties}

* `cq:wcmmode`: modo WCM de los editores (por ejemplo, página, plantilla)
* `cq:pagemodel_root_url`: URL del modelo raíz de la aplicación. Crucial al acceder directamente a una página secundaria, ya que el modelo de página secundaria es un fragmento del modelo raíz de la aplicación. A continuación, `PageModelManager` recompone sistemáticamente el modelo inicial de aplicación como si entrara en la aplicación desde su punto de entrada raíz.
* `cq:pagemodel_router`: habilitar o deshabilitar [`ModelRouter`](routing.md) de la biblioteca `PageModelManager`
* `cq:pagemodel_route_filters`: lista separada por comas o expresiones regulares para proporcionar rutas que [`ModelRouter`](routing.md) debe ignorar.

## Sincronización de superposición del editor de páginas {#page-editor-overlay-synchronization}

La sincronización de las superposiciones está garantizada por el mismo Observador de mutaciones proporcionado por la categoría `cq.authoring.page`.

## Configuración de la estructura exportada de JSON del modelo Sling {#sling-model-json-exported-structure-configuration}

SPA AEM Cuando las capacidades de enrutamiento están habilitadas, se supone que la exportación JSON de la aplicación contiene las diferentes rutas de la aplicación gracias a la exportación JSON del componente de navegación de la. AEM SPA La salida JSON del componente de navegación de la se puede configurar en la directiva de contenido de la página raíz de la página a través de las dos propiedades siguientes:

* `structureDepth`: número correspondiente a la profundidad del árbol exportado
* `structurePatterns`: regex de una matriz de expresiones regulares correspondientes a la página que se va a exportar
