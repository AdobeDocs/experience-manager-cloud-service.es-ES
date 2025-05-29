---
title: Propiedades del Selector de recursos para la personalización
description: Utilice el selector de recursos para buscar y recuperar metadatos y representaciones de recursos dentro de la aplicación.
role: Admin, User
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: 89a7346f5b6bc1d65524c5ead935aa4a2a764ebb
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 41%

---

# Propiedades del Selector de recursos {#asset-selector-properties}

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

Puede utilizar las propiedades del Selector de recursos para personalizar la forma en que se procesa el Selector de recursos. En la tabla siguiente se enumeran las propiedades que puede utilizar para personalizar y utilizar el Selector de recursos.

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| *carril* | Booleano | No | Falso | Si se marca `true`, el Selector de recursos se representa en una vista del carril izquierdo. Si está marcado como `false`, el Selector de recursos se representa en la vista modal. |
| *imsOrg* | Cadena | Sí | | ID del sistema Identity Management de Adobe (IMS) asignado durante el aprovisionamiento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para su organización. La clave `imsOrg` es necesaria para autenticar si la organización a la que accede se encuentra en Adobe IMS o no. |
| *imsToken* | Cadena | No | | Token de portador de IMS utilizado para la autenticación. `imsToken` es necesario si utiliza una aplicación [!DNL Adobe] para la integración. |
| *apiKey* | Cadena | No | | Clave de API utilizada para acceder al servicio AEM Discovery. `apiKey` es necesario si utiliza una integración de aplicación [!DNL Adobe]. |
| *filterSchema* | Matriz | No | | Modelo que se utiliza para configurar las propiedades del filtro. Esto resulta útil cuando desea limitar ciertas opciones de filtro en el Selector de recursos. |
| *Props filterForm* | Objeto | No | | Especifique las propiedades del filtro que debe utilizar para restringir la búsqueda. ¡Por! Por ejemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | No |                 | Especificar los recursos seleccionados cuando se procese el selector de recursos. Se requiere una matriz de objetos que contenga una propiedad id de los recursos. Por ejemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Un recurso debe estar disponible en el directorio actual. Si necesita utilizar un directorio diferente, proporcione un valor para la propiedad de `path` también. |
| *acvConfig* | Objeto | No | | Propiedad de vista de colección de recursos que contiene un objeto con una configuración personalizada para anular los valores predeterminados. Además, esta propiedad se usa con la propiedad `rail` para habilitar la vista de carril del visor de recursos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Si las traducciones OOTB no son suficientes para las necesidades de la aplicación, puede exponer una interfaz a través de la cual puede pasar sus propios valores localizados personalizados mediante la propiedad `i18nSymbols`. Al pasar un valor a través de esta interfaz, se anulan las traducciones predeterminadas proporcionadas y, en su lugar, se utilizan las suyas. Para realizar la anulación, debe pasar un objeto [Descriptor del mensaje](https://formatjs.io/docs/react-intl/api/#message-descriptor) válido a la clave de `i18nSymbols` que desee anular. |
| *intl* | Objeto | No | | El Selector de recursos proporciona traducciones OOTB predeterminadas. Puede seleccionar el idioma de traducción proporcionando una cadena de configuración regional válida a través del prop `intl.locale`. Por ejemplo: `intl={{ locale: "es-es" }}` </br></br> Las cadenas de configuración regional admitidas siguen los [Códigos ISO 639](https://www.iso.org/iso-639-language-codes.html) para la representación de los estándares de nombres de idiomas. </br></br> Lista de configuraciones regionales admitidas: Inglés - &#39;en-us&#39; (predeterminado) Español - &#39;es-es&#39; Alemán - &#39;de-de&#39; Francés - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonés - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portugués - &#39;pt-br&#39; Chino (tradicional) - &#39;zh-cn&#39; Chino (Taiwán) - &#39;zh-tw&#39; |
| *repositoryId* | Cadena | No | &#39;&#39; | Repositorio desde el que el Selector de recursos carga el contenido. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Permite añadir una lista de repositorios de AEM adicionales. Si no se proporciona información en esta propiedad, solo se tienen en cuenta los repositorios de la biblioteca de medios o de AEM Assets. |
| *hideTreeNav* | Booleano | No |  | Especifica si se muestra u oculta la barra lateral de navegación del árbol de recursos. Solo se utiliza en la vista modal y, por lo tanto, no hay ningún efecto de esta propiedad en la vista de carril. |
| *onDrop* | Función | No | | La funcionalidad al soltar se utiliza para arrastrar un recurso y soltarlo en un área de colocación designada. Permite interfaces de usuario interactivas en las que los recursos se pueden mover y procesar sin problemas. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura las opciones de colocación mediante &#39;allowList&#39;. |
| *colorScheme* | Cadena | No | | Configurar tema (`light` o `dark`) para el Selector de recursos. |
| *Tema* | Cadena | No | Predeterminado | Aplicar tema a la aplicación Selector de recursos entre `default` y `express`. También admite `@react-spectrum/theme-express`. |
| *handleSelection* | Función | No | | Se invoca con la matriz de elementos de recurso cuando se seleccionan los recursos y se hace clic en el botón `Select` en el modal. Esta función solo se invoca en la vista modal. Para la vista de carril, utilice las funciones `handleAssetSelection` o `onDrop`. Ejemplo: <pre>handleSelection=(recursos: Asset[])=> {...}</pre> Consulte [selección de recursos](/help/assets/asset-selector-customization.md#selection-of-assets) para obtener detalles. |
| *handleAssetSelection* | Función | No | | Se invoca con una matriz de elementos cuando los recursos se seleccionan o no. Esto resulta útil cuando desea escuchar los recursos a medida que el usuario los selecciona. Ejemplo: <pre>handleSelection=(recursos: Asset[])=> {...}</pre> Consulte [selección de recursos](/help/assets/asset-selector-customization.md#selection-of-assets) para obtener detalles. |
| *onClose* | Función | No | | Se invoca cuando se pulsa el botón `Close` en la vista modal. Esto solo se llama en la vista `modal` y se ignora en la vista `rail`. |
| *onFilterSubmit* | Función | No | | Se invoca con elementos de filtro cuando el usuario cambia criterios de filtro diferentes. |
| *selectionType* | Cadena | No | Soltero/a | Configuración para selección de `single` o `multiple` de recursos a la vez. |
| *dragOptions.lista de permitidos* | booleano | No | | La propiedad se utiliza para permitir o denegar el arrastre de recursos que no se pueden seleccionar. Ver [propiedad dragOptions](/help/assets/asset-selector-customization.md#drag-options-property) |
| *aemTierType* | Cadena | No |  | Permite seleccionar si desea mostrar los recursos del nivel de entrega, del nivel de creación o de ambos. Sintaxis <br><br>: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Por ejemplo, si se usan `["author","delivery"]`, el conmutador de repositorios mostrará opciones de autor y envío. |
| *handleNavigateToAsset* | Función | No | | Es una función de llamada de retorno para gestionar la selección de un recurso. |
| *noWrap* | Booleano | No | | La propiedad *noWrap* ayuda a procesar el Selector de recursos en el panel de raíl lateral. Si no se menciona esta propiedad, se representa la *vista del cuadro de diálogo* de forma predeterminada. |
| *dialogSize* | adquisición en pequeña, mediana, grande, pantalla completa o pantalla completa | Cadena | Opcional | Puede controlar el diseño especificando su tamaño con las opciones dadas. |
| *colorScheme* | Claro u oscuro | No | | Esta propiedad se utiliza para establecer la temática de una aplicación Selector de recursos. Puede elegir entre tema claro u oscuro. |
| *filterRepoList* | Función | No |  | Puede utilizar la función de devolución de llamada `filterRepoList` que llama al repositorio de Experience Manager y devuelve una lista filtrada de repositorios. |
| *expiryOptions* | Función | | | Puede usar entre las dos propiedades siguientes: **getExpiryStatus**, que proporciona el estado de un recurso caducado. La función devuelve `EXPIRED`, `EXPIRING_SOON` o `NOT_EXPIRED` según la fecha de caducidad del recurso que proporcione. Consulte [personalizar recursos caducados](/help/assets/asset-selector-customization.md#customize-expired-assets). Además, puede usar **allowSelectionAndDrag**, en el que el valor de la función puede ser `true` o `false`. Cuando el valor se establece en `false`, el recurso caducado no se puede seleccionar ni arrastrar al lienzo. |
| *showToast* | | No | | Permite que el Selector de recursos muestre un mensaje de mensaje personalizado para el recurso caducado. |
| *metadataSchema* | Matriz | No | | Añada una matriz de campos que proporcione para recopilar metadatos del usuario. Con esta propiedad, también puede utilizar metadatos ocultos que se asignan automáticamente a un recurso, pero que no son visibles para el usuario. |
| *onMetadataFormChange* | Función Callback | No | | Consta de `property` y `value`. `Property` es igual a *mapToProperty* del campo pasado desde *metadataSchema* cuyo valor se está actualizando. Mientras que `value` es igual al nuevo valor proporcionado como entrada. |
| *targetUploadPath* | Cadena |  | `"/content/dam"` | La ruta de carga de destino para los archivos que tiene el valor predeterminado de raíz del repositorio de recursos. |
| *hideUploadButton* | Booleano | | Falso | Garantiza si el botón de carga interno debe estar oculto o no. |
| *onUploadStart* | Función | No |  | Es una función de llamada de retorno que se utiliza para pasar el origen de carga entre Dropbox, OneDrive o local. La sintaxis es `(uploadInfo: UploadInfo) => void` |
| *importSettings* | Función | | | Habilita la compatibilidad para importar recursos de origen de terceros. `sourceTypes` utiliza una matriz de los orígenes de importación que desea habilitar. Las fuentes compatibles son Onedrive y Dropbox. La sintaxis es `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }` |
| *onUploadComplete* | Función | No | | Es una función de llamada de retorno que se utiliza para pasar el estado de carga del archivo entre correcto, fallido o duplicado. La sintaxis es `(uploadStats: UploadStats) => void` |
| *onFilesChange* | Función | No | | Es una función de llamada de retorno que se utiliza para mostrar el comportamiento de carga cuando se cambia un archivo. Pasa la nueva matriz de archivos pendientes de carga y el tipo de origen de la carga. El tipo de Source puede ser nulo en caso de error. La sintaxis es `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadingPlaceholder* | Cadena | | | Es una imagen de marcador de posición que reemplaza el formulario de metadatos cuando se inicia una carga del recurso. La sintaxis es `{ href: string; alt: string; } ` |
| *uploadConfig* | Objeto | | | Es un objeto que contiene una configuración personalizada para la carga. |
| *featureSet* | Matriz | Cadena | | La propiedad `featureSet:[ ]` se usa para habilitar o deshabilitar una funcionalidad en particular en la aplicación Selector de recursos. Para habilitar el componente o una función, puede pasar un valor de cadena en la matriz o dejar la matriz vacía para deshabilitar ese componente.  Por ejemplo, si desea habilitar la funcionalidad de carga en el Selector de recursos, utilice la sintaxis `featureSet:[0:"upload"]`. Del mismo modo, puede usar `featureSet:[0:"collections"]` para habilitar colecciones en el Selector de recursos. Además, use `featureSet:[0:"detail-panel"]` para habilitar [el panel de detalles](overview-asset-selector.md#asset-details-and-metadata) de un recurso. Para usar estas características juntas, la sintaxis es `featureSet:["upload", "collections", "detail-panel"]`. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

>[!MORELIKETHIS]
>
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Integre el Selector de recursos con Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Integrar el Selector de recursos con aplicaciones de terceros](/help/assets/integrate-asset-selector-non-adobe-app.md)
