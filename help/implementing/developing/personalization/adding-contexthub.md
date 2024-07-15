---
title: Adición de ContextHub a las páginas y acceso a las tiendas
description: Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y para vincular a las bibliotecas de JavaScript de ContextHub
exl-id: 8bfe2cff-3944-4e86-a95c-ebf1cb13913c
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# Adición de ContextHub a las páginas y acceso a las tiendas {#adding-contexthub-to-pages-and-accessing-stores}

Agregue ContextHub a sus páginas para habilitar las funciones de ContextHub y para vincular a las bibliotecas de JavaScript de ContextHub.

La API de JavaScript de ContextHub proporciona acceso a los datos de contexto que administra ContextHub. Esta página describe brevemente las principales funciones de la API para acceder y manipular los datos de contexto. Siga los vínculos a la documentación de referencia de la API para ver información detallada y ejemplos de código.

## Adición de ContextHub a un componente de página {#adding-contexthub-to-a-page-component}

Para habilitar las funciones de ContextHub y vincular a las bibliotecas de JavaScript de ContextHub, incluya el componente `contexthub` en la sección `head` de su página. El código HTL del componente de página debe ser similar al siguiente ejemplo:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

También debe configurar si la barra de herramientas de ContextHub aparece en el modo de vista previa. Ver [Mostrar y ocultar la IU de ContextHub](configuring-contexthub.md#showing-and-hiding-the-contexthub-ui).

## Acerca de las tiendas ContextHub {#about-contexthub-stores}

Utilice los almacenes de ContextHub para mantener los datos de contexto. ContextHub proporciona los siguientes tipos de tiendas que forman la base de todos los tipos de tiendas:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Todos los tipos de almacén son extensiones de la clase [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core). Para obtener información acerca de cómo crear un tipo de almacén, vea [Crear almacenes personalizados](extending-contexthub.md#creating-custom-store-candidates). Para obtener información acerca de los tipos de almacén de ejemplo, vea [Candidatos de tienda de ContextHub de muestra](sample-stores.md).

### Modos de persistencia {#persistence-modes}

Las tiendas de Context Hub utilizan uno de los siguientes modos de persistencia:

* **Local:** Utiliza localStorage de HTML5 para mantener los datos. El almacenamiento local se mantiene en el explorador entre sesiones.
* **Sesión:** Utiliza sessionStorage de HTML5 para mantener los datos. El almacenamiento de sesión se mantiene durante la sesión del explorador y está disponible para todas las ventanas del explorador.
* **Cookie:** Utiliza la compatibilidad nativa del explorador con las cookies para el almacenamiento de datos. Los datos de cookies se envían y reciben del servidor en solicitudes HTTP.
* **Window.name:** Utiliza la propiedad window.name para mantener los datos.
* **Memoria:** Utiliza un objeto JavaScript para mantener los datos.

De forma predeterminada, ContextHub utiliza el modo de persistencia local. Si el explorador no admite ni permite el almacenamiento local de HTML5, se utiliza la persistencia de la sesión. Si el explorador no admite ni permite sessionStorage de HTML5, se utiliza la persistencia Window.name.

### Almacenar datos {#store-data}

Internamente, los datos se almacenan en una estructura de árbol, lo que permite agregar valores como tipos principales u objetos complejos. Cuando se agregan objetos complejos a los almacenes, las propiedades de los objetos forman ramas en el árbol de datos. Por ejemplo, el siguiente objeto complejo se agrega a un almacén vacío denominado ubicación:

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

La estructura de árbol de los datos del almacén se puede conceptualizar de la siguiente manera:

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

La estructura de árbol define los elementos de datos del almacén como pares clave/valor. En el ejemplo anterior, la clave `/number` corresponde al valor `321`, y la clave `/data/country` corresponde al valor `Switzerland`.

### Manipulación de objetos {#manipulating-objects}

ContextHub proporciona la clase [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) para manipular objetos JavaScript. Utilice las funciones de esta clase para manipular los objetos JavaScript antes de agregarlos a un almacén o después de obtenerlos de un almacén.

Además, la clase [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) proporciona funciones para serializar objetos en cadenas y deserializar cadenas en objetos. Utilice esta clase para administrar datos JSON con el fin de admitir exploradores que no incluyan de forma nativa las funciones `JSON.parse` y `JSON.stringify`.

## Interactuar con tiendas de ContextHub {#interacting-with-contexthub-stores}

Utilice el objeto JavaScript [`ContextHub`](contexthub-api.md#ui-event-constants) para obtener un almacén como objeto JavaScript. Una vez obtenido el objeto de almacén, puede manipular los datos que contiene. Utilice la función [`getAllStores`](contexthub-api.md#getallstores) o [`getStore`](contexthub-api.md#getstore-name) para obtener el almacén.

### Acceso a datos de tienda {#accessing-store-data}

La clase JavaScript [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) define varias funciones para interactuar con los datos del almacén. Las siguientes funciones almacenan y recuperan varios elementos de datos contenidos en objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Los elementos de datos individuales se almacenan como un conjunto de pares clave/valor. Para almacenar y recuperar valores, especifique la clave correspondiente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Los candidatos de tienda personalizados pueden definir funciones adicionales que proporcionen acceso para almacenar datos.

>[!NOTE]
>
>ContextHub no tiene en cuenta de forma predeterminada la sesión iniciada actualmente en los servidores de publicación y ContextHub considera que estos usuarios son &quot;anónimos&quot;.
>
>Para que ContextHub sepa que los usuarios que han iniciado sesión deben cargar el almacén de perfiles. Consulte [código de ejemplo en GitHub aquí](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos de ContextHub {#contexthub-eventing}

ContextHub incluye un marco de trabajo de eventos que le permite reaccionar automáticamente ante los eventos de almacenamiento. Cada objeto de almacén contiene un objeto [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) que está disponible como propiedad [`eventing`](contexthub-api.md#eventing) del almacén. Utilice la función [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) o [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para enlazar una función de JavaScript a un evento de almacén.

## Uso de ContextHub para manipular las cookies {#using-context-hub-to-manipulate-cookies}

La API de JavaScript de ContextHub proporciona compatibilidad entre exploradores para administrar las cookies del explorador. El espacio de nombres [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) define varias funciones para crear, manipular y eliminar cookies.

## Determinación de segmentos de ContextHub resueltos {#determining-resolved-contexthub-segments}

El motor de segmentos de ContextHub permite determinar qué segmentos registrados se resuelven en el contexto actual. Utilice la función getResolvedSegments de la clase [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) para recuperar segmentos resueltos. A continuación, utilice la función `getName` o `getPath` de la clase [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) para probar un segmento.

### Segmentos de ContextHub {#contexthub-segments}

Los segmentos de ContextHub se instalan debajo del nodo `/conf/<site>/settings/wcm/segments`.

Los siguientes segmentos se instalan con el [sitio de tutoriales WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* verano
* invierno

Las reglas que se utilizan para resolver estos segmentos se resumen de la siguiente manera:

* Primero se usa el almacén [geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) para determinar la latitud del usuario.
* A continuación, el elemento de datos de mes de [surferinfo store](sample-stores.md#contexthub-surferinfo-sample-store-candidate) determina qué temporada se encuentra en esa latitud.

>[!WARNING]
>
>Los segmentos instalados se proporcionan como configuraciones de referencia para ayudarle a crear su propia configuración dedicada para su proyecto. No los utilice directamente.

## Depuración de ContextHub {#debugging-contexthub}

Existen varias opciones para depurar ContextHub, incluida la generación de registros. Consulte [Configuración de ContextHub para obtener más información.](configuring-contexthub.md#logging-debug-messages-for-contexthub)

## Consulte Información general sobre el marco de trabajo de ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub proporciona una [página de diagnósticos](contexthub-diagnostics.md) en la que puede ver una descripción general del marco de trabajo de ContextHub.
