---
title: Modelo SPA
description: SPA SPA AEM En este documento se describe el contrato general independiente del marco de trabajo que cualquier marco de trabajo de debe cumplir para que pueda implementar componentes de la estructura editables dentro de los componentes de la.
exl-id: 9d47c0e9-600c-4f45-9169-b3c9bbee9152
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 1%

---

# Modelo SPA {#spa-blueprint}

AEM SPA SPA SPA Para permitir que el autor use el Editor de de trabajo para editar el contenido de un, hay requisitos que el autor debe cumplir. El Editor de la de trabajo de la publicación de contenido de la publicación de contenido debe cumplir varios requisitos.

{{ue-over-spa}}

## Introducción {#introduction}

SPA AEM SPA AEM En este documento se describe el contrato general que cualquier marco de trabajo debe cumplir (es decir, el tipo de capa de soporte de la) para que pueda implementar componentes editables de la dentro de los elementos de trabajo.

AEM AEM Para permitir que el autor utilice el Editor de páginas de la página de la aplicación para editar los datos expuestos por un marco de trabajo de aplicación de una sola página, un proyecto debe poder interpretar la estructura del modelo que representa la semántica de los datos almacenados para una aplicación dentro del repositorio de la aplicación de la aplicación. Para lograr este objetivo, se proporcionan dos bibliotecas no basadas en marcos: la `PageModelManager` y la `ComponentMapping`.

>[!NOTE]
>
>Los siguientes requisitos son independientes del marco de trabajo. Si se cumplen estos requisitos, se puede proporcionar una capa específica del marco de trabajo compuesta por módulos, componentes y servicios.
>
>**Estos requisitos ya se han cumplido para los marcos de React y Angular de la aplicación de la aplicación de la aplicación de la aplicación de AEM de la aplicación de.AEM** Los requisitos de este modelo solo son relevantes si desea implementar otro marco de trabajo para utilizarlo con el modelo de datos de.

>[!CAUTION]
>
>SPA AEM Aunque las capacidades de la de los módulos son independientes de los módulos, actualmente solo se admiten los módulos React y Angular.

## PageModelManager {#pagemodelmanager}

SPA La biblioteca `PageModelManager` se proporciona como un paquete NPM para su uso en un proyecto de la red de trabajo de la red de trabajo (NPMs) de un proyecto de la red de trabajo. SPA Acompaña a la y sirve como administrador del modelo de datos.

SPA En nombre de la, resume la recuperación y administración de la estructura JSON que representa la estructura de contenido real. SPA También es responsable de la sincronización con el para hacerle saber cuándo tiene que volver a procesar sus componentes.

Consulte el paquete NPM [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

Al inicializar `PageModelManager`, la biblioteca primero carga el modelo raíz proporcionado de la aplicación (mediante parámetro, metapropiedad o dirección URL actual). Si la biblioteca identifica que el modelo de la página actual no forma parte del modelo raíz, lo recupera e inclúyalo como el modelo de una página secundaria.

![Consolidación del modelo de página](assets/page-model-consolidation.png)

### ComponentMapping {#componentmapping}

El módulo `ComponentMapping` se proporciona como paquete NPM al proyecto front-end. SPA AEM Almacena componentes front-end y proporciona una forma para que los usuarios de la aplicación asignen componentes front-end a tipos de recursos de. Esto permite una resolución dinámica de componentes al analizar el modelo JSON de la aplicación.

AEM Cada elemento presente en el modelo contiene un campo `:type` que expone un tipo de recurso de. Cuando se monta, el componente front-end puede representarse a sí mismo utilizando el fragmento de modelo que ha recibido de las bibliotecas subyacentes.

#### Asignación de modelos dinámicos a componentes {#dynamic-model-to-component-mapping}

Para obtener más información sobre cómo se produce la asignación de modelos dinámicos a componentes en JavaScript SPA SDK AEM SPA para su uso, consulte el artículo [Asignación de modelos dinámicos a componentes para la aplicación de modelos de](model-to-component-mapping.md).

### Capa específica del marco de trabajo {#framework-specific-layer}

Se debe implementar una tercera capa para cada módulo front-end. Esta tercera biblioteca es responsable de interactuar con las bibliotecas subyacentes y proporciona una serie de puntos de entrada bien integrados y fáciles de usar para interactuar con el modelo de datos.

El resto de este documento describe los requisitos de esta capa específica del marco intermediario y aspira a ser independiente del marco. Respetando los siguientes requisitos, se puede proporcionar una capa específica del marco de trabajo para que los componentes del proyecto interactúen con las bibliotecas subyacentes a cargo de la administración del modelo de datos.

## Conceptos generales {#general-concepts}

### Modelo de página {#page-model}

AEM La estructura de contenido de la página se almacena en el archivo de datos de. SPA El modelo de la página se utiliza para asignar e instanciar componentes de la. SPA SPA AEM Los desarrolladores de la crean componentes de la a los que asignan componentes de la aplicación. AEM Para ello, utilizan el tipo de recurso (o la ruta al componente de) como clave única.

SPA Los componentes de la página deben estar sincronizados con el modelo de página y se deben actualizar con cualquier cambio en su contenido en consecuencia. Se debe utilizar un patrón que utilice componentes dinámicos para crear instancias de los componentes sobre la marcha siguiendo la estructura del modelo de página proporcionada.

### Metadatos de campos {#meta-fields}

El modelo de página utiliza el Exportador de modelos JSON, que a su vez se basa en la API [Sling Model](https://sling.apache.org/documentation/bundles/models.html). Los modelos de sling exportables exponen la siguiente lista de campos para permitir que las bibliotecas subyacentes interpreten el modelo de datos:

* AEM `:type`: tipo de recurso de la (predeterminado = tipo de recurso)
* `:children`: elementos secundarios jerárquicos del recurso actual. Los elementos secundarios no forman parte del contenido interno del recurso actual (se pueden encontrar en elementos que representan una página)
* `:hierarchyType`: tipo jerárquico de un recurso. `PageModelManager` admite actualmente el tipo de página

* `:items`: recursos de contenido secundario del recurso actual (estructura anidada, solo presente en contenedores)
* `:itemsOrder`: lista ordenada de los elementos secundarios. El objeto de asignación JSON no garantiza el orden de sus campos. Al tener el mapa y la matriz actual, el consumidor de la API tiene las ventajas de ambas estructuras
* `:path`: ruta de contenido de un elemento (presente en elementos que representan una página)

AEM Consulte también [Introducción a los servicios de contenido de la](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es).

### Módulo específico del marco de trabajo {#framework-specific-module}

La separación de las preocupaciones ayuda a facilitar la ejecución del proyecto. Por lo tanto, debe proporcionarse un paquete específico de npm. Este paquete es responsable de agregar y exponer los módulos, servicios y componentes base. Estos componentes deben encapsular la lógica de administración del modelo de datos y proporcionar acceso a los datos que espera el componente del proyecto. El módulo también es responsable de exponer transitivamente puntos de entrada útiles de las bibliotecas subyacentes.

Para facilitar la interoperabilidad de las bibliotecas, los Adobes recomiendan al módulo específico del marco que agrupe las siguientes bibliotecas. Si es necesario, la capa puede encapsular y adaptar las API subyacentes antes de exponerlas al proyecto.

* [@adobe/aem-spa-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementaciones {#implementations}

#### Reaccionar {#react}

módulo npm: [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

módulo npm: [@adobe/aem-angular-editable-components](https://www.npmjs.com/package/@adobe/aem-angular-editable-components)

## Servicios y componentes principales {#main-services-and-components}

Las siguientes entidades deben aplicarse de conformidad con las directrices específicas de cada marco. En función de la arquitectura del marco, la implementación puede variar ampliamente, pero deben proporcionarse las funcionalidades descritas.

### El proveedor de modelos {#the-model-provider}

Los componentes de proyecto deben delegar el acceso a los fragmentos de un modelo a un proveedor de modelos. El proveedor de modelos se encarga de escuchar los cambios realizados en el fragmento especificado del modelo y devolver el modelo actualizado al componente de delegación.

Para ello, el proveedor de modelos debe registrarse en [`PageModelManager`](#pagemodelmanager). A continuación, cuando se produce un cambio, recibe y pasa los datos actualizados al componente que delega. De forma predeterminada, la propiedad disponible para el componente de delegación que llevará el fragmento del modelo se denomina `cqModel`. La implementación es libre de proporcionar esta propiedad al componente, pero debe tener en cuenta aspectos como la integración con la arquitectura del marco de trabajo, la capacidad de detección y la facilidad de uso.

### El decorador del HTML de componentes {#the-component-html-decorator}

El decorador de componentes es responsable de decorar el HTML externo del elemento de cada instancia de componente con una serie de atributos de datos y nombres de clase esperados por el editor de páginas.

#### Declaración de componente {#component-declaration}

Los siguientes metadatos deben agregarse al elemento HTML externo producido por el componente del proyecto. Permiten que el Editor de páginas recupere la configuración de edición correspondiente.

* `data-cq-data-path`: ruta de acceso al recurso relativa al `jcr:content`

#### Declaración de capacidad de edición y marcador de posición {#editing-capability-declaration-and-placeholder}

Los siguientes metadatos y nombres de clase deben agregarse al elemento HTML externo producido por el componente del proyecto. Permiten al editor de páginas ofrecer funcionalidades relacionadas.

* `cq-placeholder`: nombre de clase que identifica el marcador de posición de un componente vacío
* `data-emptytext`: etiqueta que se mostrará en la superposición cuando una instancia de componente esté vacía

**Marcador de posición para componentes vacíos**

Cada componente debe ampliarse con una funcionalidad que decore el elemento HTML externo con atributos de datos y nombres de clase específicos de marcadores de posición y superposiciones relacionadas cuando el componente se identifique como vacío.

**Acerca del vacío de un componente**

* ¿Está el componente vacío lógicamente?
* ¿Cuál debería ser la etiqueta mostrada por la superposición cuando el componente está vacío?

### Contenedor {#container}

Un contenedor es un componente diseñado para contener y procesar componentes secundarios. Para ello, el contenedor se repite en las propiedades `:itemsOrder`, `:items` y `:children` de su modelo.

El contenedor obtiene dinámicamente los componentes secundarios del almacén de la biblioteca [`ComponentMapping`](#componentmapping). A continuación, el contenedor amplía el componente secundario con las capacidades del proveedor de modelos y, finalmente, crea una instancia de él.

### Página {#page}

El componente `Page` amplía el componente `Container`. Un contenedor es un componente diseñado para contener y procesar componentes secundarios, incluidas páginas secundarias. Para ello, el contenedor repite las propiedades `:itemsOrder`, `:items` y `:children` de su modelo. El componente `Page` obtiene dinámicamente los componentes secundarios del almacén de la biblioteca [`ComponentMapping`](#componentmapping). `Page` es responsable de crear instancias de componentes secundarios.

### Cuadrícula adaptable {#responsive-grid}

El componente Cuadrícula interactiva es un contenedor. Contiene una variante específica del proveedor de modelos que representa sus columnas. La cuadrícula adaptable y sus columnas son responsables de decorar el elemento HTML externo del componente del proyecto con los nombres de clase específicos contenidos en el modelo.

AEM El componente Cuadrícula interactiva debe estar preasignado a su homólogo de la, ya que este componente es complejo y rara vez se personaliza.

#### Campos de modelo específicos {#specific-model-fields}

* `gridClassNames:` proporcionó nombres de clase para la cuadrícula adaptable
* `columnClassNames:` proporcionó nombres de clase para la columna adaptable

Consulte también el recurso npm [@adobe/aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Marcador de posición de la cuadrícula interactiva {#placeholder-of-the-responsive-grid}

SPA El componente se asigna a un contenedor gráfico como Cuadrícula interactiva y debe agregar un marcador de posición secundario virtual cuando se crea el contenido. SPA Cuando el editor de páginas crea el contenido de la, ese contenido se incrusta en el editor mediante un iframe y el atributo `data-cq-editor` se agrega al nodo del documento de ese contenido. Cuando el atributo `data-cq-editor` está presente, el contenedor debe incluir un elemento HTML para representar el área con la que el autor interactúa al insertar un nuevo componente en la página.

Por ejemplo:

```html
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>El editor de páginas requiere actualmente los nombres de clase utilizados en el ejemplo.
>
>* `"new section"`: indica que el elemento actual es el marcador de posición del contenedor
>* `"aem-Grid-newComponent"`: normaliza el componente para la creación de diseños
>

#### Asignación de componentes {#component-mapping}

La biblioteca [`Component Mapping`](#componentmapping) subyacente y su función `MapTo` se pueden encapsular y ampliar para proporcionar las funcionalidades relativas a la configuración de edición proporcionada junto con la clase de componente actual.

```javascript
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

En la implementación anterior, el componente de proyecto se amplía con la funcionalidad vacía antes de que se registre realmente en el almacén [Component Mapping](#componentmapping). Esto se hace encapsulando y ampliando la biblioteca [`ComponentMapping`](#componentmapping) para introducir la compatibilidad del objeto de configuración `EditConfig`:

```javascript
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data is decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Contrato con el editor de páginas {#contract-with-the-page-editor}

Los componentes del proyecto deben generar como mínimo los siguientes atributos de datos para permitir que el editor interactúe con ellos.

* `data-cq-data-path`: ruta relativa del componente proporcionada por `PageModel` (por ejemplo, `"root/responsivegrid/image"`). Este atributo no debe añadirse a las páginas.

En resumen, para que el editor de páginas lo interprete como editable, un componente de proyecto debe respetar el siguiente contrato:

* AEM Proporcione los atributos esperados para asociar una instancia de componente de front-end a un recurso de.
* Proporcione la serie esperada de atributos y nombres de clase que permita la creación de marcadores de posición vacíos.
* Proporcione los nombres de clase esperados que permitan arrastrar y soltar recursos.

### Estructura típica del elemento HTML {#typical-html-element-structure}

El siguiente fragmento ilustra la representación típica del HTML de una estructura de contenido de página. Estos son algunos puntos importantes:

* El elemento de cuadrícula adaptable lleva nombres de clase con el prefijo `aem-Grid--`
* El elemento de columna adaptable lleva nombres de clase con el prefijo `aem-GridColumn--`
* Una cuadrícula adaptable que también es la columna de una cuadrícula principal está ajustada, como los dos prefijos anteriores no aparecen en el mismo elemento
* Los elementos correspondientes a los recursos editables llevan una propiedad `data-cq-data-path`. Consulte la sección [Contrato con el editor de páginas](#contract-with-the-page-editor) de este documento.

```javascript
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navegación y enrutamiento {#navigation-and-routing}

La aplicación es propietaria del enrutamiento. AEM En primer lugar, el desarrollador front-end debe implementar un componente de navegación (asignado a un componente de navegación de). Este componente procesaría vínculos de URL para usarlos junto con una serie de rutas que mostrarán u ocultarán fragmentos de contenido.

La biblioteca [`PageModelManager`](#pagemodelmanager) subyacente y su módulo [`ModelRouter`](routing.md) (habilitado de forma predeterminada) son responsables de la recuperación previa y de proporcionar acceso al modelo asociado con una ruta de recurso determinada.

Las dos entidades están relacionadas con la noción de enrutamiento, pero [`ModelRouter`](routing.md) solo es responsable de cargar [`PageModelManager`](#pagemodelmanager) con un modelo de datos estructurado en sincronización con el estado de la aplicación actual.

SPA Consulte el artículo [Enrutamiento de modelo de](routing.md) para obtener más información.

## SPA En acción {#spa-in-action}

SPA SPA Vea cómo funciona un simple y experimente con un usuario de la misma manera continuando con los siguientes documentos:

* SPA AEM [Introducción a la en el uso de React](getting-started-react.md).
* SPA AEM [Introducción a la en el uso del Angular de trabajo](getting-started-angular.md).

## Lectura adicional {#further-reading}

SPA AEM Para obtener más información acerca de la de en la documentación de, consulte los siguientes documentos:

* SPA SPA AEM [Información general del editor de](editor-overview.md) para obtener una descripción general de la información general sobre el modelo de comunicación y el formato de la comunicación en el sitio web de
