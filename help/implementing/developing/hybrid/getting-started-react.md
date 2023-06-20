---
title: Introducción a SPA en AEM usando React
description: SPA SPA Este artículo presenta una aplicación de ejemplo para la creación de informes, explica cómo se crea y le permite ponerse en marcha con su propia aplicación de forma rápida mediante el marco de trabajo React.
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 8%

---

# Introducción a SPA en AEM usando React {#getting-started-with-spas-in-aem-using-react}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. SPA SPA En este artículo se presenta una aplicación de simplificada sobre el marco de trabajo de React, que explica cómo se crea, lo que le permite ponerse en marcha con sus propios recursos de forma rápida y sin problemas para la ejecución de sus propios programas de trabajo de la aplicación de la aplicación.

>[!NOTE]
>
>Este artículo se basa en el marco de React. Para ver el documento correspondiente al marco de Angular, consulte [SPA AEM Introducción a la administración de la en Angular](getting-started-angular.md).

## Introducción {#introduction}

SPA Este artículo resume el funcionamiento básico de un sencillo y el mínimo que necesita saber para poner en marcha el suyo.

SPA AEM Para obtener más información sobre cómo funcionan los en la, consulte los siguientes documentos:

* [Introducción y tutorial de SPA](introduction.md)
* [Información general del editor de SPA](editor-overview.md)
* [Modelo SPA](blueprint.md)

>[!NOTE]
>
>SPA AEM Para poder crear contenido dentro de un elemento de contenido, el contenido debe almacenarse en el elemento de contenido y ser expuesto por el modelo de contenido de, lo que hace que el contenido se almacene en el elemento de contenido.
>
>SPA AEM Un desarrollado fuera de la aplicación de la ley no será legible si no respeta el contrato del modelo de contenido.

SPA SPA Este documento recorrerá la estructura de un documento simplificado creado con el marco de trabajo de React e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propia.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

SPA SPA Además de la dependencia de React esperada, el ejemplo puede utilizar bibliotecas adicionales para que la creación de la biblioteca de React sea más eficiente. En este ejemplo, se puede usar una biblioteca adicional para hacer que la creación de la biblioteca de React sea más eficiente.

### Dependencias {#dependencies}

El `package.json` SPA define los requisitos del paquete de trabajo global de la. AEM SPA Las dependencias mínimas de la para un grupo de trabajo se enumeran aquí.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Dado que este ejemplo se basa en el marco de React, hay dos dependencias específicas de React obligatorias en el `package.json` archivo:

```
 react
 react-dom
```

El `aem-clientlib-generator` se utiliza para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Se pueden encontrar más detalles al respecto [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

El `aem-clientlib-generator` está configurado en la `clientlib.config.js` como se indica a continuación.

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

La creación de la aplicación utiliza [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "webpack && clientlib --verbose"`

AEM Una vez creado, el paquete se puede cargar en una instancia de.

### Tipo de archivo del proyecto AEM. {#aem-project-archetype}

AEM Cualquier proyecto debe utilizar la variable [AEM Tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)SPA , que es compatible con proyectos de que utilizan React o Angular SPA y utiliza el SDK de.

## Estructura de aplicación {#application-structure}

SPA AEM Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de trabajo de la aplicación que puede cargar en su instancia de.

SPA AEM En la siguiente sección de este documento se explica cómo se estructura una en el trabajo, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### index.js {#index-js}

SPA El punto de entrada en la es, por supuesto, el `index.js` archivo que se muestra aquí simplificado para centrarse en el contenido importante.

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

La función principal de `index.js` es utilizar el `ReactDOM.render` función para determinar en qué parte del DOM insertar la aplicación.

Este es un uso estándar de esta función, no exclusivo de esta aplicación de ejemplo.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla del componente (por ejemplo, JSX), el valor debe pasarse del modelo a las propiedades del componente.

### App.js {#app-js}

Al procesar la aplicación, `index.js` llamadas `App.js`, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` sirve principalmente para envolver los componentes raíz que componen la aplicación. El punto de entrada de cualquier aplicación es la página.

### Page.js {#page-js}

Al procesar la página, `App.js` llamadas `Page.js` se enumera aquí en una versión simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

En este ejemplo, la variable `AppPage` ampliación de clase `Page`, que contiene los métodos de contenido interno que se pueden utilizar.

El `Page` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. Más información sobre la `Page` se puede encontrar en el documento [SPA Modelo de.](blueprint.md)

### Image.js {#image-js}

Con la página representada, los componentes como `Image.js` como se muestra aquí, se puede procesar.

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

SPA AEM SPA AEM La idea central de la en la práctica es la idea de asignar componentes de la a componentes de la y actualizar el componente cuando se modifica el contenido (y viceversa). Ver el documento [SPA Resumen del editor de](editor-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

El `MapTo` SPA AEM El método asigna el componente de la al componente de la. Admite el uso de una sola cadena o matriz de cadenas.

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

El `MapTo` función devuelve un valor `Component` que es el resultado de una composición que amplía el `PageClass` con los nombres de clase y atributos que habilitan la creación. Este componente se puede exportar para que se cree una instancia más adelante en el marcado de la aplicación.

Cuando se exporta mediante `MapTo` o `withModel` funciones, el `Page` componente, se ajusta con un `ModelProvider` componente que proporciona a los componentes estándar acceso a la última versión del modelo de página o a una ubicación precisa en ese modelo de página.

Para obtener más información, consulte [SPA Documento de modelo de](blueprint.md).

>[!NOTE]
>
>De forma predeterminada, recibe todo el modelo del componente al utilizar el `withModel` función.

## SPA Uso Compartido De Información Entre Componentes De La {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando el contexto de React.
* **Opción 2:** Comparta estados de componentes mediante una biblioteca de estados como Redux.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Pasos siguientes {#next-steps}

* [Introducción a SPA en AEM usando Angular](getting-started-angular.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA en AEM usando Angular.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [SPA Proyecto de WKND](wknd-tutorial.md) SPA AEM es un tutorial paso a paso sobre la implementación de un proyecto de simple en el sector de la.
* [SPA Asignación de modelos dinámicos a componentes para la creación de](model-to-component-mapping.md) SPA AEM explica el modelo dinámico para la asignación de componentes y cómo funciona dentro de la asignación de componentes de la interfaz de usuario de la aplicación de datos en la.
* [SPA Modelo de](blueprint.md) SPA AEM SPA AEM ofrece una explicación detallada de cómo funciona el SDK de la para la creación de informes en caso de que desee implementar un esquema de trabajo de forma más sencilla que no sea React o Angular, o simplemente desee tener una comprensión más profunda de la aplicación.
