---
title: Configuración de Cross-Origin Resource Sharing (CORS) con AEM sin encabezado
description: El uso compartido de recursos de origen cruzado (CORS) de Adobe Experience Manager permite que las aplicaciones web sin periféricos realicen llamadas del lado del cliente a AEM. Se necesita una configuración CORS para habilitar el acceso al extremo GraphQL.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Configuración de Cross-Origin Resource Sharing (CORS)

>[!NOTE]
>
>Para obtener una descripción detallada de la política de uso compartido de recursos CORS en AEM consulte [Comprender el uso compartido de recursos de origen cruzado (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Para acceder al extremo de GraphQL, se debe configurar una directiva CORS y añadirla a un proyecto AEM que [implementado en AEM mediante Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Para ello, agregue un archivo de configuración OSGi CORS apropiado para los puntos de conexión deseados. Se pueden crear e implementar varias configuraciones CORS en distintos entornos. Se pueden encontrar ejemplos en el [Sitio de referencia de WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

La configuración de CORS debe especificar un origen de sitio web de confianza `alloworigin` o `alloworiginregexp` para los que debe concederse acceso.

El nombre del archivo de configuración debe ser: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` donde `appname` refleja el nombre de la aplicación.

Por ejemplo, para conceder acceso al extremo de GraphQL `/content/cq:graphql/wknd/endpoint` y extremo de consultas persistentes para `https://my.domain` puede utilizar:

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Si ha configurado una ruta mnemónica para el extremo, también puede utilizarla en `allowedpaths`.


