---
title: Introducción a SPA en AEM con React
description: Este artículo presenta una aplicación de SPA de ejemplo, explica cómo se crea y le permite ponerse en marcha con sus propios SPA rápidamente utilizando el marco React.
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 1%

---

# Introducción a SPA en AEM con React {#getting-started-with-spas-in-aem-using-react}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado mediante marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA dentro de AEM. Este artículo presenta una aplicación de SPA simplificada en el marco de React, explica cómo se integra, lo que le permite ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para ver el documento correspondiente del marco de Angular, consulte [Introducción a SPA en AEM - Angular](getting-started-angular.md).

## Introducción {#introduction}

Este artículo resume el funcionamiento básico de un simple SPA y el mínimo que necesita saber para que el suyo funcione.

Para obtener más información sobre cómo funciona SPA en AEM, consulte los siguientes documentos:

* [Introducción y tutorial de SPA](introduction.md)
* [Información general del Editor de SPA](editor-overview.md)
* [Modelo SPA](blueprint.md)

>[!NOTE]
>
>Para poder crear contenido dentro de un SPA, el contenido debe almacenarse en AEM y ser expuesto por el modelo de contenido.
>
>Una SPA desarrollada fuera de AEM no será autorizada si no respeta el contrato del modelo de contenido.

Este documento recorrerá la estructura de un SPA simplificado creado con el marco React e ilustrará cómo funciona para que pueda aplicar este entendimiento a su propia SPA.

## Dependencias, configuración y creación {#dependencies-configuration-and-building}

Además de la dependencia esperada de React, el SPA de muestra puede aprovechar bibliotecas adicionales para hacer que la creación del SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete de SPA general. Las dependencias de AEM mínimas para un SPA en funcionamiento se enumeran aquí.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Dado que este ejemplo se basa en el marco de React, hay dos dependencias específicas de React que son obligatorias en el archivo `package.json`:

```
 react
 react-dom
```

El `aem-clientlib-generator` se aprovecha para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Puede encontrar más detalles sobre esto [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

El `aem-clientlib-generator` se configura en el archivo `clientlib.config.js` de la siguiente manera.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Compilando {#building}

La creación de la aplicación aprovecha el [Webpack](https://webpack.js.org/) para la transpilación, además del aem-clientlib-generator para la creación automática de la biblioteca del cliente. Por lo tanto, el comando build se parecerá a:

`"build": "webpack && clientlib --verbose"`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos con React o Angular y aprovecha el SDK de SPA.

## Estructura de la aplicación {#application-structure}

Al incluir las dependencias y crear la aplicación tal como se describió anteriormente, dispondrá de un paquete de SPA de trabajo que puede cargar en la instancia de AEM.

La siguiente sección de este documento le explica cómo se estructura un SPA en AEM, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Se utiliza un componente de imagen simplificado como ejemplo, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

El punto de entrada a la SPA es, por supuesto, el archivo `index.js` que se muestra aquí simplificado para centrarse en el contenido importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La función principal de `index.js` es aprovechar la función `ReactDOM.render` para determinar dónde en el DOM se inyecta la aplicación.

Se trata de un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Creación de instancias estáticas {#static-instantiation}

Cuando se crea una instancia del componente estáticamente utilizando la plantilla de componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

### App.js {#app-js}

Al procesar la aplicación, `index.js` llama a `App.js`, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` principalmente sirve para envolver los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, `App.js` llama a `Page.js` enumeradas aquí en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la clase `AppPage` amplía `Page`, que contiene los métodos de contenido interno que se pueden utilizar.

El `Page` ingesta la representación JSON del modelo de página y procesa el contenido para ajustar/decorar cada elemento de la página. Puede encontrar más información sobre el `Page` en el documento [SPA modelo.](blueprint.md)

### Image.js {#image-js}

Con la página representada, se pueden procesar los componentes como `Image.js` como se muestra aquí.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

La idea central de SPA en AEM es la idea de asignar componentes SPA a AEM componentes y actualizar el componente cuando se modifica el contenido (y viceversa). Consulte el documento [SPA Editor Overview](editor-overview.md) para ver un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente SPA al componente AEM. Admite el uso de una sola cadena o una matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

## Exportación de contenido editable {#exporting-editable-content}

Puede exportar un componente y mantenerlo editable.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La función `MapTo` devuelve un `Component` que es el resultado de una composición que amplía el `PageClass` proporcionado con los nombres de clase y atributos que habilitan la creación. Este componente se puede exportar a y posteriormente se puede crear una instancia en el marcado de la aplicación.

Cuando se exporta utilizando las funciones `MapTo` o `withModel` , el componente `Page` se ajusta con un componente `ModelProvider` que proporciona acceso a los componentes estándar a la última versión del modelo de página o a una ubicación precisa en ese modelo de página.

Para obtener más información, consulte el [SPA documento del modelo](blueprint.md).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente al utilizar la función `withModel`.

## Uso compartido de información entre componentes SPA {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Hay varias formas recomendadas de hacerlo, enumeradas a continuación en orden creciente de complejidad.

* **Opción 1:** centralice la lógica y la emisión a los componentes necesarios, por ejemplo, utilizando Contexto de Reacción.
* **Opción 2:** Compartir estados de componentes utilizando una biblioteca de estados como Redux.
* **Opción 3:** aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Pasos siguientes {#next-steps}

* [Introducción a SPA en AEM con ](getting-started-angular.md) Angularis muestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM con Angular.
* [SPA ](editor-overview.md) Información general del editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [WKND SPA ](wknd-tutorial.md) Project es un tutorial paso a paso que implementa un proyecto de SPA simple en AEM.
* [Asignación de modelos dinámicos a componentes para ](model-to-component-mapping.md) SPAs explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de SPA en AEM.
* [SPA ](blueprint.md) Blueprintoofrece una explicación detallada sobre cómo funciona el SDK de SPA para AEM en caso de que desee implementar SPA en AEM para un marco que no sea React o Angular, o simplemente desee un entendimiento más profundo.
