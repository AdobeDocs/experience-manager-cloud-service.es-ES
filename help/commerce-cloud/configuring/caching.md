---
title: Almacenamiento en caché y rendimiento
description: Obtenga información sobre las diferentes configuraciones disponibles para habilitar GraphQL y el almacenamiento en caché de contenido para optimizar el rendimiento de su implementación comercial.
exl-id: 21ccdab8-4a2d-49ce-8700-2cbe129debc6
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 40%

---

# Almacenamiento en caché y rendimiento {#caching}

## Almacenamiento en caché de respuestas de GraphQL y componentes {#graphql}

Los componentes principales del CIF de AEM ya cuentan con una compatibilidad integrada para almacenar en caché las respuestas de GraphQL para los componentes individuales. Esta función se puede utilizar para reducir en gran medida el número de llamadas de back-end de GraphQL. Se puede lograr un almacenamiento en caché efectivo, especialmente para las consultas repetidas como recuperar el árbol de categorías de un componente de navegación o recuperar todos los valores de facetas/acumulados disponibles que se muestran en las páginas de categoría y búsqueda de productos.

Para los componentes principales del CIF de AEM, el almacenamiento en caché se configura en base a componentes, por lo que es posible controlar si (y durante cuánto tiempo) las solicitudes/respuestas de GraphQL se almacenan en la caché para cada componente. También es posible definir el comportamiento del almacenamiento en caché para los servicios OSGi mediante el cliente de GraphQL.

### Configuración {#configuration}

Una vez configurada para un componente determinado, los inicios de caché almacenan las consultas y respuestas de GraphQL según se define en cada entrada de configuración de caché. El tamaño de la caché y la duración de almacenamiento en caché de cada entrada se definen en función del proyecto, por ejemplo, en función de lo siguiente:

* La frecuencia con la que pueden cambiar los datos del catálogo.
* Qué importancia tiene que un componente siempre muestre los datos más recientes posibles, etc.

No hay ninguna invalidación de caché, por lo que tenga cuidado al configurar las duraciones de la caché.

Al configurar el almacenamiento en caché para los componentes, el nombre de la caché debe ser el nombre de los componentes **proxy** que defina en el proyecto.

Antes de que el cliente envíe una solicitud de GraphQL, comprueba si es así **exacto** La misma solicitud de GraphQL ya se ha almacenado en caché y es posible que devuelva la respuesta almacenada en caché. Para coincidir, la petición GraphQL _debe_ coincide exactamente. Es decir, la consulta, el nombre de la operación (si existe), las variables (si existe) _debe_ todos deben ser iguales a la solicitud almacenada en caché. Y todos los encabezados HTTP personalizados que se puedan configurar _debe_ también ser el mismo. Por ejemplo, Adobe Commerce `Store` encabezado _debe_ coincide.

### Ejemplos {#examples}

El Adobe recomienda configurar el almacenamiento en caché para el servicio de búsqueda que recupere todos los valores de acumulados y facetas disponibles que se muestran en las páginas de categoría y búsqueda de productos. Estos valores solo cambian normalmente cuando se añade un nuevo atributo a los productos, por ejemplo. Por lo tanto, la duración de esta entrada de caché puede ser &quot;grande&quot; si el conjunto de atributos de producto no cambia con frecuencia. Aunque esta entrada es específica del proyecto, el Adobe recomienda valores de unos minutos en las fases de desarrollo del proyecto y unas pocas horas en los sistemas de producción estables.

Esta configuración suele configurarse con la siguiente entrada de caché:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Otro escenario de ejemplo en el que se recomienda utilizar la función de almacenamiento en caché GraphQl es el componente de navegación. El motivo es que envía la misma consulta de GraphQL a todas las páginas. En este caso, la entrada de caché se configuraría normalmente en:

```
venia/components/structure/navigation:true:10:600
```

Teniendo en cuenta que la variable [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia) se utiliza. Tenga en cuenta el uso del nombre del proxy del componente `venia/components/structure/navigation`, y **no** el nombre del componente de navegación de CIF (`core/cif/components/structure/navigation/v1/navigation`).

El almacenamiento en caché de otros componentes debe definirse sobre la base de un proyecto, normalmente en coordinación con el almacenamiento en caché configurado a nivel de Dispatcher. Recuerde que no hay ninguna invalidación activa de estas memorias caché, por lo que la duración del almacenamiento en caché debe configurarse cuidadosamente. No hay valores &quot;únicos&quot; que coincidan con todos los proyectos y casos de uso posibles. Asegúrese de definir una estrategia de almacenamiento en caché en el nivel de proyecto que se ajuste mejor a los requisitos del proyecto.

## Almacenamiento en caché de Dispatcher {#dispatcher}

El almacenamiento en caché de páginas de AEM o fragmentos en [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) es una práctica recomendada para cualquier proyecto AEM. Generalmente, se basa en técnicas de invalidación que garantizan que cualquier cambio de contenido en AEM se actualice correctamente en Dispatcher. AEM Esta función es fundamental para la estrategia de almacenamiento en caché de Dispatcher de.

AEM Además del CIF de contenido administrado por el propio usuario, una página generalmente puede mostrar datos de comercio que se recuperan dinámicamente desde Adobe Commerce a través de GraphQL. Aunque la estructura de la página en sí podría no cambiar nunca, el contenido comercial podría cambiar. Por ejemplo, si los datos del producto, como el nombre y el precio, cambian en Adobe Commerce.

AEM Para garantizar que las páginas de CIF se almacenen en caché durante un tiempo limitado en la instancia de Dispatcher de la, Adobe recomienda utilizar [Invalidación de caché basada en tiempo](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) AEM (conocido como almacenamiento en caché basado en TTL) al almacenar en caché páginas del CIF en la interfaz de usuario de Dispatcher de. Esta función se puede configurar en AEM usando el paquete adicional [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/).

Con el almacenamiento en caché basado en TTL, un desarrollador suele definir una o varias duraciones de almacenamiento en caché para páginas de AEM seleccionadas. AEM Esta duración garantiza que las páginas de CIF solo se almacenen en caché en la instancia de Dispatcher hasta la duración configurada y que el contenido se actualice con frecuencia.

>[!NOTE]
>
>AEM Aunque Dispatcher puede almacenar en caché los datos del lado del servidor, algunos componentes del CIF, como los de Dispatcher, son los siguientes: `product`, `productlist`, y `searchresults` normalmente, los componentes siempre recuperan los precios del producto en una solicitud del explorador del lado del cliente cuando se carga la página. Al hacerlo, se garantiza que el contenido dinámico crucial siempre se obtenga al cargar la página.

## Recursos adicionales {#additional}

* [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Configuración de almacenamiento en caché de GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
* [Dispatcher de AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es)
