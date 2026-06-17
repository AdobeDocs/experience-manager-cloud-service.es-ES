---
title: Integración del Asesor de contenido con Dynamic Media
description: Obtenga información sobre cómo integrar el Asesor de contenido con Dynamic Media para permitir a los usuarios examinar, previsualizar y seleccionar representaciones de Dynamic Media para utilizarlas en sus aplicaciones y flujos de trabajo.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
source-git-commit: 95209a154a0d3208c5fcda8d4117f80d1015d2fe
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---

# Integración con Dynamic Media {#integrate-dynamic-media}

El Asesor de contenido se integra con Dynamic Media para permitir a los usuarios examinar, previsualizar y seleccionar representaciones de Dynamic Media para utilizarlas en sus aplicaciones y flujos de trabajo. Los usuarios pueden seleccionar entre las representaciones, los ajustes preestablecidos de imagen y los recortes inteligentes disponibles, y aplicar los modificadores de Dynamic Media admitidos para personalizar la entrega de recursos. Las secciones siguientes describen cómo procesar la información de representación seleccionada y generar direcciones URL de entrega de Dynamic Media para utilizarlas en la aplicación.

## Generar URL de Dynamic Media con selectedMedia {#build-dynamic-media-urls-selectedmedia}

Cuando un usuario selecciona una representación de Dynamic Media del panel Dynamic Media del Asesor de contenido, la información de representación seleccionada se devuelve en el objeto `selectedMedia`. La aplicación host debe utilizar esta información para generar la URL de entrega de Dynamic Media adecuada.

>[!NOTE]
>
> La aplicación host debe implementar la lógica de generación de URL descrita en esta sección para utilizar representaciones de Dynamic Media seleccionadas desde el Asesor de contenido. La información de representación seleccionada se devuelve como metadatos y no se convierte automáticamente en una dirección URL de envío.

### selectedMedia, objeto {#selectedmedia-object}

El objeto `selectedMedia` se agrega al recurso seleccionado y contiene información sobre la representación de Dynamic Media seleccionada por el usuario.

```javascript
'selectedMedia': Array<{
    base?: string;
    preset?: string;
    smartcrop?: string;
    modifiers?: Array<string>;
    apiStyle?: 'scene7' | 'openapi'
}>;
```

El objeto `selectedMedia` contiene las siguientes propiedades:

| Propiedad | Descripción |
|---|---|
| `base` | Representación base seleccionada. |
| `preset` | El ajuste preestablecido de imagen seleccionado. |
| `smartcrop` | Representación del recorte inteligente seleccionada. |
| `modifiers` | Uno o más modificadores de Dynamic Media agregados por el usuario. |
| `apiStyle` | Indica si la representación seleccionada utiliza la pila de entrega Scene7 (`scene7`) u OpenAPI (`openapi`). |

Por ejemplo, cuando un usuario selecciona una representación base y aplica el modificador `rotate=90`, el objeto devuelto es similar al siguiente:

```javascript
selectedMedia: {
    apiStyle: "scene7",
    base: "scene7company/image",
    modifiers: ["rotate=90"]
}
```

![Ver representaciones de Dynamic Media](assets/content-advisor-dm-renditions.png)

### Acceder a selectedMedia en la llamada de retorno handleSelection {#access-selectedmedia}

Una vez seleccionada una representación, el objeto `selectedMedia` queda disponible en la carga `selectedAssets` devuelta por la llamada de retorno `handleSelection`.

```javascript
async function handleSelection(assets) {

    const dmUrls = [];

    assets.forEach((asset) => {

        if(asset?.selectedMedia){

            const dmUrl = createDMUrlFromSelectedMedia(
                asset.selectedMedia,
                asset
            );

            dmUrls.push({ asset, dmUrl });

        }

    });
}
```

La llamada de retorno se repite en los recursos seleccionados. Para cada recurso que contiene un objeto `selectedMedia`, la aplicación genera una URL de Dynamic Media usando la información de representación seleccionada.

## Generación de una URL de Dynamic Media {#generate-dynamic-media-url}

La siguiente función valida la información de representación seleccionada y determina qué pila de entrega de Dynamic Media se debe utilizar.

```javascript
const DM_OPENAPI_API_STYLE = 'openapi';
const DM_SCENE7_API_STYLE = 'scene7';
const ASSET_REPO_NAME_KEY = 'repo:name';
const ASSET_REPO_ID_KEY = 'repo:id';
const REPO_ID_KEY = 'repo:repositoryId';

export const createDMUrlFromSelectedMedia = (
    selectedMedia,
    repoMetadata
) => {
    if (!selectedMedia || !selectedMedia?.apiStyle) {
        throw new Error(
            'Selected media or api style is not valid'
        );
    }

    if (
        selectedMedia?.apiStyle === DM_OPENAPI_API_STYLE
    ) {
        return buildDMOpenApiUrl(
            selectedMedia,
            repoMetadata
        );
    } else if (
        selectedMedia?.apiStyle === DM_SCENE7_API_STYLE
    ) {
        return buildDMScene7Url(
            selectedMedia,
            repoMetadata
        );
    }
};
```

Esta función realiza las siguientes acciones:

* Valida que la representación seleccionada contenga un valor `apiStyle`.
* Determina si la representación seleccionada utiliza Dynamic Media con las funciones de OpenAPI o Dynamic Media Scene7.
* Llama a la función de generación de URL adecuada en función de la pila de envíos seleccionada.

### Creación de una URL de OpenAPI de Dynamic Media {#build-openapi-url}

La siguiente función genera una URL de API abierta de Dynamic Media utilizando la información de representación y los metadatos del repositorio seleccionados.

```javascript
export const buildDMOpenApiUrl = (
    selectedMedia,
    repoMetadata
) => {
    const { base, preset, smartcrop, modifiers }
        = selectedMedia;

    const dmDomain =
        repoMetadata?.[REPO_ID_KEY]
            .replace('author-', 'delivery-');

    const assetName =
        repoMetadata?.[ASSET_REPO_NAME_KEY];

    const assetId =
        repoMetadata?.[ASSET_REPO_ID_KEY];

    const seoName =
        assetName?.split('.')[0];

    const assetFormat =
        repoMetadata?.['dc:format'];

    let dmUrl;

    if (
        assetFormat &&
        assetFormat.startsWith('video/')
    ) {

        dmUrl =
`https://${dmDomain}/adobe/assets/${assetId}/play`;

    } else {

        dmUrl =
`https://${dmDomain}/adobe/assets/${assetId}/as/${seoName}.avif`;

        if (base) {
        } else if (preset) {
            dmUrl =
`${dmUrl}?preset=${preset}`;
        } else if (smartcrop) {
            dmUrl =
`${dmUrl}?smartcrop=${smartcrop}`;
        }
    }

    if (modifiers && dmUrl) {

        const modifierString =
            getModifierString(selectedMedia);

        if(base) {
            dmUrl =
`${dmUrl}?${modifierString}`;
        } else {
            dmUrl =
`${dmUrl}&${modifierString}`;
        }
    }

    return dmUrl;
};
```

Esta función:

* Recupera la información del repositorio necesaria para construir la dirección URL de envío.
* Crea la dirección URL de entrega base de OpenAPI.
* Añade el ajuste preestablecido o recorte inteligente seleccionado a la dirección URL cuando corresponde.
* Añade cualquier modificador seleccionado por el usuario.
* Devuelve la dirección URL de entrega final de OpenAPI.

Para los recursos de vídeo, la función genera la URL del reproductor de vídeo de Dynamic Media.

### Creación de una URL de Scene7 de Dynamic Media {#build-scene7-url}

La siguiente función genera una URL de Scene7 de Dynamic Media.

```javascript
export const buildDMScene7Url = (
    selectedMedia,
    repoMetadata
) => {

    const {
        base,
        preset,
        smartcrop,
        modifiers
    } = selectedMedia;

    let scene7Domain =
        repoMetadata?.['repo:scene7Domain'];

    const scene7File =
        repoMetadata?.['repo:scene7File'];

    if (!scene7Domain || !scene7File) {
        return null;
    }

    scene7Domain =
        scene7Domain.startsWith('http://')
        ? scene7Domain.replace(
            'http://',
            'https://'
          )
        : scene7Domain;

    scene7Domain =
        scene7Domain?.endsWith('/')
        ? scene7Domain
        : `${scene7Domain}/`;

    let dmUrl;

    if (base) {

        dmUrl =
`${scene7Domain}is/image/${base}`;

    } else if (preset) {

        dmUrl =
`${scene7Domain}is/image/${scene7File}?$${preset}$`;

    } else if (smartcrop) {

        dmUrl =
`${scene7Domain}is/image/${scene7File}:${smartcrop}`;
    }

    if (modifiers && dmUrl) {

        const modifierString =
            getModifierString(selectedMedia);

        if (preset) {
            dmUrl =
`${dmUrl}&${modifierString}`;
        } else {
            dmUrl =
`${dmUrl}?${modifierString}`;
        }
    }

    return dmUrl;
};
```

Esta función:

* Recupera la información de recursos y dominios de Scene7 a partir de los metadatos del repositorio.
* Crea una URL para la representación base, el ajuste preestablecido de imagen o el recorte inteligente seleccionados.
* Añade cualquier modificador seleccionado.
* Devuelve la dirección URL de entrega final de Scene7.

## Generar la cadena de modificadores {#generate-modifiers-string}

La siguiente función de ayuda convierte la matriz de modificadores en una cadena de consulta compatible con URL.

```javascript
export const getModifierString = (
    selectedMedia
) => {

    const { modifiers } = selectedMedia;

    if (modifiers) {

        const modifierString =
            modifiers.length > 0
                ? modifiers.join('&')
                : '';

        return modifierString;
    }

    return null;
};
```

La función combina todos los modificadores seleccionados en una sola cadena separada por el símbolo et (`&`).

Por ejemplo:

```javascript
[
    'rotate=90',
    'width=1200'
]
```

devuelve:

```text
rotate=90&width=1200
```

La cadena generada se anexa a la dirección URL final de Dynamic Media y aplica las transformaciones seleccionadas cuando se envía el recurso.

