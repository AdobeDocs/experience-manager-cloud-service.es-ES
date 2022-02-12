---
title: Configuración del filtro de referente con AEM sin encabezado
description: El filtro de referente de Adobe Experience Manager habilita el acceso desde hosts de terceros. Se necesita una configuración OSGi para el filtro de referente para habilitar el acceso al extremo GraphQL para aplicaciones sin encabezado.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Filtro de referente {#referrer-filter}

El filtro de referente de Adobe Experience Manager habilita el acceso desde hosts de terceros. Se necesita una configuración OSGi para el filtro de referente para habilitar el acceso al extremo GraphQL para aplicaciones sin encabezado.

Para ello, agregue una configuración OSGi adecuada para el filtro de referente que:

* especifica un nombre de host de sitio web de confianza; o `allow.hosts` o `allow.hosts.regexp`,
* concede acceso a este nombre de host.

El nombre del archivo debe ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Por ejemplo, para conceder acceso a solicitudes con el referente `my.domain` puede:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Sigue siendo responsabilidad del cliente:
>
>* solo conceder acceso a dominios de confianza
>* asegúrese de que no se expone ninguna información confidencial
>* no usar un comodín [*] sintaxis; esto deshabilitará el acceso autenticado al extremo de GraphQL y también lo expondrá a todo el mundo.


>[!CAUTION]
>
>Todos los GraphQL [esquemas](#schema-generation) (derivada de los modelos de fragmento de contenido que se han **Habilitado**) se pueden leer a través del extremo GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.
