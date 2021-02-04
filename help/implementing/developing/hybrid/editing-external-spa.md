---
title: Edición de un SPA externo en AEM
description: En este documento se describen los pasos recomendados para cargar un SPA independiente en una instancia de AEM, añadir secciones de contenido editables y habilitar la creación.
translation-type: tm+mt
source-git-commit: bb8ab907dbeb422db410328f9c559c6794c16a8f
workflow-type: tm+mt
source-wordcount: '2127'
ht-degree: 0%

---

# Edición de un SPA externo dentro de AEM {#editing-external-spa-within-aem}

Al decidir [qué nivel de integración](/help/implementing/developing/headful-headless.md) le gustaría tener entre su SPA externa y AEM, a menudo necesita poder editar y vista el SPA dentro de AEM.

## Información general {#overview}

En este documento se describen los pasos recomendados para cargar un SPA independiente en una instancia de AEM, añadir secciones de contenido editables y habilitar la creación.

## Requisitos previos {#prerequisites}

Los requisitos previos son sencillos.

* Asegúrese de que una instancia de AEM se esté ejecutando localmente.
* Cree un proyecto AEM base SPA usando [el arquetipo del proyecto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)
   * Esto constituirá la base del proyecto AEM que se actualizará para incluir la SPA externa.
   * Para los ejemplos de este documento, estamos utilizando el punto de partida del [proyecto de SPA WKND.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)
* Tenga a mano la SPA de Reacción externa que desea integrar.

## Cargar SPA en AEM proyecto {#upload-spa-to-aem-project}

En primer lugar, debe cargar la SPA externa en el proyecto AEM.

1. Reemplace `src` en la carpeta del proyecto `/ui.frontend` por la carpeta `src` de la aplicación React.
1. Incluya dependencias adicionales en el `package.json` archivo `/ui.frontend/package.json` de la aplicación.
   * Asegúrese de que las dependencias del SDK SPA sean de [versiones recomendadas.](/help/implementing/developing/hybrid/getting-started-react.md#dependencies)
1. Incluya cualquier personalización en la carpeta `/public`.
1. Incluya las secuencias de comandos o los estilos en línea agregados en el archivo `/public/index.html`.

## Configurar el SPA remoto {#configure-remote-spa}

Ahora que la SPA externa es parte de su proyecto AEM, debe configurarse dentro de AEM.

### Incluir paquetes de SDK de Adobe SPA {#include-spa-sdk-packages}

Para aprovechar AEM características SPA, hay dependencias en los tres paquetes siguientes.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` proporciona la API para inicializar un Administrador de modelos y recuperar el modelo desde la instancia de AEM. Este modelo se puede utilizar para procesar componentes AEM mediante API de `@adobe/aem-react-editable-components` y `@adobe/aem-spa-component-mapping`.

#### Instalación {#installation}

Ejecute el siguiente comando npm para instalar los paquetes necesarios.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inicialización de ModelManager {#model-manager-initialization}

Antes de que la aplicación se procese, debe inicializarse [`ModelManager`](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager) para gestionar la creación del AEM `ModelStore`.

Esto debe realizarse dentro del archivo `src/index.js` de la aplicación o donde se procese la raíz de la aplicación.

Para ello, podemos utilizar la `initializationAsync` API proporcionada por la `ModelManager`.

La siguiente captura de pantalla muestra cómo habilitar la inicialización de `ModelManager` en una aplicación React simple. La única restricción es que `initializationAsync` debe llamarse antes de `ReactDOM.render()`.

![Inicializar ModelManager](assets/external-spa-initialize-modelmanager.png)

En este ejemplo, se inicializa `ModelManager` y se crea un `ModelStore` vacío.

`initializationAsync` opcionalmente, puede aceptar un  `options` objeto como parámetro:

* `path` - En la inicialización, el modelo de la ruta definida se recupera y se almacena en la  `ModelStore`. Esto se puede usar para recuperar el `rootModel` en la inicialización si es necesario.
* `modelClient` - Permite proporcionar un cliente personalizado responsable de recuperar el modelo.
* `model` - Un  `model` objeto que se pasa como parámetro normalmente se llena al  [utilizar SSR.](/help/implementing/developing/hybrid/ssr.md)

### Componentes de hoja AEM autorizados {#authorable-leaf-components}

1. Cree o identifique un componente de AEM para el que se creará un componente React con autorización. En este ejemplo, utilizamos el componente de texto del proyecto WKND.

   ![Componente de texto WKND](assets/external-spa-text-component.png)

1. Cree un componente de texto Reaccionar sencillo en el SPA. En este ejemplo, se ha creado un nuevo archivo `Text.js` con el siguiente contenido.

   ![Text.js](assets/external-spa-textjs.png)

1. Cree un objeto de configuración para especificar los atributos necesarios para activar AEM edición.

   ![Crear objeto config](assets/external-spa-config-object.png)

   * `resourceType` es obligatorio asignar el componente React al componente AEM y activar la edición al abrirlo en el editor de AEM.

1. Utilice la función de envoltorio `withMappable`.

   ![Usar conAsignable](assets/external-spa-withmappable.png)

   Esta función de envoltorio asigna el componente React al AEM `resourceType` especificado en la configuración y habilita las capacidades de edición cuando se abre en el editor de AEM. En el caso de los componentes independientes, también se recuperará el contenido del modelo para el nodo específico.

   >[!NOTE]
   >
   >En este ejemplo hay versiones independientes del componente: AEM componentes de Reacción envueltos y sin envolver. La versión ajustada debe utilizarse cuando se utiliza explícitamente el componente. Cuando el componente forma parte de una página, puede seguir utilizando el componente predeterminado tal como se hace actualmente en el editor de SPA.

1. Representar contenido en el componente.

   Las propiedades JCR del componente de texto aparecen de la siguiente manera en AEM.

   ![Propiedades del componente de texto](assets/external-spa-text-properties.png)

   Estos valores se pasan como propiedades al componente React recién creado y se pueden usar para representar el contenido.`AEMText`

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   Así es como aparecerá el componente cuando se completen las configuraciones de AEM.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >En este ejemplo, hemos realizado más personalizaciones del componente procesado para que coincida con el componente de texto existente. Sin embargo, esto no está relacionado con la creación en AEM.

#### Añadir componentes autorizados a la página {#add-authorable-component-to-page}

Una vez creados los componentes de React con autorización, podemos utilizarlos en toda la aplicación.

Veamos una página de ejemplo donde necesitamos agregar un texto del proyecto de SPA WKND. Para este ejemplo, queremos mostrar el texto &quot;Hello World!&quot; en `/content/wknd-spa-react/us/en/home.html`.

1. Determinar la ruta del nodo que se va a mostrar.

   * `pagePath`:: La página que contiene el nodo, en nuestro ejemplo  `/content/wknd-spa-react/us/en/home`
   * `itemPath`:: Ruta al nodo dentro de la página, en nuestro ejemplo  `root/responsivegrid/text`
      * Consiste en los nombres de los elementos que los contienen en la página.

   ![Ruta del nodo](assets/external-spa-path.png)

1. Añada el componente en la posición requerida en la página.

   ![Añadir componente a la página](assets/external-spa-add-component.png)

   El componente `AEMText` se puede agregar en la posición requerida dentro de la página con valores `pagePath` y `itemPath` establecidos como propiedades. `pagePath` es una propiedad obligatoria.

#### Verificar la edición del contenido de texto en AEM {#verify-text-edit}

Ahora podemos probar el componente en nuestra instancia de AEM en ejecución.

1. Ejecute el siguiente comando Maven desde el directorio `aem-guides-wknd-spa` para crear e implementar el proyecto en AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. En la instancia de AEM, navegue a `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Edición del SPA en AEM](assets/external-spa-edit-aem.png)

El componente `AEMText` ahora se puede autorizar en AEM.

### Páginas autorizadas de AEM {#aem-authorable-pages}

1. Identifique la página que se agregará para la creación en el SPA. Este ejemplo utiliza `/content/wknd-spa-react/us/en/home.html`.
1. Crear un nuevo archivo (p. ej. `Page.js`) para el componente de página de creación. Aquí, podemos reutilizar el componente de página proporcionado en `@adobe/cq-react-editable-components`.
1. Repita el paso cuatro en la sección [AEM componentes de hoja de creación.](#authorable-leaf-components) Utilice la función envolvente  `withMappable` en el componente.
1. Como se hizo anteriormente, aplique `MapTo` a los tipos de recursos AEM para todos los componentes secundarios dentro de la página.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >En este ejemplo se utiliza el componente de texto React sin ajustar en lugar del `AEMText` ajustado creado anteriormente. Esto se debe a que, cuando el componente forma parte de una página o contenedor y no es independiente, el contenedor se encargará de asignar el componente de forma recursiva y de habilitar las funciones de creación, y el envoltorio adicional no es necesario para cada elemento secundario.

1. Para agregar una página de creación en la SPA, siga los mismos pasos en la sección [Añadir componentes autorizados en la página.](#add-authorable-component-to-page) Sin embargo, aquí podemos omitir la  `itemPath` propiedad.

#### Verificar el contenido de la página en AEM {#verify-page-content}

Para verificar que la página se puede editar, siga los mismos pasos en la sección [Verificar edición de contenido de texto en AEM.](#verify-text-edit)

![Edición de una página en AEM](assets/external-spa-edit-page.png)

La página ahora se puede editar en AEM con un contenedor de diseño y un componente de texto secundario.

### Componentes de hoja virtual {#virtual-leaf-components}

En los ejemplos anteriores, hemos agregado componentes a la SPA con contenido AEM existente. Sin embargo, hay casos en los que el contenido aún no se ha creado en AEM, pero debe agregarlo más adelante el autor del contenido. Para adaptarse a esto, el desarrollador front-end puede agregar componentes en las ubicaciones adecuadas dentro del SPA. Estos componentes mostrarán marcadores de posición cuando se abran en el editor de AEM. Una vez que el autor del contenido agrega contenido dentro de estos marcadores de posición, los nodos se crean en la estructura JCR y el contenido se mantiene. El componente creado permitirá el mismo conjunto de operaciones que los componentes independientes de hoja.

En este ejemplo, reutilizamos el componente `AEMText` creado anteriormente. Queremos que se agregue texto nuevo debajo del componente de texto existente en la página de inicio WKND. La adición de componentes es la misma que para los componentes normales de hoja. Sin embargo, el `itemPath` se puede actualizar a la ruta en la que se debe agregar el nuevo componente.

Dado que el nuevo componente debe agregarse debajo del texto existente en `root/responsivegrid/text`, la nueva ruta será `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

El componente `TestPage` tiene el aspecto siguiente después de agregar el componente virtual.

![Prueba del componente virtual](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Asegúrese de que el componente `AEMText` tiene su `resourceType` establecido en la configuración para habilitar esta función.

Ahora puede implementar los cambios en AEM siguiendo los pasos de la sección [Verificar edición de contenido de texto en AEM.](#verify-text-edit) Se mostrará un marcador de posición para el  `text_20` nodo no existente actualmente.

![El nodo text_20 en aem](assets/external-spa-text20-aem.png)

Cuando el autor del contenido actualiza este componente, se crea un nuevo nodo `text_20` en `root/responsivegrid/text_20` en `/content/wknd-spa-react/us/en/home`.

![El nodo text20](assets/external-spa-text20-node.png)

#### Requisitos y limitaciones {#limitations}

Existen varios requisitos para agregar componentes de hoja virtual, así como algunas limitaciones.

* La propiedad `pagePath` es obligatoria para crear un componente virtual.
* El nodo de página proporcionado en la ruta en `pagePath` debe existir en el proyecto de AEM.
* El nombre del nodo que se va a crear debe proporcionarse en `itemPath`.
* El componente se puede crear en cualquier nivel.
   * Si proporcionamos un `itemPath='text_20'` en el ejemplo anterior, el nuevo nodo se creará directamente debajo de la página, por ejemplo: `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* La ruta al nodo en el que se crea un nuevo nodo debe ser válida cuando se proporciona mediante `itemPath`.
   * En este ejemplo, `root/responsivegrid` debe existir para que el nuevo nodo `text_20` pueda crearse allí.
* Solo se admite la creación de componentes de hoja. El contenedor virtual y la página serán compatibles en versiones futuras.

## Personalizaciones adicionales {#additional-customizations}

Si ha seguido los ejemplos anteriores, la SPA externa ahora se puede editar dentro de AEM. Sin embargo, hay aspectos adicionales de su SPA externa que puede personalizar aún más.

### ID de nodo raíz {#root-node-id}

De forma predeterminada, suponemos que la aplicación React se procesa dentro de un `div` ID de elemento `spa-root`. Si es necesario, se puede personalizar.

Por ejemplo, supongamos que tenemos un SPA en el que la aplicación se procesa dentro de un `div` ID de elemento `root`. Esto debe reflejarse en tres archivos.

1. En el `index.js` de la aplicación React (o donde se llama a `ReactDOM.render()`)

   ![ReactDOM.render() en el archivo index.js](assets/external-spa-root-index.png)

1. En el `index.html` de la aplicación React

   ![El index.html de la aplicación](assets/external-spa-index.png)

1. En el cuerpo del componente de página de la aplicación de AEM mediante dos pasos:

   1. Cree un `body.html` nuevo para el componente de página.

   ![Crear un nuevo archivo body.html](assets/external-spa-update-body.gif)

   1. Añada el nuevo elemento raíz en el nuevo archivo `body.html`.

   ![Añadir el elemento raíz en body.html](assets/external-spa-add-root.png)

### Edición de un SPA React con Enrutamiento {#editing-react-spa-with-routing}

Si la aplicación externa React SPA tiene varias páginas, [puede utilizar enrutamiento para determinar la página o componente que se va a procesar.](/help/implementing/developing/hybrid/routing.md) El caso de uso básico es comparar la dirección URL activa con la ruta proporcionada para una ruta. Para habilitar la edición en estas aplicaciones habilitadas para el enrutamiento, la ruta que se debe comparar debe transformarse para dar cabida a información específica de AEM.

En el siguiente ejemplo tenemos una aplicación React simple con dos páginas. La página que se procesará se determina mediante la coincidencia de la ruta proporcionada al router con la dirección URL activa. Por ejemplo: si estamos en `mydomain.com/test`, se procesará `TestPage`.

![Enrutamiento en un SPA externo](assets/external-spa-routing.png)

Para habilitar la edición dentro de AEM para este SPA de ejemplo, se requieren los pasos siguientes.

1. Identifique el nivel que actuaría como la raíz en AEM.

   * Para nuestra muestra, estamos considerando wknd-spa-response/us/en como la raíz del SPA. Esto significa que todo lo anterior a esa ruta es AEM sólo páginas/contenido.

1. Cree una nueva página en el nivel requerido.

   * En este ejemplo, la página que se va a editar es `mydomain.com/test`. `test` está en la ruta raíz de la aplicación. Esto también debe conservarse al crear la página en AEM. Por lo tanto, podemos crear una nueva página en el nivel raíz definido en el paso anterior.
   * La nueva página creada debe tener el mismo nombre que la página que se va a editar. En este ejemplo para `mydomain.com/test`, la nueva página creada debe ser `/path/to/aem/root/test`.

1. Añada los asistentes dentro SPA enrutamiento.

   * La página recién creada aún no procesará el contenido esperado en AEM. Esto se debe a que el router espera una ruta de `/test` mientras que la ruta activa AEM es `/wknd-spa-react/us/en/test`. Para dar cabida a la porción específica de AEM de la dirección URL, debemos agregar algunos asistentes en el lado SPA.

   ![Auxiliar de enrutamiento](assets/external-spa-router-helper.png)

   * El asistente `toAEMPath` proporcionado por `@adobe/cq-spa-page-model-manager` puede utilizarse para esto. Transforma la ruta proporcionada para el enrutamiento para incluir partes específicas de AEM cuando la aplicación está abierta en una instancia de AEM. Acepta tres parámetros:
      * La ruta requerida para enrutamiento
      * Dirección URL de origen de la instancia de AEM donde se edita el SPA
      * La raíz del proyecto en AEM, según se determinó en el primer paso
   * Estos valores se pueden configurar como variables de entorno para obtener más flexibilidad.



1. Compruebe que está editando la página en AEM.

   * Implemente el proyecto para AEM y navegue a la página `test` recién creada. El contenido de la página ahora se procesa y AEM componentes son editables.

## Recursos adicionales {#additional-resources}

El siguiente material de referencia puede ser útil para comprender SPA en el contexto de AEM.

* [Encabezado y sin cabeza en AEM](/help/implementing/developing/headful-headless.md)
* [El arquetipo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [El proyecto WKND SPA](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html)
* [Introducción a SPA en AEM con React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Materiales de referencia de SPA (referencias de API)](/help/implementing/developing/hybrid/reference-materials.md)
* [SPA modelo y PageModelManager](/help/implementing/developing/hybrid/blueprint.md#pagemodelmanager)
* [enrutamiento del modelo SPA](/help/implementing/developing/hybrid/routing.md)
* [Procesamiento en el lado de SPA y servidor](/help/implementing/developing/hybrid/ssr.md)
