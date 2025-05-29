---
title: Personalizar la aplicación Selector de recursos
description: Utilice funciones para personalizar el selector de recursos en la aplicación.
role: Admin, User
exl-id: 0fd0a9f7-8c7a-4c21-9578-7c49409df609
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 28%

---

# Personalizaciones del Selector de recursos {#asset-selector-customization}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

El Selector de recursos le permite personalizar varios componentes según sus preferencias, requisitos o necesidades funcionales. Puede personalizar los siguientes componentes [Selector de recursos de Micro-Frontend](#overview-asset-selector.md):

* [Personalizar panel de filtro](#customize-filter-panel)
* [Personalizar información en la vista modal](#customize-info-in-modal-view)
* [Habilitar o deshabilitar el modo de arrastrar y soltar](#enable-disable-drag-and-drop)
* [Selección de Assets](#selection-of-assets)
* [Personalizar recursos caducados](#customize-expired-assets)
* [Filtro de invocación contextual](#contextual-invocation-filter)
* [propiedad dragOptions](#drag-options-property)

Debe definir los requisitos previos del archivo **index.html** o un archivo similar dentro de la implementación de la aplicación para definir los detalles de autenticación para acceder al repositorio [!DNL Experience Manager Assets]. Una vez finalizado, puede agregar fragmentos de código según sus necesidades.

## Personalizar panel de filtro {#customize-filter-panel}

Puede agregar el siguiente fragmento de código en el objeto `assetSelectorProps` para personalizar el panel de filtro:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

## Personalizar información en la vista modal {#customize-info-in-modal-view}

Puede personalizar la vista de detalles de un recurso al hacer clic en el icono ![información](assets/info-icon.svg). Ejecute el siguiente código:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path')
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

## Habilitar o deshabilitar el modo de arrastrar y soltar {#enable-disable-drag-and-drop}

Agregue las siguientes propiedades a `assetSelectorProp` para habilitar el modo de arrastrar y soltar. Para deshabilitar la función de arrastrar y soltar, reemplace el parámetro `true` por `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

## Selección de Assets {#selection-of-assets}

El tipo de recurso seleccionado es una matriz de objetos que contiene la información del recurso al utilizar las funciones `handleSelection`, `handleAssetSelection`, y `onDrop`.

Ejecute los siguientes pasos para configurar la selección de uno o varios recursos:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

**Sintaxis de esquema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

En la tabla siguiente se describen algunas de las propiedades importantes del objeto Recurso seleccionado.

| Propiedad | Tipo | Descripción |
|---|---|---|
| *repo:repositoryId* | cadena | Identificador único del repositorio en el que se almacena el recurso. |
| *repo:id* | cadena | Identificador único del recurso. |
| *repo:assetClass* | cadena | La clasificación del recurso (por ejemplo, imagen o vídeo, documento). |
| *repo:name* | cadena | Nombre del recurso, incluida la extensión de archivo. |
| *repo:size* | número | El tamaño del recurso en bytes. |
| *repo:path* | cadena | La ubicación del recurso dentro del repositorio. |
| *repo:ancestors* | `Array<string>` | Matriz de elementos antecesores del recurso en el repositorio. |
| *repo:state* | cadena | Estado actual del recurso en el repositorio (por ejemplo, activo, eliminado, etc.). |
| *repo:createdBy* | cadena | El usuario o sistema que creó el recurso. |
| *repo:createDate* | cadena | La fecha y la hora en que se creó el recurso. |
| *repo:modifiedBy* | cadena | Usuario o sistema que modificó el recurso por última vez. |
| *repo:modifyDate* | cadena | La fecha y la hora en que se modificó el recurso por última vez. |
| *dc:format* | cadena | El formato del recurso, como el tipo de archivo (por ejemplo, JPEG, PNG, etc.). |
| *tiff:imageWidth* | número | La anchura de un recurso. |
| *tiff:imageLength* | número | Altura de un recurso. |
| *computedMetadata* | `Record<string, any>` | Un objeto que representa un cubo para todos los metadatos del recurso de todo tipo (repositorio, aplicación o metadatos incrustados). |
| *_links* | `Record<string, any>` | Vínculos de hipermedia para el recurso asociado. Incluye vínculos para recursos como metadatos y representaciones. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition>`* | `Array<Object>` | Matriz de objetos que contiene información sobre las representaciones del recurso. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>`* | cadena | URI de la representación. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>`* | cadena | Tipo MIME de la representación. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>`* | número | El tamaño de la representación en bytes. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>`* | número | La anchura de la representación. |
| *`_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>`* | número | Altura de la representación. |

### Gestión de la selección de recursos mediante el esquema de objetos {#handling-selection}

La propiedad `handleSelection` se utiliza para gestionar una o varias selecciones de recursos en el Selector de recursos. El ejemplo siguiente indica la sintaxis de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

### Desactivación de la selección de Assets {#disable-selection}

Deshabilitar selección se utiliza para ocultar o deshabilitar la selección de recursos o carpetas. Oculta la casilla de verificación de selección de la tarjeta o el recurso, lo que impide que se seleccione. Para utilizar esta función, puede declarar la posición de un recurso o carpeta que desee deshabilitar en una matriz. Por ejemplo, si desea deshabilitar la selección de una carpeta que aparece en la primera posición, puede agregar el siguiente código:
`disableSelection: [0]:folder`

Puede proporcionar a la matriz una lista de tipos MIME (como imagen, carpeta, archivo u otros tipos MIME, por ejemplo, imagen/jpeg) que desee desactivar. Los tipos MIME que declare se asignan a los atributos `data-card-type` y `data-card-mimetype` de un recurso.

Además, se pueden arrastrar Assets con la selección deshabilitada. Para deshabilitar la función de arrastrar y soltar de un tipo de recurso concreto, puede utilizar la propiedad `dragOptions.allowList`.

La sintaxis de la selección de deshabilitar es la siguiente:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> En el caso de un recurso, la casilla de verificación de selección está oculta, mientras que en el caso de una carpeta, la carpeta no se puede seleccionar, pero sigue apareciendo la navegación por la carpeta mencionada.

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

## Personalizar recursos caducados {#customize-expired-assets}

El Selector de recursos permite controlar el uso de un recurso caducado. Puede personalizar el recurso caducado con un distintivo de **Vencimiento pronto** que le ayudará a conocer de antemano los recursos que caducarán dentro de los 30 días posteriores a la fecha actual. Además, esto se puede personalizar según el requisito. También puede permitir la selección de un recurso caducado en el lienzo o viceversa. La personalización de un recurso caducado se puede realizar mediante algunos fragmentos de código de varias formas:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

### Selección de un recurso caducado {#selection-of-expired-asset}

Puede personalizar el uso de un recurso caducado para que se pueda seleccionar o no. Puede personalizar si desea permitir o no la operación de arrastrar y soltar un recurso caducado en el lienzo del Selector de recursos. Para ello, utilice los siguientes parámetros para que un recurso no se pueda seleccionar en el lienzo:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```
<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

### Configuración de la duración de un recurso caducado {#set-duration-of-expired-asset}

El siguiente fragmento de código le ayuda a establecer el distintivo **caducará pronto** para los recursos que caduquen en los próximos cinco días: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Consulte el siguiente ejemplo para comprender cómo funciona la propiedad para recuperar la fecha y la hora actuales:

```
const currentData = new Date();
currentData.getTime(),
```

devuelve `1718779013959`, que es según el formato de fecha 2024-06-19T06:36:53.959Z.

### Personalizar el mensaje de mensaje de un recurso caducado {#customize-toast-message}

La propiedad `showToast` se usa para personalizar el mensaje de mensaje que desea mostrar en un recurso caducado.

Sintaxis:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

El tiempo de espera predeterminado es de 500 milisegundos. Por su parte, puede modificarla según los requisitos. Además, al pasar el valor `timeout: 0`, se mantiene abierto el mensaje hasta que se hace clic en el botón cruzado.

A continuación se muestra un ejemplo para mostrar un mensaje de mensaje cuando es necesario impedir la selección de una carpeta y mostrar un mensaje correspondiente:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Utilice el siguiente fragmento de código para mostrar el mensaje de mensaje para el uso de un recurso caducado:

```
(args) => {
    const [selectedAssets, setSelectedAssets] = useState([]);
    const [showToast, setShowToast] = React.useState(false);
    const handleAssetSelection = (assets) => {
        let directorySelectedFlag = false;
        const temp = assets.filter((asset) => {
            if (asset['repo:assetClass'] === 'directory') {
                directorySelectedFlag = true;
                setShowToast(true);
            }
            return !(asset['repo:assetClass'] === 'directory');
        });
        if (!directorySelectedFlag) {
            setShowToast(false);
        }
        setSelectedAssets(temp);
    };
    return (
        <ASDialogWrapper
            {...args}
            showToast={showToast ? args.showToast : null}
            selectedAssets={selectedAssets}
            handleAssetSelection={handleAssetSelection}
        />
    );
}
```

## Filtro de invocación contextual{#contextual-invocation-filter}

El Selector de recursos le permite agregar un filtro de selector de etiquetas. Admite un grupo de etiquetas que combina todas las etiquetas relevantes con un grupo de etiquetado concreto. Además, le permite seleccionar etiquetas adicionales correspondientes al recurso que está buscando. Además, también puede establecer los grupos de etiquetas predeterminados en el filtro de invocación contextual que utiliza principalmente para que le sean accesibles en sus desplazamientos.

>
>
> * Se debe añadir un fragmento de código de invocación contextual para habilitar el filtro de etiquetado en la búsqueda.
> * Es obligatorio usar la propiedad name correspondiente al tipo de grupo de etiquetas `(property=xcm:keywords.id=)`.

Sintaxis:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Para agregar grupos de etiquetas en el panel Filtros, es obligatorio agregar al menos un grupo de etiquetas como predeterminado. Además, utilice el siguiente fragmento de código para añadir las etiquetas predeterminadas preseleccionadas del grupo de etiquetas.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![filtro de grupo de etiquetas](assets/tag-group.gif)

## Cargar en el selector de recursos {#upload-in-asset-selector}

Puede cargar archivos o carpetas en el Selector de recursos desde su sistema de archivos local. Para cargar archivos mediante el sistema de archivos local, suele ser necesario utilizar una función de carga proporcionada por una aplicación de microfront-end del Selector de recursos. Varios fragmentos de código necesarios para invocar la carga en el selector de recursos implican:

* [Fragmento de código de formulario de carga básico](#basic-upload)
* [Cargar con metadatos](#upload-with-metadata)
* [Carga personalizada](#customized-upload)
* [Carga mediante fuentes de terceros](#upload-using-third-party-source)

### Formulario de carga básico {#basic-upload}

```
import { AllInOneUpload } from '@assets/upload';
import { TextField, ContextualHelp } from '@adobe/react-spectrum';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

export const UploadExample = () => {
    return (
        <>
            <TextField
                marginStart="size-200"
                width="size-6000"
                isDisabled={true}
                label="Target Upload Path"
                value={targetUploadPath}
                contextualHelp={
                    <ContextualHelp>
                        <Content>Use Storybook Controls panel to change the default upload location</Content>
                    </ContextualHelp>
                }
            />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
            />
        <>
    )
}
```

### Cargar con metadatos {#upload-with-metadata}

```
import { AllInOneUpload } from '@assets/upload';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

/**
 * see https://git.corp.adobe.com/CQ/assets-upload/blob/main/packages/@assets/upload/stories/data/SampleMetadataSchemas.ts
 * for full schema shape used in rendered example below
 */
const metadataSchema = [
    {
        mapToProperty: 'gmo:lineofBusiness',
        label: 'Line of Business',
        placeholder: 'Select one',
        required: true,
        element: 'dropdown',
        dropdownOptions: [
            {
                id: 'corporate',
                name: 'Corporate',
            },
            {
                id: 'digital-media-dme',
                name: 'Digital Media (DMe)',
            },
            {
                id: 'digital-experience-dx',
                name: 'Digital Experience (DX)',
            },
            {
                id: 'business-solutions',
                name: 'Business Solutions',
            },
        ],
    },
    // ... see link above for full schema
    {
        mapToProperty: 'dam:assetStatus',
        value: 'approved',
        // hidden metadata element, this metadata will be applied to the asset without rendering UI for user input
        element: 'hidden',
    },
];

const handleMetadataFormChange = (event: MetadataChangeEvent) => {
    const { property, value } = event;

    console.log({ property, value });
}

const UploadExampleWithMetadataForm = () => {
    return (
        <AllInOneUpload
            repositoryId={repoId}
            apiToken={apiToken}
            targetUploadPath={targetUploadPath}
            metadataSchema={sampleMetadataSchema}
            onMetadataFormChange={handleMetadataFormChange}
        />
    )
}
```

### Carga personalizada {#customized-upload}

```
const MultipleAllInOneUploadExample = () => {
    const mfeRef = React.useRef<{ iframeRef: { current: HTMLIFrameElement } }>(null);

    return (
        <>
            <Button
                onPress={() => UploadCoordinator.initiateUpload(mfeRef.current?.iframeRef?.current)}
            >
                External Initiate Upload
            </Button>
            <AllInOneUpload
                {...otherProps}
                ref={mfeRef}
            />
        <>
    );
}
```

### Carga mediante fuentes de terceros {#upload-using-third-party-source}

```
import { useState, useRef } from 'react';
import { AllInOneUpload, UploadCoordinator } from '@assets/upload';
import { Button, Flex, Divider } from '@adobe/react-spectrum';
import { sampleMetadataSchema } from './SampleMetadataSchemas';

const repoId = 'author-p52554-e145207-cmstg.adobeaemcloud.com'
const apiToken = 'eyJhbG....';
const targetUploadPath = '/content/dam/hydrated-assets/cq/as/cq-assets-upload-storybook-testing';

const defaultFiles = [
    new File(['file-content'], 'Controlled File 1'),
    new File(['file-content-with-more'], 'Controlled File 2')
];

const ControlledUploadExample = () => {
    const [controlledFiles, setControlledFiles] = useState<File[]>(defaultFiles)
    const inputRef = React.useRef<HTMLInputElement>(null);

    const handleFileInputChange = useCallback((e: ChangeEvent<HTMLInputElement>) => {
        if (e.target.files) {
            setMyFiles([...e.target.files]);
        }
    }, []);

    return (
        <Flex height="100%" alignItems="center" direction="column">
            <Flex direction="row" alignItems="center" justifyContent="center">
                <Button
                    variant="accent"
                    onPress={() => UploadCoordinator.initiateUpload()}
                    isDisabled={files.length < 1}
                >
                    External Initiate Upload
                </Button>
                <Button
                    variant="secondary"
                    onPress={() => {
                        inputRef.current?.click();
                    }}
                >
                    External Browse files
                </Button>
            </Flex>
            <Divider size="M" marginTop="size-200" />
            <AllInOneUpload
                repositoryId={repoId}
                apiToken={apiToken}
                targetUploadPath={targetUploadPath}
                files={controlledFiles}
                onFilesChange={setControlledFiles}
                hideUploadButton={true}
                metadataSchema={sampleMetadataSchema}
            />
            <input
                ref={inputRef}
                type="file"
                style={{ display: 'none' }}
                onChange={handleFileInputChange}
                multiple={true}
            />
        </Flex>
    )
}
```

### Propiedad dragOptions {#drag-options-property}

```
dragOptions: {
            allowList: {
                '*': true,          // allow all types to be dragged
                'folder': false,    // except those explicitly set to disallow
                'image/jpeg': false // or those with specific mimeTypes
            },
         }
```

>[!MORELIKETHIS]
>
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integre el Selector de recursos con Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
