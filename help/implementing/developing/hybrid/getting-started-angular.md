---
title: SPA AEM Introducción a la administración de la en Angular
description: SPA SPA Este artículo presenta una aplicación de ejemplo para la creación de informes, explica cómo se crea y le permite ponerse en marcha con su propia aplicación de forma rápida mediante el marco de trabajo de Angular de trabajo de.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 6%

---

# SPA AEM Introducción a la administración de la en Angular {#getting-started-with-spas-in-aem-using-angular}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. SPA AEM SPA Los desarrolladores quieren poder crear sitios utilizando marcos de trabajo de y los autores quieren editar contenido sin problemas en para un sitio creado con marcos de trabajo de la.

SPA SPA AEM La función de creación de ofrece una solución completa para la asistencia de la creación de contenido en el ámbito de la. SPA En este artículo se presenta una aplicación de simplificada sobre el marco de trabajo de Angular SPA, y se explica cómo se crea, lo que le permite ponerse en marcha con sus propios rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de Angular de. SPA AEM Para ver el documento correspondiente del marco de React, consulte [Introducción a la administración de datos en la - React](getting-started-react.md).

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

SPA SPA Este documento recorrerá la estructura de un documento simplificado e ilustrará cómo funciona para que pueda aplicar esta comprensión a su propio.

## Dependencias, configuración y generación {#dependencies-configuration-and-building}

Además de la dependencia de Angular SPA SPA esperada, el ejemplo puede utilizar bibliotecas adicionales para que la creación de los recursos de ejemplo sea más eficiente. En este ejemplo, se puede usar una biblioteca de bibliotecas adicionales para hacer que la creación de los recursos sea más eficiente

### Dependencias {#dependencies}

SPA El archivo `package.json` define los requisitos del paquete general de. AEM Aquí se enumeran las dependencias mínimas requeridas de la.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator` se usa para hacer que la creación de bibliotecas de cliente sea automática como parte del proceso de compilación.

`"aem-clientlib-generator": "^1.4.1",`

Encontrará más detalles al respecto [en GitHub aquí](https://github.com/wcm-io-frontend/aem-clientlib-generator).

`aem-clientlib-generator` está configurado en el archivo `clientlib.config.js` de la siguiente manera.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

### Generación {#building}

En realidad, al crear la aplicación se usa [Webpack](https://webpack.js.org/) para la transpilación, además de aem-clientlib-generator para la creación automática de bibliotecas de cliente. Por lo tanto, el comando build será similar a:

`"build": "ng build --build-optimizer=false && clientlib",`

AEM Una vez creado, el paquete se puede cargar en una instancia de.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debería utilizar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite proyectos de SPA que utilizan React o Angular y aprovecha el SDK de SPA.

## Estructura de aplicación {#application-structure}

SPA AEM Incluir las dependencias y crear la aplicación como se describió anteriormente le dejará con un paquete de trabajo de la aplicación que puede cargar en su instancia de.

SPA AEM La siguiente sección de este documento le explicará cómo se estructura una en la, los archivos importantes que impulsan la aplicación y cómo funcionan juntos.

Como ejemplo se utiliza un componente de imagen simplificado, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

SPA El punto de entrada en la es el archivo `app.module.ts` que se muestra aquí simplificado para centrarse en el contenido importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

El archivo `app.module.ts` es el punto de partida de la aplicación, contiene la configuración inicial del proyecto y usa `AppComponent` para arrancar la aplicación.

#### Instanciación estática {#static-instantiation}

Cuando se crea una instancia del componente de forma estática mediante la plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para que estén disponibles posteriormente como propiedades de componente.

### app.component.ts {#app-component-ts}

Una vez que `app.module.ts` arranca `AppComponent`, puede inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Al procesar la página, `app.component.ts` llamadas `main-content.component.ts` se muestran aquí en una versión simplificada.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` ingiere la representación JSON del modelo de página y procesa el contenido para envolver o decorar cada elemento de la página. SPA Para obtener más información sobre `Page`, consulte el documento [Modelo de la aplicación de código ](blueprint.md) de la aplicación de código abierto .

### image.component.ts {#image-component-ts}

`Page` está compuesto por componentes. Con el JSON introducido, `Page` puede procesar esos componentes como `image.component.ts`, como se muestra aquí.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

SPA AEM SPA AEM La idea central de la en la práctica es la idea de asignar componentes de la a componentes de la y actualizar el componente cuando se modifica el contenido (y a la inversa). SPA Consulte el documento [Información general sobre el editor de](editor-overview.md) para obtener un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

SPA AEM El método `MapTo` asigna el componente de la al componente de la. Admite el uso de una sola cadena o matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede procesar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## SPA Uso Compartido De Información Entre Componentes De La {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Existen varias formas recomendadas de hacerlo, enumeradas de la siguiente manera en orden creciente de complejidad.

* **Opción 1:** Centralice la lógica y difunda a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes mediante una biblioteca de estado como NgRx.
* **Opción 3:** Aproveche la jerarquía de objetos personalizando y extendiendo el componente contenedor.

## Siguientes pasos {#next-steps}

* SPA AEM SPA SPA AEM [Introducción a la en el uso de React](getting-started-react.md) muestra cómo se crea un básico para trabajar con el Editor de la en el uso de React.
* La [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* SPA SPA AEM El [Proyecto de WKND de](wknd-tutorial.md) es un tutorial paso a paso para implementar un proyecto de simple en el área de trabajo de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de.
* SPA SPA AEM [Asignación de modelos dinámicos a componentes para el modelo dinámico para el que se ha asignado el componente ](model-to-component-mapping.md) explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de la asignación de componentes de la de trabajo de la.
* [Modelo de](blueprint.md) ofrece una explicación detallada de cómo funciona el SDK de la para el trabajo en caso de que desee implementar un módulo de trabajo en el que no sea React o Angular, o simplemente desee tener una comprensión más detallada de cómo funciona el SDK de la para el trabajo en el caso de que desee implementar un módulo de trabajo en un entorno de trabajo que no sea React o SPA SPA AEM SPA AEM.
