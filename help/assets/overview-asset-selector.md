---
title: Selector de recursos para [!DNL Adobe Experience Manager] como un [!DNL Cloud Service]
description: Utilice el Selector de recursos para buscar, buscar y recuperar metadatos y representaciones de recursos en la aplicación.
role: Admin, User
exl-id: 62b0b857-068f-45b7-9018-9c59fde01dc3
source-git-commit: 0b8c345efa4c8f59b423644944ca2a6f8d54cbb4
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 34%

---

# Selector de recursos de Micro-Frontend {#Overview}

El Selector de recursos de Micro-Frontend proporciona una interfaz de usuario que se integra fácilmente con el repositorio de [!DNL Experience Manager Assets] para poder examinar o buscar recursos digitales disponibles en el repositorio y utilizarlos en la experiencia de creación de la aplicación.

La interfaz de usuario de Micro-Frontend está disponible en la experiencia de su aplicación mediante el paquete Selector de recursos. Las actualizaciones del paquete se importan automáticamente y el último Selector de recursos implementado se carga automáticamente en la aplicación.

![Información general](assets/overview.png)

El Selector de recursos ofrece muchas ventajas, como las siguientes:

* Facilidad de integración con cualquiera de las aplicaciones de [Adobe](/help/assets/integrate-asset-selector-adobe-app.md) o [que no son de Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md) que usan la biblioteca JavaScript de Vanilla.
* Son fáciles de mantener, ya que las actualizaciones del paquete del Selector de recursos se implementan automáticamente en el Selector de recursos disponible para su aplicación. No se requieren actualizaciones dentro de la aplicación para cargar las modificaciones más recientes.
* Facilidad de personalización, ya que hay propiedades disponibles que controlan la visualización del Selector de recursos en la aplicación.
* Filtros personalizados, de búsqueda de texto completo y listos para usar para navegar rápidamente a los recursos y utilizarlos en la experiencia de creación.
* Capacidad para cambiar repositorios dentro de una organización IMS para la selección de recursos.
* Capacidad para ordenar recursos por nombre, dimensiones y tamaño y verlos en las vistas Lista, Cuadrícula, Galería o Cascada.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Requisitos previos{#prereqs}

Debe asegurarse de que dispone de los siguientes métodos de comunicación:

* La aplicación se está ejecutando en HTTPS.
* La dirección URL de la aplicación está en la lista de permitidos de direcciones URL de redireccionamiento del cliente IMS.
* El flujo de inicio de sesión de IMS se configura y se representa mediante una ventana emergente en el explorador web. Por lo tanto, las ventanas emergentes deben habilitarse o permitirse en el explorador de destino.

Utilice los requisitos previos anteriores si necesita el flujo de trabajo de autenticación IMS del Selector de recursos. Alternativamente, si ya está autenticado con el flujo de trabajo de IMS, puede añadir la información de IMS en su lugar.

**Ver más**

* [Integración del Selector de recursos con una aplicación de Adobe](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integración del Selector de recursos con una aplicación que no sea de Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integrar las API de apertura de Dynamic Media Selector de recursos](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!IMPORTANT]
>
> Este repositorio está diseñado para servir como documentación suplementaria que describa las API disponibles y ejemplos de uso para la integración del Selector de recursos. Antes de intentar instalar o utilizar el Selector de recursos, asegúrese de que su organización tenga acceso al Selector de recursos como parte del perfil as a Cloud Service de Experience Manager Assets. Si no se ha aprovisionado, no puede integrar ni utilizar estos componentes. Para solicitar el aprovisionamiento, el administrador del programa debe enviar un ticket de asistencia marcado como P2 al Admin Console e incluir la siguiente información:
>
>* Nombres de dominio en los que está alojada la aplicación integradora.
>* Después del aprovisionamiento, se proporcionará a su organización `imsClientId`, `imsScope` y un `redirectUrl` correspondientes a los entornos solicitados que son esenciales para la configuración del Selector de recursos. Sin estas propiedades válidas, no se pueden ejecutar los pasos de instalación.

## Instalación {#installation}

El Selector de recursos está disponible a través de la CDN de ESM (por ejemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) y la versión [UMD](https://github.com/umdjs/umd).

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

## Uso del Selector de recursos {#using-asset-selector}

Una vez configurado el Selector de recursos y autenticado para usar el Selector de recursos con su aplicación [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], puede seleccionar recursos o realizar otras operaciones para buscar los recursos dentro del repositorio.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Ocultar/Mostrar panel](#hide-show-panel)
* **B**: [Conmutador de repositorios](#repository-switcher)
* **C**: [Recursos](#repository)
* **D**: [Filtros](#filters)
* **E**: [Barra de búsqueda](#search-bar)
* **F**: [Ordenación](#sorting)
* **G**: [Ordenación en orden ascendente o descendente](#sorting)
* **H**: [Ver](#types-of-view)

### Ocultar/Mostrar panel {#hide-show-panel}

Para ocultar carpetas en el panel de navegación izquierdo, haga clic en el icono **[!UICONTROL Ocultar carpetas]**. Para deshacer los cambios, haga clic en el icono **[!UICONTROL Ocultar carpetas]** de nuevo.

### Conmutador de repositorios {#repository-switcher}

El Selector de recursos también le permite cambiar de repositorio para la selección de recursos. Puede seleccionar el repositorio que desee en la lista desplegable disponible en el panel izquierdo. Las opciones del repositorio disponibles en la lista desplegable se basan en la propiedad `repositoryId` definida en el archivo `index.html`. Se basa en el entorno de la organización de IMS seleccionada al que accede el usuario que ha iniciado sesión. Los consumidores pueden aprobar un `repositoryID` preferido y, en ese caso, el Selector de recursos deja de procesar el conmutador de repositorios y solo procesa los recursos del repositorio dado.

### Repositorio de recursos

Es una colección de carpetas de recursos que puede utilizar para realizar operaciones.

### Filtros listos para usar {#filters}

El Selector de recursos también proporciona opciones de filtro listas para usar para restringir los resultados de búsqueda. Los filtros disponibles son los siguientes:

* **[!UICONTROL Estado]:** incluye el estado actual del recurso entre `all`, `approved`, `rejected` o `no status`.
* **[!UICONTROL Tipo de archivo]:** incluye `folder`, `file`, `images`, `documents` o `video`.
* **[!UICONTROL Estado de caducidad]:** menciona los recursos en función de su duración de caducidad. Puede marcar la casilla de verificación `[!UICONTROL Expired]` para filtrar los recursos que han caducado o establecer `[!UICONTROL Expiration Duration]` de un recurso para mostrar los recursos en función de su duración de caducidad. Cuando un recurso ya ha caducado o está a punto de caducar, aparece un distintivo que muestra lo mismo. Además, puede controlar si desea permitir el uso (o arrastrar y soltar) de un recurso caducado. Ver más sobre [personalizar recursos caducados](/help/assets/asset-selector-customization.md#customize-expired-assets). De manera predeterminada, se muestra el distintivo **Vence pronto** para los recursos que caduquen en los próximos 30 días. Sin embargo, puede configurar la caducidad mediante la propiedad `expirationDate`.

  >[!TIP]
  >
  > Si desea ver o filtrar recursos en función de su fecha de caducidad futura, mencione el intervalo de fechas futuras en el campo `[!UICONTROL Expiration Duration]`. Muestra los recursos que tienen el distintivo **caducará pronto**.

* **[!UICONTROL Tipo MIME]:** incluye `JPG`, `GIF`, `PPTX`, `PNG`, `MP4`, `DOCX`, `TIFF`, `PDF`, `XLSX`.
* **[!UICONTROL Tamaño de imagen]:** incluye anchura mínima/máxima, altura mínima/máxima de la imagen.

  ![rail-view-example](assets/filters-asset-selector.png)

### Búsqueda personalizada

Además de la búsqueda de texto completo, el Selector de recursos permite buscar recursos dentro de los archivos mediante búsquedas personalizadas. Puede utilizar filtros de búsqueda personalizados en los modos Vista modal y Vista de carril.

![custom-search](assets/custom-search1.png)

También puede crear un filtro de búsqueda predeterminado para guardar los campos que busca con frecuencia y utilizarlos más adelante. Para crear una búsqueda personalizada de sus recursos, puede utilizar la propiedad `filterSchema`.

### Barra de búsqueda {#search-bar}

El Selector de recursos permite realizar una búsqueda de texto completo de los recursos del repositorio seleccionado. Por ejemplo, si escribe la palabra clave `wave` en la barra de búsqueda, se muestran todos los recursos con la palabra clave `wave` mencionada en cualquiera de las propiedades de metadatos.

### Ordenación {#sorting}

Puede ordenar los recursos en el Selector de recursos por nombre, dimensiones o tamaño de un recurso. También puede ordenar los recursos en orden ascendente o descendente.

### Tipos de vista {#types-of-view}

El Selector de recursos le permite ver el recurso en cuatro vistas diferentes:

* **![vista de lista](assets/do-not-localize/list-view.png) [!UICONTROL Vista de lista]** La vista de lista muestra archivos y carpetas desplazables en una sola columna.
* **![vista de cuadrícula](assets/do-not-localize/grid-view.png) [!UICONTROL Vista de cuadrícula]** La vista de cuadrícula muestra archivos y carpetas desplazables en una cuadrícula de filas y columnas.
* **![vista de galería](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista de galería]** La vista de galería muestra archivos o carpetas en una lista horizontal bloqueada en el centro.
* **![Vista de cascada](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista de cascada]** La vista de cascada muestra archivos o carpetas en forma de Bridge.

**Gráfico de información general**


## Más información sobre las funcionalidades clave {#key-capabilities-asset-selector}

<table>
<tr>
    <td>
        <img src="assets/integrate-asset-selector.gif" width="70px" height="70px" alt="Gráfico del selector Integrar recursos"><br/>
        <a href="integrate-asset-selector.md">Selector de recursos integrado</a>
        <p>
        <em>Conozca varias funcionalidades para integrar el Selector de recursos con varias aplicaciones.
        </p>
     </td>
    <td>
        <img src="assets/with-adobe-app.gif" width="70px" height="70px" alt="Integrar el Selector de recursos con el gráfico de aplicaciones de Adobe"><br/>
        <a href="integrate-asset-selector.md">Integrar el Selector de recursos con las aplicaciones de Adobe</a>
        <p>
        <em>Descubra cómo integrar el Selector de recursos con varias aplicaciones de Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/third-party-app.gif" width="70px" height="70px" alt="Gráfico del selector Integrar recursos"><br/>
        <a href="integrate-asset-selector.md">Integrar el Selector de recursos con aplicaciones de terceros</a>
        <p>
        <em>Descubra las funcionalidades para integrar el Selector de recursos con aplicaciones que no sean de Adobe.</em>
        </p>
    </td>
    <td>
        <img src="assets/with-dynamic-media-open-api.gif" width="70px" height="70px" alt="Gráfico del selector Integrar recursos"><br/>
        <a href="integrate-asset-selector.md">Integrar el Selector de recursos con las API abiertas de Dynamic Media</a>
        <p>
        <em>Obtenga información sobre cómo integrar el Selector de recursos con las API abiertas de Dynamic Media.</em>
        </p>
     </td>
</tr>
<tr>
    <td>
        <img src="assets/asset-selector-examples.gif" width="70px" height="70px" alt="Gráfico de propiedades del Selector de recursos"><br/>
        <a href="asset-selector-customization.md">Propiedades del selector de recursos</a>
        <p>
        <em>Conozca los conceptos básicos de la personalización de varios componentes del Selector de recursos, como filtros, selección de recursos, recursos caducados y mucho más. </em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-properties.gif" width="70px" height="70px" alt="Gráfico de ejemplos del Selector de recursos"><br/>
        <a href="asset-selector-customization.md">Ejemplos de selector de recursos</a>
        <p>
        <em>Comprenda el uso de las propiedades de forma práctica. </em>
        </p>
    </td>
    <td>
        <img src="assets/customize-asset-selector.gif" width="70px" height="70px" alt="Personalizar gráfico del Selector de recursos"><br/>
        <a href="asset-selector-customization.md">Personalizaciones del selector de recursos</a>
        <p>
        <em>Configure y personalice varios componentes del Selector de recursos en función de su facilidad de uso. </em>
        </p>
    </td>
    <td>
        <img src="assets/asset-selector-upload.gif" width="70px" height="70px" alt="Gráfico de carga del selector de recursos"><br/>
        <a href="asset-selector-upload.md">Carga del selector de recursos</a>
        <p>
        <em>Aprenda a cargar archivos o carpetas en el Selector de recursos desde su sistema de archivos local o de terceros. </em>
        </p>
    </td>
</tr>
</table>

>[!MORELIKETHIS]
>
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integrar el Selector de recursos con Dynamic Media con capacidades OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
