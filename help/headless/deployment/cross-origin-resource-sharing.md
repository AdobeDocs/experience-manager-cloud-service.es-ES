---
title: Configuración de Intercambio de Recursos de Origen Cruzado (CORS) con AEM Headless
description: El Intercambio de Recursos de Origen Cruzado (CORS) de Adobe Experience Manager permite que las aplicaciones web sin encabezado realicen llamadas del lado del cliente a AEM. Se necesita una configuración de CORS para habilitar el acceso al punto de conexión de GraphQL.
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%

---

# Configuración de Intercambio de Recursos de Origen Cruzado (CORS)

>[!NOTE]
>
>Para obtener una descripción detallada de la política de uso compartido de recursos CORS en AEM, consulte [Comprender el Intercambio de Recursos de Origen Cruzado (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=es#understand-cross-origin-resource-sharing-(cors)).

Para acceder al punto de conexión de GraphQL, se debe configurar una política CORS y añadirla a un proyecto de AEM que está [implementado en AEM mediante Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Para ello, añada un archivo de configuración OSGi CORS apropiado para los puntos de conexión deseados. Se pueden crear e implementar varias configuraciones CORS en distintos entornos. Se pueden encontrar ejemplos en el [Sitio de referencia de WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

La configuración de CORS debe especificar un origen de sitio web de confianza `alloworigin` o `alloworiginregexp`, para los que debe concederse acceso.

El nombre del archivo de configuración debe ser: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json`, donde `appname` refleja el nombre de la aplicación.

Por ejemplo, para conceder acceso al punto de conexión de GraphQL `/content/cq:graphql/wknd/endpoint` y punto de conexión de consultas persistentes para `https://my.domain`, puede utilizar:

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

Si ha configurado una ruta de vanidad para el punto de conexión, también puede utilizarla en `allowedpaths`.
