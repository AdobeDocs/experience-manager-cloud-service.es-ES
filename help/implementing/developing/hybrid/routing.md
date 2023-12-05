---
title: SPA Enrutamiento de modelo de
description: AEM Para las aplicaciones de una sola página en la, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de ruta, el contrato y las opciones disponibles.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# SPA Enrutamiento de modelo de{#spa-model-routing}

AEM Para las aplicaciones de una sola página en la, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de ruta, el contrato y las opciones disponibles.

## Enrutamiento de proyectos {#project-routing}

La aplicación es propietaria del enrutamiento y luego la implementan los desarrolladores de front-end del proyecto. AEM Este documento describe la ruta específica del modelo devuelto por el servidor de la. La estructura de datos del modelo de página expone la dirección URL del recurso subyacente. El proyecto front-end puede utilizar cualquier biblioteca personalizada o de terceros que proporcione funcionalidades de enrutamiento. Una vez que una ruta espera un fragmento de modelo, se llama a la función `PageModelManager.getData()` función se puede realizar. Cuando la ruta de un modelo ha cambiado, se debe activar un evento para advertir a las bibliotecas que escuchan, como el Editor de páginas.

## Arquitectura {#architecture}

Para ver una descripción detallada, consulte [PageModelManager](blueprint.md#pagemodelmanager) SPA del documento de modelo de la.

## ModelRouter {#modelrouter}

El `ModelRouter` - cuando está activada - encapsula las funciones de la API History de HTML5 `pushState` y `replaceState` para garantizar que un fragmento de modelo determinado se obtenga previamente y sea accesible. A continuación, notifica al componente front-end registrado que el modelo se ha modificado.

## Enrutamiento manual frente al automático del modelo {#manual-vs-automatic-model-routing}

El `ModelRouter` automatiza la captura de fragmentos del modelo. Pero como cualquier herramienta automatizada, viene con limitaciones. Cuando sea necesario, el `ModelRouter` puede deshabilitarse o configurarse para que ignore las rutas mediante propiedades meta (consulte la sección Propiedades meta de la [SPA Componente de página](page-component.md) documento). Los desarrolladores de front-end pueden implementar su propia capa de enrutamiento de modelo solicitando la variable `PageModelManager` para cargar cualquier fragmento de modelo determinado utilizando `getData()` función.

>[!CAUTION]
>
>La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recurso real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

## Contrato de enrutamiento {#routing-contract}

SPA La implementación actual se basa en la suposición de que el proyecto de utiliza la API Historial de HTML5 para el enrutamiento a las diferentes páginas de la aplicación.

### Configuración {#configuration}

El `ModelRouter` admite el concepto de enrutamiento de modelos a medida que escucha `pushState` y `replaceState` llamadas a fragmentos de modelo de recuperación previa. Internamente, déclencheur el `PageModelManager` para cargar el modelo que corresponde a una URL determinada y activa una `cq-pagemodel-route-changed` evento que otros módulos pueden escuchar.

De forma predeterminada, este comportamiento se habilita automáticamente. SPA Para deshabilitarlo, el usuario debe procesar la siguiente propiedad meta:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

SPA AEM Cada ruta de la debe corresponder a un recurso accesible en el que se puede acceder a través de la ruta (por ejemplo, &quot; `/content/mysite/mypage"`), ya que `PageModelManager` intentará cargar automáticamente el modelo de página correspondiente una vez seleccionada la ruta. SPA Sin embargo, si es necesario, el también puede definir una &quot;lista de bloqueados&quot; de rutas que el `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
