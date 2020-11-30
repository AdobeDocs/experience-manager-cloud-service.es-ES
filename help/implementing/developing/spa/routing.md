---
title: enrutamiento del modelo SPA
description: Para las aplicaciones de una sola página en AEM, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de enrutamiento, el contrato y las opciones disponibles.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# enrutamiento del modelo SPA{#spa-model-routing}

Para las aplicaciones de una sola página en AEM, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de enrutamiento, el contrato y las opciones disponibles.

## Enrutamiento del proyecto {#project-routing}

La aplicación es propietaria del enrutamiento y luego la implementan los desarrolladores del front-end del proyecto. Este documento describe el enrutamiento específico del modelo devuelto por el servidor de AEM. La estructura de datos del modelo de página expone la dirección URL del recurso subyacente. El proyecto front-end puede utilizar cualquier biblioteca personalizada o de terceros que proporcione funcionalidades de enrutamiento. Una vez que una ruta espera un fragmento de modelo, se puede realizar una llamada a la `PageModelManager.getData()` función. Cuando una ruta de modelo ha cambiado, se debe activar un evento para advertir a bibliotecas de escucha como el Editor de páginas.

## Arquitectura {#architecture}

Para obtener una descripción detallada, consulte la sección [PageModelManager](blueprint.md#pagemodelmanager) del documento de modelo de SPA.

## ModelRouter {#modelrouter}

El `ModelRouter` - cuando está activado - encapsula las funciones de la API de historial de HTML5 `pushState` y `replaceState` garantiza que un fragmento determinado del modelo se recupere previamente y sea accesible. A continuación, notifica al componente front-end registrado que el modelo se ha modificado.

## Enrutamiento de modelo manual vs automático {#manual-vs-automatic-model-routing}

El `ModelRouter` automatiza la captura de fragmentos del modelo. Pero como cualquier herramienta automatizada viene con limitaciones. Cuando sea necesario, `ModelRouter` se puede deshabilitar o configurar para que omita las rutas mediante metapropiedades (consulte la sección Meta Properties del documento de componentes [de la página](page-component.md) SPA). A continuación, los desarrolladores de front-end pueden implementar su propia capa de enrutamiento de modelo solicitando que `PageModelManager` se cargue cualquier fragmento de modelo determinado mediante la `getData()` función .

>[!CAUTION]
>
>La versión actual del modelo `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo de Sling. No admite el uso de direcciones URL o alias de vanidad.

## Contrato de enrutamiento {#routing-contract}

La implementación actual se basa en el supuesto de que el proyecto SPA utiliza la API de historial de HTML5 para el enrutamiento a las distintas páginas de la aplicación.

### Configuración {#configuration}

El modelo `ModelRouter` admite el concepto de enrutamiento de modelo, ya que escucha `pushState` y `replaceState` llama a recuperar previamente fragmentos de modelo. Internamente activa el `PageModelManager` para cargar el modelo que corresponde a una URL determinada y activa un `cq-pagemodel-route-changed` evento que otros módulos pueden escuchar.

De forma predeterminada, este comportamiento se activa automáticamente. Para deshabilitarlo, el SPA debe representar la siguiente propiedad meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Tenga en cuenta que cada ruta del SPA debe corresponder a un recurso accesible en AEM (por ejemplo: &quot; `/content/mysite/mypage"`) ya que el `PageModelManager` intentará cargar automáticamente el modelo de página correspondiente una vez seleccionada la ruta. Aunque, si es necesario, el SPA también puede definir una &quot;lista de bloqueados&quot; de rutas que el `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
