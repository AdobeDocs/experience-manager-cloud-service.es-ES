---
title: Configuración del filtro de referente con AEM sin encabezado
description: El filtro de remitente de Adobe Experience Manager habilita el acceso desde hosts de terceros. Se necesita una configuración OSGi para el filtro de referente para habilitar el acceso al punto de conexión de GraphQL para aplicaciones sin encabezado.
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: ht
source-wordcount: '275'
ht-degree: 100%

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

Por ejemplo, para conceder acceso a solicitudes con el referente `my.domain` puede:

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

>[!CAUTION]
>
>Sigue siendo responsabilidad del cliente:
>
>* solo conceder acceso a dominios de confianza
>* asegurarse de que no se expone ninguna información confidencial
>* no usar sintaxis de comodín [*]; esto deshabilitará el acceso autenticado al punto de conexión de GraphQL y también lo expondrá a todo el mundo.

>[!CAUTION]
>
>Todos los [esquemas](#schema-generation) GraphQL (derivados de los modelos de fragmento de contenido que se han **habilitado**) se pueden leer a través del punto de conexión de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.
