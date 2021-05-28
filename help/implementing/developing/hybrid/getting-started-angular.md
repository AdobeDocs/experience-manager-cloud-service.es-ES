---
title: Introducción a SPA en AEM Uso de Angular
description: Este artículo presenta una aplicación de SPA de ejemplo, explica cómo se integra y le permite ponerse en marcha con sus propios SPA rápidamente mediante el marco de Angular.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Introducción a SPA en AEM Uso de Angular {#getting-started-with-spas-in-aem-using-angular}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado mediante marcos de SPA.

La función de creación de SPA ofrece una solución completa para admitir SPA dentro de AEM. Este artículo presenta una aplicación de SPA simplificada en el marco del Angular, explica cómo se ha creado, lo que le permite ponerse en marcha con su propia SPA rápidamente.

>[!NOTE]
>
>Este artículo se basa en el marco de Angular. Para el documento correspondiente del marco de React, consulte [Introducción a SPA en AEM - React](getting-started-react.md).

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

Este documento recorrerá la estructura de un SPA simplificado e ilustrará cómo funciona para que pueda aplicar este entendimiento a su propia SPA.

## Dependencias, configuración y creación {#dependencies-configuration-and-building}

Además de la dependencia de Angular esperada, el SPA de ejemplo puede aprovechar bibliotecas adicionales para que la creación de la SPA sea más eficiente.

### Dependencias {#dependencies}

El archivo `package.json` define los requisitos del paquete de SPA general. Aquí se enumeran las dependencias AEM mínimas requeridas.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

### Compilando {#building}

La creación de la aplicación aprovecha el [Webpack](https://webpack.js.org/) para la transpilación, además del aem-clientlib-generator para la creación automática de la biblioteca del cliente. Por lo tanto, el comando build se parecerá a:

`"build": "ng build --build-optimizer=false && clientlib",`

Una vez creado, el paquete se puede cargar en una instancia de AEM.

### Tipo de archivo del proyecto AEM {#aem-project-archetype}

Cualquier proyecto AEM debe aprovechar el [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos con React o Angular y aprovecha el SDK de SPA.

## Estructura de la aplicación {#application-structure}

Al incluir las dependencias y crear la aplicación tal como se describió anteriormente, dispondrá de un paquete de SPA de trabajo que puede cargar en la instancia de AEM.

La siguiente sección de este documento le explica cómo se estructura un SPA en AEM, los archivos importantes que dirigen la aplicación y cómo funcionan juntos.

Se utiliza un componente de imagen simplificado como ejemplo, pero todos los componentes de la aplicación se basan en el mismo concepto.

### app.module.ts {#app-module-ts}

El punto de entrada en el SPA es el archivo `app.module.ts` que se muestra aquí simplificado para centrarse en el contenido importante.

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

El archivo `app.module.ts` es el punto de partida de la aplicación, contiene la configuración inicial del proyecto y utiliza `AppComponent` para arrancar la aplicación.

#### Creación de instancias estáticas {#static-instantiation}

Cuando se crea una instancia del componente estáticamente utilizando la plantilla de componente, el valor debe pasarse del modelo a las propiedades del componente. Los valores del modelo se pasan como atributos para que más adelante estén disponibles como propiedades de componente.

### app.component.ts {#app-component-ts}

Una vez `app.module.ts` bootstraps `AppComponent`, puede inicializar la aplicación, que se muestra aquí en una versión simplificada para centrarse en el contenido importante.

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

Al procesar la página, `app.component.ts` llama a `main-content.component.ts` enumeradas aquí en una versión simplificada.

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

El `MainComponent` ingesta la representación JSON del modelo de página y procesa el contenido para ajustar/decorar cada elemento de la página. Puede encontrar más detalles sobre el `Page` en el documento [SPA modelo](blueprint.md).

### image.component.ts {#image-component-ts}

El `Page` está compuesto por componentes. Con el JSON incorporado, el `Page` puede procesar esos componentes como `image.component.ts` como se muestra aquí.

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

La idea central de SPA en AEM es la idea de asignar componentes SPA a AEM componentes y actualizar el componente cuando se modifica el contenido (y viceversa). Consulte el documento [SPA Editor Overview](editor-overview.md) para ver un resumen de este modelo de comunicación.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

El método `MapTo` asigna el componente SPA al componente AEM. Admite el uso de una sola cadena o una matriz de cadenas.

`ImageEditConfig` es un objeto de configuración que contribuye a habilitar las capacidades de creación de un componente al proporcionar los metadatos necesarios para que el editor genere marcadores de posición

Si no hay contenido, las etiquetas se proporcionan como marcadores de posición para representar el contenido vacío.

#### Propiedades pasadas dinámicamente {#dynamically-passed-properties}

Los datos procedentes del modelo se pasan dinámicamente como propiedades del componente.

### image.component.html {#image-component-html}

Finalmente, la imagen se puede representar en `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Uso compartido de información entre componentes SPA {#sharing-information-between-spa-components}

Normalmente, es necesario que los componentes de una aplicación de una sola página compartan información. Hay varias formas recomendadas de hacerlo, enumeradas a continuación en orden creciente de complejidad.

* **Opción 1:** centralice la lógica y la emisión a los componentes necesarios, por ejemplo, utilizando una clase util como solución pura orientada a objetos.
* **Opción 2:** Compartir estados de componentes utilizando una biblioteca de estado como NgRx.
* **Opción 3:** aproveche la jerarquía de objetos personalizando y ampliando el componente contenedor.

## Pasos siguientes {#next-steps}

* [Introducción a SPA en AEM con ](getting-started-react.md) Reactancia muestra cómo se crea un SPA básico para trabajar con el Editor SPA en AEM con React.
* [SPA ](editor-overview.md) Información general del editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [WKND SPA ](wknd-tutorial.md) Project es un tutorial paso a paso que implementa un proyecto de SPA simple en AEM.
* [Asignación de modelos dinámicos a componentes para ](model-to-component-mapping.md) SPAs explica el modelo dinámico a la asignación de componentes y cómo funciona dentro de SPA en AEM.
* [SPA ](blueprint.md) Blueprintoofrece una explicación detallada sobre cómo funciona el SDK de SPA para AEM en caso de que desee implementar SPA en AEM para un marco que no sea React o Angular, o simplemente desee un entendimiento más profundo.
