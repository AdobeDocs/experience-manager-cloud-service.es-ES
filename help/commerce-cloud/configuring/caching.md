---
title: Almacenamiento en caché y rendimiento
description: Almacenamiento en caché y rendimiento
translation-type: tm+mt
source-git-commit: 2997a28e79b51e88ececbd46c81dbc6a6c443e68
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# Almacenamiento en caché y rendimiento {#caching}

## Caché de respuesta de Componente y GraphQL {#graphql}

Los componentes principales AEM de CIF ya cuentan con compatibilidad integrada para almacenar en caché las respuestas de GraphQL para componentes individuales. Esta función se puede utilizar para reducir el número de llamadas de back-end de GraphQL por un factor importante. Se puede lograr un almacenamiento en caché efectivo, especialmente para consultas repetidas como recuperar el árbol de categorías de un componente de navegación o recuperar todos los valores de facetas/agregaciones disponibles que se muestran en las páginas de categoría y búsqueda de productos.

Para los componentes principales AEM de CIF, el almacenamiento en caché se configura en base a componentes, por lo que es posible controlar si (y durante cuánto tiempo) las solicitudes/respuestas de GraphQL se almacenan en la caché para cada componente. También es posible definir el comportamiento de almacenamiento en caché para los servicios OSGi mediante el cliente GraphQL.

### Configuración

Una vez configurada para un componente determinado, los inicios de caché almacenan las consultas y respuestas de GraphQL según se define en cada entrada de configuración de caché. El tamaño de la caché y la duración de almacenamiento en caché de cada entrada se definirán en función del proyecto, por ejemplo en función de la frecuencia con la que cambien los datos del catálogo, la importancia de que un componente siempre muestre los datos más recientes posibles, etc. Tenga en cuenta que no hay ninguna invalidación de caché, por lo que tenga cuidado al configurar las duraciones de caché.

Al configurar el almacenamiento en caché para los componentes, el nombre de la caché debe ser el nombre de los componentes **proxy** que defina en el proyecto.

Antes de que el cliente envíe una solicitud de GraphQL, comprobará si esa solicitud de GraphQL **exacta** ya se ha almacenado en caché y posiblemente devolverá la respuesta en caché. Para coincidir, la solicitud de GraphQL DEBE coincidir exactamente, es decir, la consulta, el nombre de la operación (si existe), las variables (si existe) DEBEN ser iguales a la solicitud en caché, y también todos los encabezados HTTP personalizados que se puedan establecer DEBEN ser iguales. Por ejemplo, el encabezado `Store` del Magento DEBE coincidir.

### Ejemplos

Se recomienda configurar el almacenamiento en caché para el servicio de búsqueda que recoge todos los valores de agregaciones y facetas disponibles que se muestran en las páginas de búsqueda y categoría del producto. Estos valores solo cambian normalmente cuando, por ejemplo, se agrega un nuevo atributo a productos, por lo que la duración de esta entrada de caché puede ser &quot;grande&quot; si el conjunto de atributos de producto no cambia con frecuencia. Aunque esto es específico para cada proyecto, recomendamos valores de unos minutos en las fases de desarrollo del proyecto y unas pocas horas en los sistemas de producción estables.

Esto suele configurarse con la siguiente entrada de caché:

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

Otro escenario de ejemplo en el que se recomienda utilizar la función de caché GraphQl es el componente de navegación porque envía la misma consulta GraphQL a todas las páginas. En este caso, la entrada de caché se configuraría normalmente en:

```
venia/components/structure/navigation:true:10:600
```

cuando se considere el [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) . Tenga en cuenta el uso del nombre del proxy del componente `venia/components/structure/navigation`, y **no** el nombre del componente de navegación CIF (`core/cif/components/structure/navigation/v1/navigation`).

El almacenamiento en caché de otros componentes debe definirse en base a un proyecto, normalmente en coordinación con el almacenamiento en caché configurado a nivel de Dispatcher. Recuerde que no hay ninguna invalidación activa de estas memorias caché, por lo que la duración del almacenamiento en caché debe configurarse con cuidado. No hay valores de &quot;un tamaño para todos&quot; que coincidan con todos los proyectos y casos de uso posibles. Asegúrese de definir una estrategia de almacenamiento en caché en el nivel de proyecto que se ajuste mejor a los requisitos del proyecto.

## Almacenamiento en caché de Dispatcher {#dispatcher}

El almacenamiento en caché AEM páginas o fragmentos en el [AEM Dispatcher](https://docs.adobe.com/content/help/es-ES/experience-manager-dispatcher/using/dispatcher.html) es una práctica recomendada para cualquier proyecto AEM. Normalmente, se basa en técnicas de invalidación que garantizan que cualquier cambio de contenido en AEM se actualice correctamente en Dispatcher. Esta es una característica central de la estrategia de almacenamiento en caché de AEM Dispatcher.

Además del CIF de contenido administrado puro AEM, una página generalmente puede mostrar datos de comercio que se recuperan dinámicamente desde el Magento a través de GraphQL. Aunque la estructura de la página en sí podría no cambiar nunca, el contenido comercial podría cambiar, por ejemplo, si algunos datos del producto (nombre, precio, etc.) cambian de Magento.

Para asegurarse de que las páginas CIF se pueden almacenar en caché durante un tiempo limitado en el despachante de AEM, recomendamos el uso de la Invalidación [de caché basada en](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-time-based-cache-invalidation-enablettl) tiempo (también conocida como caché basada en TTL) al almacenar en caché páginas CIF en el Dispatcher AEM. Esta función se puede configurar en AEM usando el paquete extra [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) .

Con el almacenamiento en caché basado en TTL, un desarrollador suele definir una o varias duraciones de almacenamiento en caché para páginas AEM seleccionadas. Esto garantiza que las páginas CIF solo se almacenen en caché en el despachante de AEM hasta la duración configurada y que el contenido se actualice con frecuencia.

>[!NOTE]
>
>Aunque el despachante de AEM puede almacenar en caché los datos del lado del servidor, algunos componentes de CIF, como los componentes `product`, `productlist`y `searchresults` , generalmente recuperan los precios del producto en una solicitud del explorador del lado del cliente cuando se carga la página. Esto garantiza que el contenido dinámico crucial siempre se obtenga al cargar la página.

## Recursos adicionales

- [Tienda de referencia de Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de almacenamiento en caché de GraphQL](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://docs.adobe.com/content/help/es-ES/experience-manager-dispatcher/using/dispatcher.html)