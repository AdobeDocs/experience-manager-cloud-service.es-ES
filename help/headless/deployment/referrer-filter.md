---
title: Configuración del filtro de referente con AEM sin encabezado
description: El filtro de remitente de Adobe Experience Manager habilita el acceso desde hosts de terceros. Se necesita una configuración OSGi para el filtro de referente para habilitar el acceso al punto de conexión de GraphQL para aplicaciones sin encabezado.
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 55%

---

# Filtro de referente {#referrer-filter}

El filtro de remitente de Adobe Experience Manager habilita el acceso desde hosts de terceros.

Se necesita una configuración OSGi para el filtro de referente para habilitar el acceso al punto final de GraphQL para aplicaciones sin encabezado en HTTP POST. Cuando se utilizan consultas persistentes de AEM sin encabezado que acceden a AEM a través de HTTP GET, no es necesario configurar un filtro de referente.

>[!WARNING]
> El filtro de referente de AEM no es una fábrica de configuración OSGi, lo que significa que solo una configuración está activa en un servicio de AEM a la vez. Cuando sea posible, evite agregar configuraciones de filtro de referente personalizadas, ya que esto sobrescribirá las configuraciones nativas de AEM y puede dañar la funcionalidad del producto.

Para ello, añada una configuración OSGi adecuada para el filtro de referente que:

* especifique un nombre de host de sitio web de confianza; o `allow.hosts` o `allow.hosts.regexp`,
* conceda acceso a este nombre de host.

El nombre del archivo debe ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

## Ejemplo de configuración {#example-configuration}

Por ejemplo, para conceder acceso a solicitudes con el referente `my.domain` puede:

>[!CAUTION]
>
>Este es un ejemplo básico que puede sobrescribir la configuración estándar. Debe asegurarse de que las actualizaciones de productos siempre se aplican a cualquier personalización.

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

## Seguridad de datos {#data-security}

>[!CAUTION]
>
>Sigue siendo responsabilidad suya abordar plenamente los siguientes puntos.

Para garantizar que sus datos siguen siendo seguros, debe asegurarse de que:

* se ha concedido acceso de **solamente** a los dominios de confianza

* se usó la sintaxis comodín [`*`] en **no**; esto deshabilita el acceso autenticado al extremo de GraphQL y también lo expone a todo el mundo

* la información confidencial **nunca** se expone; ni directa ni indirectamente:

   * Por ejemplo, todos los [esquemas de GraphQL](/help/headless/graphql-api/content-fragments.md#schema-generation) son:

      * Derivado de modelos de fragmento de contenido que se han **habilitado**

     **y**

      * se pueden leer a través del extremo de GraphQL

     Esto significa que la información presente como nombres de campo en la definición del modelo puede estar disponible.

Debe asegurarse de que no haya datos confidenciales disponibles por ningún medio, por lo que dichos detalles deben considerarse cuidadosamente.
