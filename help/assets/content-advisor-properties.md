---
title: Propiedades del Asesor de contenido
description: Utilice propiedades para personalizar el modo en que el Asesor de contenido se procesa al integrarlo con la aplicación.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: cd5ec1de-36b0-48a5-95c9-9bd22fac9719
source-git-commit: c92611e4b815e49887e175943b81177e60623067
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 24%

---

# Instalación y propiedades del Asesor de contenido {#content-advisor-installation-properties}

El Asesor de contenido también está disponible para la integración con aplicaciones que no son de Adobe (de terceros), lo que amplía la detección inteligente de recursos más allá de las aplicaciones de Adobe. El mismo conjunto de funciones enriquecidas, que incluye búsqueda con tecnología de IA, recomendaciones según el contexto, detección basada en instrucciones de campaña, acceso a representaciones de Dynamic Media, detección de fragmentos de contenido, filtros y metadatos de recursos, se admite en integraciones de terceros.

## Requisitos previos{#prereqs}

Debe asegurarse de que dispone de los siguientes métodos de comunicación:

* La aplicación host se está ejecutando en HTTPS.
* No puede ejecutar la aplicación en `localhost`. Si desea integrar el Asesor de contenido en su equipo local, debe crear un dominio personalizado, por ejemplo `[https://<your_campany>.localhost.com:<port_number>]`, y agregar este dominio personalizado en `redirectUrl list`.
* Puede configurar y añadir clientID a la variable de entorno de AEM as a Cloud Service con el `imsClientId` correspondiente.
<!--
* You can configure and add `ADOBE_PROVIDED_CLIENT_ID` into the AEM Cloud Service environment variable with the respective `imsClientId`.
![Asset Selector IMS Client id environment](assets/asset-selector-ims-client-id-env.png)
-->
* La lista de ámbitos de IMS debe definirse en la configuración del entorno.
* La URL de la aplicación está en la lista de URL de redirección permitidas del cliente de IMS.
* El flujo de inicio de sesión de IMS se configura y se representa mediante una ventana emergente en el explorador web. Por lo tanto, las ventanas emergentes deben habilitarse o permitirse en el explorador de destino.

Utilice los requisitos previos anteriores si necesita el flujo de trabajo de autenticación IMS del Asesor de contenido. Alternativamente, si ya está autenticado con el flujo de trabajo de IMS, puede añadir la información de IMS en su lugar.

>[!IMPORTANT]
>
> Este repositorio está diseñado para servir como documentación suplementaria que describa las API disponibles y ejemplos de uso para la integración del Asesor de contenido. Antes de intentar instalar o utilizar el Asesor de contenido, asegúrese de que su organización dispone de acceso al Asesor de contenido como parte del perfil de as a Cloud Service de Experience Manager Assets. Si no se le ha proporcionado acceso, no puede integrar ni utilizar estos componentes. Para solicitar el aprovisionamiento, el administrador del programa debe enviar un vale de asistencia marcado como P2 a Admin Console e incluir la siguiente información:
>
>* Nombres de dominio en los que está alojada la aplicación integradora.
>* Después del aprovisionamiento, se proporcionará a su organización `imsClientId`, `imsScope` y un `redirectUrl` correspondientes a los entornos solicitados que son esenciales para la configuración del Asesor de contenido. Sin estas propiedades válidas, no se pueden ejecutar los pasos de instalación.

## Instalación {#content-advisor-installation}

El Asesor de contenido está disponible a través de la CDN de ESM (por ejemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) y la versión [UMD](https://github.com/umdjs/umd).

En navegadores que utilizan la **Versión de UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

En navegadores con compatibilidad con `import maps` con **Versión de CDN de ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

En la federación de módulos Deno/Webpack mediante **Versión de CDN de ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

## Propiedades del Asesor de contenido {#content-advisor-propertiess}

Puede utilizar las propiedades del Asesor de contenido para personalizar la forma en que se procesa el Asesor de contenido. En la tabla siguiente se enumeran las propiedades que puede utilizar para personalizar y utilizar el Asesor de contenido.

| Propiedad | Tipo | Requerido | Predeterminado | Descripción |
|---|---|---|---|---|
| *carril* | Booleano | No | Falso | Si se marca `true`, el Asesor de contenido se representa en una vista del carril izquierdo. Si está marcado `false`, el Asesor de contenido se procesará en la vista modal. |
| *imsOrg* | Cadena | Sí | | ID del sistema Identity Management de Adobe (IMS) asignado durante el aprovisionamiento [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para su organización. La clave `imsOrg` es necesaria para autenticar si la organización a la que accede se encuentra en Adobe IMS o no. |
| *imsToken* | Cadena | No | | Token de portador de IMS utilizado para la autenticación. `imsToken` es necesario si utiliza una aplicación [!DNL Adobe] para la integración. |
| *apiKey* | Cadena | No | | Clave de API utilizada para acceder al servicio AEM Discovery. `apiKey` es necesario si utiliza una integración de aplicación [!DNL Adobe]. |
| *externalBrief* | Cadena | No | | Permite cargar un documento de información de campaña para descubrir recursos relevantes sin introducir manualmente las palabras clave de búsqueda. El Asesor de contenido analiza la información de la información de la campaña para comprender la intención de la campaña y recomienda los activos relevantes disponibles en los AEM Assets. |
| *filterSchema* | Matriz | No | | Modelo que se utiliza para configurar las propiedades del filtro. Esto resulta útil cuando desea limitar ciertas opciones de filtro en el Asesor de contenido. |
| *filterFormProps* | Objeto | No | | Especifique las propiedades del filtro que debe utilizar para restringir la búsqueda. ¡Por! Por ejemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | No |                 | Especifique el Assets seleccionado cuando se represente el Asesor de contenido. Se requiere una matriz de objetos que contenga una propiedad id de los recursos. Por ejemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Un recurso debe estar disponible en el directorio actual. Si necesita utilizar un directorio diferente, proporcione un valor para la propiedad de `path` también. |
| *acvConfig* | Objeto | No | | Propiedad de vista de colección de recursos que contiene un objeto con una configuración personalizada para anular los valores predeterminados. Además, esta propiedad se usa con la propiedad `rail` para habilitar la vista de carril del visor de recursos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | No |                 | Si las traducciones OOTB no son suficientes para las necesidades de la aplicación, puede exponer una interfaz a través de la cual puede pasar sus propios valores localizados personalizados mediante la propiedad `i18nSymbols`. Al pasar un valor a través de esta interfaz, se anulan las traducciones predeterminadas proporcionadas y, en su lugar, se utilizan las suyas. Para realizar la anulación, debe pasar un objeto [Descriptor del mensaje](https://formatjs.io/docs/react-intl/api/#message-descriptor) válido a la clave de `i18nSymbols` que desee anular. |
| *intl* | Objeto | No | | El Asesor de contenido proporciona traducciones OOTB predeterminadas. Puede seleccionar el idioma de traducción proporcionando una cadena de configuración regional válida a través del prop `intl.locale`. Por ejemplo: `intl={{ locale: "es-es" }}` </br></br> Las cadenas de configuración regional admitidas siguen la norma [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para la representación de nombres de estándares de idiomas. </br></br> Lista de configuraciones regionales admitidas: Inglés - &#39;en-us&#39; (predeterminado) Español - &#39;es-es&#39; Alemán - &#39;de-de&#39; Francés - &#39;fr-fr&#39; Italiano - &#39;it-it&#39; Japonés - &#39;ja-jp&#39; Coreano - &#39;ko-kr&#39; Portugués - &#39;pt-br&#39; Chino (tradicional) - &#39;zh-cn&#39; Chino (Taiwán) - &#39;zh-tw&#39; |
| *repositoryId* | Cadena | No | &#39;&#39; | Repositorio desde el que el Asesor de contenido carga el contenido. |
| *additionalAemSolutions* | `Array<string>` | No | [ ] | Permite añadir una lista de repositorios de AEM adicionales. Si no se proporciona información en esta propiedad, solo se tienen en cuenta los repositorios de la biblioteca de medios o de AEM Assets. |
| *hideTreeNav* | Booleano | No |  | Especifica si se muestra u oculta la barra lateral de navegación del árbol de recursos. Solo se utiliza en la vista modal y, por lo tanto, no hay ningún efecto de esta propiedad en la vista de carril. |
| *onDrop* | Función | No | | La funcionalidad al soltar se utiliza para arrastrar un recurso y soltarlo en un área de colocación designada. Permite interfaces de usuario interactivas en las que los recursos se pueden mover y procesar sin problemas. |
| *dropOptions* | `{allowList?: Object}` | No | | Configura las opciones de colocación mediante &#39;allowList&#39;. |
| *tema* | Cadena | No | Predeterminado | Aplicar tema a la aplicación Asesor de contenido entre `default` y `express`. También admite `@react-spectrum/theme-express`. |
| *handleSelection* | Función | No | | Se invoca con la matriz de elementos de recurso cuando se seleccionan los recursos y se hace clic en el botón `Select` en el modal. Esta función solo se invoca en la vista modal. Para la vista de carril, utilice las funciones `handleAssetSelection` o `onDrop`. Ejemplo: <pre>handleSelection=(recursos: Asset[])=> {...}</pre> Consulte [selección de recursos](/help/assets/content-advisor-customization.md#selection-of-assets) para obtener detalles. |
| *handleAssetSelection* | Función | No | | Se invoca con una matriz de elementos cuando los recursos se seleccionan o no. Esto resulta útil cuando desea escuchar los recursos a medida que el usuario los selecciona. Ejemplo: <pre>handleAssetSelection=(assets: Asset[])=> {...}</pre> Consulte [selección de recursos](/help/assets/content-advisor-customization.md#selection-of-assets) para obtener detalles. |
| *onClose* | Función | No | | Se invoca cuando se pulsa el botón `Close` en la vista modal. Esto solo se llama en la vista `modal` y se ignora en la vista `rail`. |
| *onFilterSubmit* | Función | No | | Se invoca con elementos de filtro cuando el usuario cambia criterios de filtro diferentes. |
| *selectionType* | Cadena | No | Soltero/a | Configuración para selección de `single` o `multiple` de recursos a la vez. |
| *dragOptions.lista de permitidos* | booleano | No | | La propiedad se utiliza para permitir o denegar el arrastre de recursos que no se pueden seleccionar. Ver [propiedad dragOptions](/help/assets/content-advisor-customization.md#drag-options-property) |
| *aemTierType* | Cadena | No |  | Permite seleccionar si desea mostrar los recursos del nivel de entrega, del nivel de creación o de ambos. <br><br> Sintaxis: `aemTierType: "author"  "delivery"` <br><br> Por ejemplo, si se usan ambos `["author","delivery"]`, el conmutador de repositorios mostrará opciones para la creación y la entrega. |
| *handleNavigateToAsset* | Función | No | | Es una función de llamada de retorno para gestionar la selección de un recurso. |
| *noWrap* | Booleano | No | | La propiedad *noWrap* evita que el Asesor de contenido se ajuste en un cuadro de diálogo. Si no se menciona esta propiedad, se representa la *vista del cuadro de diálogo* de forma predeterminada. |
| *dialogSize* | S, M, L, pantalla completa, pantalla completa | Cadena | Opcional | Puede controlar el diseño especificando su tamaño con las opciones dadas. |
| *colorScheme* | Cadena (claro, oscuro) | No | | Esta propiedad se utiliza para establecer la temática de una aplicación de Asesor de contenido. Puede elegir entre tema claro u oscuro. |
| *filterRepoList* | Función | No | | Función que recibe la lista de repositorios y devuelve una lista filtrada. |
| *expiryOptions* | Función | | | Puede usar entre las dos propiedades siguientes: **getExpiryStatus**, que proporciona el estado de un recurso caducado. La función devuelve `EXPIRED`, `EXPIRING_SOON` o `NOT_EXPIRED` según la fecha de caducidad del recurso que proporcione. Consulte [personalizar recursos caducados](/help/assets/content-advisor-customization.md#customize-expired-assets). Además, puede usar **allowSelectionAndDrag**, en el que el valor de la función puede ser `true` o `false`. Cuando el valor se establece en `false`, el recurso caducado no se puede seleccionar ni arrastrar al lienzo. |
| *showToast* | | No | | Permite al Asesor de contenido mostrar un mensaje de mensaje personalizado para el recurso caducado. |
| *uploadConfig* | Objeto | | | Es un objeto que contiene una configuración personalizada para la carga. Consulte [configuración de carga](#content-advisor-customization.md#upload-config) para ver la facilidad de uso. |
| *uploadConfig* > *metadataSchema* | Matriz | No | | Esta propiedad está anidada en la propiedad `uploadConfig`. Añada una matriz de campos que proporcione para recopilar metadatos del usuario. Con esta propiedad, también puede utilizar metadatos ocultos que se asignan automáticamente a un recurso, pero que no son visibles para el usuario. |
| *uploadConfig* > *onMetadataFormChange* | Función Callback | No | | Esta propiedad está anidada en la propiedad `uploadConfig`. Consta de `property` y `value`. `Property` es igual a *mapToProperty* del campo pasado desde *metadataSchema* cuyo valor se está actualizando. Mientras que `value` es igual al nuevo valor proporcionado como entrada. |
| *uploadConfig* > *targetUploadPath* | Cadena |  | `"/content/dam"` | Esta propiedad está anidada en la propiedad `uploadConfig`. La ruta de carga de destino para los archivos que tiene el valor predeterminado de raíz del repositorio de recursos. |
| *uploadConfig* > *hideUploadButton* | Booleano | | Falso | Garantiza si el botón de carga interno debe estar oculto o no. Esta propiedad está anidada en la propiedad `uploadConfig`. |
| *uploadConfig* > *onUploadStart* | Función | No |  | Es una función de llamada de retorno que se utiliza para pasar el origen de carga entre Dropbox, OneDrive o local. La sintaxis es `(uploadInfo: UploadInfo) => void`. Esta propiedad está anidada en la propiedad `uploadConfig`. |
| *uploadConfig* > *importSettings* | Función | | | Habilita la compatibilidad para importar recursos de origen de terceros. `sourceTypes` utiliza una matriz de los orígenes de importación que desea habilitar. Las fuentes compatibles son Onedrive y Dropbox. La sintaxis es `{ sourceTypes?: ImportSourceType[]; apiKey?: string; }`. Además, esta propiedad está anidada en la propiedad `uploadConfig`. |
| *uploadConfig* > *onUploadComplete* | Función | No | | Es una función de llamada de retorno que se utiliza para pasar el estado de carga del archivo entre correcto, fallido o duplicado. La sintaxis es `(uploadStats: UploadStats) => void`. Además, esta propiedad está anidada en la propiedad `uploadConfig`. |
| *uploadConfig* > *onFilesChange* | Función | No | | Esta propiedad está anidada en la propiedad `uploadConfig`. Es una función de llamada de retorno que se utiliza para mostrar el comportamiento de carga cuando se cambia un archivo. Pasa la nueva matriz de archivos pendientes de carga y el tipo de origen de la carga. El tipo de Source puede ser nulo en caso de error. La sintaxis es `(newFiles: File[], uploadType: UploadType) => void` |
| *uploadConfig* > *uploadPlaceholder* | Cadena | | | Es una imagen de marcador de posición que reemplaza el formulario de metadatos cuando se inicia una carga del recurso. La sintaxis es `{ href: string; alt: string; }`. Además, esta propiedad está anidada en la propiedad `uploadConfig`. |
| *featureSet* | Matriz | Cadena | | La propiedad `featureSet:[ ]` se usa para habilitar o deshabilitar una funcionalidad concreta en la aplicación Asesor de contenido. Para habilitar el componente o una función, puede pasar un valor de cadena en la matriz o dejar la matriz vacía para deshabilitar las funciones agregadas y simplemente tener la funcionalidad base. Por ejemplo, si desea habilitar la funcionalidad de carga en el Asesor de contenido, utilice la sintaxis `featureSet:["upload"]`. Del mismo modo, puede utilizar `featureSet:["content-fragments"]` para habilitar los fragmentos de contenido en el Asesor de contenido. Para usar varias características juntas, la sintaxis es featureSet:[&quot;upload&quot;, &quot;content-fragments&quot;]. |

<!--
| *selectedRendition* | Object | | | This property allows users to define and control which renditions of an asset are displayed when the panel is accessed. This customization enhances user experience by filtering out unnecessary renditions and showcasing only the most relevant renditions. For example, `CopyUrlHref` allows you to use Dynamic Media renditions in your Asset Selector application (delivery URL). |
| *featureSet* | Array | String | | The `featureSet:[ ]` property is used to enable or disable a particular functionaly in the Asset Selector application. To enable the component or a feature, you can pass a string value in the array or leave the array empty to disable that component. For example, you want to enable upload functionality in the Asset Selector, use the syntax `featureSet:[0:"upload"]`. Similarly, you can use `featureSet:[0:"collections"]` to enable collections in the Asset Selector. Addidionally, use `featureSet:[0:"detail-panel"]` to enable [details panel](overview-asset-selector.md#asset-details-and-metadata) of an asset. Also, `featureSet:[0:"dm-renditions"]` to show Dynamic Media renditions of an asset.|
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](/help/assets/asset-selector-customization.md#customize-expired-assets). |
-->

### ImsAuthProps {#ims-auth-props}

Las propiedades de `ImsAuthProps` definen la información de autenticación y el flujo que utiliza el Asesor de contenido para obtener un `imsToken`. Al establecer estas propiedades, puede controlar cómo debe comportarse el flujo de autenticación y registrar los agentes de escucha para varios eventos de autenticación.

| Nombre de la propiedad | Descripción |
|---|---|
| `imsClientId` | Valor de cadena que representa el ID de cliente de IMS utilizado con fines de autenticación. Este valor lo proporciona Adobe y es específico de su organización de Adobe AEM CS. |
| `imsScope` | Describe los ámbitos utilizados en la autenticación. Los ámbitos determinan el nivel de acceso que la aplicación tiene a los recursos de su organización. Los ámbitos múltiples se pueden separar con comas. |
| `redirectUrl` | Representa la dirección URL a la que se redirige al usuario después de la autenticación. Este valor se suele establecer en la dirección URL actual de la aplicación. Si no se proporciona `redirectUrl`, `ImsAuthService` usa la redirectUrl utilizada para registrar `imsClientId` |
| `modalMode` | Un booleano que indica si el flujo de autenticación debe mostrarse en un modal (emergente) o no. Si se establece en `true`, el flujo de autenticación se mostrará en una ventana emergente. Si se establece en `false`, el flujo de autenticación se mostrará en una recarga de página completa. _Note :_para un mejor UX, puede controlar dinámicamente este valor si el usuario tiene deshabilitada la ventana emergente del navegador. |
| `onImsServiceInitialized` | Una función de llamada de retorno que se llama cuando se inicializa el servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `service`, que es un objeto que representa el servicio IMS de Adobe. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obtener más detalles. |
| `onAccessTokenReceived` | Una función de llamada de retorno que se llama cuando se recibe un `imsToken` del servicio de autenticación IMS de Adobe. Esta función toma un parámetro, `imsToken`, que es una cadena que representa el token de acceso. |
| `onAccessTokenExpired` | Función de llamada de retorno a la que se llama cuando ha caducado un token de acceso. Esta función se utiliza generalmente para almacenar en déclencheur un nuevo flujo de autenticación para obtener un nuevo token de acceso. |
| `onErrorReceived` | Función de llamada de retorno a la que se llama cuando se produce un error durante la autenticación. Esta función toma dos parámetros: el tipo de error y el mensaje de error. El tipo de error es una cadena que representa el tipo de error y el mensaje de error es una cadena que representa el mensaje de error. |

### ImsAuthService {#ims-auth-service}

La clase `ImsAuthService` administra el flujo de autenticación para el Asesor de contenido. Es responsable de obtener un `imsToken` del servicio de autenticación IMS de Adobe. `imsToken` se usa para autenticar al usuario y autorizar el acceso a [!DNL Adobe Experience Manager] como un repositorio de Assets de [!DNL Cloud Service]. ImsAuthService usa las propiedades `ImsAuthProps` para controlar el flujo de autenticación y registrar agentes de escucha para varios eventos de autenticación. Puede utilizar la práctica función [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar la instancia de _ImsAuthService_ con el Asesor de contenido. Las funciones siguientes están disponibles en la clase `ImsAuthService`. Sin embargo, si está utilizando la función _registerAssetsSelectorsAuthService_, no necesita llamar a estas funciones directamente.

| Nombre de función | Descripción |
|---|---|
| `isSignedInUser` | Determina si el usuario ha iniciado sesión en el servicio y devuelve un valor booleano en consecuencia. |
| `getImsToken` | Recupera la autenticación `imsToken` del usuario que ha iniciado sesión actualmente, que se puede utilizar para autenticar solicitudes en otros servicios como la generación de _representación de recursos. |
| `signIn` | Inicia el proceso de inicio de sesión del usuario. Esta función utiliza `ImsAuthProps` para mostrar la autenticación en una ventana emergente o en una recarga de página completa |
| `signOut` | Cierra la sesión del usuario del servicio, invalidando su token de autenticación y obligándole a iniciar sesión de nuevo para acceder a los recursos protegidos. Al invocar esta función, se volverá a cargar la página actual. |
| `refreshToken` | Actualiza el token de autenticación del usuario que ha iniciado sesión, lo que evita que caduque y garantiza un acceso ininterrumpido a los recursos protegidos. Devuelve un nuevo token de autenticación que puede utilizarse para solicitudes posteriores. |

### contentFragmentSelectorProps {#content-fragment-selector-properties}

`contentFragmentSelectorProps` le permite configurar cómo se accede y se muestran los fragmentos de contenido dentro del Asesor de contenido. Al habilitar la característica de fragmentos de contenido en `featureSet` y proporcionar la configuración necesaria, puede integrar sin problemas la selección de fragmentos de contenido junto con los recursos. Esto permite a los usuarios examinar, buscar y seleccionar fragmentos de contenido dentro de la misma interfaz unificada, lo que garantiza una experiencia de selección de contenido coherente en todos los recursos y el contenido estructurado.

```
const assetSelectorProps = {
     featureSet: [
       'upload',            /* Include upload or other featureSet values to ensure no missing functionality */
       'content-fragments', /* Content Fragments pill will be shown */
     ],
     contentFragmentSelectorProps: {
       /* Configures the Content Fragments Pill experience */
       /* ...props @aem-sites/content-fragment-selector MFE supports */
    }
}

<AssetSelector {...assetSelectorProps} />
```

En `contentFragmentSelectorProps`, puede mencionar cualquiera de las propiedades disponibles en [Propiedades del selector de fragmentos de contenido](/help/headless/content-fragment-selector/properties.md).

Para obtener información sobre cómo integrar el Asesor de contenido con aplicaciones de Angular, React y JavaScript, consulte [Ejemplos de integración del Asesor de contenido](https://github.com/adobe/aem-assets-selectors-mfe-examples/tree/consolidate-docs-to-experience-league/examples).


