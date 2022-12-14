---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar SPA React remoto dentro de AEM.
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: d213dd0788e66015237d241caf0f3b5737ce725c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# El componente RemotePage {#remote-page-component}

Al decidir [qué nivel de integración](/help/implementing/developing/headful-headless.md) le gustaría tener entre el SPA externo y el AEM, a menudo está claro que necesita poder ver y editar el SPA dentro de AEM. El componente RemotePage es un componente de página personalizado solo para este fin.

## Información general {#overview}

El componente RemotePage obtiene todos los recursos necesarios del `asset-manifest.json` y utiliza esto para procesar el SPA dentro de AEM.

* RemotePage permite insertar las secuencias de comandos y las hojas de estilo de una SPA en el cuerpo de un componente Página AEM.
* Los componentes del front-end virtual permiten marcar secciones como editables en AEM editor SPA.
* En conjunto, una SPA alojada en un dominio diferente se puede hacer editable en AEM.

Consulte el artículo [Edición de un SPA externo dentro de AEM](editing-external-spa.md) para obtener más información sobre SPA externas editables en AEM.

## Requisitos  {#requirements}

* Habilitar CORS en desarrollo
* Configuración de URL remota en Propiedades de página
* Procesar el SPA en AEM
* La aplicación web debe utilizar un manifiesto de recurso de bundler como uno de los siguientes y exponer un `asset-manifest.json` en la raíz de dominio que enumera una `entrypoints property` todos los archivos CSS y JS que se van a cargar:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![ejemplo de propiedad entrypoints](assets/asset-manifest-entrypoints.png)
* La aplicación debe poder inicializarse en una `<div id="root"></div>` debajo del `body` elemento. Si se espera un marcado diferente para que la aplicación cree una instancia, entonces esto debe ajustarse en consecuencia en los scripts HTL del componente proxy que tenga un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Restricciones {#limitations}

* El componente RemotePage espera que la implementación proporcione un manifiesto de recurso como el [encontrado aquí.](https://github.com/shellscape/webpack-manifest-plugin) Sin embargo, el componente RemotePage solo se ha probado para funcionar con el marco React (y Next.js mediante el componente Remote-page-next) y, por lo tanto, no admite la carga remota de aplicaciones desde otros marcos, como el Angular.
* El CSS interno definido en el archivo HTML raíz de la aplicación, así como el CSS en línea en el nodo DOM raíz, no estarán disponibles al realizar el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto AEM SPA, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
